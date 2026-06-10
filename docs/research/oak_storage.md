# Oak Storage

## Overview

Oak is Stanford's high-capacity research storage system and serves as ECHOLab's primary platform for shared data storage.

Most lab datasets, project data, and shared resources should be stored on Oak whenever practical. Researchers use Oak to store large datasets, share data across projects, and access resources from both local machines and Sherlock.

Within ECHOLab, Oak is generally considered the canonical location for shared data resources. While researchers may maintain local working copies of datasets, Oak should be treated as the primary storage location for lab-mangaed data.

!!! note

```
Oak is ECHOLab's primary platform for shared data storage.

Researchers are encouraged to store shared datasets relaed to shared projects on Oak whenever practical rather than maintaining shared project-critical data solely on local machines.
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

For detailed guidance on Sherlock, see the [ECHOLab Computing Guide](computing.md).

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

Note that synchronization between Oak and local machines is generally an explicit action.

This means:

* New files created on Oak do not automatically appear on your laptop.
* New files created on your laptop do not automatically appear on Oak.
* Researchers are responsible for running synchronization commands when appropriate.

Always verify what will be transferred before performing large synchronization operations.

## Connecting to Oak

It is sometimes convenient to access Oak directly from your local machines using SSHFS. Mounting Oak locally can make it easier to browse files, inspect datasets, and work with project resources without repeatedly copying data between systems.

Typical setup steps include:

1. Configure SSH access to Oak.
2. Create a local mount point (e.g., `~/oak`).
3. Mount Oak using SSHFS.
4. Configure SSH keys to reduce repeated two-factor authentication prompts.
5. Access Oak through Finder or the command line.

Researchers who regularly work with Oak may find it helpful to create shell aliases for mounting and unmounting Oak.

Example workflow:

```text
Local Machine
      ↓
 Mount Oak with SSHFS
      ↓
 Access files through ~/oak
      ↓
 Synchronize data as needed with rsync
```

Oak can also be accessed directly through SSH and rsync without mounting the filesystem locally. This approach is often more reliable for large file transfers and automated workflows.

For current Stanford-specific setup instructions, see the official Oak documentation.


### Synchronization Best Practices

Researchers may maintain local working copies of datasets while storing shared resources on Oak.

When synchronizing files:

* Use dry runs before large transfers whenever possible.
* Verify that files are moving in the expected direction.
* Be especially cautious when overwriting or deleting files.
* Remember that synchronization is not automatic.
* Confirm that important local work has been copied back to Oak.

In general, Oak should be treated as the authoritative copy of shared project data, while local copies should be treated as working copies.


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

## Related Resources

- [Working with Oak](working_with_oak.md)
- [Managing Shared Data](data_governance.md)
- [Official Oak Documentation](https://docs.oak.stanford.edu/user-guide/)

These resources describe the underlying storage system and institutional policies. The ECHOLab documentation focuses on lab-specific workflows, conventions, and best practices.

For detailed guidance on using Sherlock, see the [ECHOLab Computing Guide](computing.md)
