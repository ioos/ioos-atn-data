---
title: Submission of Profiles to the National Data Buoy Center
keywords: [ioos, metadata, netCDF, archive, NCEI]
tags: [ioos, metadata, netCDF, archive, NCEI]
toc: false
#permalink: index.html
summary: This page documents the process for archiving the ATN observations at NCEI.
mermaid: true
---

# Ocean Profiles from Animal-borne Sensor Tags

This page documents the standard operating procedures for formatting and submitting ocean profile data from animal-borne sensor tags that are registered with the Animal Telemetry Network. Once these data are formatted into BUFR and quality controlled with QARTOD, they are submitted in near real-time to the National Data Buoy Center (NDBC) for incorporation into the [Global Telecommunications System](https://community.wmo.int/site/knowledge-hub/programmes-and-initiatives/global-telecommunication-system-gts) (GTS). 




## Data Scope

Data are submitted near real-time, or within 24 hours of profile data collection by the animal-borne tag, but within a maximum of 10 days. Data older than this is not useful for the Global Telecommunication System.

Profile data from deployments marked for submission to NDBC will be converted to BUFR messages throughout the deployment period and made accessible on a [WAF](https://ndbc-bufr.srv.axds.co/platforms/atn/smru/). 

Once the BUFR messages are generated, it will go through a NDBC submission checker, and pushed to NDBC via FTP for pickup.

Data can be accessed [here](https://www.ndbc.noaa.gov/faq/rt_data_access.shtml) on the NDBC website.

Currently we are only submitting profile data from SMRU data. But eventually we'll want to integration additional manufacturers and tag types

## BUFR Conversion

Each profile generated from the active deployment is converted into a BUFR message. A BUFR Section 4 descriptor record in CSV format will also be generated, serving as a diagnostic companion to the BUFR message that makes the encoded data values human-readable without needing a BUFR decoder.

The formatting follows the World Meteorological Organization (WMO) updated v.39 tables. Conversion is done using [`bufrtools`](https://github.com/axiom-data-science/bufrtools).

For each profile available,
1. Read data file (parquet or netCDF) and query for the single target profile
2. Coerce depth (z) to numeric, drops duplicate (profile, time, z) rows, and sorts by time then z.
3. Truncate profile id is only 8 characters maximum because the field is limited to 64 bits (8 bytes)
4. Encode dataframe into a BUFR message using [`bufrtools`](https://github.com/axiom-data-science/bufrtools); see `bufrtools` documentation for implementation


Create a BUFR message for profile data, `df`:

```
from bufrtools.encoding.wildlife_computers import encode

random_uuid = uuid # random unique identifier associated with this profile deployment
random_ptt_id = ptt_id # from metadata

encode(profile_dataset=df, output="profiles.bufr", uuid=random_uuid, ptt=random_ptt_id)
```

Get Section 4 Records of the BUFR Message:
```
from bufrtools.encoding.wildlife_computers import get_section4

records = get_section4(df, random_uuid)
```

BUFR Messages will be created if
* The deployment's PTT attribute is filled out in ADR
* The deployment has at least one of  `wmo_platform_code` or `wigos_platform_code` set to a non-empty value in ADR
* The 'send to NDBC' flag is checked for this deployment in the ADR


**NOTE: ADD SOMETHING ABOUT QC? WE APPLY IT BUT FLAGS ARE NOT CONVERTED TO BUFR REQUIRED QC FIELDS YET..**

## Submitting to NDBC

Data that meet the following criteria are submitted to NDBC via their SFTP server (requires authentication) for incorporation into GTS:
* at least one observation collected in the profile data
* data was collected in the last 96 hours

The time window guards against sending stale data to the GTS which only accepts near real-time observations.

For data that meet these criteria for submission, the status of submission is tracked on this dashboard: https://atn-submission-dashboard.srv.axds.co/.

Note: the SFTP folder is not a final repository for the data and may occasionally be cleared as part of normal NDBC workflow once submitted to the GTS.