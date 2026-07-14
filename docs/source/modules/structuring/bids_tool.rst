BIDS Transformer
================

The BIDS Transformer scans an existing directory, proposes how detected files
could be organized and renamed within a BIDS-oriented dataset, and creates a
reviewable transfer plan before any file operation is performed.

The module is intended for the controlled curation of existing datasets,
vendor exports, legacy folder structures, and partially organized research
data. It does not assume that automated detection is always correct. Every
proposed mapping remains visible and editable, and execution is blocked until
the user has reviewed the mapping and completed a successful dry run.

Overview
--------

The BIDS Transformer separates dataset transformation into distinct review
stages:

#. Scan the source directory.
#. Detect probable subjects, sessions, tasks, runs, datatypes, and suffixes.
#. Generate proposed BIDS names and destination paths.
#. Review and edit the mapping table.
#. Validate the proposed destination architecture.
#. Create missing destination components when appropriate.
#. Run a non-destructive dry run.
#. Execute the reviewed transfer plan.

The application deliberately separates detection from execution. A source scan
only creates a proposed mapping and does not copy, rename, move, or delete any
research files. :contentReference[oaicite:0]{index=0}

Source and Destination
----------------------

Users select:

* A source directory containing the files to inspect.
* A destination directory that will serve as the proposed BIDS dataset root.
* A detection mode.
* A subject identifier strategy.
* A collision-handling policy.
* A transfer mode.

When no destination has been selected, the application proposes a
``bids_output`` directory beside the source folder. :contentReference[oaicite:1]{index=1}

The source directory is scanned recursively. Each file is inspected
individually and represented as one row in the mapping table.

Detection Modes
---------------

The Transformer can scan all supported datatypes or restrict detection to a
selected datatype.

Available modes include:

* Automatic detection of all supported files
* Anatomical MRI
* Functional MRI
* Diffusion MRI
* Field maps
* Perfusion imaging
* MR spectroscopy
* PET
* Microscopy
* CT
* EEG, iEEG, MEG, EMG, and NIRS
* Behavioral and phenotype data
* Physiological recordings
* Eye tracking
* Motion and wearable data
* Biomechanics
* Ecological momentary assessment
* Digital and mobile data
* Virtual-reality data
* Behavioral audio and video
* Speech and voice data
* Vendor or source data

The selected mode filters the scan; it does not itself establish that the
resulting dataset is valid BIDS.

Automated Detection
-------------------

For each source file, NIM Studio attempts to infer:

* Datatype or modality
* Participant identifier
* Session identifier
* Task label
* Run number
* BIDS suffix
* File extension
* Proposed BIDS filename
* Proposed destination path

Detection is based primarily on existing BIDS entities, directory names,
filename suffixes, file extensions, and recognizable terms within source
paths. Explicit BIDS datatype folders and known BIDS suffixes generally receive
higher confidence than keyword-based detection. Files that cannot be mapped
confidently are marked for review rather than silently accepted. :contentReference[oaicite:2]{index=2}

The module may also use BIDS Extension Proposal or custom-extension selections
configured through Dataset Setup as routing hints. Such hints can influence a
proposed datatype or destination, but the resulting row remains marked for
review. :contentReference[oaicite:3]{index=3}

Subject Handling
----------------

Detected subject identifiers can either be preserved or renumbered
sequentially.

When sequential renumbering is selected, NIM Studio creates an internal mapping
between detected subject identifiers and zero-padded numerical identifiers.
The proposed subject values and paths are then updated in the mapping table.

This operation changes only the proposed transfer plan until the user executes
the reviewed transformation.

Mapping Table
-------------

The mapping table is the central review interface of the BIDS Transformer. For
each source file it displays:

* Inclusion status
* Detection confidence
* Review status
* Warnings
* Original source path
* Detected modality
* Detected subject
* Detected session
* Detected task
* Detected run
* Detected suffix
* File extension
* Proposed BIDS filename
* Proposed BIDS destination
* Whether the destination already exists
* The rule used for detection

Several fields are editable, including inclusion, modality, subject, session,
task, run, suffix, proposed filename, and proposed path. When detected entities
are changed, NIM Studio recalculates the proposed destination. Any change made
after a dry run invalidates that dry run and requires the review process to be
repeated. :contentReference[oaicite:4]{index=4}
:contentReference[oaicite:5]{index=5}

Rows can be filtered by status, modality, warning state, source path, or
proposed destination path.

Confidence and Review Status
----------------------------

Each proposed mapping is assigned a confidence score and a status such as:

``ok``
   The file matched a relatively explicit detection rule, such as an existing
   BIDS datatype directory or recognized BIDS suffix.

``review``
   The mapping is plausible but requires manual confirmation.

``excluded``
   The file is excluded by the selected detection mode or has been manually
   removed from the transfer plan.

Low-confidence files, files without a recognized subject, and files without a
recognized suffix prevent the dry run from passing while they remain included.

Destination Architecture
------------------------

The Transformer checks whether the directories and root-level files required by
the current mapping already exist.

The architecture check includes:

* The destination root
* ``dataset_description.json``
* ``participants.tsv``
* Participant and session directories
* Detected datatype directories
* Root support structures required by the proposed mappings

The preview identifies existing and missing components and displays examples of
the proposed source-to-destination mappings. It also summarizes detected
subjects, modalities, and warnings. :contentReference[oaicite:6]{index=6}

With user confirmation, NIM Studio can create missing folders and basic
root-level placeholders. The generated ``dataset_description.json`` contains a
minimal NIM Studio-generated description, while ``participants.tsv`` is
initialized with a ``participant_id`` header. These files are starting
templates and must still be reviewed and completed by the user.
:contentReference[oaicite:7]{index=7}

Dry Run
-------

The dry run is mandatory before an executable transfer mode becomes available.

A dry run:

* Does not copy files.
* Does not rename files.
* Does not move files.
* Does not modify the source dataset.
* Reviews the proposed paths and architecture.
* Checks for blocking mapping issues.
* Records possible destination collisions.
* Calculates source-file hashes where available.
* Writes a JSON manifest of the proposed operation.

Dry-run manifests are stored under:

.. code-block:: text

   code/
   └── nim_transformer_manifests/
       └── bids_transformer_dry_run_YYYYMMDD_HHMMSS.json

A dry run fails when included mappings still contain blocking issues, including
unknown subjects, unknown suffixes, low-confidence mappings, rows still marked
for review, excluded rows incorrectly included, missing destination paths, or
an incomplete destination architecture. :contentReference[oaicite:8]{index=8}

Transfer Modes
--------------

The current beta provides four transfer settings:

``Dry-run only``
   Generates and evaluates the proposed plan without transferring files.

``Copy and rename``
   Copies each included source file to its proposed destination using the
   proposed BIDS-oriented filename.

``Copy without renaming``
   Copies each included file into the proposed destination directory while
   preserving its original filename.

``Move and rename``
   Moves the original source file to the proposed destination and applies the
   proposed filename.

The move option modifies the original source structure and therefore requires
additional confirmation. Users should use it only when a verified, untouched
backup exists. :contentReference[oaicite:9]{index=9}

Collision Handling
------------------

When a proposed target already exists, the selected collision policy determines
how the operation proceeds.

Available policies include:

* Add a UUID suffix to the new file
* Skip the file
* Ask before overwriting
* Never overwrite

The default safety model is intended to prevent silent replacement of existing
files. Nevertheless, users must inspect the destination and transfer manifest
after execution.

Transfer Manifests
------------------

After execution, NIM Studio writes a JSON manifest describing the transfer.

The manifest may include:

* Source path
* Proposed path
* Final destination path
* Source and destination sizes
* Source and destination hashes
* Transfer action
* Completion status
* Collision policy
* Errors
* Execution timestamp

Hashes use BLAKE3 when the optional package is available and otherwise fall back
to SHA-256. :contentReference[oaicite:10]{index=10}
:contentReference[oaicite:11]{index=11}

Review Outside NIM Studio
-------------------------

The mapping table can be exported as CSV for external review and imported back
into NIM Studio.

Imported mappings must use the same column structure as the current Transformer
table. Importing a mapping resets both the review confirmation and dry-run
status, ensuring that externally edited plans are checked again before
execution. :contentReference[oaicite:12]{index=12}

The destination architecture preview can also be exported as Markdown or PDF.

What the BIDS Transformer Does Not Do
-------------------------------------

The current beta should not be interpreted as a complete automated BIDS
conversion or certification system.

Specifically, it does not:

* Guarantee that automated datatype or entity detection is correct.
* Guarantee complete compliance with the full BIDS specification.
* Replace review using an official BIDS validator.
* Fully interpret arbitrary vendor-specific acquisition exports.
* Convert proprietary imaging formats into NIfTI.
* Extract or generate all modality-specific metadata required by BIDS.
* Automatically create complete scientific sidecars for every modality.
* Resolve field-map ``IntendedFor`` relationships automatically.
* Confirm task-event synchronization.
* Confirm physiological sampling rates, units, or channel descriptions.
* Determine whether sensitive or identifiable data may legally be shared.
* Replace institutional data-governance, ethics, or GDPR review.
* Preserve every possible relationship between paired files without user
  inspection.
* Determine whether a proposed BIDS label is scientifically meaningful.
* Modify source files during scanning or dry-run mode.

The Transformer produces a transparent and editable proposal. It does not make
an authoritative scientific or regulatory determination.

Recommended Workflow
--------------------

For beta testing, the recommended workflow is:

#. Work from an untouched backup or disposable test copy.
#. Select the source and destination directories.
#. Scan the source using the most appropriate detection mode.
#. Review all warnings and low-confidence rows.
#. Correct subjects, sessions, modalities, suffixes, and destination paths.
#. Exclude files that should not enter the BIDS dataset.
#. Validate the proposed destination architecture.
#. Create only the missing components that are appropriate for the study.
#. Export the mapping CSV when an additional review is needed.
#. Run the dry run and inspect its JSON manifest.
#. Use a copy-based transfer mode before considering move operations.
#. Run an official BIDS validator on the resulting dataset.
#. Review metadata and sidecars using the Metadata Curator.
#. Compare source and destination files before using the transformed dataset
   for analysis or sharing.

Beta Safety Notice
------------------

Automated detection may be imperfect for heterogeneous datasets, historical
folder structures, custom naming systems, and vendor exports.

During the beta phase, users should test the BIDS Transformer on backed-up,
non-critical data in an isolated environment. The original source dataset
should remain unchanged until the proposed mapping, transfer manifest, and
resulting dataset have been independently reviewed.