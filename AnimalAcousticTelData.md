

# Improving Access to Animal Acoustic Telemetry (AAT) Observations #

[IOOS](http://www.ioos.noaa.gov) - [NANOOS](http://www.nanoos.org) - [OTN](http://oceantrackingnetwork.org/) - [POST](http://en.wikipedia.org/wiki/Pacific_Ocean_Shelf_Tracking_Project) (Pacific Ocean Shelf Tracking Project, no longer in operation)

## Introduction and Objectives ##
As part of the [IOOS Animal Telemetry Network](http://www.ioos.noaa.gov/observing/animal_telemetry/welcome.html) efforts, in 2012-2013 IOOS supported a community needs assessment and data-access standards and technology development project for animal acoustic telemetry (AAT) data. The project was co-led by IOOS, NANOOS (the IOOS Regional Association for the Pacific Northwest), the Pacific Ocean Shelf Tracking Project (POST, which is no longer in operation) and the Ocean Tracking Network (OTN). While it focused on the Pacific NW for needs assessments and data testing, it brought together not only regional partners such as the [NOAA Northwest Fisheries Center](http://www.nwfsc.noaa.gov) and the [Hydra system](http://hydra3.sound-data.com/about/), but also national, Canadian and Australian collaborators.

The **primary outcomes** were the development of data exchange standards and best-practice data delivery systems that are now being implemented at a wider scale by OTN to provide access to their [OTN Northeast Pacific data node](http://members.oceantrack.org/data/discovery/NEPACIFIC.htm), which includes POST data.
This project will build on existing [IOOS DMAC guidance and activities regarding biological and broader oceanographic data access](http://www.ioos.noaa.gov/data/welcome.html).


## Project Documents and Reports ##
  1. [Statement of Work](http://habu.apl.washington.edu/mayorga/aat/Animal%20Acoustic%20Telemetry%20Obs_SOW.pdf)
  1. [POST Data System Description](http://habu.apl.washington.edu/mayorga/aat/POST_DataSystemDescription_DRAFT1.0.pdf)
  1. Customer Requirements Assessment
    * [Survey Questionnaire](http://habu.apl.washington.edu/mayorga/aat/AAT_CustomerRequirementsQuestionnaire.pdf)
    * [Survey results and requirements synthesis](http://habu.apl.washington.edu/mayorga/aat/AAT_CustomerRequirements_2012Sep4.pdf). This document includes a brief comparison of some existing systems
  1. [Content Standard: A metadata convention for animal acoustic telemetry data (document and tables)](http://ioostech.googlecode.com/files/AAT%20Metadata%20Convention%20v1.2.pdf)
  1. [Data System Architecture Implementation Plan](http://habu.apl.washington.edu/mayorga/aat/AAT_DataSystemArchitectureImplementationPlan_FINAL.pdf)
    * [Presentation by Emilio at the Final meeting, June 2013](http://habu.apl.washington.edu/mayorga/aat/Emilio_Presentation_AATworkshop_2013Jun13.pdf)


## Project Data Services ##
Data Services being implemented by this project are based on [ERDDAP](http://coastwatch.pfeg.noaa.gov/erddap/index.html) and [GeoServer](http://geoserver.org). Configuration files and instructions to set up ERDDAP and GeoServer instances for AAT data will be provided at the end of the project.

A collection of Python data access and visualization scripts that illustrated these services are [accessible as IPython notebooks at https://www.mygists.info/emiliom/tags/animalacoustictelem](https://www.mygists.info/emiliom/tags/animalacoustictelem). Here are two that access data from ERDDAP: [Example 1](http://nbviewer.ipython.org/6767422) and [Example 2](http://nbviewer.ipython.org/6767450).

**IN PROGRESS RIGHT NOW: Other documents and configuration files that will be made available here.**

  * Dataset ISO Metadata from ERDDAP, with experimental, partial XSL style sheet
    * [Live-rendering (as HTML) example, in javascript](http://habu.apl.washington.edu/mayorga/aat/ISOMetadataFinalExamplePackage/xslt_client.html)
    * [XML](http://habu.apl.washington.edu/mayorga/aat/ISOMetadataFinalExamplePackage/otnnepMOSERAnTags_iso19115.xml) and [XSL](http://habu.apl.washington.edu/mayorga/aat/ISOMetadataFinalExamplePackage/OTNmetadata_Emilio.xsl) documents used in the example. The XML document is static and was pre-fetched from ERDDAP.
  * AAT NANOOS PostgreSQL/PostGIS database and ERDDAP service configuration
    * [Package documentation](http://habu.apl.washington.edu/mayorga/aat/AAT_NANOOSConfigurations_FinalPackageDocs.pdf)
    * [Zip file with documentation, code, and configuration files](http://habu.apl.washington.edu/mayorga/aat/AAT_NANOOSpg2erddap_exchange.zip)
  * [AAT\_ERDDAP\_datasets\_listing\_and\_properties.xls](http://habu.apl.washington.edu/mayorga/aat/AAT_ERDDAP_datasets_listing_and_properties.xls)
  * [ERDDAPDatasetMetadata-UseAndStatus-FINAL.pdf](http://habu.apl.washington.edu/mayorga/aat/ERDDAPDatasetMetadata-UseAndStatus-FINAL.pdf)
  * QGIS project file
  * GeoServer GetCapabilities XML documents (static, pre-generated): [WMS](http://habu.apl.washington.edu/mayorga/aat/geoserver-otnnep-WMS-GetCapabilities.xml) & [WFS](http://habu.apl.washington.edu/mayorga/aat/geoserver-otnnep-WFS-GetCapabilities.xml)


## AAT Metadata Convention ##

### Origin of the Convention ###

The AAT Metadata Convention is based on data input forms from Pacific Ocean Shelf Tracking (POST), Ocean Tracking Network (OTN), Great Lakes Acoustic Telemetry Observation System (GLATOS), HYDRA, and The Integrated Marine Observing System (IMOS, the Australian Animal Tagging and Monitoring System (AATAMS), with additional feedback from other individual researchers and database operators such as Tagging Of Pacific Predators (TOPP) and Kintama Research.

### Purpose of the Convention ###
The purpose of the [AAT Metadata Convention (pdf)](http://ioostech.googlecode.com/files/AAT%20Metadata%20Convention%20v1.2.pdf) is to ensure that:
  * Enough information is transmitted to make data understandable (hence “required” fields)
  * The origin of the data is clear, and credit (attribution) is maintained
  * The receiving system can interpret the transmitted data without human intervention, including if necessary how flat files can be reassembled into a structure such as linked database tables.

The [vocabulary defined by the AAT Metadata Convention is hosted on the MMI ontological repository](http://mmisw.org/ont/ioos/animal_acoustic_telemetry). Individual terms may be referenced from it via MMI URL's, such as http://mmisw.org/ont/ioos/animal_acoustic_telemetry/animal_origin

## Other Resources ##

### IOOS Biology Data projects ###
  * http://www.ioos.noaa.gov/dmac/biology/welcome.html
  * http://www.ioos.noaa.gov/observing/animal_telemetry/welcome.html
  * [NOAA National Ocean Service Podcast (April 2013): Today on Diving Deeper, we explore the world of animal tagging with Zdenka Willis from the U.S. Integrated Ocean Observing System.](http://oceanservice.noaa.gov/podcast/p0413.html#dd46)

### POST and relevant OTN Data repository ###
  * [Ocean Tracking Network NE PACIFIC Ocean Data Series](http://members.oceantrack.org/data/discovery/NEPACIFIC.htm)

### ISO Dataset metadata (the 19115-related family) ###
The NOAA Geo-IDE site [has a nice summary of the differences between the three inter-related ISO metadata standards 19139, 19115 and 19115-2](https://geo-ide.noaa.gov/wiki/index.php?title=ISO_FAQ#What_are_all_of_these_numbers.3F). But it doesn't address the "Marine Community Profile (MCP) of ISO 19115". Here's a summary of the 3 ISO standards and one community profile:
  * **ISO 19115** is the main geospatial metadata standard that ["describes the general content of the metadata and relationships between metadata elements. It does not, however, provide any guidance on how the metadata records should be built and formatted."](http://www.fgdc.gov/metadata/fgdc-iso-activities)
  * **ISO 19139** [provides the XML encoding schema implementation for ISO 19115.](http://www.fgdc.gov/metadata/fgdc-iso-activities) So, 19115 is the content model, 19139 is the packaging.
  * **ISO 19115-2** has emerged in IOOS, oceanographic and meteorological circles as the ISO standard of choice for environmental datasets. ["Unfortunately, the name of 19115-2 is a bit misleading. It is essentially an extension of 19115 that adds information about missions, platforms and sensors, along with a few other things. Most environmental observations involve sensors, so 19115-2 is probably the right standard to use for most environmental datasets, not just imagery or gridded data."](https://geo-ide.noaa.gov/wiki/index.php?title=ISO_FAQ#What_are_all_of_these_numbers.3F). _ERDDAP uses ISO 19115-2 as its ISO dataset metadata standard._
  * The **Marine Community Profile (MCP) of ISO 19115** was defined by the Australian Ocean Data Centre around 2008. MCP ["supports the documentation and discovery of marine spatial datasets and forms the foundation of the Marine Catalogue. The MCP has been developed in accordance with the rules established by the International Standard ISO 19115 Geographic information - Metadata. The MCP is a subset of the standard and includes all ISO 19115 core metadata elements. In addition, the MCP has defined supplementary elements, codelists and controlled vocabularies to assist in the description of marine resources."](http://www.aodc.org.au/index.php?id=37). _OTN is using the MCP._

### Data Services used by animal acoustic telemetry groups ###
  * [OTN](http://oceantrackingnetwork.org/): Geoserver, OGC WMS, KML

### Other relevant systems ###
  * http://hydra3.sound-data.com
  * http://data.glos.us/glatos
  * http://aatams.emii.org.au/aatams/

### Miscellaneous ###
  * From Bob Simons, Regarding "Xtracto scripts": The R and Matlab scripts which make it easy to get the physical oceanography data (e.g., sea surface temperature, chlorophyll a) related to each point of an animal's track are available from http://coastwatch.pfel.noaa.gov/xtracto/ The author is Dave Foley, dave.foley(at)noaa.gov
  * From Derrick Snowden: [Here are a bunch of ipython notebook examples put together by Rich Signell](https://gist.github.com/rsignell-usgs). Many of them are focused on accessing netCDF/OPeNDAP datasets.