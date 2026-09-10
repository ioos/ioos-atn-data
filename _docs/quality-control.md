---
title: "ATN Satellite Telemetry Quality Control"
keywords: [ioos, metadata, netCDF, quality control, QC]
tags: [ioos, metadata, netCDF, quality control, QC]
toc: false
#permalink: index.html
summary: This page documents the quality control protocols for ATN observation in the IOOS ATN Data Assembly Center
mermaid: true 
---

## Quality Control Protocols

ATN DAC quality control (QC) protocols handle animal trajectory and dive profile data and use the `ioos_qc` Python package (see [docs](https://ioos.github.io/ioos_qc/)) to implement multiple QARTOD tests and an aggregate rollup flag. 

The following `ioos_qc` tests are applied: 
* [`ioos_qc.argo.speed_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.argo.speed_test)
* [`ioos_qc.qartod.location_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.qartod.location_test)
* [`ioos_qc.qartod.gross_range_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.qartod.gross_range_test)

The Location and Speed tests are applied to trajectory data only, while the Gross Range Test is applied to temperature and salinity profile observations. Data are not removed during the QC step, but the QC flag results are included in the processed datasets. 

**Quality Control Flags and Definitions**

| Flag | Meaning |
|------|---------|
| 1 | PASS - Data passed all QC tests |
| 2 | NOT_EVALUATED - Test not performed |
| 3 | SUSPECT - Data questionable, use with caution |
| 4 | FAIL - Data failed QC, should not be used |
| 9 | MISSING - Data is missing |

Prior to applying the quality control protocols, raw trajectory and profile data for each deployment are first truncated based on deployment start and end dates provided in the metadata. This is a necessary data cleaning step since telemetry tags are often activated and begin pinging their locations before and after they are attached to the animal and officially "deployed". These out-of-bounds locations may appear either on land or at sea.

Processed, tidy data with QC flags are then submitted to a variety of downstream locations and repositories including the ATN Portal, NDBC for integration into the GTS, NCEI, and ERDDAP for increased data accessibility and archival. Please see the [ATN DAC Flow Overview](https://ioos.github.io/ioos-atn-data/overview.html) for more details.

### Raw Data Tidying

The `ioos_qc.axds.valid_range_test()` is applied to the raw trajectory and profile data to keep only data falling within valid deployment dates. Typically, this data cleaning step involves checking the ingested data against provider-supplied start and end deployment dates, if available. While the raw data will retain the data falling outside the deployment dates, only the clean deployment data will visualized on the ATN Portal and submitted to downstream national repositories such as NCEI and ERDDAP.

Valid start and end deployment dates are either accessed from manually submitted deployment information saved in the [ATN Data Registration portal (ADR)](https://dacregistration.atn.ioos.us/) or directly from the upstream data source (ATN manufacturer API or server). For the latter, this information is typically stored in the XML metadata file packaged alongside the data files. When both are available, the ADR deployment dates are used as the source of truth, since there is currently no good way of automatically including actual start/end deployment dates in the upstream data source. 

The provided deployment date ranges are converted to `datetime` and used to truncate the data on both ends, to account for time on land before deployment and after retrieval.

Currently, only auto-ingested Wildlife Computer tag data include start and end date metadata (epoch time) in the corresponding XML file, which might look something like this:

```
<deployment>
    <start>
        <date>1464789420</date>
        <latitude>34.2178</latitude>
        <longitude>-120.5634</longitude>
    </start>
    <end>
        <date>1465776000</date>
    </end>
</deployment>
```

### Trajectory QC Tests

The table below summarizes the tests and thresholds that are set for each ATN trajectory parameter:

| Module | Test | Parameter | Suspect | Fail |
|----------|----------|----------|----------|----------|
| ioos_qc.argo | speed_test | Speed | If over 8.0 m/s | If over 10.0 m/s |
| ioos_qc.argo | location_test | Latitude / Longitude | n/a | If falls outside of [-180, -90, 180, 90] |

### Profile QC Tests

The table below summarizes the tests and thresholds that are set for each ATN profile parameter:

| Module | Test | Parameter | Suspect | Fail |
|----------|----------|----------|----------|----------|
| ioos_qc.qartod | gross_range_test | Temperature (C) | n/a | If falls outside of [-2.5, 40] |
| ioos_qc.qartod | gross_range_test | Salinity (psu) | n/a | If falls outside of [0.0, 41.0] |

The min and max temperature thresholds and salinity upper bound threshold are taken from the [Argo Quality Control Manual for CTD and Trajectory Data](https://archimer.ifremer.fr/doc/00228/33951/) and are physical sensor bounds. 

While the Argo Quality Control Manual suggests a gross range lower bound of 2 psu for salinity, modern conductivity-based salinity sensors can measure near 0 psu conditions with reasonable accuracy and without signal degradation ([Menn & Nair 2022](https://www.frontiersin.org/journals/marine-science/articles/10.3389/fmars.2022.1031824/full)). NOAA's [Manual for Real-Time Quality Control](https://repository.library.noaa.gov/view/noaa/23701) defines the Gross Range Test to flag measurements outside of a sensor's operational limits. Therefore, the lower bound we use here is 0 psu.

