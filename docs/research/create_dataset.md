# Creating a Shared Dataset

## Overview

Shared datasets are most useful when future researchers can understand and use them without relying on the original creators.

The goal is not to document every detail of data processing, but to provide enough information that future collaborators can understand what the dataset contains, where it came from, and how it should be used.

Every shared dataset should include a README describing those key elements.


## What Should Be Shared?

Different datasets require different levels of processing and documentation.

The answers will differ across datasets. Some shared datasets may consist primarily of raw data, while others may include multiple processed versions. Not every file needs to become a shared dataset. The goal is not necessarily to store every intermediate file. The goal is to preserve the highest-value outputs that would be costly for future researchers to recreate. 


### Raw Data

For some datasets, maintaining a shared copy of the raw data can reduce duplication of effort and ensure that researchers are working from a common source.

Examples include:

* ERA5 climate data
* Administrative records
* Survey microdata
* Satellite products

Even when raw data can be downloaded from external sources, maintaining a local copy may save substantial time and computing resources.

### Processed Data

If substantial processing, harmonization, quality control, or aggregation is required, researchers should consider sharing processed versions of the data in addition to the raw inputs.

Examples include:

* Cleaned and harmonized PurpleAir sensor data
* Harmonized DHS datasets
* Aggregated climate exposure datasets
* Survey crosswalks

### Analysis Datasets

Project-specific analysis files are typically not appropriate for long-term shared storage unless they are likely to be reused by multiple future projects. Those datasets can be stored in project/ specific directories.


## Recommended Structure for Shared Data

```text
dataset_name/
├── README.md
├── data/
├── code/
└── documentation/
```

Exact organization may vary, but every shared dataset should include documentation.

## Minimum Documentation

Each shared dataset should include a README describing:

* Dataset name
* Brief description
* Data source(s)
* Geographic coverage
* Temporal coverage
* Unit of observation
* Key variables
* File structure
* Access restrictions
* Contact person
* Related projects or publications

Future users should be able to determine whether the dataset is relevant before downloading or opening large files.

## Example Documentation

The template below provides a minimum structure for documenting a shared dataset. Researchers are encouraged to adapt it as needed.

For an example of a completed dataset README, see:

* [PurpleAir Sensor Data README (example completed dataset documentation)](PurpleAir_readme_example.md)

The example illustrates:

* Dataset overview
* Folder structure
* Variable documentation
* Data quality procedures
* Reproducibility information
* Known limitations
* References and related resources

Reviewing an existing dataset README is often the easiest way to understand the level of detail that is expected.

## Dataset README Template

Every shared dataset should include a README. The goal is not to document every processing step, but to provide enough information that future collaborators can understand what the dataset contains, where it came from, and how it should be used.

### Template

```md
# Dataset Name

## At a Glance

**Description:**  
One- or two-sentence description of the dataset.

**Coverage:**  
Countries, regions, or geographic units included.

**Time Period:**  
Years or dates covered.

**Unit of Observation:**  
Examples: individual, household, survey cluster, grid cell, county-year.

**Approximate Size:**  
Number of observations, files, or storage size.

**Maintainer:**  
Name and contact information.

## Overview

Brief description of the dataset and its intended use.

## Sources

- Source 1
- Source 2

## Coverage

### Geography

Countries, regions, or spatial units included.

### Time Period

Years or dates covered.

## Unit of Observation

Examples:

- Individual
- Household
- Survey cluster
- Administrative unit
- Grid cell
- Country-year

## Key Variables

| Variable | Description |
|-----------|-------------|
| var1 | Description |
| var2 | Description |

## File Structure

Describe the files included and their purpose.

## Data Processing

Brief summary of major processing steps.

## Access and Restrictions

Any licensing, confidentiality, or access considerations.

## Related Resources

- GitHub repository
- Data processing pipeline
- Documentation
- Publications
- Project pages

## Contact

Person most familiar with the dataset.
```

## Guiding Principle

A future collaborator should be able to answer the following questions without contacting the dataset creator:

* What is this dataset?
* Where did it come from?
* What does it contain?
* How should it be used?
* Who should I contact if I have questions?

If the answer to those questions exists only in someone's memory, the dataset is not fully documented.


