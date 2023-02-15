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

Identifier | Location in file | Description | Example value
:--------- | :---------------: | :----------- | :------------:
test | test | test | test


## ATN Satellite Trajectory Specification Attributes

### Global attributes

NEED TO UPDATE

Name | Convention | Description | Type 
:--------- | :-------: | :------------------- | :--------: 
`Conventions` | CF | A comma-separated list of the conventions that are followed by the dataset. For files that follow this version of the IOOS Metadata Profile, include the string "IOOS-1.2".<br><br>Example: {::nomarkdown}<ul><li><b><code>Conventions = "CF-1.6, ACDD-1.3, IOOS-1.2"</b></code></li></ul>{:/} | global
`featureType` | CF | CF attribute for identifying the featureType.   <br><br>Example:{::nomarkdown}<ul><li><b><code>featureType = "timeSeries"</b></code></li></ul>{:/} | global
`id` | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global
`infoUrl`  | IOOS | URL for background information about this dataset. This attributed is also required by ERDDAP. | global
`keywords` | ACDD | A comma separated list of key words and phrases. | global
`license`  | ACDD | Describe the restrictions to data access and distribution. | global
`naming_authority`  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:{::nomarkdown}<ul><li><b><code>naming_authority = "edu.ucar.unidata"</b></code></li></ul>{:/} | global
`references`  | ACDD/CF | Published or web-based references that describe the data or methods used to produce it. Recommend URIs (such as a URL or DOI) for papers or other references. Multiple references should be separated by commas. | global
`standard_name_vocabulary`  | ACDD | The name and version of the controlled vocabulary from which variable standard names are taken. Values for any variable's **`standard_name`** attribute must come from the CF Standard Names vocabulary for the dataset to comply with CF. <br><br>The format for the **`standard_name`** attribute must follow the ACDD recommendation ('CF Standard Name Table vXX', where 'XX' is a version of the standard name table), in order to be valid and meet the ACDD conventions.<br><br>If a variables does not have an existing standard name in the CF-managed list, the variable should not include a **`standard_name`** attribute. In these cases, a standard name can be proposed to the CF community for consideration.<br><br>  Example:<br>{::nomarkdown}<ul><li><b><code>standard_name_vocabulary = "CF Standard Name Table v72"</b></code></li></ul>{:/} | global
`summary`  | ACDD | One paragraph describing the data set. |  global
`title`  | ACDD | One sentence about the data contained within the file. | global

### Variable attributes

#### time

#### z

### Dataset Description

The attributes listed below are a collection of high-level attributes recommended largely by the parent conventions of the IOOS Metadata Profile (CF, ACDD).  Their purpose is to describe the dataset in human-readable terms, define specific conventions used by other attributes (**`standard_name_vocabulary`**), or qualify other attributes (**`naming_authority`**).  A high-quality dataset will generally include meaningful values for all of these attributes, even though they are not all required according to the profile.

Name | Convention | Description | Type 
:--------- | :-------: | :------------------- | :--------: 
`Conventions` | CF | A comma-separated list of the conventions that are followed by the dataset. For files that follow this version of the IOOS Metadata Profile, include the string "IOOS-1.2".<br><br>Example: {::nomarkdown}<ul><li><b><code>Conventions = "CF-1.6, ACDD-1.3, IOOS-1.2"</b></code></li></ul>{:/} | global
`featureType` | CF | CF attribute for identifying the featureType.   <br><br>Example:{::nomarkdown}<ul><li><b><code>featureType = "timeSeries"</b></code></li></ul>{:/} | global
`id` | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global
`infoUrl`  | IOOS | URL for background information about this dataset. This attributed is also required by ERDDAP. | global
`keywords` | ACDD | A comma separated list of key words and phrases. | global
`license`  | ACDD | Describe the restrictions to data access and distribution. | global
`naming_authority`  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:{::nomarkdown}<ul><li><b><code>naming_authority = "edu.ucar.unidata"</b></code></li></ul>{:/} | global
`references`  | ACDD/CF | Published or web-based references that describe the data or methods used to produce it. Recommend URIs (such as a URL or DOI) for papers or other references. Multiple references should be separated by commas. | global
`standard_name_vocabulary`  | ACDD | The name and version of the controlled vocabulary from which variable standard names are taken. Values for any variable's **`standard_name`** attribute must come from the CF Standard Names vocabulary for the dataset to comply with CF. <br><br>The format for the **`standard_name`** attribute must follow the ACDD recommendation ('CF Standard Name Table vXX', where 'XX' is a version of the standard name table), in order to be valid and meet the ACDD conventions.<br><br>If a variables does not have an existing standard name in the CF-managed list, the variable should not include a **`standard_name`** attribute. In these cases, a standard name can be proposed to the CF community for consideration.<br><br>  Example:<br>{::nomarkdown}<ul><li><b><code>standard_name_vocabulary = "CF Standard Name Table v72"</b></code></li></ul>{:/} | global
`summary`  | ACDD | One paragraph describing the data set. |  global
`title`  | ACDD | One sentence about the data contained within the file. | global

#### Example

Taken from the [ATN satellite trajectory Example dataset]().

```
add example ncml (json) here
```

### Attribution

The attributes listed in the table below allow for consistent attribution of datasets within IOOS' national products.  Data providers are encouraged to follow these attribute guidelines exactly to ensure datasets appear with proper attribution.  

Consult the [Gold Standard Example Datasets](gold-standard-examples.html) for good examples to start from.

Name | Convention | Description | Type 
:--------- | :-------: | :------------------- | :--------: 
`contributor_email` | IOOS | Email addresses of the individuals or institutions that contributed to the creation of this data. Multiple emails should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global
`contributor_name` | ACDD | The name of any individuals or institutions that contributed to the creation of this data. Combined with the **`contributor_role`**, it provides the full description of the contributor. Multiple names should be given in CSV format. <br><br>Examples: {::nomarkdown}<ul><li><b><code>contributor_name = "Pacific Islands Ocean Observing System (PacIOOS)"</b></code></li> <li><b><code>contributor_name = "Great Lakes Observing System (GLOS),LimnoTech"</b></code></li></ul>{:/} | global
`contributor_role` | ACDD | The role of any individuals or institutions that contributed to the creation of this data. The CI_RoleCode vocabulary ([NERC](https://vocab.nerc.ac.uk/collection/G04/current/), [NOAA-NCEI](https://www.ngdc.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#CI_RoleCode)) should be used. Multiple roles should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**.<br>For the IOOS ncSOS, **`contributor_role = "sponsor"`** defines a person, group, or organization’s full or partial support of an IOOS activity, asset, model, or product. <br><br>Examples:  {::nomarkdown}<ul><li><b><code>contributor_role = "sponsor"</b></code></li> <li><b><code>contributor_role = "sponsor, collaborator"</b></code></li></ul>{:/} | global
`contributor_role_vocabulary` | IOOS | The URL of the controlled vocabulary used for the **`contributor_role`** attribute. <br><br>The default is ["https://vocab.nerc.ac.uk/collection/G04/current/"](https://vocab.nerc.ac.uk/collection/G04/current/). | global
`contributor_url` | IOOS | The URL of the individuals or institutions that contributed to the creation of this data. Multiple URLs should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global
`creator_address` | IOOS | Street address of the person or organization that collected the data.  | global
`creator_city` | IOOS | City of the person or organization that collected the data.  | global
`creator_country` | IOOS | Country of the person or organization that operates a platform or network, which collected the observation data. | global
`creator_email`  | ACDD | Email address of the person or institution that collected the data. | global
`creator_institution`  | ACDD | Institution that collected the data. This should be specified even if it matches the value of **`publisher_institution`**, **`institution`** or if **`creator_type`** is institution. | global
`creator_institution_url`  | IOOS | URL for the institution that collected the data. For clarity, it is recommended that this field is specified even if the creator_type is institution and a creator_url is provided. | global
`creator_name`  | ACDD | Name of the person or organization that collected the data. <br><br>Follow the guidance described in the **`creator_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global
`creator_phone` | IOOS | The phone number of the person or group that collected the data. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global
`creator_sector` | IOOS | [IOOS classifier](https://mmisw.org/ont/ioos/sector) that best describes the platform (network) operator's societal sector. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_sector = "academic"</b></code></li></ul>{:/} | global
`creator_state` | IOOS | State of the person or organization that collected the data.  | global
`creator_type` | ACDD | Specifies type of creator with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the creator is assumed to be a person.  | global
`creator_url`  | ACDD | URL of the person or organization that collected the data.  | global
`creator_postalcode` | IOOS | The postal code of the person or organization that collected the data.  | global
`institution`  | ACDD | The institution of the person or group that collected the data. | global
`publisher_address` | IOOS | Street address of the person or organization that distributes the data.   | global
`publisher_city` | IOOS | City of the person or organization that distributes the data.   | global
`publisher_country` | IOOS | Country of the person or organization that distributes the data.   | global
`publisher_email`  | ACDD | The email address of the person or group that distributes the data files. | global
`publisher_institution`  | ACDD | Institution that distributes the data. This should be specified even if **`publisher_type`** is institution (in which case **`publisher_name`** would have an identical value). | global
`publisher_name`  | ACDD | Name of the person or group that distributes the data files. <br><br>Follow the guidance described in the **`publisher_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global
`publisher_phone` | IOOS | The phone number of the person or group that distributes the data files. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global
`publisher_state` | IOOS | State of the person or organization that distributes the data.   | global
`publisher_type` | ACDD | Specifies type of publisher with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the publisher is assumed to be a person. | global
`publisher_url`  | ACDD/IOOS | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if **`publisher_type=person`**.   | global
`publisher_postalcode` | IOOS | The postal code of the person or organization that distributes the data.   | global

#### Example

Taken from the [ATN Satellite Trajectory Example dataset]().

```
add example ncml (json) here
```

```
add example ncml (json) here
```

```
add example ncml (json) here
```

### Variables

A collection of variable attributes that should be applied to all geophysical or other measured parameter variable contained in the dataset.  This is mostly a re-listing and description of how to use CF convention attributes, with the addition of a few IOOS-specific attributes for variable precision/accuracy and standard name identification.  

**Note:** the table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data.

Name | Convention | Description | Type 
:--------- | :-------: | :------------------- | :--------: 
`geophysical_variable:_FillValue` | CF | This value is considered to be a special value that indicates undefined or missing data, and is returned when reading values that were not written. The type of this variable should match the type of the unpacked variable data. {::nomarkdown}<ul><b><code>  <li>time:_FillValue = -999999.0f    <li>lat:_FillValue = -999999.0f    <li>lon:_FillValue = -999999.0f    <li>z:_FillValue = -999999.0f    <li>sea_water_temperature:_FillValue = Float.NaN</li></b></code></ul>{:/} | variable
`geophysical_variable:accuracy` | IOOS | The sensor accuracy is the closeness of the measurements to the variable's true value. It should be given in the same units as the measured variable. If the instrument has been calibrated multiple times with different results, the most recent accuracy should be provided here (see **`instrument_variable:calibration_date`**). | variable
`geophysical_variable:missing_value` | CF | This should always be equal to the `_FillValue` attribute and both are used for legacy library support. {::nomarkdown}<ul><b><code> <li>time:missing_value = -999999.0f    <li>lat:missing_value = -999999.0f    <li>lon:missing_value =-999999.0f    <li>z:missing_value = -999999.0f <li>sea_water_temperature:missing_value = Float.NaN</li></b></code></ul>{:/} | variable
`geophysical_variable:precision` | IOOS | The sensor precision is the closeness of the measurements to each other. It should be given in the same units as the measured variable. If the instrument has been calibrated multiple times with different results, the most recent precision should be provided here (see **`instrument_variable:calibration_date`**). | variable 
`geophysical_variable:resolution` | IOOS | The sensor resolution is the smallest change it can represent in the quantity that it is measuring. It should be given in the same units as the measured variable. | variable 
`geophysical_variable:standard_name` | CF | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | variable
`geophysical_variable:standard_name_url` | IOOS | The URL of a **`standard_name`** in the online vocabulary listed in the global **`standard_name_vocabulary`** attribute.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:standard_name_url = "https://vocab.nerc.ac.uk/collection/P07/current/CFSN0335/"</code></b> </li>  <li> <b><code>sea_water_temperature:standard_name = "sea_water_temperature"</code></b> </li> </ul>{:/} | variable
`geophysical_variable:units`  | CF | Required for most all variables that represent dimensional quantities. The value for a geophysical variable's **`units`** attribute should match or be derived from the canonical units specified for the variable's **`standard_name`** in the CF Standard Name table. <br><br>CF units are specified by the  [**`udunits`**](https://www.unidata.ucar.edu/software/udunits/) package, which includes a file `udunits.dat` listing the valid individual unit names (e.g., "g" and "m") from which which composite **`units`** strings can be formed (e.g., "kg m-3"). <br><br>For example, all temperature standard names have canonical units of "K", but often geophysical variables that measure temperature are specified with **`units`** of `degree_Celsius` or some variant thereof. | variable

#### Example

Taken from the [ATN Satellite Trajecotry Example dataset]().

```
add example ncml (json) here
```


### Platform

The method for specifying platform metadata for in situ measurements has historically been a source of confusion. CF Discrete Sampling Geometries (DSG) guidelines represent observing platforms as 'featureTypes' (e.g. 'timeSeries', 'profile', 'trajectory'), and allow multiple platforms to be included in a single file by way of a coordinate variable that uniquely identifies each feature by ID.  For example, each buoy in a timeSeries feature dataset with multiple buoys can be differentiated by storing its identifier in this coordinate variable, which varies by the instance (or 'station' dimension in the case of timeSeries) according to the number of timeSeries features in the dataset.  This feature ID coordinate variable is specified by the **`cf_role`** attribute - more info available in the table below.

For animals tracked via satellite telemetry methods, we recommend the CF DSG FeatureType [`trajectory`](https://cfconventions.org/cf-conventions/cf-conventions.html#trajectory-data).

More information about CF DSG and associated requirements is available in [CF Documentation - Chapter 9](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries).
<br><br>

**Guidelines for the treatment of Platforms in animal telemetry Datasets**:   

For animal satellite telemetry datasets, the `platform` variable is intended to be a container variable which documents specific information about the animal that was tagged. This variable is then referenced in the `platform` attribute of the appropriate observational variables. To reduce confusion, we have elected to name this variable `animal` in the provided examples and template.

<br><br>

**Platform Attribution:**

Name | Convention | Description | Type 
:--------- | :-------: | :------------------- | :--------: 
`cf_role` | CF | Indicates the values of this variable contain identifiers for the CF DSG [featureType](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#_features_and_feature_types) features in the dataset (the 'instance' variable). Allowed values are defined in [Chapter 9.5](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#coordinates-metadata) CF guidelines and consist of: `timeseries_id`, `profile_id`, and `trajectory_id`, depending on the featureType represented in the dataset, as specified by the **`featureType`** global attribute.  The dimension of this coordinate variable is referred to as the 'instance' dimension of a CF DSG file, or alternatively as the 'station', 'profile', or 'trajectory' dimension, respectively. <br> <br> **`cf_role`** may be applied to the 'Platform Variable', as indicated by **`geophysical_variable:platform`**, but it may also be an independent variable.  To comply with the **single platform per dataset** rule of the IOOS Metadata Profile, the **`cf_role`** variable will typically have a dimension of 1, unless it is a TimeSeries dataset following the 'TimeSeries - multiple-station' format.<br><br>Example: {::nomarkdown}<ul><li><b><code>cf_role = "timeseries_id"</code></b></li></ul>{:/}| variable
`geophysical_variable:platform` | NCEI | **Variable** level attribute to be specified on each **`geophysical_variable`** (i.e. data variable) with the value indicating the name of a container variable containing platform metadata (i.e. the 'Platform Variable').<br><br>Because the IOOS Metadata Profile restricts datasets to a **single platform per dataset**, each dataset must only contain one platform container variable (usually named `station` or `platform`), and each data variable in the dataset must include a **`platform`** attribute with the name of this variable.  The **`cf_role`** attribute may optionally be applied to this variable to assign it as the CF DSG 'instance' variable.<br><br> Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:platform = "station"</code></b></li><li><b><code>station:cf_role = "profile_id"</code></b></li><li><b><code>station:ncei_code = "3164"</code></b></li></ul>{:/} | variable
`platform` | ACDD |  **Global** attribute specifying the name of the *type* of platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or other. The controlled vocabulary must be indicated in the **`platform_vocabulary`** field.<br><br>**`platform`** should be a single string with no blank spaces.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>platform = "buoy";</code></b> <li><b><code>platform_vocabulary = "https://mmisw.org/ont/ioos/platform";</code></b> </ul>{:/}<br>The value of the **`platform`** global attribute is used in generating the [IOOS Asset Identifier]([https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html]) for the dataset.  Consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below this table for details on how this formula works. | global
`platform_id` | IOOS | An optional, short identifier for the platform, if the data provider prefers to define an id that differs from the dataset identifier, as specified by the  **`id`** attribute.<br><br>**`platform_id`** should be a single alphanumeric string with no blank spaces.<br><br>  When **`platform_id`** is defined for a dataset, it is used in place of the **`id`** field in generating the IOOS Asset Identifier (consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below).<br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_id = "carquinez"</code></b> <li><b><code>platform_id = "cb0102"</code></b> </ul>{:/} | global
`platform_name` | IOOS | A descriptive, long name for the platform used in collecting the data.  <br><br>The value of **`platform_name`** will be used to label the platform in downstream applications, such as IOOS' National Products (Environmental Sensor Map, EDS, etc) <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_name = "Morro Bay - BS1 MET"</code></b> <li><b><code>platform_name = "Chesapeake Bay Buoy 102"</code></b> </ul>{:/} | global
`platform_vocabulary` | ACDD | Controlled vocabulary for the names used in the **`platform`** attribute.<br><br> The recommended value for the **`platform_vocabulary`** attribute is a URL to either the [IOOS Platform Category vocabulary](https://mmisw.org/ont/ioos/platform), or [NERC SeaVoX Platform Categories vocabulary](https://vocab.nerc.ac.uk/collection/L06/current/). <br><br>Example:{::nomarkdown}<ul> <li> <b><code> platform_vocabulary = "https://mmisw.org/ont/ioos/platform"</code></b> </ul>{:/}<br>The IOOS Metadata Profile diverges from the NCEI Templates 2.0 in that the use of the "NASA GCMD Platform Keywords 8.1" as a **`platform_vocabulary`** is not allowed.  The reason for this is that the **`platform`** global attribute is used in generating the [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) for the dataset, and thus requires a single string platform name with no blank characters.  GCMD Platform Keywords do not follow this pattern and therefore are disallowed.  See the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more info. | global
`wmo_platform_code` | IOOS | The WMO identifier for the platform used to measure the data.  This identifier can be any of the following types:<br>{::nomarkdown}<ul> <li>WMO ID for buoys (numeric, 5 digits)</li><li>WMO ID for gliders (numeric, 7 digits)</li><li>NWS ID (alphanumeric, 5 digits)</ul>{:/} When a dataset is assigned a **`wmo_platform_code`** it is thereby assigned a secondary Asset Identifier for the **'wmo' `naming_authority`**.  See the  [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more information.  <br><br>Example: {::nomarkdown}<ul> <li> <b><code>wmo_platform_code = "44011"</code></b> </ul>{:/} | global



### Quality Control/QARTOD

Guidance for implementing [QARTOD](https://ioos.noaa.gov/project/qartod/) quality control flag variables in a standardized fashion.  QARTOD flag variables are associated with data variables using the CF "Ancillary Variables" approach.  More information on this is available in [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data).  

This profile requires that all variables containing results from QARTOD tests be referenced by ancillary variables, and those variables use a valid CF Standard Name to reflect the test performed (see **`qartod_variable:standard_name`** in the table below for a list of suitable standard names).

**Notes:**
*  The table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data, and **`qartod_variable`** as an alias for an ancillary QC flag variable.

Name | Convention | Description | Type
:--------- | :-------: | :------------------- | :--------: 
`geophysical_variable:ancillary_variables` | CF | From [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data):{::nomarkdown}<ul> <li>"When one data variable provides metadata about the individual values of another data variable it may be desirable to express this association by providing a link between the variables. For example, instrument data may have associated measures of uncertainty. The attribute <code><b>ancillary_variables</b></code> is used to express these types of relationships. It is a string attribute whose value is a blank separated list of variable names. The nature of the relationship between variables associated via ancillary_variables must be determined by other attributes." </li></ul>{:/}For purposes of the IOOS Metadata Profile, the **`ancillary_variables`** attribute associates the data variable with one or many QARTOD flag variables containing test results. Multiple QARTOD ancillary variables should be represented as a space-separated list of individual test variable names (for cases where data provider includes multiple test results, or includes the QARTOD "Aggregate/Rollup" flag in addition to individual flags, as required by this profile). | variable
`qartod_variable:standard_name` | CF | The full set of CF Standard Names available to identify QARTOD flag ancillary variables can be found in [Standard Name Table v72](http://cfconventions.org/Data/cf-standard-names/72/build/cf-standard-name-table.html) (March 2020) and includes: {::nomarkdown}<ul><li><code><b>aggregate_quality_flag</b></code>: an Aggregate/Rollup flag combining multiple individual flags</li><li><code><b>attenuated_signal_test_quality_flag</b></code>: Attenuated Signal Test flag</li><li><code><b>climatology_test_quality_flag</b></code>: Climatology Test flag</li><li><code><b>flat_line_test_quality_flag</b></code>: Flat Line Test flag</li><li><code><b>gap_test_quality_flag</b></code>: Timing/Gap Test flag</li><li><code><b>gross_range_test_quality_flag</b></code>: Gross Range Test flag</li><li><code><b>location_test_quality_flag</b></code>: Location Test flag</li><li><code><b>multi_variate_test_quality_flag</b></code>: Multi-variate Test flag</li><li><code><b>neighbor_test_quality_flag</b></code>: Neighbor Test flag </li><li><code><b>rate_of_change_test_quality_flag</b></code>: Rate of Change Test flag</li><li><code><b>spike_test_quality_flag</b></code>: Spike Test flag</li><li><code><b>syntax_test_quality_flag</b></code>:  Syntax Test flag</li></ul>{:/} | variable
`qartod_variable:flag_values` | CF | The **`flag_values`** and **`flag_meanings`** attributes describe a status flag consisting of mutually exclusive coded values. The **`flag_values`** attribute is the same type as the variable to which it is attached, and contains a list of the possible flag values.  See the below example for recommended usage of **`flag_values`** for QARTOD flagging.  | variable
`qartod_variable:flag_meanings` | CF | The **`flag_meanings`** attribute is a string whose value is a blank separated list of descriptive words or phrases, one for each flag value.  If multi-word phrases are used to describe the flag values, then the words within a phrase should be connected with underscores. See the below example for recommended usage of **`flag_meanings`** for QARTOD flagging. | variable
`qartod_variable:references` | CF | This should be a URL to a resource that describes the test configuration, parameters used, etc, if such a resource is available. The global `references` attribute can also be used to describe QC methods in general. | variable

#### Example

Adapted from: [ATN Satellite Trajectory Dataset Example]().

```
Add ncml (json) example here
```

### Instrument

The IOOS Metadata Profile generally follows the [NCEI Templates](https://www.ncei.noaa.gov/netcdf-templates) guidance on usage of the **`instrument`** attribute and associated **`instrument_variable`**s.  The NCEI Templates define two different usages of the **`instrument`** attribute in a dataset:

1) as a variable attribute **`instrument`** that references an **`'instrument_variable'`** by name that contains additional metadata, if needed. <br /> <br />

The IOOS Metadata Profile defines specific attributes that can be attached to a dataset's **`instrument_variable`**s:

* attributes that describe the instrument details (e.g. **`calibration_date`**, **`make_model`**)

* attributes that allow compliance with the [IOOS Convention for Asset Identification](https://ioos.github.io/conventions-for-observing-asset-identifiers/) by further qualifying the resulting Asset Identifier for measured variables (e.g. **`component`**, **`discriminant`**) <br><br>

Name | Convention | Description | Type
:--------- | :-------: | :------------------- | :--------:
`geophysical_variable:instrument` | NCEI | **Variable** attribute to be specified on each **`geophysical variable`** to identify the instrument that collected the data.  The value of the attribute should be set to another variable which contains the details of the instrument. There can be multiple instruments involved depending on if all the instances of the featureType in the collection come from the same instrument or not. If multiple instruments are involved, a variable should be defined for each instrument and referenced from the **`geophysical variable`** in a comma separated string. | variable
`instrument` | ACDD | **Global**, vocabulary-constrained attribute indicating the name of the contributing instrument(s) or sensor(s) used to create this dataset. Indicate controlled vocabulary used in the **`instrument_vocabulary`** attribute.  Separate multiple instruments using commas. | global
`instrument_variable:calibration_date` | IOOS | The date the instrument was last calibrated. Value should be specified using ISO\-8601 compatible strings. | variable
`instrument_variable:component` | IOOS | The value of a **`component`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it is used to identify individual, distinct components, or sub-assets (for example, two different sensor types), on a single platform. The **`:component`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label<b>[:component]</b>[:discriminant][#functional_parameters]</code><br><br>See examples below.| variable
`instrument_variable:discriminant` | IOOS | The value of a **`discriminant`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it ensures that in case of multiple deployments of identical sensors on the same platform (for example, measuring the same **`observedProperty`**), each sensor has a unique ID in the Identifier.  The **`:discriminant`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label[:component]<b>[:discriminant]</b>[#functional_parameters]</code> <br><br>See examples below. | variable
`instrument_variable:make_model` | IOOS | The make and model of the instrument. | variable
`instrument_vocabulary` | ACDD | Controlled vocabulary for the names used in the **`instrument`** attribute. <br><br>The recommended value for the **`instrument_vocabulary`** attribute is a URL to a controlled vocabulary of instrument terms, similar to guidance for **`platform_vocabulary`**. | global

#### Example

```
add example ncml (json) here
```

```
add ncml (json) here
```
<br><br>

#### Examples
