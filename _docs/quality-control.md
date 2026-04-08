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

ATN DAC quality control protocols handle animal trajectory and dive profile data and use the `ioos_qc` Python package (see [docs](https://ioos.github.io/ioos_qc/)) to implement multiple QARTOD tests and an aggregate rollup flag. 

The following `ioos_qc` tests are applied: 
* [`ioos_qc.argo.speed_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.argo.speed_test)
* [`ioos_qc.qartod.location_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.qartod.location_test)
* [`ioos_qc.qartod.gross_range_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.qartod.gross_range_test)
* [`ioos_qc.axds.valid_range_test`](https://ioos.github.io/ioos_qc/api/ioos_qc.html#ioos_qc.axds.valid_range_test)

For trajectory data, `location_test`, `speed_test` and `valid_range_test` are applied. For profile data, the `gross_range_test` is applied.


### QC Thresholds

The table below summarizes the thresholds for each test and parameter. The temperature thresholds and salinity upper bound threshold are taken from the [Argo Quality Control Manual for CTD and Trajectory Data](https://archimer.ifremer.fr/doc/00228/33951/):

| Test | Parameter | Suspect | Fail |
|----------|----------|----------|----------|
| ioos_qc.argo.speed_test | Speed | If over 8.0 m/s | If over 10.0 m/s |
| ioos_qc.argo.location_test | Latitude / Longitude | n/a | If falls outside of [-180, -90, 180, 90] |
| ioos_qc.qartod.gross_range_test | Temperature (C) | n/a | If falls outside of [-2.5, 40] |
| ioos_qc.qartod.gross_range_test | Salinity (psu) | n/a | If falls outside of [0.0, 41.0] |
| ioos_qc.axds.valid_range_test | Starting Time | n/a | Varies |
| ioos_qc.axds.valid_range_test | Ending Time | n/a | Varies |

Note: While the Argo Quality Control Manual suggests a gross range lower bound of 2 psu for salinity, modern conductivity-based salinity sensors can measure near 0 psu conditions with reasonable accuracy and without signal degradation ([Menn & Nair 2022](https://www.frontiersin.org/journals/marine-science/articles/10.3389/fmars.2022.1031824/full)). NOAA's [Manual for Real-Time Quality Control](https://repository.library.noaa.gov/view/noaa/23701) defines the Gross Range Test to flag measurements outside of a sensor's operational limits. Therefore, the lower bound we use here is 0 psu.

### Temporal Valid Range Test

The `ioos_qc.axds.valid_range_test()` is applied by checking the ingested data against provider-supplied start and end deployment dates, if available. Valid start and end deployment dates are either accessed from manually submitted deployment information saved in the [ATN Data Registration portal (ADR)](https://dacregistration.atn.ioos.us/) or from an XML metadata file packaged alongside the data files. When both are available, the ADR deployment dates are used as the source of truth. The provided date ranges are converted to `datetime` and used to truncate the data on both ends, to account for time on land before deployment and after retrieval.

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