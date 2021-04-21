# Archive SOP
This page documents the Standard Operating Procedures for archiving the ATN observations.
The observations have been split into [trajectory](#trajectory) and [profile](#profile) observation types.
Each section below documents the decisions made for the archival of the data at NCEI.

## Data flow
![ATN Data Flow](https://user-images.githubusercontent.com/8480023/115601167-74588e00-a2ab-11eb-9d8b-c8045d66a2ee.png) From https://docs.google.com/presentation/d/1yb0E9k4n2jMHjyNrjCAo6bSiEbDUaorsgoBN_gfW_6A/edit#slide=id.gd2fc8c240e_0_0

## Trajectory
* Example files can be found at this url: 
* The netCDF file template can be found at https://github.com/MathewBiddle/ATN-archive/blob/master/templates/atn_trajectory_template.cdl

### Archival procedure
* Each Archival Information Package (AIP) will consist of a single tag deployment?
* Describe how the packages will be organized on ATNs server for pickup from NCEI. 
* The packages will be updated at a frequency of **weekly?monthly?yearly?**.
* NCEI will check for new packages every **month?year?**
* _What is the process that will be used to validate the transfer to NCEI? BagIt? Manifest files?_
* For new submissions (ones that NCEI hasn't made an AIP for yet)
  * The package will be tranferred to NCEI.
  * Once the package has been verified, the manifest files will be discarded as they are artifacts from the transfer.
  * Extract the metadata from the data and metadata files to populate the AIP metadata record. 
  * **What else will NCEI do?**
* Updates to already archived packages:
  * Update the *entire* package?
  * How will NCEI know there is a new version? 
    * File checksums don't match? 
    * File names don't match?
  * Should NCEI replace all of the files with new files? A *major revision* replacing the existing AIP with the new data.
  * Should NCEI only update the changed files?
  * The AIP metadata record will be updated to reflect the change in the AIP contents.
* The data will be served according to Tier 1 stewardship (basic access), and Tier 2 (enhanced access) by providing access to the netCDF files via [THREDDS](https://www.ncei.noaa.gov/thredds-ocean/catalog/catalog.html). 

### NCEI checks on the package
1. Package structure follows the identified [structure below](#submission-information-package-structure).
1. Checksums match.
1. File names match the identified convention described in [File naming convention](#file-naming-convention).
1. **Other checks?**

### File naming convention
Describe the template for the file names and provide a few examples.

### Submission Information Package structure
This sections contains an example of what the intended submission package will look like on the ATN Web Accessible Folder (WAF).
```
```

### Package sizes
These are approximate sizes of an entire SIP.
Package | SIP Size
--------|---------


## Profile

### Archival procedure

### NCEI checks on the package

### File naming convention

### Submission Information Package structure

### Package sizes
