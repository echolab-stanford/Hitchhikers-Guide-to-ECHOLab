# Managing Shared Data

## Overview

ECHOLab projects rely on a combination of shared datasets, project-specific datasets, and derived data products. We want to ensure that data resources remain discoverable, well-organized, and accessible to future researchers while minimizing unnecessary duplication.

This page describes general principles for managing shared data resources. Specific organizational structures and practices may evolve over time.

## Guiding Principles

### Maintain Shared Resources

Datasets that are used across multiple projects should be maintained as shared resources whenever possible.

Examples include:

- ERA5
- DHS
- WorldClim
- CMIP6
- PurpleAir

### Minimize Duplication

Researchers should look for existing shared resources before creating new copies of large datasets.

The Shared Data Catalog can help researchers identify existing datasets and data products.

### Preserve Canonical Copies

Shared datasets should have a clearly identified canonical location.

Researchers should avoid modifying shared raw datasets directly. Other projects may rely on those data, and changes can make it difficult to reproduce prior analyses.

When updates are needed, new data should generally be added rather than replacing existing files.

When multiple versions of a dataset exist, they should be clearly versioned and retained whenever feasible. Preserving older versions helps ensure that previous projects remain reproducible and allows researchers to understand which version of a dataset was used in a particular analysis.

In general, raw data should be treated as immutable. Data cleaning, processing, and analysis should occur in project-specific workflows rather than by modifying shared raw datasets.

### Separate Shared Data from Project Data

Not all data belong in shared storage.

In general:

- Shared datasets support multiple projects.
- Project data are specific to a particular project.
- Derived products may fall into either category depending on anticipated reuse.

### Support Reproducibility

Project workflows should make it possible to identify:

- Which datasets were used
- Where they were stored
- How they were processed

Good project documentation can substantially reduce the effort required to prepare replication materials.

## Future Topics

The following topics are still under discussion:

- Shared dataset stewardship
- Dataset versioning
- Canonical storage locations
- Archive policies
- Data lifecycle management
- Project offboarding