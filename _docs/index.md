---
title: ATN Specification
keywords: [ioos, metadata, netCDF]
tags: [ioos, metadata, netCDF]
toc: false
#permalink: index.html
summary: The ATN specification contains dataset attribution guidelines and examples which describe ATN's file format specification following the netCDF data model.
---

## **Introduction**

Animal telemetry observations come from many types of instruments and deployment devices. This page provides guidance as to how specific types of animal telemetry datasets should be aligned to the netCDF data model.
Currently, the US IOOS ATN has been developing netCDF templates for satellite trajectory observations (specifically **Argos**{: style="color: red"} tags??). However, this page (and subsequent pages) will be updated as ATN develops templates for other animal tracking observation methods and manufacturers.

## **Current Specification Versions**

### [**IOOS ATN Satellite Telemetry Specification v1.0**](atn-sat-telem-specification-v1-0.html)

Looking for the latest version?  Follow the links above for details on requirements for the most recent ATN netCDF templates.

## **Specification Overview**

The specification defines recommended and required global and variable attributes for animal telemetry data providers to include when publishing their datasets and accompanying services.

Global and variable attributes are concepts of the [netCDF specification](https://www.unidata.ucar.edu/software/netcdf/docs/) which is 'a set of software libraries and self-describing, machine-independent data formats that support the creation, access, and sharing of array-oriented scientific data.'  

The IOOS DMAC data management system has adopted netCDF as a standard data format.  These guidelines are targeted towards netCDF files, however to the degree that they can be applied to other data formats they are referred to as a generalized 'Metadata Profile' rather than a netCDF-specific profile.  They are based on several community netCDF conventions, which each build off of each other in the following order:

- [Climate and Forecast Conventions (CF)](http://cfconventions.org/)
- [Attribute Convention for Data Discovery](http://wiki.esipfed.org/index.php?title=Attribute_Convention_for_Data_Discovery)
- [NOAA NCEI NetCDF Templates](https://www.ncei.noaa.gov/netcdf-templates)

## Specification Versions:

### [**IOOS ATN Satellite Telemetry Specification v1.0**](atn-sat-telem-specification-v1-0.html)

IOOS ATN Specification 0.1 (released in 2023) is the current **valid**{: style="color: green"} specification, and is based upon the following convention versions:

- [IOOS Metadata Profile v1.2](https://ioos.github.io/ioos-metadata/ioos-metadata-profile-v1-2.html)
- [Climate and Forecast Conventions (CF) 1.9](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.9/cf-conventions.html)
- [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
- [NOAA NCEI NetCDF Templates 2.0 DSG:trajectory](https://www.ncei.noaa.gov/data/oceans/ncei/formats/netcdf/v2.0/index.html)

## Compliance Checker:

The IOOS Compliance Checker is a Python tool and library that can be used to verify a data provider's datasets comply with the IOOS Metadata Profile, as well as the community conventions listed above.  The Compliance Checker can be installed and run on the command line on any Conda-based Python platform, can be used programmatically in custom Python code, as is also available on-line to evaluate with your own data.  Compliance Checker can read remote ERDDAP and THREDDS OPeNDAP endpoints directly and output text, HTML, or JSON compliance status reports.  For more information, see:

- [Compliance Checker Web - https://compliance.ioos.us/](https://compliance.ioos.us/)
- [Compliance Checker GitHub - https://github.com/ioos/compliance-checker](https://github.com/ioos/compliance-checker)
