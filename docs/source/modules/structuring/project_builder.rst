Project Builder
===============

The Project Builder is the entry point for creating standardized research
projects in NIM Studio. It provides a guided workflow for generating complete
project structures that support reproducible research, organized data
management, and long-term maintainability.

Rather than creating only a dataset, the Project Builder establishes a
comprehensive research workspace containing administrative documentation,
study design, code, datasets, analyses, outputs, and publication material.

Overview
--------

Research projects often evolve over many years and involve multiple
researchers, study phases, datasets, and analysis pipelines. Without a
consistent organizational strategy, project structures frequently become
difficult to maintain, reproduce, or share.

The Project Builder addresses this challenge by automatically generating a
structured project hierarchy based on recommended neuroinformatics and research
data management practices.

Features
--------

The Project Builder enables users to:

* Create standardized research project structures.
* Generate configurable directory hierarchies.
* Define project metadata during project creation.
* Initialize documentation and administrative folders.
* Prepare projects for downstream BIDS workflows.
* Support both small and large collaborative studies.
* Customize project structures according to institutional or study-specific
  requirements.

Project Creation Workflow
-------------------------

Project creation follows a guided workflow consisting of several steps:

#. Enter general project information.
#. Select a destination directory.
#. Configure the project structure.
#. Choose optional project components.
#. Generate the project hierarchy.
#. Review the generated structure before continuing.

Each project is created locally without modifying existing files unless
explicitly confirmed by the user.

Generated Structure
-------------------

The generated project structure may include components such as:

* Administration
* Study Design
* Code
* Data
* Analysis
* Outputs
* Manuscripts
* Reference Resources

Additional folders may be included depending on the selected configuration.

Customization
-------------

Although NIM Studio provides a recommended hierarchy, project structures remain
fully customizable.

Researchers can:

* Rename folders.
* Add custom branches.
* Remove unnecessary components.
* Adapt structures for different study designs.
* Organize multiple datasets within a single project.
* Extend projects throughout the research lifecycle.

The generated hierarchy therefore serves as a standardized starting point
rather than a rigid template.

Relationship to Other Modules
-----------------------------

The Project Builder forms the foundation for several other NIM Studio modules.

Projects created with the Project Builder can subsequently be expanded using:

* Dataset Builder
* BIDS Transformer
* Metadata Curator
* Duplicate Audit
* Data Management Dashboard

These modules operate within the generated project structure while preserving
its organization and metadata.

Best Practices
--------------

For optimal project organization, it is recommended to:

* Create a separate project for each research study.
* Store all study-related resources within the project directory.
* Keep administrative documentation together with research data.
* Preserve generated folder names where possible.
* Maintain consistent project organization across laboratories.

Benefits
--------

Using the Project Builder provides several advantages:

* Standardized project organization.
* Improved reproducibility.
* Simplified collaboration.
* Better discoverability of research assets.
* Easier integration with downstream NIM Studio modules.
* Support for FAIR research data management.
* Preparation for BIDS-compatible workflows.