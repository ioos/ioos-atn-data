---
title: "ATN DAC Data Flow Overview"
keywords: [ioos, metadata, netCDF, overview]
tags: [ioos, metadata, netCDF, overview]
toc: false
#permalink: index.html
summary: This page provides an overview of the ATN DAC data flows.
mermaid: true 
---

# Standard operating procedure for the Animal Telemetry Network 
This page documents the standard operating procedures for data flow in the U.S. Animal Telemetry Network (ATN) to various data repositories, national archive locations, servers, and the ATN data portal to increase discoverability, accessibility, and re-usability of ATN data. 

## Data Flow Summary

The diagram shows the ATN data ingestion and processing pipeline, from incoming data sources through QC, format conversion, and distribution pathways.

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

flowchart TB

  %% -----------------------
  %% Top-level data sources
  %% -----------------------
  ATNApp(ATN Data<br/>Registration App)
  Incoming["Incoming Data*"]@{ shape: bang}

  ATNApp --> Incoming


  %% -----------------------
  %% QC configuration
  %% -----------------------
  DefaultQC[Default QC config]
  CustomQC["Custom QC config<br/>(platform_service)"]
  %% ATN processing pipeline
  %% -----------------------
  subgraph PIPELINE[ATN processing pipeline]
    Processing((Processing))@{ shape: cloud }
    Manual(("Manual Data Curation"))@{ shape: cloud }
    PQ1[/parquet file/]
    IOOSQC((ioos_qc*))@{ shape: cloud }
    PQ2[/parquet file/]
    AniMotum((aniMotum))@{ shape: cloud }
    PQ3[/parquet file/]
    StdNC[/"Standardized<br/>netCDF"/]
    StdQCNC[/"Standardized<br/>QC netCDF"/]
    BUFR[/BUFR Messages/]
  end

  %% Pipeline flow
  Incoming --> |API/Server Access| Processing
  Incoming --> |Manual Data Curation| Processing
  Incoming -->|Research Workspace| DataONE
  Processing --> PQ1
  PQ1 --> IOOSQC
  DefaultQC --> IOOSQC
  CustomQC --> IOOSQC

  IOOSQC --> PQ2

  %% Profile branch
  PQ2 --> StdQCNC

  %% Non-profile branch
  PQ2 --> AniMotum
  AniMotum -->|CSV| PQ3
  PQ3 --> StdNC

  %% BUFR path
  PQ2 -->|Profile Data| BUFR

  %% -----------------------
  %% Data access & delivery
  %% -----------------------
  DAC["ATN DAC Portal<br/>/ Data Access"]@{ shape: curv-trap}
  
  PQ3 --> DAC
  StdNC --> DAC

  %% -----------------------
  %% Final repositories
  %% -----------------------
  DataONE([DataONE])
  ERDDAP([ERDDAP])
  NCEI([NCEI])
  OBIS([OBIS/GBIF])
  NDBC([NDBC])
  GTS([GTS])

  BUFR --> NDBC
  StdQCNC --> ERDDAP
  StdQCNC --> NCEI
  StdQCNC --> OBIS
  NDBC --> GTS

  %% -----------------------
  %% Styling for final repositories
  %% -----------------------
  classDef finalRepo fill:#D6EEF2,stroke:#007396,stroke-width:2px,color:#003087;

  class DataONE,ERDDAP,NCEI,OBIS,NDBC,GTS finalRepo;
```

## Incoming data sources

More details coming soon on incoming data sources, QC configuration, processing, and data distribution!