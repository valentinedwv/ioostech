

# Introduction #
This document summarizes the CF Feature Types as part of the [SOSReferenceImplementationWorkshop](SOSReferenceImplementationWorkshop.md) discussion.

Based on the [CF 1.6 Conventions](http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#idp6280704), we need to develop SWE encodings for the feature types in use by the IOOS community.  These have been identified as:

  * **timeSeries** - a series of data points at the same spatial location with monotonically increasing times
  * **timeSeriesProfile** - a series of profile features at the same horizontal position with monotonically increasing times
  * **trajectoryProfile** - a series of profile features located at points ordered along a trajectory
  * **trajectory** - a series of data points along a path through space with monotonically increasing times.  This has no Z dimension associated with it (path over a 2D plane over time).  It can be represented as a trajectoryProfile with a constant Z and P dimension.

The solutions for encoding the above into SWE should **NOT** exclude the other CF Feature Types from being represented (it will be likely that these will be used to represent the above):

  * **point** - a single data point having no implied coordinate relationship to other points.  x(1), y(1), t(1).  **The can be represented as a timeSeries with a single data record**
  * **profile** - an ordered set of data points along a vertical line at a fixed horizontal position and fixed time.  **This can be represented as a timeSeriesProfile with a time dimension of length 1.**


CDL representation of the geometries can be found [here](http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#appendix-examples-discrete-geometries).

It is worth mentioning here that NetCDF files in the CF 1.6 spec can only represent one featureType at a time.  If at all possible, this should not be a restriction of the SWE mappings.

NetCDF files can also represent data from multiple stations.  A timeSeries at multiple stations can be represented in one file.  I don't know how this will map to SWE.

The initial, draft SWE representations included in this wiki document were [taken from the 2009 OGC wiki document, "SWE Common encoding of CF-NetCDF coverage data"](http://external.opengis.org/twiki_public/NREwg/SWECommonNetCDFTutorial). Unfortunately, that document didn't get around to fleshing out **profile** and **trajectory** SWE Common encodings (or their corresponding time series, of course).

Here is the explanation of the different types of storage techniques: http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#representations-features

# Overlap with the IOOS CSV Specs #

See the [IOOS CSV/TSV encodings](https://geo-ide.noaa.gov/wiki/index.php?title=IOOS_Conventions_for_CSV_and_TSV_Encoding) document for prior guidance on using these data formats with SOS.  Note, the document above at the [GEO-IDE wiki](https://geo-ide.noaa.gov/wiki/index.php) is the most recent version of this information. All other documents whether they are pdf, word or google docs version of the above information should be considered deprecated.

Additional IOOS Guidelines can be found [here](https://geo-ide.noaa.gov/wiki/index.php?title=Category:IOOS_Guidelines).  As above, these wiki versions of the information supersede previous versions.

# Other netCDF Issues #

  * General construct for mapping global attributes
  * More specific mechanism for certain types of information such as contact person
  * Generic construct for variable attributes
  * Specific variable attributes
    * standard\_name
    * units
    * long\_name
    * auxillary\_variables
    * axis
  * Mapping the featureType = "timeSeries"; attribute to O&M (featureOfInterest?)
  * Mapping the cf\_role=”timeseries\_id” attribute to O&M

# Other, related information #

Other potentially documents (mostly from deprecated SWECommonPlan wiki page):

  * [Paper (pdf) on SOS mobile profile for consideration when we get to trajectories](https://wiki.52north.org/pub/Sensornet/SosMobileExtension/20080306_SOSmobile.pdf)
  * http://www.ogcnetwork.net/GEOSS_Climate_Workshop_2011
  * [WCS 2.0 Extension for netCDF-CF, CSW and THREDDS Interoperability](https://portal.opengeospatial.org/files/?artifact_id=46131)