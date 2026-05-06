---
title: Near Real-Time Submission of Animal-Borne Ocean Profiles to the National Data Buoy Center
keywords: [ioos, metadata, netCDF, profiles, NDBC, GTS]
tags: [ioos, metadata, netCDF, profiles, NDBC, GTS]
toc: false
#permalink: index.html
summary: This page documents the process for submitting animal-borne ocean profile observations to NDBC
mermaid: true
---

# Ocean Profiles from Animal-borne Sensor Tags

This page documents the standard operating procedures for formatting and submitting near, real-time ocean profile data from animal-borne sensor tags that are registered with the Animal Telemetry Network. After quality control and formatting into BUFR, eligible profiles are submitted in near real-time to the National Data Buoy Center (NDBC), which then distributes the observations via the [Global Telecommunications System](https://community.wmo.int/site/knowledge-hub/programmes-and-initiatives/global-telecommunication-system-gts) (GTS). 


## Workflow Overview

At a high level, ocean profile data from animal-borne sensor tags are processed, converted to BUFR format, and conditionally submitted to the National Data Buoy Center (NDBC) for distribution via the Global Telecommunications System (GTS). Only observations collected within the near real-time submission window are eligible for submission.

The diagram below summarizes this workflow:

```mermaid

%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#007396',
      'primaryTextColor': '#fff',
      'primaryBorderColor': '#003087',
      'lineColor': '#003087',
      'secondaryColor': '#007396',
      'tertiaryColor': '#CCD1D1'
    }
  }
}%%

flowchart LR
    A[Animal-based profile data] --> B[Data preparation]
    B --> C[Convert to BUFR message<br/>+ Section 4 CSV]

    C --> D{Data generated<br/>within last 96 hours?}

    D -- Yes --> E[NDBC submission]
    D -- No --> F[Not submitted]

    E --> G[Global Telecommunications System (GTS)]
```


## Data Scope

## Data Scope

Profile data are submitted on a near real-time basis, with a target of within 24 hours of collection when possible. For operational purposes, only observations collected within the previous 96 hours are eligible for submission to the National Data Buoy Center (NDBC), as older data are not accepted by the Global Telecommunications System (GTS).

Profile data older than this window may still be archived and served through other ATN or IOOS-supported data access pathways (e.g., NCEI, ERDDAP), but they are not submitted to NDBC or distributed via the GTS.

Operationally, profile data from deployments marked for submission to NDBC are converted to BUFR messages on an ongoing basis throughout the deployment period. Generated BUFR messages are made available through a public [Web Accessible Folder (WAF)](https://ndbc-bufr.srv.axds.co/platforms/atn/smru/).

Once BUFR messages are generated, they are evaluated using an NDBC submission checker and, when eligible, pushed to NDBC via secure file transfer (SFTP) for pickup and processing. Near real-time data distributed through NDBC can be accessed via the NDBC [real-time data access services](https://www.ndbc.noaa.gov/faq/rt_data_access.shtml).

At present, only profile data from Sea Mammal Research Unit manufactured tags are submitted through this workflow. Support for additional manufacturers and tag types may be incorporated in the future.


## BUFR Conversion

Each eligible profile from an active deployment is converted into an individual BUFR message following World Meteorological Organization (WMO) BUFR v39 tables. A corresponding BUFR Section 4 descriptor record is also generated in CSV format to support human-readable inspection of encoded values without requiring a BUFR decoder. 


### Pre-processing Steps

For each available profile:
- Read the source data file (Parquet or netCDF)
- Extract a single target profile
- Coerce depth (z) values to numeric
- Remove duplicate (profile, time, depth) records
- Sort observations by time and depth
- Truncate profile identifiers to a maximum of 8 characters, as required by BUFR field constraints

**Quality Control Note:**  
Standard QARTOD quality control checks are applied to the ocean profile observations (e.g. temperature, salinity) prior to BUFR encoding. At present, QARTOD flag values are not yet mapped to BUFR-required quality indicator fields. This mapping may be added in a future update.


### Encoding Outputs

Profiles are encoded using [`bufrtools`](https://github.com/axiom-data-science/bufrtools), producing:
- A BUFR message file
- A Section 4 CSV diagnostic file


### Example Conversion

The following example code illustrate how BUFR encoding and Section 4 extraction are performed using `bufrtools`.

1. Create a BUFR message for profile data, `df`:

```
from bufrtools.encoding.wildlife_computers import encode

random_uuid = uuid # random unique identifier associated with this profile deployment
random_ptt_id = ptt_id # from metadata

encode(profile_dataset=df, output="profiles.bufr", uuid=random_uuid, ptt=random_ptt_id)
```

2. Get Section 4 Records of the BUFR Message:
```
from bufrtools.encoding.wildlife_computers import get_section4

records = get_section4(df, random_uuid)
```

BUFR Messages will be created if
* The deployment's Platform Terminal Transmitter (PTT) attribute is filled out in ATN Data Registration (ADR) portal
* The deployment has at least one of  `wmo_platform_code` or `wigos_platform_code` set to a non-empty value in ADR
* The 'send to NDBC' flag is checked for this deployment in the ADR



## Submitting to NDBC

Submission decisions are made at the individual profile level. A BUFR message is submitted to NDBC via SFTP when all of the following criteria are met:
- The profile contains at least one observation
- The data were collected within the previous 96 hours
- Required deployment metadata and submission flags are present

The time window guards against sending stale data to the GTS which only accepts near real-time observations.

For data that meet these criteria for submission, the status of submission is tracked on this dashboard: https://atn-submission-dashboard.srv.axds.co/.

Note: the SFTP folder is not a final repository for the data and may occasionally be cleared as part of normal NDBC workflow once submitted to the GTS. Users seeking historical ATN profile data should access those datasets through ATN or IOOS-supported data repositories rather than NDBC (e.g. NCEI, ERDDAP).