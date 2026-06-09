# Oak Access and Data Synchronization

## Overview

Oak is ECHOLab's primary platform for shared data storage. Most shared datasets, project data, and lab-maintained resources should be stored on Oak whenever practical.

Researchers commonly interact with Oak in one of three ways:

* Accessing data directly on Sherlock
* Mounting Oak as a local filesystem using SSHFS
* Synchronizing data between Oak and a local machine using rsync

This page provides guidance on common workflows used within ECHOLab.

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

---

### Local Mirrors Are Not Automatically Synchronized

Synchronization between Oak and local machines is generally an explicit action.

This means:

* New files created on Oak do not automatically appear on your laptop.
* New files created on your laptop do not automatically appear on Oak.
* Researchers are responsible for running synchronization commands when appropriate.

Always verify what will be transferred before performing large synchronization operations.

---

## Connecting to Oak

Many researchers find it convenient to mount Oak locally using SSHFS.

Example:

```bash
sshfs <SUNetID>@dtn.oak.stanford.edu:/oak/stanford/groups/<PI_SUNetID> ~/oak \
  -o cache=no \
  -o nolocalcaches \
  -o volname=oak-sshfs \
  -o defer_permissions
```

To unmount:

```bash
umount ~/oak
```

> TODO: Verify and update connection commands as Oak infrastructure evolves.

---

## Avoiding Repeated Two-Factor Authentication

Researchers may configure SSH keys to reduce the need for repeated authentication.

Typical workflow:

1. Generate an SSH key pair.
2. Add the public key to Oak.
3. Use the key for future connections.

> TODO: Expand with current recommended Oak SSH key procedures.

Note that inactive keys may expire and require recreation.

---

## Finding Your Mounted Oak Drive

On macOS:

```text
Cmd + Shift + G
```

Then navigate to:

```text
~/oak
```

---

## Data Synchronization with rsync

Many ECHOLab researchers use rsync to synchronize data between Oak and local machines.

Common workflow:

### Preview Changes First

Use a "dry run" before transferring data.

Example:

```bash
rsync -avzn --progress source destination
```

The `-n` flag previews changes without actually transferring files.

Dry runs help prevent accidental overwrites and make it easier to understand what a synchronization command will do.

---

### Synchronizing Oak → Local

Typical use cases:

* Creating a local working copy.
* Updating local files from Oak.
* Downloading newly added shared data.

Researchers should understand:

* Files are copied only when synchronization is run.
* Local files are generally not deleted automatically.
* New Oak files do not appear locally until synchronization occurs.

---

### Synchronizing Local → Oak

Typical use cases:

* Uploading processed data.
* Sharing new files with collaborators.
* Updating shared project resources.

Researchers should verify synchronization results before assuming files have been shared.

A file created locally remains local until explicitly synchronized to Oak.

---

## Oak Permissions

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

If you receive a "Permission denied" error while moving or renaming shared directories, contact the dataset owner or directory administrator.

---

## Shared Data Governance

Researchers should coordinate major structural changes to shared datasets with the dataset owner or designated steward.

Examples include:

* Renaming directories
* Moving directories
* Reorganizing shared folder structures
* Archiving datasets
* Modifying permissions

Contributors are generally encouraged to add data, update documentation, and extend datasets within established structures.

---

## Future Topics

The following topics should be expanded in future versions of this guide:

* Detailed SSH key setup
* Recommended rsync aliases
* Sherlock ↔ Oak workflows
* Common troubleshooting steps
* Oak permissions and ACLs
* Shared dataset stewardship
* Local mirror best practices
* Performance considerations for large datasets
