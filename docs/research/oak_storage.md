# Oak Storage

## Overview

Oak is Stanford's high-capacity research storage system and serves as ECHOLab's primary platform for shared data storage.

Most lab datasets, project data, and shared resources should be stored on Oak whenever practical. Researchers use Oak to store large datasets, share data across projects, and access resources from both local machines and Sherlock.

Within ECHOLab, Oak is the canonical location for shared datasets and shared project resources. While researchers may maintain local working copies of datasets, Oak should be treated as the primary storage location for lab-managed data.

!!! note

```
Oak is ECHOLab's primary platform for shared data storage.

Researchers are encouraged to store shared datasets related to shared projects on Oak whenever practical rather than maintaining project-critical data solely on local machines.
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

---

## Data Governance

ECHOLab maintains a separate guide describing expectations for managing shared datasets, maintaining canonical copies, minimizing duplication, and documenting shared resources.

See [Managing Shared Data](data_governance.md).

---

## Related Resources

* [Working with Oak](working_with_oak.md)
* [Managing Shared Data](data_governance.md)
* [SSH Configuration Guide](ssh_configuration.md)
* [Official Oak Documentation](https://docs.oak.stanford.edu/user-guide/)

For detailed guidance on using Sherlock, see the [ECHOLab Computing Guide](computing.md).
