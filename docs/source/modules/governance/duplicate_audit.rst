Duplicate Audit
===============

Duplicate Audit scans local project folders, user directories, mounted
storage, and network locations for possible duplicate files.

It can identify duplicate candidates using filenames, version-like naming
patterns, and exact file-content hashes. Scanning is local and does not upload
files or connect to external services.

A standard scan is non-destructive. Files are not moved or deleted unless the
user explicitly selects files and executes the separate quarantine workflow.
:contentReference[oaicite:2]{index=2}

Overview
--------

Duplicate files can arise from:

* Manual copies
* Repeated downloads
* Backup folders
* Versioned filenames
* Data transfers
* Shared storage
* Renamed files with identical content
* Repeated exports from acquisition or analysis systems

Duplicate Audit helps users locate these candidates and prepare a reviewable
cleanup plan.

Detection Modes
---------------

Same Filename
^^^^^^^^^^^^^

Detects files with the same filename in different directories.

This is a fast metadata-only comparison. It does not open file contents.

Files with the same name are not necessarily identical. They may represent
different versions, participants, sessions, or processing outputs and must be
reviewed manually.

Version-Like Files
^^^^^^^^^^^^^^^^^^

Detects filenames containing patterns such as:

* ``copy``
* ``old``
* ``backup``
* ``final``
* ``final2``
* ``v2``
* ``version``
* Numbered duplicate suffixes

This mode identifies likely duplicate or superseded files based on naming only.

Exact Content Hash
^^^^^^^^^^^^^^^^^^

Detects files with exactly matching binary content, even when their filenames
or locations differ.

NIM Studio first groups files by size and hashes only files that share a size
with another candidate. This reduces unnecessary file reading.

Supported algorithms are:

* BLAKE3
* SHA-256

BLAKE3 is recommended for large storage scans when the optional ``blake3``
package is installed. SHA-256 is available through Python.

Hash scanning opens and reads local file bytes but does not modify them.
:contentReference[oaicite:3]{index=3}

Scan Scope
----------

Standard Recursive Scan
^^^^^^^^^^^^^^^^^^^^^^^

The standard scan recursively searches the selected root.

Recommended targets include:

* A single research project
* A dataset root
* ``Documents``
* ``Downloads``
* ``Desktop``
* A mounted project drive
* A specific institutional storage location

Deep System or Storage Scan
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The deep scan is intended for broader storage locations and may take
considerably longer.

Use this mode carefully because it may encounter:

* System folders
* Restricted files
* Cloud placeholders
* Symbolic links
* Large archives
* Network latency
* Permission errors
* Files owned by multiple users

Start with a narrowly defined project root whenever possible.

Safety Filters
--------------

Depending on the selected configuration, the audit can skip:

* Hidden files
* System directories
* Cloud placeholder files
* Symbolic links
* Unreadable files
* Files outside a selected owner filter
* Empty files during content hashing
* Files above a configured hash-size limit

Cloud placeholder skipping should remain enabled when scanning directories
synchronized through cloud services. Otherwise, opening a placeholder for
hashing may cause the cloud client to download it.

Owner Filtering
---------------

On shared systems, Duplicate Audit can attempt to identify file owners.

When the owner filter is enabled:

#. Select the audit root.
#. Click **Discover owners**.
#. Review the detected owner list.
#. Select the owner whose files should be included.
#. Run the duplicate scan.

Owner detection depends on the operating system and permissions. Ownership
information may be unavailable or may use a fallback value.
:contentReference[oaicite:4]{index=4}

How to Run a Duplicate Audit
----------------------------

#. Open the **Duplicate Audit** module.

#. Click **Browse** and select the folder to scan.

#. Choose the scan scope.

   Start with **Standard recursive scan** for normal project-level audits.

#. Keep the recommended safety filters enabled.

#. Select one or more detection modes:

   * Same filename
   * Version-like files
   * Exact same content fingerprint

#. When using exact-content detection, choose BLAKE3 or SHA-256.

#. Review the warning explaining that hash scanning reads local file contents.

#. Start the scan.

#. Monitor the progress indicators showing:

   * Files seen
   * Files retained after filtering
   * Candidate files
   * Files hashed
   * Duplicate groups

#. Review the candidate table after the scan completes.

#. Do not assume that the older file should always be removed.

#. Check the path, reason, size, modification time, owner, and hash before
   selecting any file.

The scan report explicitly states that nothing has been moved or deleted.
:contentReference[oaicite:5]{index=5}

Reviewing Results
-----------------

The result table includes:

* Older-file selection
* Newer-file selection
* Older path
* Newer path
* Recommended action
* File owner
* Detection reason
* Duplicate group
* File size
* Modification time
* Content hash

By default, the older file may be preselected while the newer file remains
unselected. This is only a review aid and is not proof that the older file is
unnecessary. :contentReference[oaicite:6]{index=6}

Before selecting a candidate, consider:

* Is one file located in an official raw-data location?
* Is one file part of a derivative dataset?
* Is one file linked from code or documentation?
* Do the files have the same content hash?
* Is one file the only protected backup?
* Are both files required for provenance?
* Is the newer timestamp actually meaningful?
* Does one filename indicate an approved final version?
* Are the files owned by different users?

Exporting Reports
-----------------

Duplicate Audit can export selected results as CSV.

The exported rows may include:

* Selected older and newer files
* File paths
* Recommended action
* User-selected action
* Owner
* Detection reason
* Duplicate group
* Size
* Modification time
* Content hash

The full audit package can also include:

* All duplicate candidates
* Selected candidates
* Owner summary
* Scan diagnostics
* Quarantine manifest preview

The report export does not move any files. :contentReference[oaicite:7]{index=7}

Quarantine Preview
------------------

Before moving any files, use the quarantine preview.

The preview shows:

* Selected candidate files
* Proposed quarantine locations
* Detection reasons
* Number of files selected

Previewing the quarantine manifest does not move files.
:contentReference[oaicite:8]{index=8}

Preview-Only Mode
-----------------

When **Preview only** is enabled:

* No files are moved.
* No files are deleted.
* A quarantine plan can still be reviewed and exported.
* Selected files remain in their original locations.

Preview-only mode is recommended during beta testing.

Quarantine
----------

Quarantine is a separate, explicit operation.

When executed, selected files are moved into a quarantine directory rather
than deleted. NIM Studio requests confirmation before the move.

If a file with the same name already exists in quarantine, NIM Studio adds a
duplicate suffix rather than silently replacing it.

The quarantine process may generate a manifest recording:

* Original file path
* Quarantine destination
* Detection reason
* File size
* Hash
* Move status
* Timestamp

Quarantined files should be retained until the dataset or project has been
checked and all workflows continue to operate correctly.
:contentReference[oaicite:9]{index=9}

Recommended Safe Workflow
-------------------------

#. Create or verify a current backup.

#. Select a narrow audit root.

#. Run filename and version-like detection first.

#. Review the initial candidate set.

#. Enable exact-content hashing for candidates that require stronger evidence.

#. Export the complete audit package.

#. Review candidate paths with the project owner or data steward.

#. Use the quarantine preview.

#. Keep preview-only mode enabled during initial testing.

#. Select files individually rather than bulk-selecting all older files.

#. Export the quarantine manifest.

#. Move approved candidates to quarantine only after review.

#. Re-run analyses, scripts, or project checks.

#. Retain the quarantine directory for an agreed review period.

#. Delete quarantined files manually only after independent confirmation.

What Duplicate Audit Does Not Guarantee
---------------------------------------

Duplicate Audit does not determine that a file is safe to remove.

In particular:

* Matching filenames do not prove matching content.
* Version-like names do not prove that a file is obsolete.
* Identical hashes prove identical file bytes, but not that both locations are
  unnecessary.
* Modification time does not prove which copy is authoritative.
* The older file is not automatically the less important file.
* Duplicate files may be intentional backups.
* Duplicate files may be required by separate projects.
* Symbolic links, permissions, cloud placeholders, and network shares can
  affect scan results.
* Ownership information may be incomplete.
* The audit does not understand every scientific dependency.
* The audit does not inspect code to determine whether a file is referenced.
* The audit does not delete files automatically.

Beta Safety Notice
------------------

During the beta phase:

* Use test data or a backed-up project.
* Keep preview-only mode enabled initially.
* Avoid scanning an entire operating system drive.
* Avoid moving source data before checking project dependencies.
* Export reports before quarantine.
* Review every selected file manually.
* Treat quarantine as reversible temporary storage, not immediate deletion.