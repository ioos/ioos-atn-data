---
title: Satellite telemetry to Darwin Core
keywords: [ioos, metadata, netCDF, Darwin Core, OBIS, GBIF]
tags: [ioos, metadata, netCDF, Darwin Core, OBIS, GBIF]
toc: false
#permalink: index.html
summary: This page documents the Standard Operating Procedures for mapping the ATN observations into Darwin Core.
mermaid: true
---

# Mapping ATN satellite telemetry template to Darwin Core
This page documents the Standard Operating Procedures for mapping the ATN observations into Darwin Core.
The observations have been split into [trajectory](#trajectory) and [profile](#profile) observation types.
Each section below documents the decisions made for the translation of the ATN netCDF data into DarwinCore.

## Trajectory
See this [Python library](https://github.com/MathewBiddle/atn2obis/tree/main) on performing the translation. A short summary and data flow diagram are below.

### Step-by-step
1. Pulls source netCDF data directly from NCEI.
2. Ingests netCDF data and translates to DarwinCore format
3. Creates applicable eml metadata.
4. Creates applicable file column mapping xml file.
5. Zips everything together into a compliant DwC Archive package.
6. Automatically publish DwC Archive package to OBIS-USA IPT.
7. Provide capability to version control updates to the datasets on the OBIS-USA IPT by: updating of eml metadata, updating of data files, and republishing.

### Data flow diagram
_rough draft on 2025-11-20_

```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#007396',
      'primaryTextColor': '#fff',
      'primaryBorderColor': '#003087',
      'lineColor': '#003087',
      'secondaryColor': '#007396',
      'tertiaryColor': '#CCD1D1'
    },
   'flowchart': { 'curve': 'basis' }
  }
}%%

flowchart TD

A[(ATN ingest)]
B[(QC/QC and Metadata development)]
C[(Publish to DataONE)]
D[(Generate NCEI netCDF)]
D1[(review)]
D2[(add to WAF)]
D3[(NCEI harvest)]
D4[(NCEI publish)]
E[(add DataONE refs to NCEI metadata)]
F[(add NCEI refs to DataOne metadata)]
F2[(NCEI update)]
G[(run atn2obis)]
H[(OBIS-USA IPT)]
I[(OBIS)]
J[(GBIF)]
K[(NCEI)]

A --> B
B --> C
C --> D
D --> D1
D1 --> D2
D2 --> D3
D3 --> D4
D4 --> E
D4 --> F
E --> F2
F --> F2
F2 --> G
G --> H
H --> I
H --> J
H --> K

```

## Profile
TBD
