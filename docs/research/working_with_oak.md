# Oak Access and Data Synchronization

## Overview

Oak is ECHOLab's primary platform for shared data storage.

Researchers commonly interact with Oak in one of three ways:

* Accessing data directly from Sherlock
* Mounting Oak locally using SSHFS
* Synchronizing data between Oak and a local machine using `rsync`

This page focuses on practical workflows for accessing and working with Oak.

For information on Oak's role within ECHOLab, data governance expectations, permissions, and storage philosophy, see the [Oak Storage](oak.md) guide.

!!! note

```
Oak resources are organized by PI. If you have not yet been added to the `mburke` Oak allocation, contact Sam.
```

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

### Simplifying SSH Access

Researchers who regularly use Oak or Sherlock are encouraged to configure a local SSH configuration file.

Benefits include:

* Connecting using short aliases such as `ssh oak` and `ssh sherlock`
* Reusing existing authenticated connections across multiple terminals
* Reducing repeated Duo prompts
* Simplifying `rsync`, `scp`, SSHFS, and VS Code workflows

See the [SSH Configuration Guide](ssh_configuration.md) for setup instructions.

---

### Simplifying SSH Access

Researchers who regularly use Oak or Sherlock are strongly encouraged to configure a local SSH configuration file.

Benefits include:

* Connecting using short aliases such as `ssh oak` and `ssh sherlock`
* Reusing authenticated SSH connections across multiple terminals
* Reducing repeated Duo prompts
* Simplifying SSHFS, `rsync`, `scp`, and VS Code workflows

See [SSH Configuration Guide](ssh_configuration.md) for setup instructions.

## Finding Your Mounted Oak Drive

On macOS:

```text
Cmd + Shift + G
```

Then navigate to:

```text
~/oak
```

If desired, you can add the mounted directory to Finder favorites for easier access.

---

## Data Synchronization with rsync

Many ECHOLab researchers use `rsync` to synchronize data between Oak and local machines.

### Preview Changes First

Before large transfers, perform a dry run:

```bash
rsync -avzn --progress source destination
```

The `-n` flag previews changes without actually transferring files.

Dry runs help prevent accidental overwrites and make it easier to understand exactly what a synchronization command will do.

---

### Synchronizing Oak → Local

Common use cases:

* Creating a local working copy
* Updating local files from Oak
* Downloading newly added shared datasets

Researchers should remember that files are copied only when synchronization is run. New files added to Oak will not automatically appear on local machines.

---

### Synchronizing Local → Oak

Common use cases:

* Uploading processed data
* Sharing new files with collaborators
* Updating shared project resources

Files created locally remain local until they are explicitly synchronized to Oak.

Always verify that important files have been transferred successfully before assuming they are available to collaborators.

---

## Common Workflow

A typical ECHOLab workflow looks something like:

```text
Shared datasets stored on Oak
            ↓
Processing and analysis on Sherlock
            ↓
Outputs written back to Oak
            ↓
Results synchronized locally as needed
```

Researchers should become comfortable moving data between Oak, Sherlock, and local machines early in their time in the lab.

---

## Future Topics

Potential future additions:

* Recommended rsync aliases
* Sherlock ↔ Oak workflows
* Common troubleshooting steps
* SSHFS troubleshooting
* Performance considerations for large datasets
* Strategies for maintaining local mirrors
