# ATN-archive
Code, documentation and issue tracking for U.S. IOOS Animal Telemetry Network's (ATN) development of data file specifications for submission to NOAA's
[National Centers for Environmental Information](https://www.ncei.noaa.gov/) and the [Ocean Biodiversity Information System (OBIS)]([obis.org](https://obis.org/)).

## Branches
This repository has two primary branches from which we work. Below are breif descriptions of the purposes of the two branches and where to go for more information. 

Each branch has a CONTRIBUTING guide to assist with contributions, if you'd like to participate.

### `main` branch
This branch! Used for developing the file templates, documenting the archival procedures with NCEI, documenting the crosswalk from the template to the Darwin Core standard, 
and providing example notebooks for working with these data.

#### Structure
* **crosswalk/** - contains spreadsheet crosswalking CF/ACDD to DarwinCore.
* **data/** - contains example data files.
* **notebooks/** - contains example Python notebooks for reading data files.
* **templates/** - contains [common data language (cdl)](https://www.unidata.ucar.edu/software/netcdf/workshops/most-recent/nc3model/Cdl.html#:~:text=CDL%20(Common%20Data%20Language)%20is,for%20netCDF%20objects%20and%20data.&text=This%20example%20specifies%20a%20netCDF,data%20values%20for%20the%20variable.) netCDF templates.
* README-ArchiveSOP.md - Documentation about the procedure for archiving at NCEI.
* README-ATN2DWC.md - Documentation about the mapping from ATN netCDF to DwC.

### `gh-pages` branch
Used for establishing the documentation website <https://ioos.github.io/ioos-atn-data/>. More details can be found in the [README](https://github.com/ioos/ioos-atn-data/blob/gh-pages/README.md) for that branch.
