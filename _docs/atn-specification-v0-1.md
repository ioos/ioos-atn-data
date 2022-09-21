---
title: "ATN Specification Version 0.1"
keywords: [ioos, metadata, netCDF, 0.1]
tags: [ioos, metadata, netCDF, 0.1]
toc: false
#permalink: index.html
summary: This is the currently active ATN specification version. 
---

## Revision History


| Version | Description                                                                       | Date       |
|:--------|:----------------------------------------------------------------------------------|:-----------|
| **0.1** | **Currently Active Version** <br>[Initial version](./atn-specification-v0-1.html) | 2022-09-21 |

## Notes/Caveats

1. The ATN specification is a compound profile that builds off of the [**IOOS Metadata Profile**](https://ioos.github.io/ioos-metadata/index.html) meaning the ATN specification is a combination of the full IOOS Metadata Profile, NCEI Templates plus IOOS-specific guidance included in this document, such as:
   *  

1. The IOOS Metadata Profile is a compound profile that builds off of the [**NOAA NCEI NetCDF Templates v2.0**](https://www.ncei.noaa.gov/data/oceans/ncei/formats/netcdf/v2.0/index.html), meaning the full IOOS Metadata Profile is a combination of the NCEI Templates plus IOOS-specific guidance included in this document, such as:
* attributes that are IOOS-specific (i.e. additions to the NCEI Templates)
* attributes where variations exist between the IOOS guidance and the NCEI Templates (e.g. **`platform_vocabulary`**, where NCEI recommendations are specifically disallowed)
* attributes with a different role in the NCEI Templates; for example, the attribute **`_FillValue`** is **required** by the NCEI Template; however, in the IOOS Profile it is listed as **recommended** only;  conversely the opposite is possible as well
* attributes with otherwise modified or further qualified meanings/definitions

1. The NCEI Templates in turn build off of the ACDD and CF conventions.  Some attributes in the IOOS Profile originate from ACDD and CF (consult the `Convention` field in the table to determine the origin of each attribute).  Links to each are below:
* [NOAA NCEI NetCDF Templates 2.0](https://www.ncei.noaa.gov/data/oceans/ncei/formats/netcdf/v2.0/index.html)
* [Attribute Convention for Data Discovery 1.3](http://wiki.esipfed.org/index.php/Attribute_Convention_for_Data_Discovery_1-3)
* [Climate and Forecast Conventions (CF) 1.7](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html)

1. In the IOOS Profile, attributes can be either **required** or **recommended**:
* all **required** attributes must have meaningful values assigned to them in accordance with the rules prescribed by the corresponding Convention or Template.
* each and all of the **recommended** attributes may be omitted; however, it is highly desirable that these attributes are included into the netCDF metadata ***AND*** have meaningful values assigned to them.
* consult the `Role` field value in the table to determine whether each attribute is required or recommended

1. The IOOS Profile is geared towards datasets containing in situ observations encoded in multidimensional, self-describing formats such as netCDF.  Some aspects of the profile are specific to the [CF Discrete Sampling Geometries](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries) guidance for these types of data, in particular the [Platform](#platform) section.  For datasets for which the DSG do not pertain (e.g. gridded model outputs or other gridded products), attributes in these sections can be omitted and still be compliant with the profile.  To avoid over-complicating the documentation, these Platform-related attributes are listed as '**required**' rather than '**required**, if applicable' because they are required for DSG-compliant datasets that must include a sampling platform.  

1. For in situ observation datasets, the IOOS Profile allows only one **'platform'** per dataset.  Please see the corresponding [Platform](#platform) section of the profile below for more information.

1. The [**U.S. IOOS National Glider Data Assembly Center**](https://gliders.ioos.us/index.html) currently uses a slightly different [netCDF File Format (V2)](https://ioos.github.io/ioosngdac/ngdac-netcdf-file-format-version-2); work is in progress to harmonize the NGDAC File Format and IOOS Metadata Profile.


## Gold Standard Example Datasets

IOOS provides a collection of "Gold Standard" example datasets in ERDDAP to demonstrate implementation of this Metadata Profile.  The Gold Standard datasets can be used as templates for data providers to generate their own compliant datasets in ERDDAP, and include a fully-deployable ERDDAP instance that includes both the example data and configuration files.  Consult the links below for more information:

* [IOOS Metadata Profile "Gold Standard" Example Datasets](gold-standard-examples.html)
* [IOOS "ERDDAP Gold Standard" GitHub Repository](https://github.com/ioos/erddap-gold-standard)

In addition to the Gold Standard datasets, there are some in-line examples included below that highlight specific attribute use cases that comply with the profile.



## IOOS Metadata Profile Attributes

### Dataset Description

The attributes listed below are a collection of high-level attributes recommended largely by the parent conventions of the IOOS Metadata Profile (CF, ACDD).  Their purpose is to describe the dataset in human-readable terms, define specific conventions used by other attributes (**`standard_name_vocabulary`**), or qualify other attributes (**`naming_authority`**).  A high-quality dataset will generally include meaningful values for all of these attributes, even though they are not all required according to the profile.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
`Conventions` | CF | A comma-separated list of the conventions that are followed by the dataset. For files that follow this version of the IOOS Metadata Profile, include the string "IOOS-1.2".<br><br>Example: {::nomarkdown}<ul><li><b><code>Conventions = "CF-1.6, ACDD-1.3, IOOS-1.2"</b></code></li></ul>{:/} | global | **required** |
`featureType` | CF | CF attribute for identifying the featureType.   <br><br>Example:{::nomarkdown}<ul><li><b><code>featureType = "timeSeries"</b></code></li></ul>{:/} | global | **required**
`id` | ACDD | An identifier for the data set, provided by and unique within its naming authority. The combination of the **`naming authority`** and the **`id`** should be globally unique, but the **`id`** can be globally unique by itself also. IDs can be URLs, URNs, DOIs, meaningful text strings, a local key, or any other unique string of characters. The **`id`** should not include blanks. | global | **required**
`infoUrl`  | IOOS | URL for background information about this dataset. This attributed is also required by ERDDAP. | global | **required**
`keywords` | ACDD | A comma separated list of key words and phrases. | global | recommended
`license`  | ACDD | Describe the restrictions to data access and distribution. | global | **required**
`naming_authority`  | ACDD | The organization that provides the **`id`** for the dataset. <br>The naming authority should be uniquely specified by this attribute; the combination of the **`naming_authority`** and the **`id`** should be a globally unique identifier for the dataset. A reverse-DNS naming is recommended; URIs are also acceptable. <br><br>Example:{::nomarkdown}<ul><li><b><code>naming_authority = "edu.ucar.unidata"</b></code></li></ul>{:/} | global | **required**
`references`  | ACDD/CF | Published or web-based references that describe the data or methods used to produce it. Recommend URIs (such as a URL or DOI) for papers or other references. Multiple references should be separated by commas. | global | recommended
`standard_name_vocabulary`  | ACDD | The name and version of the controlled vocabulary from which variable standard names are taken. Values for any variable's **`standard_name`** attribute must come from the CF Standard Names vocabulary for the dataset to comply with CF. <br><br>The format for the **`standard_name`** attribute must follow the ACDD recommendation ('CF Standard Name Table vXX', where 'XX' is a version of the standard name table), in order to be valid and meet the ACDD conventions.<br><br>If a variables does not have an existing standard name in the CF-managed list, the variable should not include a **`standard_name`** attribute. In these cases, a standard name can be proposed to the CF community for consideration.<br><br>  Example:<br>{::nomarkdown}<ul><li><b><code>standard_name_vocabulary = "CF Standard Name Table v72"</b></code></li></ul>{:/} | global | **required**
`summary`  | ACDD | One paragraph describing the data set. |  global | **required**
`title`  | ACDD | One sentence about the data contained within the file. | global | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
NC_GLOBAL {
    Conventions               CF-1.6, ACDD-1.3, IOOS-1.2
    featureType               TimeSeries
    id                        morro-bay-bs1-met
    infoUrl                   https://data.cencoos.org/#metadata/57163/station
    license                   The data may be used and redistributed for free but is not intended for legal use, since it may contain inaccuracies.  Neither the data Contributor, ERD, NOAA, nor the United States Government, nor any of their employees or contractors, makes any warranty, express or implied, including warranties of merchantability and fitness for a particular purpose, or assumes any legal liability for the accuracy, completeness, or usefulness, of this information.
    naming_authority          edu.calpoly.marine
    standard_name_vocabulary  CF Standard Name Table v72
    summary                   Timeseries data from 'Morro Bay - BS1 MET' (morro-bay-bs1-met)
    title                     Morro Bay - BS1 MET
}
```

### Attribution

The attributes listed in the table below allow for consistent attribution of datasets within IOOS' national products.  Data providers are encouraged to follow these attribute guidelines exactly to ensure datasets appear with proper attribution.  

Consult the [Gold Standard Example Datasets](gold-standard-examples.html) for good examples to start from.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
contributor_email | IOOS | Email addresses of the individuals or institutions that contributed to the creation of this data. Multiple emails should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
contributor_name | ACDD | The name of any individuals or institutions that contributed to the creation of this data. Combined with the **`contributor_role`**, it provides the full description of the contributor. Multiple names should be given in CSV format. <br><br>Examples: {::nomarkdown}<ul><li><b><code>contributor_name = "Pacific Islands Ocean Observing System (PacIOOS)"</b></code></li> <li><b><code>contributor_name = "Great Lakes Observing System (GLOS),LimnoTech"</b></code></li></ul>{:/} | global | recommended
contributor_role | ACDD | The role of any individuals or institutions that contributed to the creation of this data. The CI_RoleCode vocabulary ([NERC](https://vocab.nerc.ac.uk/collection/G04/current/), [NOAA-NCEI](https://www.ngdc.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#CI_RoleCode)) should be used. Multiple roles should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**.<br>For the IOOS ncSOS, **`contributor_role = "sponsor"`** defines a person, group, or organization’s full or partial support of an IOOS activity, asset, model, or product. <br><br>Examples:  {::nomarkdown}<ul><li><b><code>contributor_role = "sponsor"</b></code></li> <li><b><code>contributor_role = "sponsor, collaborator"</b></code></li></ul>{:/} | global | recommended
contributor_role_vocabulary | IOOS | The URL of the controlled vocabulary used for the **`contributor_role`** attribute. <br><br>The default is ["https://vocab.nerc.ac.uk/collection/G04/current/"](https://vocab.nerc.ac.uk/collection/G04/current/). | global | recommended
contributor_url | IOOS | The URL of the individuals or institutions that contributed to the creation of this data. Multiple URLs should be given in CSV format, and presented in the same order and number as the names in **`contributor_names`**. | global | recommended
creator_address | IOOS | Street address of the person or organization that collected the data.  | global | recommended
creator_city | IOOS | City of the person or organization that collected the data.  | global | recommended
creator_country | IOOS | Country of the person or organization that operates a platform or network, which collected the observation data. | global | **required**
creator_email  | ACDD | Email address of the person or institution that collected the data. | global | **required**
creator_institution  | ACDD | Institution that collected the data. This should be specified even if it matches the value of **`publisher_institution`**, **`institution`** or if **`creator_type`** is institution. | global | **required**
creator_institution_url  | IOOS | URL for the institution that collected the data. For clarity, it is recommended that this field is specified even if the creator_type is institution and a creator_url is provided. | global | recommended
creator_name  | ACDD | Name of the person or organization that collected the data. <br><br>Follow the guidance described in the **`creator_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | recommended
creator_phone | IOOS | The phone number of the person or group that collected the data. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global | recommended
creator_sector | IOOS | [IOOS classifier](https://mmisw.org/ont/ioos/sector) that best describes the platform (network) operator's societal sector. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_sector = "academic"</b></code></li></ul>{:/} | global |**required**
creator_state | IOOS | State of the person or organization that collected the data.  | global | recommended
creator_type | ACDD | Specifies type of creator with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the creator is assumed to be a person.  | global | recommended
creator_url  | ACDD | URL of the person or organization that collected the data.  | global | **required**
creator_postalcode | IOOS | The postal code of the person or organization that collected the data.  | global | recommended
institution  | ACDD | The institution of the person or group that collected the data. | global | recommended
publisher_address | IOOS | Street address of the person or organization that distributes the data.   | global | recommended
publisher_city | IOOS | City of the person or organization that distributes the data.   | global | recommended
publisher_country | IOOS | Country of the person or organization that distributes the data.   | global | **required**
publisher_email  | ACDD | The email address of the person or group that distributes the data files. | global | **required**
publisher_institution  | ACDD | Institution that distributes the data. This should be specified even if **`publisher_type`** is institution (in which case **`publisher_name`** would have an identical value). | global | **required**
publisher_name  | ACDD | Name of the person or group that distributes the data files. <br><br>Follow the guidance described in the **`publisher_type`** attribute for how to populate this field depending on whether a person, institution, group, or position. | global | recommended
publisher_phone | IOOS | The phone number of the person or group that distributes the data files. <br><br>Example:{::nomarkdown}<ul><li><b><code>creator_phone = "(240) 533-9444"</b></code></li><li><b><code>creator_phone = "+1-240-533-9444"</b></code></li></ul>{:/} | global | recommended
publisher_state | IOOS | State of the person or organization that distributes the data.   | global | recommended
publisher_type | ACDD | Specifies type of publisher with one of the following: 'person', 'group', 'institution', or 'position'. If this attribute is not specified, the publisher is assumed to be a person. | global | recommended
publisher_url  | ACDD/IOOS | URL of the person or group that distributes the data files. Note that this should always reference an institution URL, and not a personal URL, even if **`publisher_type=person`**.   | global | **required**
publisher_postalcode | IOOS | The postal code of the person or organization that distributes the data.   | global | recommended

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
NC_GLOBAL {
    creator_country          USA
    creator_email            marineops at calpoly.edu
    creator_institution      California Polytechnic State University, Center for Coastal Marine Sciences
    creator_institution_url  http://www.marine.calpoly.edu/
    creator_name             California Polytechnic State University, Center for Coastal Marine Sciences
    creator_sector           academic
    creator_type             institution
    creator_url              http://www.marine.calpoly.edu/
    institution              California Polytechnic State University, Center for Coastal Marine Sciences
}
```

```
NC_GLOBAL {
    contributor_email            cencoos_communications@mbari.org,feedback@axiomdatascience.com
    contributor_name             Central & Northern California Ocean Observing System (CeNCOOS),Axiom Data Science
    contributor_role             contributor,processor
    contributor_url              http://cencoos.org/,https://www.axiomdatascience.com
    contributor_role_vocabulary  https://vocab.nerc.ac.uk/collection/G04/current/
}
```

```
NC_GLOBAL {
    publisher_country      USA
    publisher_email        marineops at calpoly.edu
    publisher_institution  California Polytechnic State University, Center for Coastal Marine Sciences
    publisher_name         California Polytechnic State University, Center for Coastal Marine Sciences
    publisher_type         institution
    publisher_url          http://www.marine.calpoly.edu/
}
```

### Variables

A collection of variable attributes that should be applied to all geophysical or other measured parameter variable contained in the dataset.  This is mostly a re-listing and description of how to use CF convention attributes, with the addition of a few IOOS-specific attributes for variable precision/accuracy and standard name identification.  

**Note:** the table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:_FillValue | CF | This value is considered to be a special value that indicates undefined or missing data, and is returned when reading values that were not written. The type of this variable should match the type of the unpacked variable data. {::nomarkdown}<ul><b><code>  <li>time:_FillValue = -999999.0f    <li>lat:_FillValue = -999999.0f    <li>lon:_FillValue = -999999.0f    <li>z:_FillValue = -999999.0f    <li>sea_water_temperature:_FillValue = Float.NaN</li></b></code></ul>{:/} | variable | recommended
geophysical_variable:accuracy | IOOS | The sensor accuracy is the closeness of the measurements to the variable's true value. It should be given in the same units as the measured variable. If the instrument has been calibrated multiple times with different results, the most recent accuracy should be provided here (see **`instrument_variable:calibration_date`**). | variable |  recommended
geophysical_variable:missing_value | CF | This should always be equal to the `_FillValue` attribute and both are used for legacy library support. {::nomarkdown}<ul><b><code> <li>time:missing_value = -999999.0f    <li>lat:missing_value = -999999.0f    <li>lon:missing_value =-999999.0f    <li>z:missing_value = -999999.0f <li>sea_water_temperature:missing_value = Float.NaN</li></b></code></ul>{:/} | variable | recommended
geophysical_variable:precision | IOOS | The sensor precision is the closeness of the measurements to each other. It should be given in the same units as the measured variable. If the instrument has been calibrated multiple times with different results, the most recent precision should be provided here (see **`instrument_variable:calibration_date`**). | variable |  recommended
geophysical_variable:resolution | IOOS | The sensor resolution is the smallest change it can represent in the quantity that it is measuring. It should be given in the same units as the measured variable. | variable |  recommended
geophysical_variable:standard_name | CF | Standardized field which uses the [CF Standard Names](http://www.cfconventions.org/documents.html). If a variables does not have an existing standard_name in the CF-managed list, this attribute should not be used. In these cases, a standard name can be proposed to the CF community for consideration and acceptance. | variable | **required**
geophysical_variable:standard_name_url | IOOS | The URL of a **`standard_name`** in the online vocabulary listed in the global **`standard_name_vocabulary`** attribute.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:standard_name_url = "https://vocab.nerc.ac.uk/collection/P07/current/CFSN0335/"</code></b> </li>  <li> <b><code>sea_water_temperature:standard_name = "sea_water_temperature"</code></b> </li> </ul>{:/} | variable | recommended
geophysical_variable:units  | CF | Required for most all variables that represent dimensional quantities. The value for a geophysical variable's **`units`** attribute should match or be derived from the canonical units specified for the variable's **`standard_name`** in the CF Standard Name table. <br><br>CF units are specified by the  [**`udunits`**](https://www.unidata.ucar.edu/software/udunits/) package, which includes a file `udunits.dat` listing the valid individual unit names (e.g., "g" and "m") from which which composite **`units`** strings can be formed (e.g., "kg m-3"). <br><br>For example, all temperature standard names have canonical units of "K", but often geophysical variables that measure temperature are specified with **`units`** of `degree_Celsius` or some variant thereof. | variable | **required**

#### Example

Taken from the [Morro Bay BS1 MET Gold Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
Attributes {
    air_temperature {
        _FillValue        -9999.0
        missing_value     -9999.0
        long_name         Air Temperature
        platform          station
        standard_name     air_temperature
        units             degree_Celsius
        standard_name_url http://vocab.nerc.ac.uk/collection/P07/current/CFSN0023/
    }
}
```


### Platform

The method for specifying platform metadata for in situ measurements has historically been a source of confusion. CF Discrete Sampling Geometries (DSG) guidelines represent observing platforms as 'featureTypes' (e.g. 'timeSeries', 'profile', 'trajectory'), and allow multiple platforms to be included in a single file by way of a coordinate variable that uniquely identifies each feature by ID.  For example, each buoy in a timeSeries feature dataset with multiple buoys can be differentiated by storing its identifier in this coordinate variable, which varies by the instance (or 'station' dimension in the case of timeSeries) according to the number of timeSeries features in the dataset.  This feature ID coordinate variable is specified by the **`cf_role`** attribute - more info available in the table below.

More information about CF DSG and associated requirements is available in [CF Documentation - Chapter 9](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#discrete-sampling-geometries).
<br><br>

**Guidelines for Platforms in Datasets**:   

**One platform per dataset:** The IOOS Metadata Profile restricts datasets to contain only a **single physical observing platform per dataset** (e.g. buoy, glider, station, or anything that might be assigned a WMO ID).  This simplifies the dataset structure significantly, and it allows the use of several global attributes to specify platform metadata that might otherwise be found in platform container variable(s) (e.g. **`platform_id`** and **`platform_name`**, as well as the OceanSITES-derived **`wmo_platform_code`**).  It also simplifies the creation of aggregated datasets at the ERDDAP level to create groups of individual platform datasets.

**Notes:**

Data providers are encouraged to carefully review this section and upstream standards, and especially to review the [Gold Standard](#gold-standard-example-datasets) example datasets to ensure compliance with platform guidance in this profile.

Aggregated ERDDAP datasets: ERDDAP provides the ability to create aggregated datasets from collections of individual datasets.  While this is encouraged as a way to streamline access for end users to related datasets, IOOS will not harvest aggregated datasets into upstream national products, nor will NDBC harvest them for GTS publication.  Therefore, you should set **`gts_ingest=false`** and **`ioos_ingest=false`** flags on any ERDDAP aggregated datasets.

Gridded Datasets: As mentioned in the [Notes/Caveats section](#notescaveats), the Platform rules do not apply to datasets that do not adhere to the CF Discrete Sampling Geometries guidelines (e.g. gridded model outputs or other gridded products).  Attributes in this section can be omitted for such datasets and still be compliant with this profile.  
<br>

**DSG FeatureType Guidance:**

Recommendations on the specific CF DSG featureTypes to use for different platform instrumentation scenarios is as follows:


Platform Type | CF DSG Dataset Type
:--------- | :-------- |
Buoy/Station with:{::nomarkdown}<ul><li>single sensor package <i><b>or</b></i></li><li>multiple sensor packages with identical vertical (height/depth) position and same sampling frequency</li></ul>{:/} | TimeSeries - single station
Buoy/Station with:{::nomarkdown}<ul><li>multiple sensor packages with different vertical (height/depth) positions <i><b>or</b></i></li><li>multiple sensor packages with different sampling frequencies</li></ul>{:/} | TimeSeries - multiple station _**or**_ <br> TimeSeriesProfile - single station _**or**_ <br> ‘single-sensor-per-dataset’
Profiling Glider | TrajectoryProfile

**TimeSeries - single station:** A [DSG TimeSeries feature](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-data) represents measurements taken at a single location (lat, lon, altitude) over time.  This can be distinguished from TimeSeries - multiple station by having a 'station dimension' of only 1, indicating only a single feature, or station, per dataset.  

**TimeSeries - multiple station:** A [DSG TimeSeries featureType](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-data) dataset with a 'station dimension' of greater than 1.  TimeSeries - multiple station represents a platform with sensors at different heights as a vertical collection of features where the altitude (depth or height) of each feature reflects the vertical position of each sensor on the platform.   Latitude/Longitude positions must be the same for each feature.

**TimeSeriesProfile - single station:** A [DSG TimeSeriesProfile feature](http://cfconventions.org/cf-conventions/cf-conventions.html#time-series-profiles) represents a platform with multiple sensors as a vertical profile with a altitude (depth or height) position for each sensor.  This can also be used for profiling sensors like ADCPs.  This metadata profile restricts TimeSeriesProfile datasets to include a 'station dimension' of only 1, indicating a single timeSeries feature (or 'station') per dataset.

**single-sensor-per-dataset:** individual ERDDAP datasets of either TimeSeries or TimeSeriesProfile type that are associated via matching **`platform_id`** and **`wmo_platform_code`** global attributes, breaking a platform's data apart into individual DSG datasets.  Some IOOS RAs use this pattern already, and provide one dataset for sensor package (e.g., CTD, ADCP, met, etc).  The code used to ingest sensor datasets for GTS by NDBC or for Sensor Map by IOOS will perform this aggregation, so data providers need not create aggregations in ERDDAP.  Each individual dataset intended for the GTS must follow the [Requirements for NDBC/GTS Ingest](#requirements-for-ioos-dataset-ndbcgts-ingest) individually.

Note that because neither **`platform_id`** or **`wmo_platform_code`** attributes are required in this profile, any dataset without them will be considered to be specifying data for only one, distinct platform, and aggregation with other datasets by downstream processes at NDBC or IOOS is not guaranteed.   

**TrajectoryProfile:** [A DSG TrajectoryProfile feature](http://cfconventions.org/cf-conventions/cf-conventions.html#trajectory-profiles) represents a series of individual profiles taken along a path across the Earth's surface.  Similar to 'TimeSeriesProfile - single station' this metadata profile restricts TrajectoryProfile to include a 'trajectory dimension' of only 1, indicating a single trajectory feature (glider, ship, or other platform) per dataset.
<br><br>

**Platform Attribution:**

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
cf_role | CF | Indicates the values of this variable contain identifiers for the CF DSG [featureType](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#_features_and_feature_types) features in the dataset (the 'instance' variable). Allowed values are defined in [Chapter 9.5](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#coordinates-metadata) CF guidelines and consist of: `timeseries_id`, `profile_id`, and `trajectory_id`, depending on the featureType represented in the dataset, as specified by the **`featureType`** global attribute.  The dimension of this coordinate variable is referred to as the 'instance' dimension of a CF DSG file, or alternatively as the 'station', 'profile', or 'trajectory' dimension, respectively. <br> <br> **`cf_role`** may be applied to the 'Platform Variable', as indicated by **`geophysical_variable:platform`**, but it may also be an independent variable.  To comply with the **single platform per dataset** rule of the IOOS Metadata Profile, the **`cf_role`** variable will typically have a dimension of 1, unless it is a TimeSeries dataset following the 'TimeSeries - multiple-station' format.<br><br>Example: {::nomarkdown}<ul><li><b><code>cf_role = "timeseries_id"</code></b></li></ul>{:/}| variable | **required**
geophysical_variable:platform | NCEI | **Variable** level attribute to be specified on each **`geophysical_variable`** (i.e. data variable) with the value indicating the name of a container variable containing platform metadata (i.e. the 'Platform Variable').<br><br>Because the IOOS Metadata Profile restricts datasets to a **single platform per dataset**, each dataset must only contain one platform container variable (usually named `station` or `platform`), and each data variable in the dataset must include a **`platform`** attribute with the name of this variable.  The **`cf_role`** attribute may optionally be applied to this variable to assign it as the CF DSG 'instance' variable.<br><br> Example: {::nomarkdown}<ul> <li> <b><code>sea_water_temperature:platform = "station"</code></b></li><li><b><code>station:cf_role = "profile_id"</code></b></li><li><b><code>station:ncei_code = "3164"</code></b></li></ul>{:/} | variable | **required**
platform | ACDD |  **Global** attribute specifying the name of the *type* of platform(s) that supported the sensor data used to create this data set or product. Platforms can be of any type, including satellite, ship, station, aircraft or other. The controlled vocabulary must be indicated in the **`platform_vocabulary`** field.<br><br>**`platform`** should be a single string with no blank spaces.<br><br>Example: {::nomarkdown}<ul> <li> <b><code>platform = "buoy";</code></b> <li><b><code>platform_vocabulary = "https://mmisw.org/ont/ioos/platform";</code></b> </ul>{:/}<br>The value of the **`platform`** global attribute is used in generating the [IOOS Asset Identifier]([https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html]) for the dataset.  Consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below this table for details on how this formula works. | global | **required**
platform_id | IOOS | An optional, short identifier for the platform, if the data provider prefers to define an id that differs from the dataset identifier, as specified by the  **`id`** attribute.<br><br>**`platform_id`** should be a single alphanumeric string with no blank spaces.<br><br>  When **`platform_id`** is defined for a dataset, it is used in place of the **`id`** field in generating the IOOS Asset Identifier (consult the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) section below).<br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_id = "carquinez"</code></b> <li><b><code>platform_id = "cb0102"</code></b> </ul>{:/} | global | recommended
platform_name | IOOS | A descriptive, long name for the platform used in collecting the data.  <br><br>The value of **`platform_name`** will be used to label the platform in downstream applications, such as IOOS' National Products (Environmental Sensor Map, EDS, etc) <br><br>Examples: {::nomarkdown}<ul> <li> <b><code>platform_name = "Morro Bay - BS1 MET"</code></b> <li><b><code>platform_name = "Chesapeake Bay Buoy 102"</code></b> </ul>{:/} | global | **required**
platform_vocabulary | ACDD | Controlled vocabulary for the names used in the **`platform`** attribute.<br><br> The recommended value for the **`platform_vocabulary`** attribute is a URL to either the [IOOS Platform Category vocabulary](https://mmisw.org/ont/ioos/platform), or [NERC SeaVoX Platform Categories vocabulary](https://vocab.nerc.ac.uk/collection/L06/current/). <br><br>Example:{::nomarkdown}<ul> <li> <b><code> platform_vocabulary = "https://mmisw.org/ont/ioos/platform"</code></b> </ul>{:/}<br>The IOOS Metadata Profile diverges from the NCEI Templates 2.0 in that the use of the "NASA GCMD Platform Keywords 8.1" as a **`platform_vocabulary`** is not allowed.  The reason for this is that the **`platform`** global attribute is used in generating the [IOOS Asset Identifier 1.0](https://ioos.github.io/conventions-for-observing-asset-identifiers/ioos-assets-v1-0.html) for the dataset, and thus requires a single string platform name with no blank characters.  GCMD Platform Keywords do not follow this pattern and therefore are disallowed.  See the [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more info. | global | **required**
wmo_platform_code | IOOS | The WMO identifier for the platform used to measure the data.  This identifier can be any of the following types:<br>{::nomarkdown}<ul> <li>WMO ID for buoys (numeric, 5 digits)</li><li>WMO ID for gliders (numeric, 7 digits)</li><li>NWS ID (alphanumeric, 5 digits)</ul>{:/} When a dataset is assigned a **`wmo_platform_code`** it is thereby assigned a secondary Asset Identifier for the **'wmo' `naming_authority`**.  See the  [Rules for Asset Identifier Generation](#rules-for-ioos-asset-identifier-generation) for more information.  <br><br>Example: {::nomarkdown}<ul> <li> <b><code>wmo_platform_code = "44011"</code></b> </ul>{:/} | global | **required**, if applicable



### Quality Control/QARTOD

Guidance for implementing [QARTOD](https://ioos.noaa.gov/project/qartod/) quality control flag variables in a standardized fashion.  QARTOD flag variables are associated with data variables using the CF "Ancillary Variables" approach.  More information on this is available in [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data).  

This profile requires that all variables containing results from QARTOD tests be referenced by ancillary variables, and those variables use a valid CF Standard Name to reflect the test performed (see **`qartod_variable:standard_name`** in the table below for a list of suitable standard names).

**Notes:**
* See the [Requirements for NDBC/GTS Ingest](#requirements-for-ioos-dataset-ndbcgts-ingest) section below for important guidelines to properly specify a dataset's QARTOD "Aggregate/Rollup" flag variable for GTS ingest by NDBC.
*  The table below uses **`geophysical_variable`** as an alias intending to represent any variable containing geophysical data, and **`qartod_variable`** as an alias for an ancillary QC flag variable.

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:ancillary_variables | CF | From [CF Chapter 3.4](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data):{::nomarkdown}<ul> <li>"When one data variable provides metadata about the individual values of another data variable it may be desirable to express this association by providing a link between the variables. For example, instrument data may have associated measures of uncertainty. The attribute <code><b>ancillary_variables</b></code> is used to express these types of relationships. It is a string attribute whose value is a blank separated list of variable names. The nature of the relationship between variables associated via ancillary_variables must be determined by other attributes." </li></ul>{:/}For purposes of the IOOS Metadata Profile, the **`ancillary_variables`** attribute associates the data variable with one or many QARTOD flag variables containing test results. Multiple QARTOD ancillary variables should be represented as a space-separated list of individual test variable names (for cases where data provider includes multiple test results, or includes the QARTOD "Aggregate/Rollup" flag in addition to individual flags, as required by this profile). | variable | **required**, if applicable
qartod_variable:standard_name | CF | The full set of CF Standard Names available to identify QARTOD flag ancillary variables can be found in [Standard Name Table v72](http://cfconventions.org/Data/cf-standard-names/72/build/cf-standard-name-table.html) (March 2020) and includes: {::nomarkdown}<ul><li><code><b>aggregate_quality_flag</b></code>: an Aggregate/Rollup flag combining multiple individual flags</li><li><code><b>attenuated_signal_test_quality_flag</b></code>: Attenuated Signal Test flag</li><li><code><b>climatology_test_quality_flag</b></code>: Climatology Test flag</li><li><code><b>flat_line_test_quality_flag</b></code>: Flat Line Test flag</li><li><code><b>gap_test_quality_flag</b></code>: Timing/Gap Test flag</li><li><code><b>gross_range_test_quality_flag</b></code>: Gross Range Test flag</li><li><code><b>location_test_quality_flag</b></code>: Location Test flag</li><li><code><b>multi_variate_test_quality_flag</b></code>: Multi-variate Test flag</li><li><code><b>neighbor_test_quality_flag</b></code>: Neighbor Test flag </li><li><code><b>rate_of_change_test_quality_flag</b></code>: Rate of Change Test flag</li><li><code><b>spike_test_quality_flag</b></code>: Spike Test flag</li><li><code><b>syntax_test_quality_flag</b></code>:  Syntax Test flag</li></ul>{:/} | variable | **required**, if applicable
qartod_variable:flag_values | CF | The **`flag_values`** and **`flag_meanings`** attributes describe a status flag consisting of mutually exclusive coded values. The **`flag_values`** attribute is the same type as the variable to which it is attached, and contains a list of the possible flag values.  See the below example for recommended usage of **`flag_values`** for QARTOD flagging.  | variable | recommended
qartod_variable:flag_meanings | CF | The **`flag_meanings`** attribute is a string whose value is a blank separated list of descriptive words or phrases, one for each flag value.  If multi-word phrases are used to describe the flag values, then the words within a phrase should be connected with underscores. See the below example for recommended usage of **`flag_meanings`** for QARTOD flagging. | variable | recommended
qartod_variable:references | CF | This should be a URL to a resource that describes the test configuration, parameters used, etc, if such a resource is available. The global `references` attribute can also be used to describe QC methods in general. | variable | recommended

#### Example

Adapted from: [Morro Bay BS1 MET Gold-Standard Example dataset](https://standards.sensors.ioos.us/erddap/info/morro-bay-bs1-met/index.html).

```
  air_temperature {
    String standard_name "air_temperature";
    String long_name "Air Temperature";
    String units "degree_Celsius";
    String ancillary_variables "air_temperature_qc_agg air_temperature_gross_range air_temperature_flat_line";
  }
  air_temperature_qc_agg {
    String standard_name "aggregate_quality_flag";
    String long_name "Air Temperature QARTOD Aggregate Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
  air_temperature_gross_range {
    String standard_name "gross_range_test_quality_flag";
    String long_name "Air Temperature QARTOD Gross Range Test Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
  air_temperature_flat_line {
    String standard_name "flat_line_test_quality_flag";
    String long_name "Air Temperature QARTOD Flat Line Test Quality Flag";
    String flag_values 1, 2, 3, 4, 9;
    String flag_meanings "PASS NOT_EVALUATED SUSPECT FAIL MISSING";
    String references "http://services.cormp.org/quality.php";
    Int32 _FillValue 2;
  }
```

### Instrument

The IOOS Metadata Profile generally follows the [NCEI Templates](https://www.ncei.noaa.gov/netcdf-templates) guidance on usage of the **`instrument`** attribute and associated **`instrument_variable`**s.  The NCEI Templates define two different usages of the **`instrument`** attribute in a dataset:

1) as a global variable containing a vocabulary-constrained string describing the instrument type, or

2) as a variable attribute **`instrument`** that references an **`'instrument_variable'`** by name that contains additional metadata, if needed. <br /> <br />

The IOOS Metadata Profile defines specific attributes that can be attached to a dataset's **`instrument_variable`**s:

* attributes that describe the instrument details (e.g. **`calibration_date`**, **`make_model`**)

* attributes that allow compliance with the [IOOS Convention for Asset Identification](https://ioos.github.io/conventions-for-observing-asset-identifiers/) by further qualifying the resulting Asset Identifier for measured variables (e.g. **`component`**, **`discriminant`**) <br><br>

Name | Convention | Description | Type | Role
:--------- | :-------: | :------------------- | :--------: | :-------:
geophysical_variable:instrument | NCEI | **Variable** attribute to be specified on each **`geophysical variable`** to identify the instrument that collected the data.  The value of the attribute should be set to another variable which contains the details of the instrument. There can be multiple instruments involved depending on if all the instances of the featureType in the collection come from the same instrument or not. If multiple instruments are involved, a variable should be defined for each instrument and referenced from the **`geophysical variable`** in a comma separated string. | variable | recommended
instrument | ACDD | **Global**, vocabulary-constrained attribute indicating the name of the contributing instrument(s) or sensor(s) used to create this dataset. Indicate controlled vocabulary used in the **`instrument_vocabulary`** attribute.  Separate multiple instruments using commas. | global | recommended
instrument_variable:calibration_date | IOOS | The date the instrument was last calibrated. Value should be specified using ISO\-8601 compatible strings. | variable | recommended
instrument_variable:component | IOOS | The value of a **`component`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it is used to identify individual, distinct components, or sub-assets (for example, two different sensor types), on a single platform. The **`:component`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label<b>[:component]</b>[:discriminant][#functional_parameters]</code><br><br>See examples below.| variable | recommended, if applicable
instrument_variable:discriminant | IOOS | The value of a **`discriminant`** applies to the like-named field in the IOOS SOS Asset Identifier URN; it ensures that in case of multiple deployments of identical sensors on the same platform (for example, measuring the same **`observedProperty`**), each sensor has a unique ID in the Identifier.  The **`:discriminant`** is mapped to the Asset Identifier as follows:<br><br> Asset Identifier = <code>urn:ioos:asset_type:authority:label[:component]<b>[:discriminant]</b>[#functional_parameters]</code> <br><br>See examples below. | variable | recommended, if applicable
instrument_variable:make_model | IOOS | The make and model of the instrument. | variable | recommended
instrument_vocabulary | ACDD | Controlled vocabulary for the names used in the **`instrument`** attribute. <br><br>The recommended value for the **`instrument_vocabulary`** attribute is a URL to a controlled vocabulary of instrument terms, similar to guidance for **`platform_vocabulary`**. | global | recommended

#### Example

Usage of **`component`** with an **`instrument_variable`**:
```
Attributes {
    sea_water_temperature {
      instrument      temperature_sensor
    }
    temperature_sensor {
      component      nortek_adp_514
    }

}
```

Usage of **`discriminant`** with an **`instrument_variable`**:
```
Attributes {
    sea_water_temperature_top {
      instrument      temperature_sensor_top
    }
    sea_water_temperature_bottom {
      instrument      temperature_sensor_bottom
    }
    temperature_sensor_top {
      component      nortek_adp_514
      discriminant   top
    }
    temperature_sensor_bottom {
      component      nortek_adp_514
      discriminant   bottom
    }

}
```
<br><br>

#### Requirements for the QARTOD Aggregate/Rollup Flag:

Currently, IOOS RAs push a custom XML format to NDBC for GTS ingestion, so they can exclude "QC fail" values while generating the XML. ERDDAP datasets will have all observed data, including observations marked "QC fail", so NDBC needs a means to filter QC passing and failing data from the full timeseries.  This will be accomplished using an "ancillary variable" according to the CF [Ancillary Data](http://cfconventions.org/Data/cf-conventions/cf-conventions-1.7/cf-conventions.html#ancillary-data) guidelines that represents the QC aggregate/rollup flag for each observation variable marked for GTS ingestion, as described below.  

**Rules governing the 'Aggregate/Rollup' flag variable:**

1. The value of the variable is the UNESCO/QARTOD v2 convention:
    * 9 = Missing
    * 2 = Not Eval
    * 1 = Pass
    * 3 = Suspect
    * 4 = Fail
1. The value of the rollup flag should be the *worst* result out of all of the individual tests. It's called a "Summary Flag" in the [QARTOD Data Flags](https://github.com/ioos/ioos_qc/blob/master/ioos_qc/qartod.py#L46-L77) manual (pg 3).
    * Here's how it's done in the [ioos_qc library](https://github.com/ioos/ioos_qc/blob/3d8efba12644eb37b9ef35e6cdcf35189e789075/ioos_qc/qartod.py#L49-L80) with the [corresponding test](https://github.com/ioos/ioos_qc/blob/3d8efba12644eb37b9ef35e6cdcf35189e789075/tests/test_qartod.py#L1096-L1113).  
1. The variable should have a standard name attribute of **`aggregate_quality_flag`**. See the [QARTOD](#quality-controlqartod) section above for more information.  
1. NDBC should exclude any values that are QC fail (and missing) but include everything else (not eval, pass, suspect) <br> <br>


#### Examples

The [WQB-04](https://pae-paha.pacioos.hawaii.edu/erddap/info/WQB-04/index.html) and [WQB-05](https://pae-paha.pacioos.hawaii.edu/erddap/info/WQB-05/index.html) PacIOOS buoys are actively used by NDBC for collecting data.
