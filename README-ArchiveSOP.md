# Archive SOP
This page documents the Standard Operating Procedures for archiving the ATN observations.
The observations have been split into [trajectory](#trajectory) and [profile](#profile) observation types.
Each section below documents the decisions made for the archival of the data at NCEI.

## Data flow
![ATN Data Flow](https://user-images.githubusercontent.com/8480023/115601167-74588e00-a2ab-11eb-9d8b-c8045d66a2ee.png) From https://docs.google.com/presentation/d/1yb0E9k4n2jMHjyNrjCAo6bSiEbDUaorsgoBN_gfW_6A/edit#slide=id.gd2fc8c240e_0_0

## Trajectory
* Example files can be found at this url: 
* The file template can be found at https://github.com/MathewBiddle/ATN-archive/blob/master/templates/atn_trajectory_template.cdl

### Archival procedure
* Each Archival Information Package (AIP) will consist of _document the package structure_
* _Describe the data source structure._ Submission Information Package (SIP) and will follow the (BagIt convention?).
* The packages will be updated at a frequency **weekly?monthly?yearly?**.
* NCEI will check for new packages every **month?year?**
* _What process will be used to validate the transfer to NCEI?_
* For new submissions (ones that NCEI hasn't made an AIP for yet)
  * The package will be tranferred to NCEI.
  * Once the package has been verified, the manifest files will be discarded as they are artifacts from the transfer.
  * Extract the metadata from the data and metadata files to populate the AIP metadata record. 
  * **What else will NCEI do?**
* Updates to already archived packages:
  * Update the *entire* package?
  * How will NCEI know there is a new version?
  * NCEI will perform a *major revision* replacing the existing AIP with the new data.
  * The AIP metadata record will be updated to reflect the replacement data.
* The data will be served according to Tier 1 stewardship (basic access), with the hopes that NCEI can make the geojson inventory files accessible using advanced access services.

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
