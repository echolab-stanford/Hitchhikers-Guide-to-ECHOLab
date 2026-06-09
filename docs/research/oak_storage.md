# Oak Storage

## Overview

Oak is Stanford's high-capacity research storage system and serves as ECHOLab's primary platform for shared data storage.

Most lab datasets, project data, and shared resources should be stored on Oak whenever practical. Researchers use Oak to store large datasets, share data across projects, and access resources from both local machines and Sherlock.

Within ECHOLab, Oak is generally considered the canonical location for shared data resources. While researchers may maintain local working copies of datasets, Oak should be treated as the primary source of truth for lab-managed data.

!!! note

```
Oak is ECHOLab's primary platform for shared data storage.

Researchers are encouraged to store shared datasets on Oak whenever practical rather than maintaining project-critical data solely on local machines.
```

## Why We Use Oak

Oak provides:

* Large-scale storage for research data
* Shared access across lab members
* Integration with Sherlock
* Backup and data management infrastructure
* A central location for long-term project resources

Because many projects rely on shared datasets, Oak plays a critical role in collaboration, reproducibility, and continuity within the lab.

## Oak in the ECHOLab Infrastructure

ECHOLab relies on several core platforms:

| Platform | Purpose                         |
| -------- | ------------------------------- |
| GitHub   | Code management and project hub |
| Oak      | Shared data storage             |
| Sherlock | Shared computing environment    |
| Overleaf | Manuscript development          |
| Notion   | Project management and planning |
| Slack    | Communication                   |

Researchers should generally be able to locate project code, data, manuscripts, and documentation by starting from a project's GitHub repository and following links to the relevant resources.

## Oak and Sherlock

Oak and Sherlock serve different roles within the ECHOLab computing environment.

* Oak is primarily used for data storage.
* Sherlock is primarily used for computation.

A common workflow is:

```text
Raw data on Oak
    ↓
Processing on Sherlock
    ↓
Outputs written back to Oak
    ↓
Analysis performed locally or on Sherlock
```

Researchers should become familiar with both systems early in their time in the lab.

For detailed guidance on Sherlock, see the ECHOLab Computing Guide.

---

# Working with Oak

## Core Principles

### Oak is the Canonical Source of Truth

Researchers may maintain local copies of datasets for performance, convenience, or offline work.

However:

* Shared datasets should live on Oak.
* Oak should be treated as the canonical source of truth.
* Local copies should be viewed as working copies.
* Important updates should be synchronized back to Oak.

The existence of a file on a researcher's laptop should not be assumed to imply that it has been shared with the rest of the lab.

### Local Mirrors Are Not Automatically Synchronized

Synchronization between Oak and local machines is generally an explicit action.

This means:

* New files created on Oak do not automatically appear on your laptop.
* New files created on your laptop do not automatically appear on Oak.
* Researchers are responsible for running synchronization commands when appropriate.

Always verify what will be transferred before performing large synchronization operations.

## Connecting to Oak

Many researchers find it convenient to mount Oak locally using SSHFS.

> TODO: Add current ECHOLab-recommended SSHFS setup instructions.

Topics to cover:

* Mounting Oak locally
* Unmounting Oak
* SSH key setup
* Avoiding repeated two-factor authentication
* Locating mounted drives

## Data Synchronization

Many ECHOLab researchers maintain local mirrors of large datasets and use `rsync` to synchronize files between Oak and local machines.

Recommended workflow:

1. Preview transfers with a dry run.
2. Verify expected changes.
3. Run the actual synchronization command.

> TODO: Add recommended ECHOLab rsync workflows and example aliases.

Topics to cover:

* Oak → Local synchronization
* Local → Oak synchronization
* Dry runs
* Common synchronization pitfalls
* Working with large datasets
* Oak ↔ Sherlock workflows

---

# Oak Permissions

## Overview

Shared Oak directories often use a permission structure that distinguishes between contributors and administrators.

Researchers may have permission to:

* Read files
* Create files
* Modify files
* Extend datasets

while lacking permission to:

* Move directories
* Rename directories
* Reorganize shared folder structures
* Modify access controls

This behavior is intentional and helps protect shared resources from accidental disruption.

## Governance and Permissions

Whenever practical, governance policies should align with Oak permissions.

Examples:

| Action                    | Contributor | Dataset Steward |
| ------------------------- | ----------- | --------------- |
| Add files                 | ✓           | ✓               |
| Update files              | ✓           | ✓               |
| Update documentation      | ✓           | ✓               |
| Rename shared directories |             | ✓               |
| Move shared directories   |             | ✓               |
| Modify permissions        |             | ✓               |

Researchers who need structural changes to shared resources should coordinate with the relevant dataset owner or steward.

> TODO: Add guidance on ACLs, ownership, and troubleshooting permission errors.

---

# Data Governance

## Shared Data Philosophy

Shared datasets are among ECHOLab's most valuable research assets.

The goal of ECHOLab's data management practices is to ensure that shared datasets are:

* Easy to find
* Easy to understand
* Easy to extend
* Easy to maintain
* Easy to reproduce

A researcher should be able to locate a shared dataset, understand how it was created, determine how it has changed over time, and use it in their own work without relying on institutional knowledge from the original creator.

Whenever practical, shared datasets should include:

* Documentation describing the data and its provenance
* Information about how the data were obtained or generated
* Changelogs documenting major updates
* Links to relevant code repositories or processing pipelines
* Identified maintainers or points of contact

The long-term objective is to ensure that shared data resources remain useful and maintainable even as researchers join and leave the lab.


## Shared vs Project-Specific Data

ECHOLab maintains both:

* Shared datasets used across multiple projects.
* Project-specific datasets maintained for individual projects.

These should be clearly distinguished whenever possible.

> TODO: Document recommended directory structures and naming conventions.

## Dataset Stewardship

Shared datasets should have designated maintainers.

Maintainers are responsible for:

* Documentation
* Versioning
* Permission management
* Structural changes

Contributors may extend datasets and update contents, but major reorganizations of shared resources should be coordinated with dataset maintainers.

> TODO: Develop dataset stewardship framework.

## Documentation Expectations

Shared datasets should include:

* README documentation
* Data dictionaries when practical
* Changelogs describing major updates
* Information on data provenance

Whenever data are added to a shared resource, documentation should be updated to record:

* Date of update
* Person making the update
* Description of changes
* Relevant code or data source information

> TODO: Create standard dataset README template.

---

# Common ECHOLab Workflows

> TODO

Potential examples:

* Working locally with a mounted Oak drive
* Synchronizing local mirrors with rsync
* Processing large datasets on Sherlock
* Maintaining shared datasets on Oak
* Collaborating across multiple projects using shared data resources

---

# Additional Resources

Official Stanford documentation:

* Oak Storage Overview
* Oak User Guide
* Oak Permissions Documentation

These resources describe the underlying storage system and institutional policies. The ECHOLab documentation focuses on lab-specific workflows, conventions, and best practices.

For detailed guidance on using Sherlock, see the ECHOLab Computing Guide.
