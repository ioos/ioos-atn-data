---
title: "ATN Satellite Telemetry Specification Version 0.1"
keywords: [ioos, metadata, netCDF, 0.1]
tags: [ioos, metadata, netCDF, 0.1]
toc: false
#permalink: index.html
summary: This is the in development ATN satellite telemetry specification version. 
---

## Revision History


| Version | Description                                                                                                     | Date       |
|:--------|:----------------------------------------------------------------------------------------------------------------|:-----------|
| **0.1** | **In development Satellite Telemetry Version** <br>[Initial version](./atn-sat-telem-specification-v0-1.html) | 2022-09-21 |

## Notes/Caveats

1. The ATN satellite trajectory specification is a compound profile that builds off of the [**IOOS Metadata Profile**](https://ioos.github.io/ioos-metadata/index.html) meaning the ATN specification is a combination of the full IOOS Metadata Profile, NCEI Templates plus IOOS-specific guidance included in this document, such as:
   * Identifying characteristics of animals 

1. The IOOS Metadata Profile is a compound profile that builds off of the [**NOAA NCEI NetCDF Templates v2.0**](https://www.ncei.noaa.gov/data/oceans/ncei/formats/netcdf/v2.0/index.html), meaning the full IOOS Metadata Profile is a combination of the NCEI Templates plus IOOS-specific guidance included in this document, such as:
* attributes that are IOOS-specific (i.e. additions to the NCEI Templates)
* attributes where variations exist between the IOOS guidance and the NCEI Templates (e.g. **`platform_vocabulary`**, where NCEI recommendations are specifically disallowed)
* attributes with a different role in the NCEI Templates; for example, the attribute **`_FillValue`** is **required** by the NCEI Template; however, in the IOOS Profile it is listed as **recommended** only;  conversely the opposite is possible as well
* attributes with otherwise modified or further qualified meanings/definitions

1. The NCEI Templates in turn build off of the ACDD and CF conventions.  Some attributes in the IOOS Profile originate from ACDD and CF (consult the `Convention` field in the table to determine the origin of each attribute).  Links to each are below:
* [NOAA NCEI NetCDF Templates 2.0](https://www.ncei.noaa.gov/data/oceans/ncei/formats/netcdf/v2.0/index.html)
* [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
* [Climate and Forecast Conventions (CF) 1.10](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.10/cf-conventions.html)

1. In the ATN specification doesn't define **required** or **recommended** attributes as it is an attempt to synthesize existing standards into a specific implementation for animal tracking observations.

## Gold Standard Example Datasets

IOOS provides a collection of "Gold Standard" example datasets in ERDDAP to demonstrate implementation of this Metadata Profile.  The Gold Standard datasets can be used as templates for data providers to generate their own compliant datasets in ERDDAP, and include a fully-deployable ERDDAP instance that includes both the example data and configuration files.  Consult the links below for more information:

* [IOOS ATN Satellite Trajectory Example Dataset](https://github.com/ioos/ioos-atn-data/blob/main/data/atn_trajectory_template_ncdump_20211006.txt)
* [Example in IOOS "ERDDAP Gold Standard" GitHub Repository]()

## Identifiers
Within the ATN netCDF files there are various identifiers which serve important purposes. Below is a table of those identifiers and the purpose they serve.

| Convention   | Attribute       | Disposition   | Description                                                                                                                                                                                                                                                                                                                                                                            | Example                              |
|:-------------|:----------------|:--------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------|
| ATN          | `animal_id`     | recommended   | An unique identifier for the instrumented animal, provided by the data owner.                                                                                                                                                                                                                                                                                                          | BP6772                               |
| ATN          | `deployment_id` | required      | A unique identifier for the deployment event, attaching an instrument on a animal during a specified deployment window (deployment_start_datetime, deployment_end_datetime), provided by either the instrument manufacturer or the data owner.  If not provided, an internal ATN DAC deployment identifier will be assigned, e.g., animal id_ptt id.                                   | 5f08ee316321be13bc7fbc37             |
| ACDD         | `id`            | required      | An identifier for the data set, provided by and unique within its naming authority. The combination of the "naming authority" and the "id" should be globally unique, but the id can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The id should not include white space characters. | 5f08ee316321be13bc7fbc37             |
| IOOS         | `platform_id`   | required      | An optional, short identifier for the platform (entity to which the instrument is attached and collecting data), if the data provider prefers to define an id that differs from the dataset identifier, as specified by the id attribute. platform_id should be a single alphanumeric string with no blank spaces. Use animal aphia id.                                                | 137205                               |
| ATN          | `ptt_id`        | required      | Platform Transmitter Terminal (PTT) number for Argos transmission.                                                                                                                                                                                                                                                                                                                     | 22275                                |
| ATN          | `uuid`          | required      | Universally Unique Indentifier, 36 character string containing numbers, letters and dashes.                                                                                                                                                                                                                                                                                            | 6f36eed4-16a8-4fac-b055-ca41b3c25da4 |
| ATN          | `vendor_id`     | required      | A unique id assigned by the vendor/manufacturer that released these data to the ATN DAC, may or may not be the same as deployment_id.                                                                                                                                                                                                                                                  | 5f08ee316321be13bc7fbc37             |

## ATN Satellite Trajectory Specification Attributes

### Global attributes

| Attribute                     | Disposition             | Convention   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|:------------------------------|:------------------------|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `acknowledgement`             | required                | ACDD         | A place to acknowledge various types of support for the project that produced this data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | NOAA IOOS, Axiom Data Science, Navy ONR, NOAA NMFS, Wildlife Computers, Argos, IOOS ATN                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `animal_common_name`          | required                | ATN          | Common name of the instrumented animal, as defined by the World Register of Marine Species (WORMS, http://www.marinespecies.org/).                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | loggerhead turtle                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `animal_id`                   | recommended             | ATN          | An unique identifier for the instrumented animal, provided by the data owner.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | BP6772                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `animal_scientific_name`      | required                | ATN          | Scientific name of the instrumented animal as defined by the World Register of Marine Species (WoRMS, http://www.marinespecies.org/). If the species name cannot be provided, this should be the lowest level taxonomic rank that can be determined.                                                                                                                                                                                                                                                                                                                                                 | Caretta caretta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `arbitrary_keywords`          | recommended             | ATN          | Common separated list of arbitary keywords, free text                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | ATN, Animal Telemetry Network, IOOS, Integrated Ocean Observing System, trajectory                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `argos_program_number`        | recommended             | ATN          | Argos program number associated with the instruments ptt_id                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 1092                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `cdm_data_type`               | required                | ACDD         | The data type, as derived from Unidata's Common Data Model Scientific Data types and understood by THREDDS, e.g., "Grid", "Image", "Station", "Trajectory", "Radial" (This is a THREDDS "dataType", and is different from the CF NetCDF attribute 'featureType', which indicates a Discrete Sampling Geometry file in CF.)                                                                                                                                                                                                                                                                           | Trajectory                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `citation`                    | required                | ATN          | The citation to be used in publications using the dataset. Format:  [creator_last_name, creator_first_name]; [contributor_last name(s), contributor_first name(s)]. [year]. [animal_common_name] ([animal_scientific_name]) location data from a [instrument] (ptt id [ptt_id]) deployed in the [sea_name] from [deployment_state_datetime] to [deployment_end_datetime], deployment id [deployment_id]. [Dataset]. [publisher_name].                                                                                                                                                                | Martin, Summer; Gaos, Alex. (2023). Loggerhead turtle (Caretta caretta) location data from a satellite telemetry tag (ptt id 22275) deployed in the North Atlantic Ocean from 2000-07-17 to 2001-07-24, deployment id 5f08ee316321be13bc7fbc37. [Dataset]. US Integrated Ocean Observing System (IOOS) Animal Telemetry Network (ATN).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `comment`                     | recommended             | ACDD/CF      | Miscellaneous information about the animal, instrument, data or methods used to produce it, not captured elsewhere. NCEI requirement. In no comment provided, leave blank.                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `contributor_email`           | recommended             | IOOS         | Email addresses of the individuals or institutions that contributed to the creation of this data. Comma seperated list.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | alexander.gaos@noaa.gov                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `contributor_name`            | recommended             | ACDD         | The name of any individuals, projects, or institutions that contributed to the creation of this data. Comma seperated list.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Alexander Gaos                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `contributor_role`            | recommended             | ACDD         | The role of any individuals or institutions that contributed to the creation of this data. Comma seperated list.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | collaborator                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `contributor_role_vocabulary` | recommended             | IOOS         | The URL of the controlled vocabulary used for the contributor_role attribute.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | http://vocab.nerc.ac.uk/collection/G04/current/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `contributor_url`             | recommended             | ATN          | The URL/id of the individuals that contributed to the creation of this data. Multiple URLs/ids can be given, comma seperated, presented in the same order and number as the names in contributor_names. Use ORCID URL.                                                                                                                                                                                                                                                                                                                                                                               | https://orcid.org/0000-0001-6100-7319                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `Conventions`                 | required                | CF           | A comma-separated list of the conventions that are followed by the dataset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | CF-1.10, ACDD-1.3, IOOS-1.2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `creator_country`             | required                | IOOS         | Country of the person or organization that operates a platform or network, which collected the observation data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | USA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `creator_email`               | required                | ACDD         | The email address of the person (or other creator type specified by the creator_type attribute) principally responsible for creating this data (i.e., the PI).                                                                                                                                                                                                                                                                                                                                                                                                                                       | summer.martin@noaa.gov                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `creator_institution`         | required                | ACDD         | Institution that collected the data. This should be specified even if it matches the value of publisher_institution, institution or if creator_type is institution.                                                                                                                                                                                                                                                                                                                                                                                                                                  | Marine Turtle Biology and Assessment Program, NOAA Pacific Islands Fisheries Science Center                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `creator_institution_url`     | required                | ACDD/IOOS    | The URL of the institution that collected the data. Note that this should always reference an institution URL, and not a personal URL, even if creator_type=person.                                                                                                                                                                                                                                                                                                                                                                                                                                  | https://www.fisheries.noaa.gov/about/pacific-islands-fisheries-science-center                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `creator_name`                | required                | ACDD         | The name of the person (or other creator type specified by the creator_type attribute) principally responsible for creating this data (i.e., the PI).                                                                                                                                                                                                                                                                                                                                                                                                                                                | Summer Martin                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `creator_role`                | required                | ACDD         | The role of the person (or other creator type specified by the creator_type attribute) principally responsible for creating this data (i.e., the PI).                                                                                                                                                                                                                                                                                                                                                                                                                                                | principalInvestigator                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `creator_role_vocabulary`     | required                | Global ATN   | The URL of the controlled vocabulary used for the creator_role attribute.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | http://vocab.nerc.ac.uk/collection/G04/current/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `creator_sector`              | required                | IOOS         | IOOS classifier that best describes the platform (network) operator’s societal sector.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | gov_federal                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `creator_sector_vocabulary`   | required                | IOOS         | The URL of the controlled vocabulary used for the creator_sector attribute.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | http://mmisw.org/ont/ioos/sector                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `creator_type`                | required                | ACDD         | Specifies type of creator with one of the following: ‘person’, ‘group’, ‘institution’, or ‘position’. If this attribute is not specified, the creator is assumed to be a person.                                                                                                                                                                                                                                                                                                                                                                                                                     | person                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `creator_url`                 | recommended             | ATN          | The URL/id of the individual (principal investigator) that created this dataset. Use ORCID URL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | https://orcid.org/0000-0003-3443-3325                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `date_created`                | required                | ACDD         | The date on which this version of the data was created. (Modification of values implies a new version, hence this would be assigned the date of the most recent values modification.) Metadata changes are not considered when assigning the date_created.                                                                                                                                                                                                                                                                                                                                           | 2021-08-12T21:02:56Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `date_issued`                 | required                | ACDD         | The date on which this data (including all modifications) was formally issued (i.e., made available to a wider audience). Note that these apply just to the data, not the metadata.                                                                                                                                                                                                                                                                                                                                                                                                                  | 2021-08-12T21:02:56Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `date_metadata_modified`      | required                | ACDD         | The date on which the metadata was last modified.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 2023-01-13T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `date_modified`               | required                | ACDD         | The date on which the data was last modified. Note that this applies just to the data, not the metadata.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 2021-08-12T21:02:56Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `deployment_end_datetime`     | required                | ATN          | The timestamp of when an instrumented animals deployment has ended. (can differ from the time_coverage_end attribute, e.g., could occur before time of last data point). Use ISO 8601:2004 date format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                                                                     | 2001-07-24T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `deployment_id`               | required                | ATN          | A unique identifier for the deployment event, attaching an instrument on a animal during a specified deployment window (deployment_start_datetime, deployment_end_datetime), provided by either the instrument manufacturer or the data owner.  If not provided, an internal ATN DAC deployment identifier will be assigned, e.g., animal id_ptt id.                                                                                                                                                                                                                                                 | 5f08ee316321be13bc7fbc37                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `deployment_start_datetime`   | required                | ATN          | The timestamp of when an instrumented animal was released, indicating start of the deployment. (can differ from the time_coverage_start attribute, e.g., could occur before or after time of first data point). Use ISO 8601:2004 date format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                              | 2000-07-17T00:00:00Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `deployment_start_lat`        | recommended             | ATN          | The latitude of the location where an instrumented animal was released. Use decimal degrees, WGS84 reference system. Leave blank if not provided by PI.                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `deployment_start_lon`        | recommended             | ATN          | The longitude of the location where an instrumented animal was released. Use decimal degrees, WGS84 reference system. Leave blank if not provided by PI.                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `featureType`                 | required                | CF           | Specifies the type of discrete sampling geometry to which the data in the file belongs, and implies that all data variables in the file contain collections of features of that type. Options are: point, timeseries, trajectroy, profile, timeseriesProfile or trajectoryProfile. http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#featureType                                                                                                                                                                                                                   | trajectory                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `geospatial_bbox`             | recommended             | ATN          | Describes the data geospatial extent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | POLYGON ((336.213 33.282, 336.213 47.816, 163.607 47.816, 163.607 33.282, 336.213 33.282))                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `geospatial_bounds`           | required                | ACDD         | Describes the data's 2D or 3D geospatial extent in OGC's Well-Known Text (WKT) Geometry format (reference the OGC Simple Feature Access (SFA) specification). The meaning and order of values for each point's coordinates depends on the coordinate reference system (CRS). The ACDD default is 2D geometry in the EPSG:4326 coordinate reference system. The default may be overridden with geospatial_bounds_crs and geospatial_bounds_vertical_crs (see those attributes). EPSG:4326 coordinate values are latitude (decimal degrees_north) and longitude (decimal degrees_east), in that order. | POLYGON ((165.1179999999999 33.282, 163.607 33.92, 236.857 47.816, 319.721 41.061, 331.475 38.34, 336.213 36.775, 335.844 35.645, 335.057 35.207, 165.1179999999999 33.282))                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `geospatial_bounds_crs`       | required                | ACDD         | The coordinate reference system (CRS) of the point coordinates in the geospatial_bounds attribute. This CRS may be 2-dimensional or 3-dimensional, but together with geospatial_bounds_vertical_crs, if that attribute is supplied, must match the dimensionality, order, and meaning of point coordinate values in the geospatial_bounds attribute. If geospatial_bounds_vertical_crs is also present then this attribute must only specify a 2D CRS. EPSG CRSs are strongly recommended. If this attribute is not specified, the CRS is assumed to be EPSG:4326.                                   | EPSG:4326                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `geospatial_lat_max`          | required                | ACDD         | Describes a simple upper latitude limit; may be part of a 2- or 3-dimensional bounding region. Geospatial_lat_max specifies the northernmost latitude covered by the dataset.                                                                                                                                                                                                                                                                                                                                                                                                                        | 47.816                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `geospatial_lat_min`          | required                | ACDD         | Describes a simple lower latitude limit; may be part of a 2- or 3-dimensional bounding region. Geospatial_lat_min specifies the southernmost latitude covered by the dataset.                                                                                                                                                                                                                                                                                                                                                                                                                        | 33.282                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `geospatial_lat_units`        | required                | ACDD         | Units for the latitude axis described in "geospatial_lat_min" and "geospatial_lat_max" attributes. These are presumed to be "degree_north"; other options from udunits may be specified instead.                                                                                                                                                                                                                                                                                                                                                                                                     | degrees_north                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `geospatial_lon_max`          | required                | ACDD         | Describes a simple longitude limit; may be part of a 2- or 3-dimensional bounding region. geospatial_lon_max specifies the easternmost longitude covered by the dataset.                                                                                                                                                                                                                                                                                                                                                                                                                             | 165.118                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `geospatial_lon_min`          | required                | ACDD         | Describes a simple longitude limit; may be part of a 2- or 3-dimensional bounding region. geospatial_lon_min specifies the westernmost longitude covered by the dataset.                                                                                                                                                                                                                                                                                                                                                                                                                             | -123.143                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `geospatial_lon_units`        | required                | ACDD         | Units for the longitude axis described in "geospatial_lon_min" and "geospatial_lon_max" attributes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | degrees_east                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `history`                     | required                | ACDD/CF      | Provides an audit trail for modifications to the original data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 2021-08-12T21:02:56Z - Created by the IOOS ATN DAC from the Wildlife Computers API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `id`                          | required                | ACDD         | An identifier for the data set, provided by and unique within its naming authority. The combination of the "naming authority" and the "id" should be globally unique, but the id can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The id should not include white space characters.                                                                                                                                                                                                               | 5f08ee316321be13bc7fbc37                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `infoUrl`                     | required                | IOOS/ERRDAP  | URL for background information about this dataset. Link for associated ATN portal project page.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | https://portal.atn.ioos.us/#metadata/d148c911-209e-44b1-a708-c155bbe4c694/project                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `institution`                 | recommended             | ACDD/CF      | The name of the institution principally responsible for originating this data. Can be the same as creator_institution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | NOAA Pacific Islands Fisheries Science Center                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `instrument`                  | required                | ACDD         | Name of the contributing instrument type used to create this data set or product (e.g., satellite, acoustic, Dtag)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | satellite telemetry tag                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `instrument_vocabulary`       | recommended             | ACDD         | Controlled vocabulary for the names used in the instrument attribute                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `keywords`                    | required                | ACDD         | A comma-separated list of key words and/or phrases. Keywords may be common words or phrases, terms from a controlled vocabulary (GCMD is often used), or URLs for terms from a controlled vocabulary                                                                                                                                                                                                                                                                                                                                                                                                 | EARTH SCIENCE > AGRICULTURE > ANIMAL SCIENCE > ANIMAL ECOLOGY AND BEHAVIOR, EARTH SCIENCE > BIOSPHERE > ECOLOGICAL DYNAMICS > SPECIES/POPULATION INTERACTIONS > MIGRATORY RATES/ROUTES, EARTH SCIENCE > OCEANSEARTH SCIENCE > CLIMATE INDICATORS > BIOSPHERIC INDICATORS > SPECIES MIGRATION, EARTH SCIENCE > OCEANS, EARTH SCIENCE > BIOLOGICAL CLASSIFICATION > ANIMALS/INVERTEBRATES, EARTH SCIENCE > BIOSPHERE > ECOSYSTEMS > MARINE ECOSYSTEMS, PROVIDERS > GOVERNMENT, AGENCIES-U.S. FEDERAL AGENCIES > DOC > NOAA > IOOS, PROVIDERS > COMMERCIAL > Axiom Data Science                                                                                                                                                                                                                                                                                                        |
| `keywords_vocabulary`         | required                | ACDD         | If you are using a controlled vocabulary for the words/phrases in your "keywords" attribute, this is the unique name or identifier of the vocabulary from which keywords are taken. If more than one keyword vocabulary is used, each may be presented with a prefix and a following comma, so that keywords may optionally be prefixed with the controlled vocabulary key.                                                                                                                                                                                                                          | GCMD 15.1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `license`                     | required                | ACDD         | Provide the URL to a standard or specific license, enter "Freely Distributed" or "None", or describe any restrictions to data access and distribution in free text.                                                                                                                                                                                                                                                                                                                                                                                                                                  | These data may be used and redistributed for free, but are not intended for legal use, since they may contain inaccuracies. No person or group associated with these data makes any warranty, expressed or implied, including warranties of merchantability and fitness for a particular purpose, or assumes any legal liability for the accuracy, completeness or usefulness of this information. This disclaimer applies to both individual use of these data and aggregate use with other data. It is strongly recommended that users read and fully comprehend associated metadata prior to use. Please acknowledge the U.S. Animal Telemetry Network (ATN) or the specified citation as the source from which these data were obtained in any publications and/or representations of these data. Communication and collaboration with dataset authors are strongly encouraged. |
| `metadata_link`               | recommended             | ACDD         | A URL that gives the location of more complete metadata. A persistent URL is recommended for this attribute. Link to NCEI collection page.                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `naming_authority`            | required                | ACDD         | The organization that provides the initial id (see above) for the dataset. The naming authority should be uniquely specified by this attribute.                                                                                                                                                                                                                                                                                                                                                                                                                                                      | com.wildlifecomputers                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `ncei_template_version`       | required                | NCEI         | Version on current NCEI template applied to dataset.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | NCEI_NetCDF_Trajectory_Template_v2.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `NCO`                         | required                | ATN          | NetCDF operators.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | netCDF Operators version 4.9.1 (Homepage = http://nco.sf.net, Code = http://github.com/nco/nco)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `platform`                    | required                | ACDD         | Name of the platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or animal. Indicate controlled vocabulary used in platform_vocabulary.                                                                                                                                                                                                                                                                                                                                                    | organism                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `platform_id`                 | required                | IOOS         | An optional, short identifier for the platform (entity to which the instrument is attached and collecting data), if the data provider prefers to define an id that differs from the dataset identifier, as specified by the id attribute. platform_id should be a single alphanumeric string with no blank spaces. Use animal aphia id.                                                                                                                                                                                                                                                              | 137205                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `platform_name `              | required                | IOOS         | A descriptive, long name for the platform used in collecting the data. The value of platform_name will be used to label the platform in downstream applications, such as IOOS’ National Products (Environmental Sensor Map, EDS, etc).                                                                                                                                                                                                                                                                                                                                                               | Caretta caretta                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `platform_vocabulary`         | required                | ACDD         | Controlled vocabulary for the names used in the platform attribute.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | http://vocab.nerc.ac.uk/collection/L06/current/                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `processing_level`            | required                | ACDD         | A textual description of the processing (or quality control) level of the data. NCEI archive levels: level 2 product - derived data product, e.g., aniMotum,  level 1 product - e.g. potentially edited by PIs to remove low quality values, has QARTOD applied, Level 0 product - would be the untrimmed raw files.                                                                                                                                                                                                                                                                                 | Level 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `product_version`             | required                | ACDD         | Version identifier of the data file or product as assigned by the data creator. For example, a new algorithm or methodology could result in a new product_version, required by NCEI netCDF trajectory template. If none assigned, leave blank.                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `program`                     | required                | ACDD         | The overarching program(s) of which the dataset is a part. A program consists of a set (or portfolio) of related and possibly interdependent projects that meet an overarching objective.                                                                                                                                                                                                                                                                                                                                                                                                            | US IOOS Animal Telemetry Network                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `project`                     | required                | ACDD         | The name of the project(s) principally responsible for originating this data. Multiple projects can be separated by commas, as described under Attribute Content Guidelines.                                                                                                                                                                                                                                                                                                                                                                                                                         | Spatial Ecology of loggerhead turtles tagged at the Azores, 1994-2000                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `ptt_id`                      | required                | ATN          | Platform Transmitter Terminal (PTT) number for Argos transmission.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | 22275                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `publisher_country`           | required                | IOOS         | Country of the person or organization that distributes the data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | USA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `publisher_email`             | required                | ACDD         | The email address of the person or group that distributes the data files.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | atndata@ioos.us                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `publisher_institution`       | required                | ACDD         | Institution that distributes the data. This should be specified even if publisher_type is institution (in which case publisher_name would have an identical value).                                                                                                                                                                                                                                                                                                                                                                                                                                  | US Integrated Ocean Observing System Office                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `publisher_name`              | required                | ACDD         | Name of the person or group that distributes the data files.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | US Integrated Ocean Observing System (IOOS) Animal Telemetry Network (ATN)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `publisher_type`              | required                | ACDD         | Specifies type of publisher with one of the following: ‘person’, ‘group’, ‘institution’, or ‘position’. If this attribute is not specified, the publisher is assumed to be a person.                                                                                                                                                                                                                                                                                                                                                                                                                 | institution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `publisher_url`               | required                | ACDD/IOOS    | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if publisher_type=person.                                                                                                                                                                                                                                                                                                                                                                                                                        | https://atn.ioos.us                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `references`                  | recommended             | NCEI         | List of related references, required by NCEI netCDF trajectory template.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `sea_name`                    | required                | NCEI         | Geographical coverage area, report actual sea name(s). Comma seperated list.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | North Atlantic Ocean                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `source`                      | required                | CF           | Method of production of the original data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Service Argos                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `standard_name_vocabulary`    | required                | ACDD         | The name and version of the controlled vocabulary from which variable standard names are taken. (Values for any standard_name attribute must come from the CF Standard Names vocabulary for the data file or product to comply with CF).                                                                                                                                                                                                                                                                                                                                                             | CF Standard Name Table v78                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `summary`                     | required                | ACDD         | A paragraph describing the dataset, analogous to an abstract for a paper. Format:  [tag_manufacturer] [tag_model] (ptt id [ptt_id]) deployed on [animal_common_name] ([animal_scientific_name]) by [creator_name] in [sea_name] from [deployment__start_datetime] to [deployment_end_datetime].                                                                                                                                                                                                                                                                                                      | Wildlife Computers SDR tag (ptt id 22275) deployed on a loggerhead turtle (Caretta caretta) by Summer Martin in North Atlantic Ocean from 2000-07-17 to 2001-07-24.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `time_coverage_duration`      | required                | ACDD         | Describes the duration of the data set. Use ISO 8601:2004 duration format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                                                                                                                                                                                                  | P1681DT23H52M42S                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `time_coverage_end`           | required                | ACDD         | Describes the time of the last data point in the data set. Use ISO 8601:2004 date format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                                                                                                                                                                                   | 2004-02-26T02:31:35Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `time_coverage_resolution`    | required                | ACDD         | Describes the targeted time period between each value in the data set. Use ISO 8601:2004 duration format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                                                                                                                                                                   | P2DT9H15M34S                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `time_coverage_start`         | required                | ACDD         | Describes the time of the first data point in the data set. Use ISO 8601:2004 date format, preferably the extended format as recommended in the Attribute Content Guidance section.                                                                                                                                                                                                                                                                                                                                                                                                                  | 1999-07-20T02:38:53Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `title`                       | required                | ACDD         | A short phrase or sentence describing the dataset. In many discovery systems, the title will be displayed in the results list from a search, and therefore should be human readable and reasonable to display in a list of such names. title format: [common name] ([species]) location data from a [instrument] (ptt id [ptt id]) deployed in the [sea_name] from [deployment_start_datetime] to [deployment_end_datetime], deployment id [deployment id].                                                                                                                                          | Loggerhead turtle (Caretta caretta) location data from a satellite telemetry tag (ptt id 22275) deployed  in the North Atlantic Ocean from 2000-07-17 to 2001-07-24, deployment id 5f08ee316321be13bc7fbc37                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `uuid`                        | required                | ATN          | Universally Unique Indentifier, 36 character string containing numbers, letters and dashes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 6f36eed4-16a8-4fac-b055-ca41b3c25da4                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `vendor`                      | required                | ATN          | Name of vendor that released the raw data files to the ATN DAC, may or may not be the same as the tag manufacturer.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Wildlife Computers                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `vendor_id`                   | required                | ATN          | A unique id assigned by the vendor/manufacturer that released these data to the ATN DAC, may or may not be the same as deployment_id.                                                                                                                                                                                                                                                                                                                                                                                                                                                                | 5f08ee316321be13bc7fbc37                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `wmo_platform_code`           | required, if applicable | IOOS         | The WMO identifier for the platform used to measure the data., if gts_ingest = false this field will display not applicable or be blank. if gts_ingest = true, provide WMO id.                                                                                                                                                                                                                                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Variable attributes

#### qartod_location_flag

| Attribute             | Disposition   | Description   | Example                                                                           |
|:----------------------|:--------------|:--------------|:----------------------------------------------------------------------------------|
| _FillValue            |               |               | 241                                                                               |
| coordinates           |               |               | time z lon lat                                                                    |
| flag_meanings         |               |               | PASS NOT_EVALUATED SUSPECT FAIL MISSING                                           |
| implementation        |               |               | https://github.com/ioos/ioos_qc/                                                  |
| long_name             |               |               | Location QC test - Location test                                                  |
| references            |               |               | https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf |
| standard_name         |               |               | location_test_quality_flag                                                        |
| flag_values           |               |               | [1, 2, 3, 4, 9]                                                                   |
| coverage_content_type |               |               | qualityInformation                                                                |
| ioos_category         |               |               | Quality                                                                           |

```
 <xarray.DataArray 'qartod_location_flag' (obs: 115)>
array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1.])
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Location QC test - Location test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   location_test_quality_flag
    flag_values:     [1 2 3 4 9] 
```

#### qartod_rollup_flag

| Attribute             | Disposition   | Description   | Example                                                                           |
|:----------------------|:--------------|:--------------|:----------------------------------------------------------------------------------|
| _FillValue            |               |               | 241                                                                               |
| coordinates           |               |               | time z lon lat                                                                    |
| flag_meanings         |               |               | PASS NOT_EVALUATED SUSPECT FAIL MISSING                                           |
| implementation        |               |               | https://github.com/ioos/ioos_qc/                                                  |
| long_name             |               |               | Aggregate QC value                                                                |
| references            |               |               | https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf |
| standard_name         |               |               | aggregate_quality_flag                                                            |
| flag_values           |               |               | [1, 2, 3, 4, 9]                                                                   |
| coverage_content_type |               |               | qualityInformation                                                                |
| ioos_category         |               |               | Quality                                                                           |

```
 <xarray.DataArray 'qartod_rollup_flag' (obs: 115)>
array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 3., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 3., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1.])
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Aggregate QC value
    references:      https://github.com/ioos/ioos_qc/
    standard_name:   aggregate_quality_flag
    flag_values:     [1 2 3 4 9] 
```

#### qartod_speed_flag

| Attribute             | Disposition   | Description   | Example                                                                           |
|:----------------------|:--------------|:--------------|:----------------------------------------------------------------------------------|
| _FillValue            |               |               | 241                                                                               |
| coordinates           |               |               | time z lon lat                                                                    |
| flag_meanings         |               |               | PASS NOT_EVALUATED SUSPECT FAIL MISSING                                           |
| implementation        |               |               | https://github.com/ioos/ioos_qc/                                                  |
| long_name             |               |               | Speed QC test - gross range test                                                  |
| references            |               |               | https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf |
| standard_name         |               |               | gross_range_test_quality_flag                                                     |
| flag_values           |               |               | [1, 2, 3, 4, 9]                                                                   |
| coverage_content_type |               |               | qualityInformation                                                                |
| ioos_category         |               |               | Quality                                                                           |


```
 <xarray.DataArray 'qartod_speed_flag' (obs: 115)>
array([2., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 3., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 3., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1.])
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Speed QC test - gross range test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   gross_range_test_quality_flag
    flag_values:     [1 2 3 4 9] 
```

#### qartod_time_flag

| Attribute             | Disposition   | Description   | Example                                                                           |
|:----------------------|:--------------|:--------------|:----------------------------------------------------------------------------------|
| _FillValue            |               |               | 241                                                                               |
| coordinates           |               |               | time z lon lat                                                                    |
| flag_meanings         |               |               | PASS NOT_EVALUATED SUSPECT FAIL MISSING                                           |
| implementation        |               |               | https://github.com/ioos/ioos_qc/                                                  |
| long_name             |               |               | Time QC test - gross range test                                                   |
| references            |               |               | https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf |
| standard_name         |               |               | gross_range_test_quality_flag                                                     |
| flag_values           |               |               | [1, 2, 3, 4, 9]                                                                   |
| coverage_content_type |               |               | qualityInformation                                                                |
| ioos_category         |               |               | Quality                                                                           |


```
 <xarray.DataArray 'qartod_time_flag' (obs: 115)>
array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1., 1.,
       1., 1., 1., 1., 1., 1., 1.])
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Time QC test - gross range test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   gross_range_test_quality_flag
    flag_values:     [1 2 3 4 9] 
```

#### trajectory

| Attribute   | Disposition   | Description   | Example               |
|:------------|:--------------|:--------------|:----------------------|
| cf_role     |               |               | trajectory_id         |
| long_name   |               |               | trajectory identifier |


```
 <xarray.DataArray 'trajectory' ()>
array('63d36a62e9b351752d1e6fdf', dtype='<U24')
Attributes:
    cf_role:    trajectory_id
    long_name:  trajectory identifier 
```

#### time

| Attribute             | Disposition   | Description   | Example                                               |
|:----------------------|:--------------|:--------------|:------------------------------------------------------|
| _FillValue            |               |               | -9999                                                 |
| units                 |               |               | "seconds since 1970-01-01 00:00:00Z"                  |
| standard_name         |               |               | time                                                  |
| axis                  |               |               | T                                                     |
| _CoordinateAxisType   |               |               | Time                                                  |
| calendar              |               |               | standard                                              |
| actual_min            |               |               | 2023-01-31T08:00:00Z                                  |
| actual_max            |               |               | 2023-03-03T17:21:56Z                                  |
| long_name             |               |               | Time of the measurement, in seconds since 1970-01-01  |
| ancillary_variables   |               |               | qartod_time_flag qartod_rollup_flag qartod_speed_flag |
| coverage_content_type |               |               | coordinate                                            |
| ioos_category         |               |               | Time                                                  |


```
 <xarray.DataArray 'time' (obs: 115)>
[115 values with dtype=datetime64[ns]]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    standard_name:        time
    axis:                 T
    _CoordinateAxisType:  Time
    actual_min:           2023-01-31T08:00:00Z
    actual_max:           2023-03-03T17:21:56Z
    long_name:            Time of the measurement, in seconds since 1990-01-01
    ancillary_variables:  qartod_time_flag qartod_rollup_flag qartod_speed_flag 
```

#### z

| Attribute             | Disposition   | Description   | Example              |
|:----------------------|:--------------|:--------------|:---------------------|
| _FillValue            |               |               | -9999.9              |
| axis                  |               |               | Z                    |
| positive              |               |               | down                 |
| standard_name         |               |               | depth                |
| units                 |               |               | m                    |
| actual_min            |               |               | 0.0                  |
| actual_max            |               |               | 0.0                  |
| long_name             |               |               | depth of measurement |
| instrument            |               |               | instrument_location  |
| platform              |               |               | animal               |
| coverage_content_type |               |               | coordinate           |
| ioos_category         |               |               | Depth                |


```
 <xarray.DataArray 'z' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    axis:           Z
    positive:       down
    standard_name:  depth
    units:          m
    actual_min:     0.0
    actual_max:     0.0
    long_name:      depth of measurement
    instrument:     intrument_pressure
    platform:       animal 
```

#### lat

| Attribute             | Disposition   | Description   | Example                                                                                                                                              |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999.9                                                                                                                                              |
| axis                  |               |               | Y                                                                                                                                                    |
| _CoordinateAxisType   |               |               | Lat                                                                                                                                                  |
| standard_name         |               |               | latitude                                                                                                                                             |
| units                 |               |               | degrees_north                                                                                                                                        |
| valid_max             |               |               | 90.0                                                                                                                                                 |
| valid_min             |               |               | -90.0                                                                                                                                                |
| actual_min            |               |               | 45.6618                                                                                                                                              |
| actual_max            |               |               | 45.9472                                                                                                                                              |
| long_name             |               |               | Latitude portion of location in decimal degrees North                                                                                                |
| instrument            |               |               | instrument_location                                                                                                                                  |
| platform              |               |               | animal                                                                                                                                               |
| ancillary_variables   |               |               | qartod_location_flag qartod_rollup_flag qartod_speed_flag error_radius semi_major_axis semi_minor_axis ellipse_orientation offset offset_orientation |
| coverage_content_type |               |               | coordinate                                                                                                                                           |
| ioos_category         |               |               | Location                                                                                                                                             |


```
 <xarray.DataArray 'lat' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    axis:                 Y
    _CoordinateAxisType:  Lat
    standard_name:        latitude
    units:                degrees_north
    valid_max:            90.0
    valid_min:            -90.0
    actual_min:           45.6618
    actual_max:           45.9472
    long_name:            Latitude portion of location in decimal degrees North
    instrument:           instrument_location
    platform:             animal
    ancillary_variables:  qartod_location_flag qartod_rollup_flag qartod_spee... 
```

#### lon

| Attribute             | Disposition   | Description   | Example                                                                                                                                              |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999.9                                                                                                                                              |
| axis                  |               |               | X                                                                                                                                                    |
| _CoordinateAxisType   |               |               | Lon                                                                                                                                                  |
| standard_name         |               |               | longitude                                                                                                                                            |
| units                 |               |               | degrees_east                                                                                                                                         |
| valid_max             |               |               | 180.0                                                                                                                                                |
| valid_min             |               |               | -180.0                                                                                                                                               |
| actual_min            |               |               | 50.8371                                                                                                                                              |
| actual_max            |               |               | 51.1888                                                                                                                                              |
| long_name             |               |               | Longitude portion of location in decimal degrees East                                                                                                |
| instrument            |               |               | instrument_location                                                                                                                                  |
| platform              |               |               | platform                                                                                                                                             |
| ancillary_variables   |               |               | qartod_location_flag qartod_rollup_flag qartod_speed_flag error_radius semi_major_axis semi_minor_axis ellipse_orientation offset offset_orientation |
| coverage_content_type |               |               | coordinate                                                                                                                                           |
| ioos_category         |               |               | Location                                                                                                                                             |


```
 <xarray.DataArray 'lon' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    axis:                 X
    _CoordinateAxisType:  Lon
    standard_name:        longitude
    units:                degrees_east
    valid_max:            180.0
    valid_min:            -180.0
    actual_min:           50.8371
    actual_max:           51.1888
    long_name:            Longitude portion of location in decimal degrees East
    instrument:           instrument_location
    platform:             animal
    ancillary_variables:  qartod_location_flag qartod_rollup_flag qartod_spee... 
```

#### deploy_id

| Attribute             | Disposition   | Description   | Example                                                                                                |
|:----------------------|:--------------|:--------------|:-------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                  |
| coordinates           |               |               | time z lon lat                                                                                         |
| comment               |               |               | Friendly name given to the tag by the user. If no specific friendly name is given, this is the PTT id. |
| long_name             |               |               | id for this deployment. This is typically the tag ptt                                                  |
| instrument            |               |               | instrument_location                                                                                    |
| platform              |               |               | platform                                                                                               |
| coverage_content_type |               |               | referenceInformation                                                                                   |
| ioos_category         |               |               | Other                                                                                                  |


```
 <xarray.DataArray 'deploy_id' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    comment:                Friendly name given to the tag by the user. If no...
    long_name:              id for this deployment. This is typically the tag...
    coverage_content_type:  referenceInformation 
```

#### ptt

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                      |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                                                                        |
| coordinates           |               |               | time z lon lat                                                                                                                                                               |
| comment               |               |               | PTT id for this deployment. PTT ids may be used on multiple deployments, but not concurrently. When combined with deployment dates, PTTs can uniquely identify a deployment. |
| long_name             |               |               | Platform Transmitter Terminal (PTT) id used for Argos transmissions                                                                                                          |
| instrument            |               |               | instrument_location                                                                                                                                                          |
| platform              |               |               | platform                                                                                                                                                                     |
| coverage_content_type |               |               | referenceInformation                                                                                                                                                         |
| ioos_category         |               |               | Other                                                                                                                                                                        |


```
 <xarray.DataArray 'ptt' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    long_name:              Platform Transmitter Terminal (PTT) id used for A...
    comment:                PTT code for this deployment. PTT codes may be us...
    coverage_content_type:  referenceInformation 
```

#### instrument

| Attribute             | Disposition   | Description   | Example                               |
|:----------------------|:--------------|:--------------|:--------------------------------------|
| coordinates           |               |               | time z lon lat                        |
| comment               |               |               | Wildlife Computers instrument family. |
| long_name             |               |               | Instrument family                     |
| instrument            |               |               | instrument_location                   |
| platform              |               |               | platform                              |
| coverage_content_type |               |               | referenceInformation                  |
| ioos_category         |               |               | Other                                 |


```
 <xarray.DataArray 'instrument' (obs: 115)>
[115 values with dtype=object]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    long_name:  Instrument
    comment:    Wildlife Computers instrument family.  
```

#### type

| Attribute             | Disposition   | Description   | Example                                                                       |
|:----------------------|:--------------|:--------------|:------------------------------------------------------------------------------|
| coordinates           |               |               | time z lon lat                                                                |
| comment               |               |               | Type of location: Argos, FastGPS or User                                      |
| long_name             |               |               | Type of location information - Argos, GPS satellite or user provided location |
| instrument            |               |               | instrument_location                                                           |
| platform              |               |               | platform                                                                      |
| coverage_content_type |               |               | referenceInformation                                                          |
| ioos_category         |               |               | Other                                                                         |


```
 <xarray.DataArray 'type' (obs: 115)>
[115 values with dtype=object]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    comment:    Type of location: Argos
    long_name:  Type of location information - Argos satellite location 
```

#### location_class

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| coordinates           |               |               | time z lon lat                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| standard_name         |               |               | quality_flag                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| comment               |               |               | Quality codes from the ARGOS satellite (in meters): G,3,2,1,0,A,B,Z. See http://www.argos-system.org/manual/3-location/34_location_classes.htm                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| long_name             |               |               | Location Quality Code from ARGOS satellite system                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| code_values           |               |               | G,3,2,1,0,A,B,Z                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| code_meanings         |               |               | estimated error less than 100m and 1+ messages received per satellite pass, estimated error less than 250m and 4+ messages received per satellite pass, estimated error between 250m and 500m and 4+ messages per satellite pass, estimated error between 500m and 1500m and 4+ messages per satellite pass,  estimated error greater than 1500m and 4+ messages received per satellite pass, no least squares estimated error or unbounded kalman filter estimated error and 3 messages received per satellite pass, no least squares estimated error or unbounded kalman filter estimated error and 1 or 2 messages received per satellite pass, invalid location (available for Service Plus or Auxilliary Location Processing) |
| instrument            |               |               | instrument_location                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| platform              |               |               | animal                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ancillary_variables   |               |               | lat lon                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| coverage_content_type |               |               | qualityInformation                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ioos_category         |               |               | Quality                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |


```
 <xarray.DataArray 'location_class' (obs: 115)>
[115 values with dtype=object]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    standard_name:        quality_flag
    comment:              Quality codes from the ARGOS satellite (in meters):...
    long_name:            Location Quality Code from ARGOS satellite system
    code_values:          G,3,2,1,0,A,B,Z
    code_meanings:        estimated error less than 100m and 1+ messages rece...
    instrument:           instrument_location
    platform:             animal
    ancillary_variables:  lat lon 
```

#### error_radius

| Attribute             | Disposition   | Description   | Example                                                                                                |
|:----------------------|:--------------|:--------------|:-------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                  |
| coordinates           |               |               | time z lon lat                                                                                         |
| comment               |               |               | If the position is best represented as a circle, this field gives the radius of that circle in meters. |
| long_name             |               |               | Error radius                                                                                           |
| units                 |               |               | m                                                                                                      |
| instrument            |               |               | instrument_location                                                                                    |
| platform              |               |               | animal                                                                                                 |
| ancillary_variables   |               |               | lat lon offset offset_orientation                                                                      |
| coverage_content_type |               |               | qualityInformation                                                                                     |
| ioos_category         |               |               | Quality                                                                                                |


```
 <xarray.DataArray 'error_radius' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    long_name:              Error radius
    units:                  m
    comment:                If the position is best represented as a circle, ...
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  qualityInformation 
```

#### semi_major_axis

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                                                                  |
| coordinates           |               |               | time z lon lat                                                                                                                                                         |
| comment               |               |               | If the estimated position error is best expressed as an ellipse, this field gives the length in meters of the semi-major elliptical axis (one half of the major axis). |
| long_name             |               |               | Error - ellipse semi-major axis                                                                                                                                        |
| units                 |               |               | m                                                                                                                                                                      |
| instrument            |               |               | instrument_location                                                                                                                                                    |
| platform              |               |               | animal                                                                                                                                                                 |
| ancillary_variables   |               |               | lat lon ellipse_orientation offset offset_orientation                                                                                                                  |
| coverage_content_type |               |               | qualityInformation                                                                                                                                                     |
| ioos_category         |               |               | Quality                                                                                                                                                                |


```
 <xarray.DataArray 'semi_major_axis' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    units:                  m
    comment:                If the estimated position error is best expressed...
    long_name:              Error-elipse semi-major axis
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  auxillaryInformation 
```

#### semi_minor_axis

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                                                                  |
| coordinates           |               |               | time z lon lat                                                                                                                                                         |
| comment               |               |               | If the estimated position error is best expressed as an ellipse, this field gives the length in meters of the semi-minor elliptical axis (one half of the minor axis). |
| long_name             |               |               | Error - ellipse semi-major axis                                                                                                                                        |
| units                 |               |               | m                                                                                                                                                                      |
| instrument            |               |               | instrument_location                                                                                                                                                    |
| platform              |               |               | animal                                                                                                                                                                 |
| ancillary_variables   |               |               | lat lon ellipse_orientation offset offset_orientation                                                                                                                  |
| coverage_content_type |               |               | qualityInformation                                                                                                                                                     |
| ioos_category         |               |               | Quality                                                                                                                                                                |


```
 <xarray.DataArray 'semi_minor_axis' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    units:                  m
    comment:                If the estimated position error is best expressed...
    long_name:              Error-elipse semi-minor axis
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  auxillaryInformation 
```

#### ellipse_orientation

| Attribute             | Disposition   | Description   | Example                                                                                                                   |
|:----------------------|:--------------|:--------------|:--------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                     |
| coordinates           |               |               | time z lon lat                                                                                                            |
| comment               |               |               | The angle in degrees of the ellipse from true north, proceeding clockwise (0 to 360). A blank field represents 0 degrees. |
| long_name             |               |               | Error - ellipse orientation in degrees clockwise from true north                                                          |
| units                 |               |               | degrees                                                                                                                   |
| instrument            |               |               | instrument_location                                                                                                       |
| platform              |               |               | animal                                                                                                                    |
| ancillary_variables   |               |               | lat lon semi_major_axis semi_minor_axis offset offset_orientation                                                         |
| coverage_content_type |               |               | qualityInformation                                                                                                        |
| ioos_category         |               |               | Quality                                                                                                                   |


```
 <xarray.DataArray 'ellipse_orientation' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    units:                  degrees
    comment:                The angle in degrees of the ellipse from true nor...
    long_name:              Error ellipse orientation in degrees clockwise fr...
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  auxillaryInformation 
```

#### offset

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                                                          |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                                                                                                            |
| coordinates           |               |               | time z lon lat                                                                                                                                                                                                   |
| comment               |               |               | This field is non-zero if the circle or ellipse are not centered on the (Latitude, Longitude) values on this row. "Offset" gives the distance in meters from (Latitude, Longitude) to the center of the ellipse. |
| long_name             |               |               | Error - Offset in meters to center of error elipse or circle                                                                                                                                                     |
| units                 |               |               | m                                                                                                                                                                                                                |
| instrument            |               |               | instrument_location                                                                                                                                                                                              |
| platform              |               |               | animal                                                                                                                                                                                                           |
| ancillary_variables   |               |               | lat lon error_radius semi_major_axis semi_minor_axis offset_orientation                                                                                                                                          |
| coverage_content_type |               |               | qualityInformation                                                                                                                                                                                               |
| ioos_category         |               |               | Quality                                                                                                                                                                                                          |


```
 <xarray.DataArray 'offset' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    units:                  m
    comment:                This field is non-zero if the circle or ellipse a...
    long_name:              Offset in meters to center of error elipse or circle
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  auxillaryInformation 
```

#### offset_orientation

| Attribute             | Disposition   | Description   | Example                                                                                                                                                                                        |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                                                                                                                          |
| coordinates           |               |               | time z lon lat                                                                                                                                                                                 |
| comment               |               |               | If the "Offset" field is non-zero, this field is the angle in degrees from (Latitude, Longitude) to the center of the ellipse. Zero degrees is true north; a blank field represents 0 degrees. |
| long_name             |               |               | Error - Offset orientation angle to ellipse center                                                                                                                                             |
| units                 |               |               | degrees                                                                                                                                                                                        |
| instrument            |               |               | instrument_location                                                                                                                                                                            |
| platform              |               |               | animal                                                                                                                                                                                         |
| ancillary_variables   |               |               | lat lon error_radius semi_major_axis semi_minor_axis offset                                                                                                                                    |
| coverage_content_type |               |               | qualityInformation                                                                                                                                                                             |
| ioos_category         |               |               | Quality                                                                                                                                                                                        |


```
 <xarray.DataArray 'offset_orientation' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    units:                  degrees
    comment:                If the "Offset" field is non-zero, this field is ...
    long_name:              Offset orientation angle to ellipse center
    instrument:             instrument_location
    platform:               animal
    coverage_content_type:  auxillaryInformation 
```

#### gpe_msd

| Attribute             | Disposition   | Description   | Example                           |
|:----------------------|:--------------|:--------------|:----------------------------------|
| _FillValue            |               |               | -9999.9                           |
| coordinates           |               |               | time z lon lat                    |
| comment               |               |               | Historical. No longer applicable. |
| long_name             |               |               |                                   |
| units                 |               |               |                                   |
| instrument            |               |               | instrument_location               |
| platform              |               |               | animal                            |
| coverage_content_type |               |               | auxillaryInformation              |
| ioos_category         |               |               | Other                             |


```
 <xarray.DataArray 'gpe_msd' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs 
```

#### gpe_u

| Attribute             | Disposition   | Description   | Example                           |
|:----------------------|:--------------|:--------------|:----------------------------------|
| _FillValue            |               |               | -9999.9                           |
| coordinates           |               |               | time z lon lat                    |
| comment               |               |               | Historical. No longer applicable. |
| long_name             |               |               |                                   |
| units                 |               |               |                                   |
| instrument            |               |               | instrument_location               |
| platform              |               |               | animal                            |
| coverage_content_type |               |               | auxillaryInformation              |
| ioos_category         |               |               | Other                             |


```
 <xarray.DataArray 'gpe_u' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs 
```

#### count

| Attribute             | Disposition   | Description   | Example                                                                                        |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------|
| _FillValue            |               |               | -9999                                                                                          |
| coordinates           |               |               | time z lon lat                                                                                 |
| comment               |               |               | Total number of times a particular data item was received, verified, and successfully decoded. |
| long_name             |               |               | Count                                                                                          |
| units                 |               |               | count                                                                                          |
| instrument            |               |               | instrument_location                                                                            |
| platform              |               |               | animal                                                                                         |
| coverage_content_type |               |               | auxillaryInformation                                                                           |
| ioos_category         |               |               | Other                                                                                          |


```
 <xarray.DataArray 'count' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    long_name:              
    units:                  count
    coverage_content_type:  auxillaryInformation 
```

#### comment

| Attribute             | Disposition   | Description   | Example              |
|:----------------------|:--------------|:--------------|:---------------------|
| coordinates           |               |               | time z lon lat       |
| comment               |               |               | Optional text field  |
| long_name             |               |               | Comment              |
| instrument            |               |               | instrument_location  |
| platform              |               |               | animal               |
| coverage_content_type |               |               | auxillaryInformation |
| ioos_category         |               |               | Other                |


```
 <xarray.DataArray 'comment' (obs: 115)>
[115 values with dtype=float64]
Coordinates:
    time     (obs) datetime64[ns] ...
    z        (obs) float64 ...
    lat      (obs) float64 ...
    lon      (obs) float64 ...
Dimensions without coordinates: obs
Attributes:
    comment:    Optional text field
    long_name:  just a comment 
```

#### crs

| Attribute             | Disposition   | Description   | Example                                                                  |
|:----------------------|:--------------|:--------------|:-------------------------------------------------------------------------|
| epsg_code             |               |               | EPSG:4326                                                                |
| grid_mapping_name     |               |               | latitude_longitude                                                       |
| inverse_flattening    |               |               | 298.257223563                                                            |
| semi_major_axis       |               |               | 6378137.0                                                                |
| long_name             |               |               | Coordinate Reference System - http://www.opengis.net/def/crs/EPSG/0/4326 |
| coverage_content_type |               |               | coordinate                                                               |
| ioos_category         |               |               | Location                                                                 |


```
 <xarray.DataArray 'crs' ()>
[1 values with dtype=int32]
Attributes:
    epsg_code:           EPSG:4326
    grid_mapping_name:   latitude_longitude
    inverse_flattening:  298.257223563
    semi_major_axis:     6378137.0
    long_name:           Coordinate Reference System - http://www.opengis.net... 
```

#### instrument_location

| Attribute             | Disposition   | Description   | Example                       |
|:----------------------|:--------------|:--------------|:------------------------------|
| location_type         |               |               | argos / modeled               |
| comment               |               |               | Location                      |
| long_name             |               |               | Wildlife Computers SPLASH10-F |
| manufacturer          |               |               | Wildlife Computers            |
| make_model            |               |               | SPLASH10-F                    |
| calibration_date      |               |               |                               |
| serial_number         |               |               | 07A0358                       |
| coverage_content_type |               |               | referenceInformation          |
| ioos_category         |               |               | Other                         |


```
 <xarray.DataArray 'instrument_location' ()>
[1 values with dtype=object]
Attributes:
    long_name:         Wildlife Computers SPLASH10-F
    location_type:     argos/modeled
    comment:           Location
    manufacturer:      Wildlife Computers
    make_model:        SPLASH10-F
    calibration_date:  NOT PROVIDED
    serial_number:     07A0358 
```

#### instrument_tag

| Attribute             | Disposition   | Description   | Example                         |
|:----------------------|:--------------|:--------------|:--------------------------------|
| long_name             |               |               | telemetry tag applied to animal |
| manufacturer          |               |               | Wildlife Computers              |
| make_model            |               |               | SPLASH10-F                      |
| calibration_date      |               |               |                                 |
| serial_number         |               |               | 07A0358                         |
| coverage_content_type |               |               | referenceInformation            |
| ioos_category         |               |               | Other                           |


```
 <xarray.DataArray 'instrument_tag' ()>
[1 values with dtype=object]
Attributes:
    manufacturer:      Wildlife Computers
    make_model:        SPLASH10-F
    calibration_date:  NOT PROVIDED
    serial_number:     07A0358
    long_name:         telemetry tag applied to animal 
```

#### animal

| Attribute             | Disposition   | Description   | Example              |
|:----------------------|:--------------|:--------------|:---------------------|
| cf_role               |               |               | trajectory_id        |
| long_name             |               |               | tagged animal id     |
| valid_name            |               |               | Pusa caspica         |
| AphiaID               |               |               | 255022               |
| scientificname        |               |               | Pusa caspica         |
| authority             |               |               | Gmelin, 1788         |
| kingdom               |               |               | Animalia             |
| phylum                |               |               | Chordata             |
| class                 |               |               | Mammalia             |
| order                 |               |               | Carnivora            |
| family                |               |               | Phocidae             |
| genus                 |               |               | Pusa                 |
| taxonRankID           |               |               | 220                  |
| rank                  |               |               | Species              |
| superdomain           |               |               | Biota                |
| subphylum             |               |               | Vertebrata           |
| infraphylum           |               |               | Gnathostomata        |
| megaclass             |               |               | Tetrapoda            |
| subclass              |               |               | Theria               |
| suborder              |               |               | Caniformia           |
| infraorder            |               |               | Pinnipedia           |
| species               |               |               | Pusa caspica         |
| coverage_content_type |               |               | referenceInformation |
| ioos_category         |               |               | Other                |


```
 <xarray.DataArray 'animal' ()>
[1 values with dtype=object]
Attributes: (12/22)
    cf_role:         trajectory_id
    long_name:       tagged animal id
    valid_name:      Pusa caspica
    AphiaID:         255022
    scientificname:  Pusa caspica
    authority:       Gmelin, 1788
    ...              ...
    infraphylum:     Gnathostomata
    megaclass:       Tetrapoda
    subclass:        Theria
    suborder:        Caniformia
    infraorder:      Pinnipedia
    species:         Pusa caspica 
```

#### animal_life_stage

| Attribute             | Disposition   | Description   | Example                                       |
|:----------------------|:--------------|:--------------|:----------------------------------------------|
| long_name             |               |               | Lifestage of the animal at time of deployment |
| animal_life_stage     |               |               | adult                                         |
| coverage_content_type |               |               | referenceInformation                          |
| ioos_category         |               |               | Other                                         |


```
 <xarray.DataArray 'animal_life_stage' ()>
[1 values with dtype=object]
Attributes:
    long_name:          Lifestage of the animal at time of deployment (adult,...
    animal_life_stage:  adult 
```

#### animal_sex

| Attribute             | Disposition   | Description   | Example                                     |
|:----------------------|:--------------|:--------------|:--------------------------------------------|
| long_name             |               |               | sex of the animal at time of tag deployment |
| animal_sex            |               |               | female                                      |
| coverage_content_type |               |               | referenceInformation                        |
| ioos_category         |               |               | Other                                       |


```
 <xarray.DataArray 'animal_sex' ()>
[1 values with dtype=object]
Attributes:
    long_name:   sex of the animal at time of tag deployment
    animal_sex:  female 
```

#### animal_length

| Attribute             | Disposition   | Description   | Example                                                     |
|:----------------------|:--------------|:--------------|:------------------------------------------------------------|
| _FillValue            |               |               | -9999.9                                                     |
| long_name             |               |               | length of the animal as measured or estimated at deployment |
| units                 |               |               | m                                                           |
| animal_length_type    |               |               | standard length                                             |
| animal_length         |               |               | 1.12 m standard length                                      |
| coverage_content_type |               |               | referenceInformation                                        |
| ioos_category         |               |               | Other                                                       |


```
 <xarray.DataArray 'animal_length' ()>
[1 values with dtype=float32]
Attributes:
    long_name:              length of the animal as measured at deployment
    units:                  m
    coverage_content_type:  referenceInformation
    animal_length_type:     curve length 
```

#### animal_length_2

| Attribute             | Disposition   | Description   | Example                                                     |
|:----------------------|:--------------|:--------------|:------------------------------------------------------------|
| _FillValue            |               |               | -9999.9                                                     |
| long_name             |               |               | length of the animal as measured or estimated at deployment |
| units                 |               |               | m                                                           |
| animal_length_type    |               |               | curve length                                                |
| animal_length_2       |               |               | 1.38 m curve length                                         |
| coverage_content_type |               |               | referenceInformation                                        |
| ioos_category         |               |               | Other                                                       |


```
 <xarray.DataArray 'animal_length_2' ()>
[1 values with dtype=float32] 
```

#### animal_weight

| Attribute             | Disposition   | Description   | Example                                                   |
|:----------------------|:--------------|:--------------|:----------------------------------------------------------|
| _FillValue            |               |               | -9999.9                                                   |
| long_name             |               |               | mass of the animal as measured or estimated at deployment |
| units                 |               |               | kg                                                        |
| animal_weight         |               |               | 67.00 kg                                                  |
| coverage_content_type |               |               | referenceInformation                                      |
| ioos_category         |               |               | Other                                                     |


```
 <xarray.DataArray 'animal_weight' ()>
[1 values with dtype=float32]
Attributes:
    long_name:              mass of the animal as measured or estimated at de...
    units:                  kg
    animal_weight:          59.00 kg
    coverage_content_type:  referenceInformation 
```

#### animal_age

| Attribute             | Disposition   | Description   | Example                                                  |
|:----------------------|:--------------|:--------------|:---------------------------------------------------------|
| _FillValue            |               |               | -9999                                                    |
| long_name             |               |               | age of the animal as measured or estimated at deployment |
| units                 |               |               |                                                          |
| animal_age            |               |               |                                                          |
| coverage_content_type |               |               | referenceInformation                                     |
| ioos_category         |               |               | Other                                                    |

```
ADD NCML here
```

#### taxon_name

| Attribute             | Disposition   | Description   | Example                                                                                                                            |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------|
| standard_name         |               |               | biological_taxon_name                                                                                                              |
| long_name             |               |               | most precise taxonomic classification for the tagged animal                                                                        |
| source                |               |               | WoRMS (2023). Pusa caspica Gmelin, 1788. Accessed at: https://www.marinespecies.org/aphia.php?p=taxdetails&id=255022 on 2023-05-05 |
| url                   |               |               | https://www.marinespecies.org/aphia.php?p=taxdetails&id=255022                                                                     |
| coverage_content_type |               |               | referenceInformation                                                                                                               |
| ioos_category         |               |               | Other                                                                                                                              |


```
 <xarray.DataArray 'taxon_name' ()>
[1 values with dtype=object]
Attributes:
    standard_name:  biological_taxon_name
    long_name:      most precise taxonomic classification for the tagged animal
    source:         WoRMS (2023). Pusa caspica Gmelin, 1788. Accessed at: htt...
    url:            https://www.marinespecies.org/aphia.php?p=taxdetails&id=2... 
```

#### taxon_lsid

| Attribute             | Disposition   | Description   | Example                                                                                                                            |
|:----------------------|:--------------|:--------------|:-----------------------------------------------------------------------------------------------------------------------------------|
| standard_name         |               |               | biological_taxon_lsid                                                                                                              |
| long_name             |               |               | Namespaced Taxon Identifier for the tagged animal                                                                                  |
| source                |               |               | WoRMS (2023). Pusa caspica Gmelin, 1788. Accessed at: https://www.marinespecies.org/aphia.php?p=taxdetails&id=255022 on 2023-05-05 |
| url                   |               |               | https://www.marinespecies.org/aphia.php?p=taxdetails&id=255022                                                                     |
| coverage_content_type |               |               | referenceInformation                                                                                                               |
| ioos_category         |               |               | Other                                                                                                                              |


```
 <xarray.DataArray 'taxon_lsid' ()>
[1 values with dtype=object]
Attributes:
    standard_name:   biological_taxon_lsid
    long_name:       Namespaced Taxon Identifier for the tagged animal
    source:          WoRMS (2023). Pusa caspica Gmelin, 1788. Accessed at: ht...
    url:             https://www.marinespecies.org/aphia.php?p=taxdetails&id=...
    id_source_name:  
    id_source_link:   
```

### Example Dataset

#### File

Taken from the ATN satellite trajectory test WAF: <https://ncei.axiomdatascience.com/atn/test/>

#### NCML
```
dimensions:
	obs = 1057 ;
variables:
	float64 Ptt(obs) ;
		Ptt:long_name = Platform Transmitter Tag code. ;
		Ptt:comment = PTT code for this deployment. PTT codes may be used on multiple deployments, but  not concurrently. When combined with deployment dates, PTTs can uniquely identify a deployment. ;
		Ptt:coverage_content_type = referenceInformation ;
	<U15 animal() ;
		animal:cf_role = trajectory_id ;
		animal:long_name = BP6772 ;
		animal:valid_name = Chelonia mydas ;
		animal:AphiaID = 137206 ;
		animal:scientificname = Chelonia mydas ;
		animal:authority = (Linnaeus, 1758) ;
		animal:kingdom = Animalia ;
		animal:phylum = Chordata ;
		animal:class =  ;
		animal:order = Testudines ;
		animal:family = Cheloniidae ;
		animal:genus = Chelonia ;
		animal:taxonRankID = 220 ;
		animal:rank = Species ;
		animal:superdomain = Biota ;
		animal:subphylum = Vertebrata ;
		animal:infraphylum = Gnathostomata ;
		animal:megaclass = Tetrapoda ;
		animal:superclass = Reptilia ;
		animal:suborder = Cryptodira ;
		animal:superfamily = Chelonioidea ;
		animal:species = Chelonia mydas ;
	float32 animal_length() ;
		animal_length:long_name = length of the animal as measured at deployment ;
		animal_length:animal_length_type = curved carapice length ;
		animal_length:units = cm ;
		animal_length:coverage_content_type = referenceInformation ;
	<U8 animal_life_stage() ;
		animal_life_stage:long_name = Lifestage of the animal (adult, juvenile) ;
		animal_life_stage:animal_life_stage = Not provided ;
	<U7 animal_sex() ;
		animal_sex:long_name = sex of the animal ;
		animal_sex:animal_sex = unknown ;
	float32 animal_weight() ;
		animal_weight:long_name = mass of the animal as measured or estimated at deployment ;
		animal_weight:units = kg ;
		animal_weight:animal_weight = Not provided ;
		animal_weight:coverage_content_type = referenceInformation ;
	object comment(obs) ;
		comment:long_name = Comment ;
		comment:comment = Optional text field ;
	float64 count(obs) ;
		count:long_name =  ;
		count:units = count ;
		count:coverage_content_type = auxillaryInformation ;
	int32 crs() ;
		crs:epsg_code = EPSG:4326 ;
		crs:grid_mapping_name = latitude_longitude ;
		crs:inverse_flattening = 298.257223563 ;
		crs:long_name = http://www.opengis.net/def/crs/EPSG/0/4326 ;
		crs:semi_major_axis = 6378137.0 ;
	float64 deploy_id(obs) ;
		deploy_id:long_name = Platform identifier ;
		deploy_id:comment = Friendly name given to the tag by the user. If no specific friendly name is given, this is the PTT id. ;
		deploy_id:coverage_content_type = referenceInformation ;
	float64 ellipse_orientation(obs) ;
		ellipse_orientation:long_name = Platform identifier ;
		ellipse_orientation:units = degrees ;
		ellipse_orientation:comment = The angle in degrees of the ellipse from true north, proceeding clockwise (0 to 360). A blank field represents 0 degrees. ;
	float64 error_radius(obs) ;
		error_radius:long_name = Error radius ;
		error_radius:units = m ;
		error_radius:comment = If the position is best represented as a circle, this field gives the radius of that circle in meters. ;
	object instrument(obs) ;
		instrument:long_name = Instrument ;
		instrument:comment = Wildlife Computers instrument family.  ;
	<U22 instrument_location() ;
		instrument_location:long_name = Wildlife Computers SPOT6 ;
		instrument_location:location_type = argos/modeled ;
		instrument_location:comment = Location ;
		instrument_location:manufacturer = Wildlife Computers ;
		instrument_location:make_model = SPOT6 ;
		instrument_location:calibration_date = NOT PROVIDED ;
		instrument_location:serial_number = 19U0611 ;
	<U24 instrument_tag() ;
		instrument_tag:long_name = telemtry tag applied to animal ;
		instrument_tag:comment = Location ;
		instrument_tag:manufacturer = Wildlife Computers ;
		instrument_tag:make_model = SPOT6 ;
		instrument_tag:calibration_date = NOT PROVIDED ;
		instrument_tag:serial_number = 19U0611 ;
	float64 lat(obs) ;
		lat:axis = Y ;
		lat:_CoordinateAxisType = Lat ;
		lat:long_name = Profile Location ;
		lat:standard_name = latitude ;
		lat:units = degrees_north ;
		lat:valid_max = 90.0 ;
		lat:valid_min = -90.0 ;
		lat:actual_min = 30.0216 ;
		lat:actual_max = 30.7745 ;
	object location_class(obs) ;
		location_class:long_name = Location Quality Code ;
		location_class:standard_name = quality_code ;
		location_class:comment = Quality codes from the ARGOS satellite (in meters): G,3,2,1,0,A,B,Z. See http://www.argos-system.org/manual/3-location/34_location_classes.htm ;
	float64 lon(obs) ;
		lon:axis = X ;
		lon:_CoordinateAxisType = Lon ;
		lon:long_name = Profile Location ;
		lon:standard_name = longitude ;
		lon:units = degrees_east ;
		lon:valid_max = 180.0 ;
		lon:valid_min = -180.0 ;
		lon:actual_min = -88.0915 ;
		lon:actual_max = -86.0433 ;
	float64 offset(obs) ;
		offset:long_name = Offset ;
		offset:units = m ;
		offset:comment = This field is non-zero if the circle or ellipse are not centered on the (Latitude, Longitude) values on this row. "Offset" gives the distance in meters from (Latitude, Longitude) to the center of the ellipse. ;
	float64 offset_orientation(obs) ;
		offset_orientation:long_name = Offset orientation ;
		offset_orientation:units = degrees ;
		offset_orientation:comment = If the "Offset" field is non-zero, this field is the angle in degrees from (Latitude, Longitude) to the center of the ellipse. Zero degrees is true north; a blank field represents 0 degrees. ;
	float64 qartod_location_flag(obs) ;
		qartod_location_flag:flag_meanings = PASS NOT_EVALUATED SUSPECT FAIL MISSING ;
		qartod_location_flag:implementation = https://github.com/ioos/ioos_qc/ ;
		qartod_location_flag:long_name = Location QC test - Location test ;
		qartod_location_flag:references = https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf ;
		qartod_location_flag:standard_name = location_test_quality_flag ;
		qartod_location_flag:flag_values = [1 2 3 4 9] ;
	float64 qartod_rollup_flag(obs) ;
		qartod_rollup_flag:flag_meanings = PASS NOT_EVALUATED SUSPECT FAIL MISSING ;
		qartod_rollup_flag:implementation = https://github.com/ioos/ioos_qc/ ;
		qartod_rollup_flag:long_name = Aggregate QC value ;
		qartod_rollup_flag:references = https://github.com/ioos/ioos_qc/ ;
		qartod_rollup_flag:standard_name = aggregate_quality_flag ;
		qartod_rollup_flag:flag_values = [1 2 3 4 9] ;
	float64 qartod_speed_flag(obs) ;
		qartod_speed_flag:flag_meanings = PASS NOT_EVALUATED SUSPECT FAIL MISSING ;
		qartod_speed_flag:implementation = https://github.com/ioos/ioos_qc/ ;
		qartod_speed_flag:long_name = Speed QC test - gross range test ;
		qartod_speed_flag:references = https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf ;
		qartod_speed_flag:standard_name = gross_range_test_quality_flag ;
		qartod_speed_flag:flag_values = [1 2 3 4 9] ;
	float64 qartod_time_flag(obs) ;
		qartod_time_flag:flag_meanings = PASS NOT_EVALUATED SUSPECT FAIL MISSING ;
		qartod_time_flag:implementation = https://github.com/ioos/ioos_qc/ ;
		qartod_time_flag:long_name = Time QC test - gross range test ;
		qartod_time_flag:references = https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual_Update2_200324_final.pdf ;
		qartod_time_flag:standard_name = gross_range_test_quality_flag ;
		qartod_time_flag:flag_values = [1 2 3 4 9] ;
	float64 semi_major_axis(obs) ;
		semi_major_axis:long_name = Error semi-major axis ;
		semi_major_axis:units = m ;
		semi_major_axis:comment = If the estimated position error is best expressed as an ellipse, this field gives the length in meters of the semi-major elliptical axis (one half of the major axis). ;
	float64 semi_minor_axis(obs) ;
		semi_minor_axis:long_name = Error semi-minor axis ;
		semi_minor_axis:units = m ;
		semi_minor_axis:comment = If the estimated position error is best expressed as an ellipse, this field gives the length in meters of the semi-minor elliptical axis (one half of the minor axis). ;
	<U41 taxon_lsid() ;
		taxon_lsid:standard_name = biological_taxon_lsid ;
		taxon_lsid:long_name = Namespaced Taxon Identifier for the tagged animal ;
		taxon_lsid:source = Uetz, P. (ed.) (2023). The Reptile Database. Chelonia mydas (Linnaeus, 1758). Accessed through: World Register of Marine Species at: https://www.marinespecies.org/aphia.php?p=taxdetails&id=137206 on 2023-04-19 ;
		taxon_lsid:url = https://www.marinespecies.org/aphia.php?p=taxdetails&id=137206 ;
		taxon_lsid:id_source_name =  ;
		taxon_lsid:id_source_link =  ;
	<U14 taxon_name() ;
		taxon_name:standard_name = biological_taxon_name ;
		taxon_name:long_name = most precise taxonomic classification for the tagged animal ;
		taxon_name:source = Uetz, P. (ed.) (2023). The Reptile Database. Chelonia mydas (Linnaeus, 1758). Accessed through: World Register of Marine Species at: https://www.marinespecies.org/aphia.php?p=taxdetails&id=137206 on 2023-04-19 ;
		taxon_name:url = https://www.marinespecies.org/aphia.php?p=taxdetails&id=137206 ;
	datetime64[ns] time(obs) ;
		time:standard_name = time ;
		time:axis = T ;
		time:_CoordinateAxisType = Time ;
		time:long_name = Time ;
		time:actual_min = 2019-10-14T16:23:09Z ;
		time:actual_max = 2020-03-03T15:46:10Z ;
	<U24 trajectory() ;
		trajectory:cf_role = trajectory_id ;
		trajectory:long_name = trajectory identifier ;
	object type(obs) ;
		type:long_name = Type of location ;
		type:comment = Type of location: Argos ;
	float64 z(obs) ;
		z:axis = Z ;
		z:long_name = depth ;
		z:positive = down ;
		z:standard_name = depth ;
		z:units = m ;
		z:actual_min = 0.0 ;
		z:actual_max = 0.0 ;
// global attributes:
	:date_created = 2021-08-12T20:47:14Z ;
	:featureType = trajectory ;
	:cdm_data_type = Trajectory ;
	:argos_program_number = 27141 ;
	:creator_email = kristen_hart@usgs.gov ;
	:id = 5e3a16da6321be14905fda08 ;
	:source = Service Argos ;
	:geospatial_lat_units = degrees_north ;
	:geospatial_lon_units = degrees_east ;
	:naming_authority = gov.noaa.ioos.atn ;
	:processing_level = NetCDF file created from position data obtained from Wildlife Computers API. ;
	:publisher_email = atndata@ioos.us ;
	:publisher_url = https://atn.ioos.us ;
	:publisher_country = USA ;
	:standard_name_vocabulary = CF-v78 ;
	:vendor = Wildlife Computers ;
	:geospatial_lat_min = 30.0216 ;
	:geospatial_lat_max = 30.7745 ;
	:geospatial_lon_min = -88.0915 ;
	:geospatial_lon_max = -86.0433 ;
	:geospatial_bbox = POLYGON ((-86.0433 30.0216, -86.0433 30.7745, -88.0915 30.7745, -88.0915 30.0216, -86.0433 30.0216)) ;
	:geospatial_bounds = POLYGON ((-88.0915 30.0216, -87.93510000000001 30.4294, -87.4914 30.6658, -87.2508 30.7745, -86.0433 30.0702, -88.0915 30.0216)) ;
	:geospatial_bounds_crs = EPSG:4326 ;
	:time_coverage_start = 2019-10-14T16:23:09Z ;
	:time_coverage_end = 2020-03-03T15:46:10Z ;
	:time_coverage_duration = P140DT23H23M1S ;
	:time_coverage_resolution = P0DT3H18M3S ;
	:date_issued = 2021-08-12T20:47:14Z ;
	:date_modified = 2021-08-12T20:47:14Z ;
	:vendor_id = 5e3a16da6321be14905fda08 ;
	:Conventions = CF-1.10, ACDD-1.3, IOOS-1.2 ;
	:acknowledgement = NOAA IOOS, Axiom Data Science, Navy ONR, NOAA NMFS, Wildlife Computers, Argos, IOOS ATN ;
	:creator_name = Kristen Hart ;
	:creator_url = https://orcid.org/0000-0002-5257-7974 ;
	:infoUrl = https://portal.atn.ioos.us/#metadata/6af10e97-4668-4dd0-9868-5ca029cb2f7a/project ;
	:institution = USGS Wetland Aquatic Research Center ;
	:license = These data may be used and redistributed for free, but are not intended for legal use, since they may contain inaccuracies. No person or group associated with these data makes any warranty, expressed or implied, including warranties of merchantability and fitness for a particular purpose, or assumes any legal liability for the accuracy, completeness or usefulness of this information. This disclaimer applies to both individual use of these data and aggregate use with other data. It is strongly recommended that users read and fully comprehend associated metadata prior to use. Please acknowledge the U.S. Animal Telemetry Network (ATN) or the specified citation as the source from which these data were obtained in any publications and/or representations of these data. Communication and collaboration with dataset authors are strongly encouraged. ;
	:metadata_link = https://anotherfakeurlforthisproject.coffee ;
	:project = Spatial Ecology of loggerhead turtles tagged at the Azores, 1994-2000 ;
	:publisher_institution = US Integrated Ocean Observing System Office ;
	:publisher_name = US Integrated Ocean Observing System (IOOS) Animal Telemetry Network (ATN) ;
	:uuid = 706a2a4f-73b1-4b0c-9498-2c61dc22cfd7 ;
	:platform_name = Chelonia mydas ;
	:platform_id = 137206 ;
	:animal_common_name = Green Sea Turtle ;
	:animal_id = 982000410612253 ;
	:animal_scientific_name = Chelonia mydas ;
	:arbitrary_keywords = ATN ,Animal Telemetry Network, IOOS, Integrated Ocean Observing System, trajectory ;
	:comment = nan ;
	:contributor_email = mcherkiss@usgs.gov ;
	:contributor_name = Michael Cherkiss ;
	:contributor_role = collaborator ;
	:contributor_role_vocabulary = https://vocab.nerc.ac.uk/collection/G04/current/ ;
	:creator_country = USA ;
	:creator_institution = USGS Wetland Aquatic Research Center ;
	:creator_institution_url = https://www.usgs.gov/centers/wetland-and-aquatic-research-center ;
	:creator_role = principalInvestigator ;
	:creator_role_vocabulary = https://vocab.nerc.ac.uk/collection/G04/current/ ;
	:creator_sector = gov_federal ;
	:creator_sector_vocabulary = https://mmisw.org/ont/ioos/sector ;
	:creator_type = person ;
	:deployment_id = 5e3a16da6321be14905fda08 ;
	:deployment_start_lat = 30.29581 ;
	:deployment_start_lon = -87.53123 ;
	:deployment_start_datetime = 2019-10-14T00:00:00Z ;
	:deployment_end_datetime = 2020-03-03T00:00:00Z ;
	:instrument = Satellite telemetry tag ;
	:instrument_vocabulary = nan ;
	:keywords_vocabulary = GCMD Science Keywords v15.1 ;
	:ncei_template_version = NCEI_NetCDF_Trajectory_Template_v2.0 ;
	:product_version = nan ;
	:program = IOOS Animal Telemetry Network ;
	:ptt_id = 181790 ;
	:publisher_type = institution ;
	:references = nan ;
	:wmo_platform_code = 990nnnn ;
	:sea_name = Coastal Waters of Florida, Coastal Waters of Alabama, and Gulf of Mexico ;
	:history = Wed Apr 19 15:22:21 2023: ncks -x -v gpe_u,gpe_msd atn_02.nc atn_03.nc
Wed Apr 19 15:21:54 2023: ncrename -v qartod_location_test,qartod_location_flag -v argo_speed_test,qartod_speed_flag -v qartod_rollup_qc,qartod_rollup_flag -v time_axds_valid_range_test,qartod_time_flag atn_00.nc atn_01.nc
2021-08-12T20:47:14Z - Created by the IOOS ATN DAC from the Wildlife Computers API ;
	:NCO = netCDF Operators version 4.9.1 (Homepage = http://nco.sf.net, Code = http://github.com/nco/nco) ;
	:platform = organism ;
	:platform_vocabulary = http://vocab.nerc.ac.uk/collection/L06/current/ ;
	:date_metadata_modified = 2023-04-19T15:17:00Z ;
	:keywords = Earth Science > Biological Classification > Animals/Vertebrates, Earth Science > Biosphere > Ecological Dynamics > Species/Population Interactions > Migratory Rates/Routes, Earth Science>Biosphere > Ecosystems > Marine Ecosystems, Providers>Government Agencies-U.S. Federal Agencies > DOC > NOAA > IOOS, Providers>Commercial>Axiom Data Science ;
	:summary = Wildlife Computers SPOT6 tag (ptt id 181790) deployed on a Green Sea Turtle (Chelonia mydas) by Kristen Hart in Coastal Waters of Florida, Coastal Waters of Alabama, and Gulf of Mexico from 2019-10-14 to 2020-03-03. ;
	:citation = Hart, Kristen; Cherkiss, Michael. (2023) Green sea turtle (Chelonia mydas) location data from a satellite telemetry tag (ptt id 181790) deployed from 2019-10-14 to 2020-03-03 in the Coastal Waters of Florida, Coastal Waters of Alabama, and Gulf of Mexico. [Dataset]. US Integrated Ocean Observing System (IOOS) Animal Telemetry Network (ATN). ;
	:title = Green sea turtle (Chelonia mydas) location data from a satellite telemetry tag (ptt id 181790) deployed from 2019-10-14 to 2020-03-03 in the Coastal Waters of Florida, Coastal Waters of Alabama, and Gulf of Mexico ;
```

Variables

```
'Ptt': <xarray.Variable (obs: 1057)>
array([181790., 181790., 181790., ..., 181790., 181790., 181790.])
Attributes:
    long_name:              Platform Transmitter Tag code.
    comment:                PTT code for this deployment. PTT codes may be us...
    coverage_content_type:  referenceInformation,

'animal': <xarray.Variable ()>
array('982000410612253', dtype='<U15')
Attributes: (12/22)
    cf_role:         trajectory_id
    long_name:       BP6772
    valid_name:      Chelonia mydas
    AphiaID:         137206
    scientificname:  Chelonia mydas
    authority:       (Linnaeus, 1758)
    ...              ...
    infraphylum:     Gnathostomata
    megaclass:       Tetrapoda
    superclass:      Reptilia
    suborder:        Cryptodira
    superfamily:     Chelonioidea
    species:         Chelonia mydas,

'animal_length': <xarray.Variable ()>
array(-9999., dtype=float32)
Attributes:
    long_name:              length of the animal as measured at deployment
    animal_length_type:     curved carapice length
    units:                  cm
    coverage_content_type:  referenceInformation,

'animal_life_stage': <xarray.Variable ()>
array('Juvenile', dtype='<U8')
Attributes:
    long_name:          Lifestage of the animal (adult, juvenile)
    animal_life_stage:  Not provided,

'animal_sex': <xarray.Variable ()>
array('unknown', dtype='<U7')
Attributes:
    long_name:   sex of the animal
    animal_sex:  unknown,

'animal_weight': <xarray.Variable ()>
array(9.96921e+36, dtype=float32)
Attributes:
    long_name:              mass of the animal as measured or estimated at de...
    units:                  kg
    animal_weight:          Not provided
    coverage_content_type:  referenceInformation,

'comment': <xarray.Variable (obs: 1057)>
array(['nan', 'nan', 'nan', ..., 'nan', 'Lon > 4 deviations from mean', 'nan'],
      dtype=object)
Attributes:
    long_name:  Comment
    comment:    Optional text field,

'count': <xarray.Variable (obs: 1057)>
array([nan, nan, nan, ..., nan, nan, nan])
Attributes:
    long_name:              
    units:                  count
    coverage_content_type:  auxillaryInformation,

'crs': <xarray.Variable ()>
array(-2147483647)
Attributes:
    epsg_code:           EPSG:4326
    grid_mapping_name:   latitude_longitude
    inverse_flattening:  298.257223563
    long_name:           http://www.opengis.net/def/crs/EPSG/0/4326
    semi_major_axis:     6378137.0,

'deploy_id': <xarray.Variable (obs: 1057)>
array([181790., 181790., 181790., ..., 181790., 181790., 181790.])
Attributes:
    long_name:              Platform identifier
    comment:                Friendly name given to the tag by the user. If no...
    coverage_content_type:  referenceInformation,

'ellipse_orientation': <xarray.Variable (obs: 1057)>
array([  9., 118.,   1., ...,  75.,  79., 173.])
Attributes:
    long_name:  Platform identifier
    units:      degrees
    comment:    The angle in degrees of the ellipse from true north, proceedi...,

'error_radius': <xarray.Variable (obs: 1057)>
array([1569., 1322., 2703., ..., 1202., 3691., 3178.])
Attributes:
    long_name:  Error radius
    units:      m
    comment:    If the position is best represented as a circle, this field g...,

'instrument': <xarray.Variable (obs: 1057)>
array(['UT', 'UT', 'UT', ..., 'UT', 'UT', 'UT'], dtype=object)
Attributes:
    long_name:  Instrument
    comment:    Wildlife Computers instrument family. ,

'instrument_location': <xarray.Variable ()>
array('Wildlife Computers SDR', dtype='<U22')
Attributes:
    long_name:         Wildlife Computers SPOT6
    location_type:     argos/modeled
    comment:           Location
    manufacturer:      Wildlife Computers
    make_model:        SPOT6
    calibration_date:  NOT PROVIDED
    serial_number:     19U0611,

'instrument_tag': <xarray.Variable ()>
array('Wildlife Computers SPOT6', dtype='<U24')
Attributes:
    long_name:         telemtry tag applied to animal
    comment:           Location
    manufacturer:      Wildlife Computers
    make_model:        SPOT6
    calibration_date:  NOT PROVIDED
    serial_number:     19U0611,

'lat': <xarray.Variable (obs: 1057)>
array([30.3119, 30.3193, 30.2943, ..., 30.4021, 30.415 , 30.4018])
Attributes:
    axis:                 Y
    _CoordinateAxisType:  Lat
    long_name:            Profile Location
    standard_name:        latitude
    units:                degrees_north
    valid_max:            90.0
    valid_min:            -90.0
    actual_min:           30.0216
    actual_max:           30.7745,

'location_class': <xarray.Variable (obs: 1057)>
array(['0', '1', 'B', ..., 'B', 'B', 'B'], dtype=object)
Attributes:
    long_name:      Location Quality Code
    standard_name:  quality_code
    comment:        Quality codes from the ARGOS satellite (in meters): G,3,2...,

'lon': <xarray.Variable (obs: 1057)>
array([-87.5671, -87.5581, -87.5399, ..., -86.8046, -86.7424, -86.8053])
Attributes:
    axis:                 X
    _CoordinateAxisType:  Lon
    long_name:            Profile Location
    standard_name:        longitude
    units:                degrees_east
    valid_max:            180.0
    valid_min:            -180.0
    actual_min:           -88.0915
    actual_max:           -86.0433,

'offset': <xarray.Variable (obs: 1057)>
array([nan, nan, nan, ..., nan, nan, nan])
Attributes:
    long_name:  Offset
    units:      m
    comment:    This field is non-zero if the circle or ellipse are not cente...,

'offset_orientation': <xarray.Variable (obs: 1057)>
array([nan, nan, nan, ..., nan, nan, nan])
Attributes:
    long_name:  Offset orientation
    units:      degrees
    comment:    If the "Offset" field is non-zero, this field is the angle in...,

'qartod_location_flag': <xarray.Variable (obs: 1057)>
array([1., 1., 1., ..., 1., 1., 1.])
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Location QC test - Location test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   location_test_quality_flag
    flag_values:     [1 2 3 4 9],

'qartod_rollup_flag': <xarray.Variable (obs: 1057)>
array([1., 1., 1., ..., 4., 1., 4.])
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Aggregate QC value
    references:      https://github.com/ioos/ioos_qc/
    standard_name:   aggregate_quality_flag
    flag_values:     [1 2 3 4 9],

'qartod_speed_flag': <xarray.Variable (obs: 1057)>
array([2., 1., 1., ..., 4., 1., 4.])
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Speed QC test - gross range test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   gross_range_test_quality_flag
    flag_values:     [1 2 3 4 9],

'qartod_time_flag': <xarray.Variable (obs: 1057)>
array([1., 1., 1., ..., 1., 1., 1.])
Attributes:
    flag_meanings:   PASS NOT_EVALUATED SUSPECT FAIL MISSING
    implementation:  https://github.com/ioos/ioos_qc/
    long_name:       Time QC test - gross range test
    references:      https://cdn.ioos.noaa.gov/media/2020/03/QARTOD_TS_Manual...
    standard_name:   gross_range_test_quality_flag
    flag_values:     [1 2 3 4 9],

'semi_major_axis': <xarray.Variable (obs: 1057)>
array([2165., 3352., 5079., ..., 1427., 4916., 3291.])
Attributes:
    long_name:  Error semi-major axis
    units:      m
    comment:    If the estimated position error is best expressed as an ellip...,

'semi_minor_axis': <xarray.Variable (obs: 1057)>
array([1137.,  521., 1438., ..., 1012., 2771., 3069.])
Attributes:
    long_name:  Error semi-minor axis
    units:      m
    comment:    If the estimated position error is best expressed as an ellip...,

'taxon_lsid': <xarray.Variable ()>
array('urn:lsid:marinespecies.org:taxname:137206', dtype='<U41')
Attributes:
    standard_name:   biological_taxon_lsid
    long_name:       Namespaced Taxon Identifier for the tagged animal
    source:          Uetz, P. (ed.) (2023). The Reptile Database. Chelonia my...
    url:             https://www.marinespecies.org/aphia.php?p=taxdetails&id=...
    id_source_name:  
    id_source_link:  ,

'taxon_name': <xarray.Variable ()>
array('Chelonia mydas', dtype='<U14')
Attributes:
    standard_name:  biological_taxon_name
    long_name:      most precise taxonomic classification for the tagged animal
    source:         Uetz, P. (ed.) (2023). The Reptile Database. Chelonia myd...
    url:            https://www.marinespecies.org/aphia.php?p=taxdetails&id=1...,

'time': <xarray.Variable (obs: 1057)>
array(['2019-10-14T16:23:09.000000000', '2019-10-14T16:43:02.000000000',
       '2019-10-15T15:45:28.000000000', ..., '2020-03-03T03:00:17.000000000',
       '2020-03-03T15:36:04.000000000', '2020-03-03T15:46:10.000000000'],
      dtype='datetime64[ns]')
Attributes:
    standard_name:        time
    axis:                 T
    _CoordinateAxisType:  Time
    long_name:            Time
    actual_min:           2019-10-14T16:23:09Z
    actual_max:           2020-03-03T15:46:10Z,

'trajectory': <xarray.Variable ()>
array('5e3a16da6321be14905fda08', dtype='<U24')
Attributes:
    cf_role:    trajectory_id
    long_name:  trajectory identifier,

'type': <xarray.Variable (obs: 1057)>
array(['Argos', 'Argos', 'Argos', ..., 'Argos', 'Argos', 'Argos'], dtype=object)
Attributes:
    long_name:  Type of location
    comment:    Type of location: Argos,

'z': <xarray.Variable (obs: 1057)>
array([0., 0., 0., ..., 0., 0., 0.])
Attributes:
    axis:           Z
    long_name:      depth
    positive:       down
    standard_name:  depth
    units:          m
    actual_min:     0.0
    actual_max:     0.0
```