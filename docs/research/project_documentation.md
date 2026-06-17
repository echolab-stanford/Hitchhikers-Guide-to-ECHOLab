# GitHub Projects

## Overview

GitHub serves as the primary entry point for ECHOLab research projects.

ECHOLab maintains a shared GitHub organization where lab repositories can be stored, maintained, and transferred across researchers over time. Storing projects within the ECHOLab organization helps improve discoverability, continuity, and collaboration while reducing the risk that project resources become inaccessible when researchers leave the lab.

The goal of a project repository is not necessarily to contain all project materials. Instead, repositories should help current and future collaborators understand the project, locate key resources, and identify where project work is taking place.

A new collaborator should be able to use a project's repository to quickly answer:

- What is this project about?
- Where are the data?
- Where is the manuscript?
- Where are project discussions occurring?
- Who should I contact with questions?

## Recommended Repository Structure

ECHOLab maintains an [ECHOLab project template](https://github.com/echolab-stanford/echolab-newproject-template) to provide a lightweight starting point for new research projects.

The template provides a lightweight starting point for new projects and helps standardize project documentation across the lab.

Example:

```text
project-name/

README.md

code/
├── 01_processing/
└── 02_analysis/

data/
└── README.md
```

Researchers may adapt this structure as needed for their projects.

## Project README

The README should serve as the primary project landing page.

Recommended sections include:

- Project Overview
- Project Description
- Contributors
- Project Resources
- Contact

Example project resources:

- Notion
- Overleaf Drafts
- Project Data Directory Location
- Slack Channel
- Presentations
- Working Paper
- Published Paper
- Public Replication Repository

## Project Data Organization

Most projects will store large datasets, intermediate files, and outputs on Oak rather than GitHub.

Project repositories should document where project data are stored and how they are organized.

A typical Oak project directory might look like:

```text
project_name/
├── raw/
├── intermediate/
├── clean/
├── outputs/
└── documentation/
```

Exact organization may vary across projects. The goal is not to enforce a single structure, but to ensure that future collaborators can easily identify:

- Raw data inputs
- Intermediate processing outputs
- Analysis-ready datasets
- Figures and tables
- Documentation

The project README should indicate where project data are stored and provide links or paths to important directories when appropriate.


## GitHub and Other Tools

GitHub is one component of a broader project workflow.

Typical project resources may include:

| Resource | Purpose |
|-----------|-----------|
| GitHub | Project hub, documentation, and code |
| Notion | Project management and notes |
| Overleaf | Manuscript development |
| Oak | Shared data storage |
| Sherlock | High-performance computing |

Different tools serve different purposes:

- **GitHub** serves as the project's long-term entry point and source of institutional knowledge.
- **Notion** supports active project management and day-to-day collaboration.
- **Overleaf** supports manuscript development.
- **Oak** stores shared datasets and large project files.
- **Sherlock** provides computational resources for large analyses.

Because access to some Stanford-managed resources may change when researchers leave the lab or Stanford, project repositories should provide sufficient documentation and links that future collaborators can understand how a project was organized and where key resources are located.

## Repository Ownership

ECHOLab maintains a shared GitHub organization where lab repositories can be stored, maintained, and transferred across researchers over time.

Whenever possible, lab projects should be maintained within the ECHOLab GitHub organization rather than personal GitHub accounts. This helps improve discoverability, continuity, and collaboration while reducing the risk that project resources become inaccessible when researchers leave the lab.

The purpose of the ECHOLab GitHub organization is not to restrict ownership of research projects, but to provide a shared home for project resources and institutional knowledge.

Former lab members will retain access to the ECHOLab GitHub organization after leaving the lab. Continued access supports ongoing collaborations, manuscript revisions, and long-term maintenance of shared research products. Maintaining repositories within the organization helps ensure that projects remain accessible to both current researchers and lab alumni.

Personal repositories remain appropriate for exploratory work, software projects not associated with ECHOLab, and other individual efforts.

## Starting a New Project

Suggested workflow:

1. Create a repository from the [ECHOLab project template](https://github.com/echolab-stanford/echolab-newproject-template) within the ECHOLab GitHub organization.
2. Create a project directory on Oak.
3. Complete the project README.
4. Create project-specific collaboration and project management resources as needed (e.g., Notion page, Slack channel, shared notes, etc.).
5. Create an Overleaf project if applicable. 
6. Identify data storage locations.
7. Link project resources from the repository.

## Replication Materials

Project repositories are intended to support active research.

When a project reaches publication, replication materials may be distributed through a separate public repository. Good project organization throughout the research process can substantially reduce the effort required to prepare replication materials.