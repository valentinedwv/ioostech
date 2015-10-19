

[Day 1](SOSRefImplementWorkshop_Day1Agenda.md) |
[Day 2](SOSRefImplementWorkshop_Day2Agenda.md) |
[Day 3](SOSRefImplementWorkshop_Day3Agenda.md)


# Overview and Workshop Goals and Objectives (Derrick) #

## Main overview ##

  * Goals for the system
  * IOOS PO view of the enterprise
  * Selected Use Cases that drive system development
    * Automate the Asset Inventory (automatic repeatable view of the system)
    * Integration via the Data Catalog/Portal/Registry
    * Various ways to connect to users
    * Integration with other major programs
  * Assumptions/Constraints/Good to Know
  * Workflow for the next three days
    * Recording decisions
    * Noting next steps
    * Noting responsibility for future work or outstanding issues

## Other considerations and statements of goals ##

Define SWE Common encodings for all of the CF sampling feature types that:
  * provide all the information required for accurate plotting of the data
  * are simple and easy to publish
  * are simple and easy to read
  * are optimized for minimum size, reduce accessing time
  * provide all information necessary to unambiguously identify essential characteristics of the CF sampling feature types (should enable nearly lossless translation between the two encoding standards)
  * Provide a mechanism to encode quality information along with data values

We need a plan for including more metadata in the capabilities response to enable automatic harvesting by the IOOS catalog and other harvesting portals  (See OGC 06-121r9 - OGC Web Services Common Standard Version 2.0.0 for more information on common elements across OGC web services especially including relationships to ISO 1911x standards)

**Roadmap:**
  * identify data sources for each feature type (actual source data including platform metadata)
  * resolve ambiguities surrounding SOS 1.0 and 2.0 interpretation of “procedure, observationOffering, featureOfInterest, observedProperty”
  * create templates for each feature type
  * implement SOS services for each feature type at each RA
  * test by multiple clients

---



# The broader SOS request and response context #

> _"While time is passing, the technological foundations upon which data management systems are built are certain to continue advancing rapidly. These considerations argue for adopting attitudes of pragmatism and realism when planning data management strategies. We should understand that technological progress is always made in incremental steps, rather than 'heroic leaps'. We should give consideration to technology choices based upon their potential contributions to the distant vision, but we should measure them by their effectiveness at addressing today's challenges."_ [(1)](#Footnotes.md)

## General SOS Issues ##

Getting the basics and common elements squared away:
  * Settling on and clearly documenting conventions, controlled vocabularies, defaults, recommended best practices, etc, for all elements of GetCapabilities requests and responses
  * Minimal required DescribeSensor (SensorML) request and response
  * Aspects of GetObservation requests and responses related to the above, and not covered by the Day 2-3 Agenda (_SWE Common Templates for CDM Scientific Feature Types_)

Or described another way:

  1. **Develop clear and consistent IOOS SOS request and response specifications to be implemented uniformly across IOOS and used to:**
    * Develop and validate SOS services
    * Develop SOS clients
  1. **Clarify and extend mandated vs recommended practices, including:**
    * [Identifiers](#Identifiers.md)
    * [Classifiers (Controlled vocabularies)](#Classifiers_(Controlled_vocabularies).md)
    * [Default values and behaviors](#Default_values_and_behaviors.md)
    * [SOS requests Interface Definition Document](#SOS_requests_Interface_Definition_Document.md) (GetCapabilities, DescribeSensor, GetObservation)
    * Existing practices vs needed enhancements
    * Some [core IOOS Guidelines documents formerly available only as Word or pdf docs have been recently migrated to the Geo-IDE wiki](https://geo-ide.noaa.gov/wiki/index.php?title=Category:IOOS_Guidelines)

Many of these goals could be applied to the entire workshop, but as described are tuned to the Day 1 agenda. They also involve laying out a path for useful, clear service documentation, both in the form of bare-bones ["Interface Definition Document" (IDD)](https://groups.google.com/d/topic/ioostech_dev/hTMaCJtkcWo/discussion) templates that should be followed by every SOS service implementation (intended as a quick-takeup guide for service and client implementers and users), and more detailed documentation.

[The OOSTethys 2008 Guides and Best Practices documents](http://www.oostethys.org/best-practices) served as a foundation for many of the current IOOS SOS implementation details. It's still a highly relevant and well structured guide that we should refer to often and re-use as needed.

Address ambiguities in the SOS 1.0 (and 2.0?) data model.  This issue has been discussed by the OGC Hyrology DWG and they have not reached a conclusion that is conformant to the SOS 1.0 spec as they understand it.  There are implications for the format of the responses from all three SOS core operations (GetCapabilities, DescribeSensor, GetObservation).  There are also performance implications due to the way searches must be performed.

---



## Identifiers ##
Each term or concept used in the SOS should be referenced with a unique identifier such as a URN or URL.  If a URL is used, we do not (or do we?) require that the URL resolve to a human readable web page although that may be desirable in the future.  Even better is to have the vocabulary host implement some sort of content negotiation that presents the information differently for different clients (i.e. a browser might receive html whereas an ontology editor might receive rdf or N3).  For now, we need to determine the form of the identifiers and a policy for what we expect the identifier to reference on the web. And which set of identifiers we're targeting.

NOTE: OGC seems to be moving from  [URNs to URLs](http://think.random-stuff.org/posts/ogc-rediscovers-urls-but-lets-tighten-up-the-terminology-a-bit) (See this [old document](http://www.opengeospatial.org/ogcUrnPolicy) for the previous policy)

Existing IOOS identifier conventions include station (sometimes described as platform), sensors, and "collections" (network). These are currently implemented as urn's only.  See also [this wiki page from Micah](DescribeSensorMetadataForIOOSSOS.md).  And refer to the ["IOOS Conventions for Asset Identifiers" document](https://geo-ide.noaa.gov/wiki/index.php?title=IOOS_Conventions_for_Observing_Asset_Identifiers). This document was previously only available as a Word or pdf document, but was recently migrated to a versioned page on the GEO-IDE Wiki; does it deserve review or is it clear enough as is?

It would be useful to have some discussion on options for distinguishing redundant data within two a result set from two services.  For example, NDBC aggregates and reserves data from multiple RAs.  How can a user determine the intersection between the RA capabilities/Content and the NDBC capabilities/Content?  With respect to station identifiers, regional stations that have a WMO ID are often referred to by their regional (provider) ID. NDBC may be developing a URL-based ID resolve that can convert between each ID in their IOOS URN forms.

## Classifiers (Controlled vocabularies) ##

The target set of controlled vocabulary types we will likely need are:
  * [organization type](ControlledVocabularies#Organization_Types_and_Roles.md) (eg, Federal agency, IOOS Regional Association, state agency, industry)
  * [organizational role](ControlledVocabularies#Organization_Types_and_Roles.md) (service provider, data provider or asset owner)
  * [platform (asset) type](ControlledVocabularies#Platform/Station_types.md)
  * [observed property](ControlledVocabularies#Observed_Property_Vocabularies.md)
  * [units-of-measure](ControlledVocabularies#Units_of_Measure.md)
  * keywords (including geographical regions?)

Address implementation details, in general and for each targeted vocabulary type. For more extensive discussions, see:
  * [ControlledVocabularies](ControlledVocabularies.md): primary wiki page on controlled vocabularies. Final decisions must be reconciled and made consistent with the information at [ControlledVocabularies](ControlledVocabularies.md).
  * [DescribeSensorMetadataForIOOSSOS](DescribeSensorMetadataForIOOSSOS.md), from Micah. Addresses several classifier types and options, particularly in SensorML.

_DPS Comment: One desirable outcome of this session would be to approve and improve [this table](ControlledVocabularies#Existing_Observed_Property_Vocabularies.md) on the ControlledVocabularies page.  In particular we should prioritize the vocabularies, correct the URLs, and provide examples.  Then, correcting the actual usage of each vocabulary in the tables that follow is a trivial exercise._


## Default values and behaviors ##

A draft of elements. These may be parsed out into different sections in the final agenda. _This is not yet comprehensive or vetted, of course!_

  * access: HTTP GET and POST, but mainly GET. Note: A recent analysis of the NDBC SOS showed that POST access is barely ever used.
  * GET KVP's are case-insensitive; both K & V, or all K's and **some** V's? See OOSTethys recommendation.
  * a request to the naked, unqualified service (no request, service or version keys) returns the GetCapabilities response. _This was the [OOSTethys](http://www.oostethys.org/)-recommended convention (Eric, is that true?). Should we continue it?_
  * use of a default namespace in XML responses is forbidden
  * correct XSD and namespace references for GetCapabilities; here's a sample, from the NANOOS SOS:
```
<sos:Capabilities 
 xmlns:xlink="http://www.w3.org/1999/xlink" 
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
 xmlns:sos="http://www.opengis.net/sos/1.0" 
 xmlns:ogc="http://www.opengis.net/ogc" 
 xmlns:ows="http://www.opengis.net/ows/1.1" 
 xmlns:gml="http://www.opengis.net/gml" 
 xmlns:swe="http://www.opengis.net/swe/1.0.1" 
 xmlns:om="http://www.opengis.net/om/1.0" 
 xsi:schemaLocation="http://www.opengis.net/sos/1.0  http://schemas.opengis.net/sos/1.0.0/sosGetCapabilities.xsd" 
 version="1.0.0">
```
  * **spatial (XYZ) conventions**
    * all x & y locations are only in lat-lon (wgs84, nothing else); these are fully qualified and parseable (srs, etc), but for now it's best to also accept that we'll only deal with lat-lon
    * depth/elevation conventions?
  * **temporal conventions**
    * all datetime values are specified as iso8601 strings, where seconds are optional (in requests)
    * only UTC/GMT time support is currently required, for both requests and responses
    * in GetCapabilities offerings response, address convention for `<gml:TimePeriod><gml:endPosition>`, including use of 'now' and 'unknown' (see our recent discussions)
    * in GetObservation request, eventTime is optional; if absent, the latest observations will be returned. [See the relevant OOSTethys 2008 document, "Get Latest"](http://www.oostethys.org/best-practices/getlatest)
    * Issues with ISO 8601 and encoding time zones or time offsets
    * See 2-3 relevant wiki pages or sections (will link to them later)
  * As the IOOS SOS guidance/profile/requirements formalize and then start to evolve, we'll have a need to define "versions" and encode the IOOS SOS version in SOS responses.
  * Any guidance on whether the SOS service should strive to include data that are now historical (eg, buoy off the water and not coming back)? Can we set up this work to also feed into the IOOS Asset Inventory?
  * In GetObservation requests, [will we support multiple stations and multiple and/or vector/composite observed properties?](ControlledVocabularies#Composite_Properties.md)
    * Requesting multiple stations can be handled via a "Network" offering and procedure requests with comma-separated station urn arguments.
  * **Other, less widely adopted or standardized components (but potentially very useful)**
    * Combinations of these components may address several important issues (eg, more granular queries) we have discussed
    * "Network" offerings (currently used by NDBC and COOPS for "All" and specific subsets). Usage, challenges, and overlap with other functionality.
    * Is there a more useful role for procedure in GetCapabilities and GetObservation, in the current IOOS usage?
    * What role, if any, for featureOfInterest and FilterEncoding implementations?
      * For some early, limited featureOfInterest discussions, [see this 2008/2009 OOSTethys page](http://www.oostethys.org/best-practices/foi). If we implement something more sophisticated than "Earth:Ocean" or just the station location (assuming fixed site), we should consider how it interacts with the practice of using "Network-`*`" offerings currently used by NDBC and NOS; there's probably overlap.
      * Discussions and examples of use of FilterEncoding, [from a 2010 wiki page by the OGC Hydrology DWG (early WaterML 2 discussions)](http://external.opengis.org/twiki_public/HydrologyDWG/GwIeSOSResultFilter)


## SOS requests Interface Definition Document ##

See [SOSGuidelines#SOS\_Requests\_(IDD)](SOSGuidelines#SOS_Requests_(IDD).md)

## Other issues ##

### Encoding Quality Control Flags (Mohamed) ###
NDBC and CO-OPS will both be working on this in FY12 and certification of RAs will require this as well.  High priority topic but for the purposes of the group the problem is about encoding QC flags, not defining or selecting QC tests.


# Footnotes #

<sup>(1)</sup> Hankin, S., L. Bermudez, J.D. Blower, B. Blumenthal, K.S. Casey, M. Fornwall, J. Graybeal, R.P. Guralnick, T. Habermann, E. Howlett, B. Keeley, R. Mendelssohn, R. Schlitzer, R. Signell, **D. Snowden** and A. Woolf, (2010), Data Management for the Ocean Sciences - Perspectives for the Next Decade, in _Proceedings of OceanObs'09: Sustained Ocean Observations and Information for Society (Vol. 1)_, Venice, Italy, 21-25 September 2009, Hall, J., Harrison, D.E. & Stammer, D., Eds., ESA Publication WPP-306, [doi:10.5270/OceanObs09.pp.21](http://www.oceanobs09.net/proceedings/pp/pp21/)