# PurpleAir Sensor Data

## At a Glance

**Description:**
Historical PurpleAir air quality sensor data, including raw downloads, intermediate processing outputs, and cleaned analysis-ready datasets.

**Coverage:**
Global PurpleAir sensor network (US and non-US sensors).

**Time Period:**
Varies by sensor; coverage extends from the earliest available PurpleAir observations through the most recent download.

**Unit of Observation:**
Sensor-hour.

**Approximate Size:**
~22,000 sensor files, ~56 GB of raw data. *(Needs updating as the archive grows.)*

**Maintainer:**
NAME, EMAIL

**Last Updated:**
6/16/2026

## Overview

This dataset contains raw, intermediate, and cleaned PurpleAir (PA) air quality sensor data for use within ECHOlab and collaborators.

All data were downloaded via the PurpleAir historical API and processed on the Stanford Sherlock HPC cluster.

## Sources

* PurpleAir Historical API
* PurpleAir Sensor Registry

## Coverage

### Geography

Global coverage including both US and non-US PurpleAir sensors.

### Time Period

Coverage varies by sensor. Data are updated periodically as new downloads are performed.

## Unit of Observation

The primary analysis-ready dataset consists of hourly observations for individual PurpleAir sensors.

## Key Variables

Selected variables in the cleaned dataset include:

| Variable         | Description                |
| ---------------- | -------------------------- |
| sensor_index     | PurpleAir sensor ID        |
| pm25             | Hourly PM2.5 concentration |
| pm_corrected     | EPA-corrected PM2.5        |
| humidity         | Relative humidity          |
| temp             | Temperature                |
| time_stamp_utc   | UTC timestamp              |
| time_stamp_local | Local timestamp            |

See the full column dictionary below for additional variables.

## File Structure

### Top-Level Organization

```text
PurpleAir/
├── raw/
│   ├── la_counties_sensors/
│   ├── non_us_sensors/
│   ├── us_indoor_sensors/
│   ├── us_outdoor_sensors/
│   ├── sensors_index_YYYYMMDD.csv
│   └── sensors_index_old/
├── V1/
├── intermediate/
│   ├── exploratory/
│   ├── processing/
│   └── orig_files/
└── clean/
    ├── non_us_indoor/
    ├── non_us_outdoor/
    ├── us_indoor/
    └── us_outdoor/
```

### raw/

Downloaded sensor data and metadata.

#### Sensor Index Crosswalk

```text
raw/
└── sensors_index_YYYYMMDD.csv
```

One or more dated snapshots of the full PurpleAir sensor registry. Each file contains one row per sensor with metadata including:

* sensor_index
* last_modified
* date_created
* last_seen
* name
* location_type
* uptime
* position_rating
* latitude
* longitude
* altitude
* geometry
* us

The most recent file is used as the crosswalk for processing.

#### Individual Sensor Time Series

```text
raw/
├── us_indoor_sensors/
│   └── ID_{sensor_index}_indoor.csv
├── us_outdoor_sensors/
│   └── ID_{sensor_index}_outdoor.csv
└── non_us_sensors/
    └── ID_{sensor_index}.csv
```

One CSV file per sensor containing the raw historical time series. Each file includes columns such as:

* time_stamp (UTC)
* pm2.5_cf_1_a
* pm2.5_cf_1_b
* temperature
* humidity

### V1/

Previous versions of cleaned sensor datasets retained for reproducibility of earlier projects.

### intermediate/

Contains processing outputs and data quality tracking files generated during the cleaning pipeline.

```text
intermediate/
└── processing/
    ├── us_indoor/
    │   ├── missing_hours.parquet
    │   └── coverage_tracker.parquet
    ├── us_outdoor/
    │   ├── missing_hours.parquet
    │   └── coverage_tracker.parquet
    └── non_us_indoor/
        ├── missing_hours.parquet
        └── coverage_tracker.parquet
```

#### missing_hours.parquet

One row per contiguous gap in a sensor's hourly time series.

| Column          | Description                         |
| --------------- | ----------------------------------- |
| sensor_index    | PurpleAir sensor ID                 |
| gap_start       | Start of missing-hour run           |
| gap_end         | End of missing-hour run             |
| n_missing_hours | Number of consecutive missing hours |

#### coverage_tracker.parquet

One row per sensor summarizing temporal coverage.

| Column        | Description                      |
| ------------- | -------------------------------- |
| sensor_index  | PurpleAir sensor ID              |
| first_year    | First year with data             |
| last_year     | Last year with data              |
| n_years       | Number of distinct years present |
| years_present | Comma-separated list of years    |

### clean/

Analysis-ready hourly datasets.

Hourly aggregated, quality-controlled sensor data. All timestamps are retained in both UTC and local time. PM2.5 values include both raw sensor averages and EPA-corrected values.

```text
clean/
├── us_indoor/
│   └── {YYYY}/
│       └── PA_indoor_{MM}.parquet
├── us_outdoor/
│   └── {YYYY}/
│       └── PA_outdoor_{MM}.parquet
└── non_us_indoor/
    └── {YYYY}/
        └── PA_indoor_{MM}.parquet
```

**Example:**
`clean/us_outdoor/2021/PA_outdoor_07.parquet`

## Data Processing

Data are downloaded from the PurpleAir Historical API and processed through a multi-stage pipeline that:

* Downloads and stores raw sensor observations
* Harmonizes metadata across sensors
* Identifies missing data periods
* Performs quality-control checks
* Aggregates observations to hourly resolution
* Applies EPA correction factors
* Creates analysis-ready parquet datasets

### Column Dictionary

| Column           | Type    | Description                |
| ---------------- | ------- | -------------------------- |
| sensor_index     | integer | PurpleAir sensor ID        |
| date_utc         | Date    | Observation date (UTC)     |
| hour_utc         | integer | Observation hour (UTC)     |
| humidity         | numeric | Relative humidity (%)      |
| temp             | numeric | Temperature (°F)           |
| pm25             | numeric | Hourly PM2.5 concentration |
| pm_corrected     | numeric | EPA-corrected PM2.5        |
| time_stamp_utc   | POSIXct | UTC timestamp              |
| time_stamp_local | POSIXct | Local timestamp            |
| date_local       | Date    | Local date                 |
| hour_local       | integer | Local hour                 |

### PM2.5 Quality Control Notes

* Dual-channel sensors (most outdoor) use the average of channels A and B.
* Observations are set to missing when both scale-difference and level-difference thresholds are exceeded.
* Single-channel sensors (most indoor) use the A channel directly.
* Sensors absent from the crosswalk index receive missing local time variables.

### How to Load in R

```r
library(arrow)
library(dplyr)

# Load a single month
df <- read_parquet("clean/us_outdoor/2021/PA_outdoor_07.parquet")

# Load a full year
ds <- open_dataset("clean/us_outdoor/2021/")
df <- ds |>
  filter(sensor_index == 12345) |>
  collect()
```

## Access and Restrictions

This dataset is intended for use within ECHOlab and collaborators. Users should consult PurpleAir terms of service and data-use policies when redistributing data.

## Related Resources

* PurpleAir download pipeline
* PurpleAir processing pipeline
* PurpleAir Historical API
* Related publications

## Notes and Known Limitations

* Sensor coverage varies substantially across sensors and locations.
* Sensors not present in the crosswalk index will have missing local time fields and location information.
* Data quality and sensor uptime vary across sensors.
* Additional limitations may be identified as the archive continues to grow.

## Contact

Contact NAME (EMAIL) with questions regarding the dataset.

## References

Barkjohn, K.K., Gantt, B., & Clements, A.L. (2021). Development and application of a United States-wide correction for PM2.5 data collected with the PurpleAir sensor. *Atmospheric Measurement Techniques*, 14, 4617–4637.

Barkjohn, K.K., Holder, A.L., Frederick, S.G., & Clements, A.L. (2022). Correction and accuracy of PurpleAir PM2.5 measurements for extreme wildfire smoke. *Sensors*, 22(24), 9669.

**Note on `pm_corrected`:** The correction equations follow Barkjohn et al. (2022), which extends the original US-wide correction with adjustments for extreme wildfire smoke concentrations.
