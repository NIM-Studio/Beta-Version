Dataset Builder
===============

The Dataset Builder transforms datasets from simple directory structures into
managed research entities. Rather than organizing files alone, it enables
researchers to define and manage cohorts, participants, sessions, modalities,
derivatives, and their relationships within a standardized research
environment.

Whether creating a new dataset or curating an existing one, the Dataset
Builder provides a flexible framework for organizing research data that
supports reproducibility, interoperability, and long-term maintainability.

Datasets are treated as modular components of a research project and may be
organized using the Brain Imaging Data Structure (BIDS) or fully customized
hierarchies, allowing NIM Studio to accommodate a wide range of study designs,
research domains, and institutional workflows.

Overview
--------

Research datasets often consist of multiple cohorts, acquisition sessions,
modalities, and derived data collected over extended periods of time. The
Dataset Builder assists researchers in organizing these components into a
consistent and scalable structure while preserving the flexibility to adapt to
specific institutional or scientific requirements.

Whether creating a new dataset or importing an existing one, the Dataset
Builder provides a unified interface for dataset organization and management.

Features
--------

The Dataset Builder enables users to:

* Create new datasets within existing research projects.
* Import existing datasets into NIM Studio.
* Organize datasets using BIDS or custom structures.
* Configure cohorts and participant groups.
* Manage participant identifiers.
* Define sessions and longitudinal timepoints.
* Organize multiple acquisition modalities.
* Configure derivatives and processed data locations.
* Prepare datasets for downstream BIDS transformation and validation.
* Support both small studies and large collaborative cohorts.

Dataset Organization
--------------------

Datasets may be organized according to the Brain Imaging Data Structure (BIDS)
or using customized directory structures appropriate for the research project.

Supported organizational approaches include:

* Native BIDS datasets.
* Clinical research datasets.
* Longitudinal cohorts.
* Cross-sectional studies.
* Multi-centre projects.
* Multi-modal acquisitions.
* Hybrid project structures.

This flexibility enables NIM Studio to support neuroimaging while remaining
applicable to a broad range of biomedical and multidisciplinary research
projects.

Cohort and Participant Management
---------------------------------

The Dataset Builder supports hierarchical dataset organization at multiple
levels.

Researchers can organize data according to:

* Cohorts
* Participant groups
* Individual participants
* Sessions and visits
* Acquisition modalities
* Experimental conditions
* Derived datasets

This structure facilitates longitudinal studies, case-control designs,
multi-site collaborations, and complex research protocols.

BIDS Integration
----------------

Although NIM Studio is designed around BIDS-compatible workflows, adoption of
the BIDS standard remains optional.

When BIDS is selected, the Dataset Builder assists in establishing a dataset
structure that is compatible with downstream validation, metadata generation,
and transformation workflows.

Researchers working with legacy datasets or non-BIDS modalities may instead
use customized organizational structures while still benefiting from the
remaining NIM Studio modules.

Relationship to Other Modules
-----------------------------

The Dataset Builder integrates closely with other components of NIM Studio.

Typical workflows include:

* Project Builder → initialize a research project.
* Dataset Builder → create or import datasets.
* BIDS Transformer → convert or validate BIDS organization.
* Metadata Curator → generate and enrich metadata.
* Duplicate Audit → identify duplicate or redundant files.
* Data Management Dashboard → monitor dataset integrity and organization.

Each module can also be used independently to curate existing research
projects.

Best Practices
--------------

For optimal dataset organization it is recommended to:

* Maintain consistent participant identifiers.
* Separate raw, processed, and derived data.
* Preserve original source data whenever possible.
* Organize longitudinal sessions consistently.
* Document custom directory structures.
* Use BIDS where appropriate to maximize interoperability.

Benefits
--------

The Dataset Builder provides:

* Standardized dataset organization.
* Flexible support for diverse study designs.
* Cohort and participant management.
* Optional BIDS-compatible workflows.
* Scalable organization for longitudinal and multi-site studies.
* Improved reproducibility and discoverability.
* Seamless integration with the remaining NIM Studio ecosystem.