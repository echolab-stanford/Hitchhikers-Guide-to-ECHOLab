# Project Setup and Organization

This page describes how to set up the core ECHOLab infrastructure for a new research project.

Suggested workflow:

1. Choose a Project Name
2. Create a GitHub repository from the [ECHOLab project template](https://github.com/echolab-stanford/echolab-newproject-template). The new repository should be created within the ECHOLab GitHub organization at github.com/echolab-stanford/project-name. Complete the project README before beginning substantive work.
3. Create a project directory in Oak at /oak/stanford/groups/mburke/projects/project-name. 
4. Create a Slack channel, Notion page, Overleaf project, if needed, titled project-name. For any tools you plan to use link/reference them from the GitHub README.

The GitHub repository should serve as the project's primary entry point and should link to other project resources such as Oak directories, Notion pages, Slack channels, and Overleaf projects.

Whenever practical, use the same project name across GitHub, Oak, Slack, Notion, Overleaf, and other project resources. Consistent naming makes projects easier to discover and reduces confusion over time.

Each step is described in more detail below.

## 1. Choose a Project Name

Every project should have a reasonably short project-name that can be used across platforms.

* Use lowercase letters, numbers, and hyphens.
* Use hyphens (`-`) rather than underscores (`_`) for project and directory names.
* Use underscores for coding variables if needed.
* Avoid spaces.
* Avoid special characters.
* Make the name specific enough to distinguish it from other projects.
* Choose a name that can be reused across GitHub, Oak, Sherlock, Notion, Overleaf, and documentation.

Examples:

- `wildfire-air-quality` initially appears descriptive, but could plausibly refer to several different projects.
- `temp-mortality` is similarly too broad.

More specific names such as:

- `temp-mortality-global-byage`
- `temp-under5-mortality-dhs-ssa`

are less likely to be confused with other projects and are more informative to future collaborators.
A useful test is whether a new lab member who understands the project's general goals could correctly match the project to its name from a list of active ECHOLab projects.

It will likely be useful to discuss potential names with others in lab, particularly Marshall or Sam, who have more familiarity with past projects that project names could potentially be confused with.



## 2. Create a GitHub Repo

Once you have a project name you can create a GitHub repo. GitHub serves as the primary entry point for ECHOLab research projects.

ECHOLab maintains a shared GitHub organization where lab repositories can be stored, maintained, and transferred across researchers over time. Storing projects within the ECHOLab organization helps improve discoverability, continuity, and collaboration while reducing the risk that project resources become inaccessible when researchers leave the lab.

The goal of a project repository is not necessarily to contain all project materials. Instead, repositories should help current and future collaborators understand the project, locate key resources, and identify where project work is taking place.

A new collaborator should be able to use a project's repository to quickly answer:

- What is this project about?
- Where are the data?
- Where is the manuscript?
- Where are project discussions occurring?
- Who should I contact with questions?

### Recommended Repository Structure

ECHOLab maintains an [ECHOLab project template](https://github.com/echolab-stanford/echolab-newproject-template) to provide a lightweight starting point for new research projects.

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

### Project README

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


## GitHub Repository Ownership

Whenever possible, ECHOLab projects should be maintained within the ECHOLab GitHub organization rather than personal GitHub accounts.

Maintaining repositories within the organization improves discoverability, continuity, and collaboration while reducing the risk that project resources become inaccessible when researchers leave the lab.

Former lab members generally retain access to ECHOLab repositories after leaving the lab, supporting ongoing collaborations and long-term maintenance of research products.

Personal repositories remain appropriate for exploratory work, software projects not associated with ECHOLab, and other individual efforts.


## 3. Create a project directory on Oak (if applicable) and verify it has shared permissions

Most projects will store large datasets, intermediate files, and outputs on Oak rather than GitHub.

Create a directory for this purpose at /oak/stanford/groups/mburke/projects/project-name. Use the same project name chosen in Step 1.

!!! warning

    When creating a directory on Oak for a shared project, **ensure that the directory is configured with shared permissions rather than the default private permissions**.

    Private project directories can be difficult to manage after researchers leave the lab, making it harder to access, reorganize, archive, or remove project resources.

    If you are unsure how to configure permissions, ask Ivan or Sam.

A typical Oak project directory might look like:

```text
project-name/
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


## 4. Setup Additional Project Resources as Necessary for the Specific Project

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

## Replication Materials

Project repositories are intended to support active research.

When a project reaches publication, replication materials may be distributed through a separate public repository. Good project organization throughout the research process can substantially reduce the effort required to prepare replication materials.




## Project Setup Checklist

Before beginning substantial work, verify that:

- [ ] A project name has been selected.
- [ ] A GitHub repository exists.
- [ ] The project README has been completed.
- [ ] An Oak project directory has been created (if needed).
- [ ] Oak permissions have been configured appropriately.
- [ ] Key project resources are linked from the README.
- [ ] Collaborators have access to required resources.