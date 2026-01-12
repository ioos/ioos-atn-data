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

This page documents the standard operating procedures for formatting and submitting ocean profile data from animal-borne sensor tags that are registered wtih the Animal Telemetry Network. Once these data are formatted into BUFR and quality controlled with QARTOD, they are submitted in near real-time to the National Data Buoy Center (NDBC) for incorporation into the [Global Telecommunications System](https://community.wmo.int/site/knowledge-hub/programmes-and-initiatives/global-telecommunication-system-gts) (GTS). 



## BUFR Format

The formatting follows the World Meteorological Organization (WMO) updated v.39 tables. Conversion is done using [`bufrtools`](https://github.com/axiom-data-science/bufrtools).

## Near Real-Time

Data are submitted within 24 hours of profile data collection by the animal-borne tag, but within a maximum of 10 days. Data older than this is not useful for the Global Telecommunication System.

Data are made available [here](https://ndbc-bufr.srv.axds.co/platforms/atn/smru/) and pushed to NDBC via FTP for pickup (https://axds.atlassian.net/browse/ATN-19).

Data can be accessed [here](https://www.ndbc.noaa.gov/faq/rt_data_access.shtml) on the NDBC website.

## Scope

Currently we are only submitting profile data from SMRU data. But eventually we'll want to integration additional manufacturers and tag types