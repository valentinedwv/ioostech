

# Purpose #

This wiki describes the architecture of the Data Management and Communications subsystem of the Integrated Ocean Observing System.  The information here shows the high level organization of DMAC with an emphasis on the Data Access Services.  The description will continue to evolve.  This wiki should be considered the developement version of the architecture description.  Occasionally material developed here on the wiki will be moved to more static locations to maintain some version control.



> _AB:<sup>IOOS Profile seems to be pretty adequate as</sup> [OGC Glossary of Terms](http://www.opengeospatial.org/ogc/glossary/p) <sup>defines "profile" as "a collection of standards, with parameters, options, classes, or subsets, necessary for building a complete computer system, application, or function. An implementation case of a more general standard or set of standards."</sup>_



### Introduction ###



### Data Services and Content Standards ###

  * DataAccessServices
    * SOS
      * [SOSGuidelines (IDD v1.0)](SOSGuidelines.md)
        * SOSConcepts (definitions and common usage for observedProperty, featureOfInterest, procedure, and ObservationOffering)
        * Request Parameters and usage
        * Response types (aka Templates)
        * SOSVocabularies (any SOS specific modifications or additions to the overall [Vocabularies\_final](Vocabularies_final.md) ControlledVocabularies page.
      * [SOSClients](SOSClients.md)
        * EnvironmentalDataConnector
        * Proteus
        * PyOOS
        * JavaNetCDFIOSP
      * SOSServers
        * 52NorthSOS
        * ncSOS
        * DIF SOS (NDBC) Probably should be renamed.  Should these server pages be included underneatht the SOSGuidleines IDD so that the information can be version specific?
        * NANOOS Python SOS
        * OostethysSOS
    * OPeNDAP based services (Guidelines for use, not necessarly an all encompassing technical documentation.  Only IOOS specifics)
      * ERDDAP
      * THREDDS
      * Hyrax
      * PyDAP
      * netCDF (Web Service agnostic discussion of file formats and data models relevant to them.  Mostly focused on netCDF and the so-called standards in use in that area (CF, Glider Files, Argo, OceanSITES, Discrete Sampling Geometries etc)
    * WMS
  * [Controlled Vocabularies](Vocabularies_final.md)
    * See the outline and content currently on that page
  * Metadata
  * QualityControl

### IOOS System Integration ###

  * ServiceRegistry
  * DataCatalog
  * [AssetInventory](AutomatedAssetInventory.md)
  * SystemViewer
  * SystemMonitor


# Pieces to consider #
  1. Do we need to maintain a complete record of the workshop (preparation/proceedings/conclusions?)
  1. Do we need a more thorough crosswalk with CF Discrete Sampling Geometries or is this something better done by other groups or on other information portals and wikis?  CF wiki, [NOAA EDM wiki](https://geo-ide.noaa.gov/wiki/) (formerly geo-ide wiki), [ESIP Federation](http://wiki.esipfed.org)?
  1. Filling out the other big pieces of DMAC (RCV, Regional Portals)
  1. Playing well with others.  How to register with ocean.data.gov, GEOSS Common Infrastructure, etc.?
  1. Intersections with the international programs
  1. Observing System specific stuff.  The CF netCDF template for gliders is almost done and doesn't have an online home yet.
  1. More direct intersections with HFR/Waves
  1. Tools for anything (web harvesting resources, other clients)
  1. Training, demos, movies, mashups, example scripts
  1. Individual regional IDD noting difference with the generic IDD:
    * <sup>AB: In my opinion the IDD should be a single document, and regional variety should be captured in the IDD sub-sectiones rather than in separate docs. Otherwise, the main IDD becomes just a notional document that will be replicated every time with regional specifics.  BTW, these specifics have to be relatively small aberrations of the main IDD or else the IOOS Profile term becomes vague.</sup>