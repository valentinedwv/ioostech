


# DISCLAIMER #

This is a holding place for the previous version of the IOOS SOS Milestone 1.0 guide book. It is now deprecated and completely taken over by the IOOS SOS [[Web Service Description Document (WSDD)](https://ioostech.googlecode.com/files/IOOS%20SOS%20WSDD%20Draft%20v0.91.docx). The WSDD is from now on the sole source of the IOOS SOS Profile v1.0 implementation. We will be in the process of cleaning this wiki in early 2014.



# Interface Definition Document #
The materials on this page refer to Version 1.0 of the IOOS SOS profile.

IOOS data from fixed and mobile observing platforms can be obtained over the internet using the Sensor Observation Service (SOS) specification published by the Open Geospatial Consortium. An SOS has three basic operations:

  * GetCapabilities provides summary information about the service and about the platforms for which it provides data.
  * DescribeSensor provides descriptions of individual sensors, platforms supporting one or more sensors, and networks of related platforms.
  * GetObservation provides time-series data from one or more sensors on one or more platforms.

# SOS Concepts #

# SOS Requests #

_See the new, draft [IDD documentation from NOS/COOPS for their test SOS service](http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos-test/). It's a terrific, dynamic, rich example that we should strive to replicate._

## HTTP GET Request ##

**NOTE** This section is taken from the Oostethys wiki and has (will be) modified to fit the current IOOS specification.   [OOSTethys 2008 "Best Practices SOS HTTP GET Request" document](http://www.oostethys.org/best-practices/best-practices-get)

An HTTP request could be of various types: GET, POST, PUT etc., as explain in the [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html). GET passes parameters to the server in the HTTP URL (e.g. http://marinemetadata.org:9600/oostethys/sos?VERSION=1.0.0&SERVICE=SOS&REQUEST=GetCapabilities). POST sends a document to the server, allowing an message or result to be returned,  or to provide a block of XML data, among others.

At OOSTethys we found that the GET request is very popular in the oceanographic community, because it is well-understood, easier to implement and easier to query. Sensor Observation Service, however,  does not explicitly use a GET request. This section explains the GET request operations supported by OOSTethys Sensor Observation Service cookbooks. The information presented here was mostly extracted from OGC specifications and in some cases clarifications and minor comments were added. If not noted, this section complies with the OGC Web Services Common Specification 1.1.0 ([OGC 06-121r3](http://portal.opengeospatial.org/files/?artifact_id=20040)) and the Sensor Observation Service Specification 1.0 ([OGC 06-009r6](https://portal.opengeospatial.org/files/?artifact_id=26667)). If there are discrepancies between the specification and the schema, the schema is preferred.

The document first presents the general structure of a GET request, notes about how to handle special characters and capitalization rules. Then, the document presents the GET request details for each of the Sensor Observation Service (SOS) supported by OOSTethys, which correspond to the three mandatory operations in a Sensor Observation Service (SOS):


  * [GetCapabilities](GetCapabilities#Request.md)  returns general metadata about the service, operations supported and list of observation offerings;
  * [DescribeSensor](DescribeSensor#Request.md) returns metadata about a sensor system. It could be an observing system, platform or a simple device, such as a bin. The return is given as a SensorML or TML document;
  * [GetObservation](GetObservation#Request.md) returns a collection of observations. each observation is composed of metadata, description of the phenomena being returned (parameter names, units of measure, reference systems) and values.


### Structure of the GET request ###
The structure of the operation is specified in Table 34 ([Whiteside, 2007](http://portal.opengeospatial.org/files/?artifact_id=20040)).

|**URL**| **Component** |	**Description**|
|:------|:--------------|:---------------|
|`!http://host[:port]/path[?{name[=value]&}]`	| URL prefix of service operation. | `[ ]` denotes 0 or 1 occurrence of an optional part; `{}` denotes 0 or more occurrences.|
|`name=value&`	| One or more standard request parameter name/value pairs as defined for each operation by this International Standard. This parameter encoding is referred to as Keyword Value Pair (KVP) encoding in this document. |                |


### Reserved characters ###
|**Character** | **Reserved usage** |
|:-------------|:-------------------|
|`?`           |	Separator indicating start of query string or the KVPs.|
|`&`           |	Separator between the parameter (name/value) pairs in query string.|
|`=`           |	Separator between name and value of parameter.|
|`,`           |	Separator between individual values given for a parameter.|

### Capitalization of Keyword Value Pair (KVP) names and values ###

**Parameter names** are case insensitive. The following example shows equivalent terms for a parameter named “request”: REQUEST, request, Request, or ReQuEsT. As a guideline, it is suggested that lowercase names be used for ease-of-reading and consistency.

**Parameter values** are case sensitive and string values are [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase). These are appropriate examples for parameter values: GetObservation, DescribeSensor.

### Escaping special characters ###
[IETF 2396 , section 2.4.1](http://www.ietf.org/rfc/rfc2396.txt) explains that special characters should be escaped as follows: percent character "%" followed by the two hexadecimal digits.  This is important because both URIs, and URNs could be sent as values for parameters, and they may include special characters . An online application that helps to convert special characters to escaped characters could be found [here](http://www.xs4all.nl/~jlpoutre/BoT/Javascript/Utils/endecode.html).

|**Special character**|**Escaped encoding**|
|:--------------------|:-------------------|
|:	                   |%3A                 |
|/	                   |%2F                 |
|#	                   |%23                 |
|?	                   |%3F                 |
|=	                   |%3D                 |


# Response #

The response given by the server to valid (as described above) requests are documented on the following pages.

  * [GetCapabilities](GetCapabilities#Response.md)
  * [DescribeSensor](DescribeSensor#Response.md)
  * [GetObservation](GetObservation#Response.md)

# OGC Standards and Specifications #

The versions of the international OGC standards and specifications used in the IOOS SOS implementation. The IOOS implementation includes some extensions.

| **Specification** | **Version** | **Comments, Resources** |
|:------------------|:------------|:------------------------|
| GML               | 3.11        |                         |
| O&M               | 1.0         | [O&M 1.0.0 for SOS 1.0.0.(52 North)](https://wiki.52north.org/bin/view/Sensornet/SosDataModeling) |
| SOS               | 1.0         |                         |
| SWE Common        | 1.01        | Used everywhere except for om:result in GetObservation response ([SWE Common 1.0 Standard coupled with SensorML Standard](http://portal.opengeospatial.org/files/?artifact_id=21273)) |
| SWE Common        | 2.0         | Used in om:result of GetObservation response |
| SensorML          | 1.0         |                         |

  * **GML**: Geographic Markup Language
  * **O&M**: Observations & Measurements
  * **SOS**: Sensor Observation Service
  * **SWE**: Sensor Web Enablement

# Rules #

This section contains IOOS specific rules that have been distilled from resolved issues or mailing list discussions. The rule should have a human readable identifier, be concise, and include a link to the original discussion for background info. Developers writing SOS clients and validators should be able to use these rules to guide their coding.


## Composite phenomena ##
Link: http://code.google.com/p/ioostech/issues/detail?id=1

Although support of composite phenomena is **OPTIONAL** for IOOS service providers, the implementation of the composite phenomena shall comply with the following rules (these rules accommodate both true composite phenomena like winds, and ad-hoc requests for multiple properties like water and air temperature):
  1. IOOS-defined vector variables (namely winds, currents and waves) shall be advertized in GetCapabilities response as composite phenomena that contains scalar properties defined in the CF standard names vocabulary.
  1. The supported composite phenomena are defined in the IOOS Parameter Vocabulary (e.g.: http://mmisw.org/ont/ioos/parameter/wave).
  1. The exact collection of individual scalar properties that is used by a service provider to form a certain composite phenomenon shall be a subset of the properties defined in the IOOS Parameter Vocabulary for that composite phenomenon.
  1. In the GetObservation response, the `<om:observedProperty>` element under each `<om:ObservationCollection>/<om:member>/<om:Observation>` block shall return a list of scalar properties only, referencing the MMI CF or IOOS parameter vocabularies.
  1. The `<swe:CompositePhenomenon>` element shall be used even when the response returns a single observed property:
    * attribute `<gml:id>` is required. Each `<om:ObservationCollection>/<om:member>/<om:Observation>` block shall have a document-wide unique `<gml:id>` value. It is recommended to use just a simple integer counter next to a fixed string, as shown in examples below.
    * child element `<gml:name>` is required; the element value may be any text string.

EXAMPLE 1 (multiple scalar properties):
```
<om:observedProperty>
  <swe:CompositePhenomenon dimension="4" gml:id="observedproperties1">
    <gml:name>Response Observed Properties</gml:name>
    <swe:component xlink:href="http://mmisw.org/ont/cf/parameter/air_temperature"/>
    <swe:component xlink:href="http://mmisw.org/ont/cf/parameter/wind_speed"/>
    <swe:component xlink:href="http://mmisw.org/ont/cf/parameter/wind_gust"/>
    <swe:component xlink:href="http://mmisw.org/ont/ioos/parameter/dissolved_oxygen"/>
  </swe:CompositePhenomenon>
</om:observedProperty>
```

EXAMPLE 2 (single scalar property):
```
<om:observedProperty>
  <swe:CompositePhenomenon dimension="1" gml:id="observedproperties1">
    <gml:name>Response Observed Properties</gml:name>
    <swe:component xlink:href="http://mmisw.org/ont/cf/parameter/wind_speed"/>
  </swe:CompositePhenomenon>
</om:observedProperty>
```


## Versions of SOS, SWE and O&M ##
Link: http://code.google.com/p/ioostech/issues/detail?id=2

In order to keep up the interoperability with IOOS-compliant services, the following versions shall be used:
  1. Both SOS and O&M version 1.0.
  1. SWECommon version depends on the function:
    * in GetCapabilities and DescribeSensor – SWECommon 1.0.1 (prefix `<swe:>`);
    * in GetObservation – SWE 1.0.1 (prefix `<swe:>`) except for the contents of `<om:result>`, which shall use SWE 2.0 (prefix `<swe2:>`).


## URN vs. URL ##
Link: http://code.google.com/p/ioostech/issues/detail?id=3

The use of both URNs and URLs are allowed for now, but it is recommended to use URLs where possible. URNs should be used only where a specific IOOS guideline has stipulated it (mainly for station id, sensor id, and "network" id).


## Support of `<observedProperty>` ##
Link: http://code.google.com/p/ioostech/issues/detail?id=4

In general, SOS servers should only support what it advertises in the GetCapabilities document. Thus, an SOS server may support both fully qualified and unqualified `<observedProperty>` parameters as far as they are advertized in GetCapabilities.

IOOS-compliant SOS server shall be able to advertise and accept fully qualified `<observedProperty>` parameters.


## Asset URN identifiers ##
Link: http://code.google.com/p/ioostech/issues/detail?id=14

Link: https://groups.google.com/forum/#!topic/ioostech_dev/F1SBuamGUrI/discussion

Asset URN identifiers generally follow the convention explained at https://geo-ide.noaa.gov/wiki/index.php?title=IOOS_Conventions_for_Observing_Asset_Identifiers, although this page needs to be updated.

Supported asset URN ids are network, sensor, and station. Platform is not a supported id.

Formats:

  * Station: urn:ioos:station:wmo:41001
  * Sensor: urn:ioos:sensor:wmo:41001:baro1
  * Network: urn:ioos:network:aoos:all-barometric

Definitions:

  * Station: http://mmisw.org/ont/ioos/definition/stationID
  * Sensor: http://mmisw.org/ont/ioos/definition/sensorID
  * Network: http://mmisw.org/ont/ioos/definition/networkID

Version (deployment date, etc) is not included in the URN standard at this time.


<font color='red'>

<h2>Representing quality flags in <code>GetObservation</code> (need more editing)</h2>
Link: <a href='http://code.google.com/p/ioostech/issues/detail?id=15'>http://code.google.com/p/ioostech/issues/detail?id=15</a>

The QC framework is significantly simplified using the new data structure with separate records for static and dynamic data.<br>
In a timeSeries feature it becomes straight forward to add static QC metadata to a station or sensor and dynamic metadata to each quantity. There is still no good solution for QC metadata for all fields in a sensor record at a single timestep.<br>
<a href='https://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-MultiStation-TimeSeries_QC.xml'>https://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-MultiStation-TimeSeries_QC.xml</a>
In a timeSeriesProfile feature it is possible to apply static QC metadata to a station or sensor and dynamic QC metadata to a profile, a bin or a quantity.<br>
<a href='https://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-SingleStation-TimeSeriesProfile_QC.xml'>https://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-SingleStation-TimeSeriesProfile_QC.xml</a>

The data array in the timeSeriesProfile provides additional structure on which to put a QC (quality) element for each timestep or profile. It is unfortunate that there is no obvious way to do the same for a timeSeries. Suggestions are welcome.<br>
<br>
</font>

## Requests with no time filtering ##
Link: http://code.google.com/p/ioostech/issues/detail?id=17

In general, any IOOS-compliant SOS server shall follow the SOS version 1.0 specification requirements. However, in the case when SOS request does not contain any time filter, the SOS v1.0 fails to properly describe the server behavior.
In that specific case, the IOOS-compliant server shall follow the SOS v2.0 specification, which requires the server to return all records matching a user request, although a result limit may be employed, and `ResponseExceedsSizeLimit` exception code shall be returned if that limit is exceeded.

## External link in `DescribeSensor` response ##
Link: http://code.google.com/p/ioostech/issues/detail?id=18

To represent an external link in the contact information part of the DescribeSensor response, an IOOS-compliant service shall use `< xlink:href>` attribute of the `<sml:contact>` element in the following manner:
```
<sml:contact xlink:role="urn:ogc:def:classifiers:OGC:contactType:publisher" xlink:href="http://sdf.ndbc.noaa.gov/">
  <sml:ResponsibleParty>
    <sml:contactInfo/>
  </sml:ResponsibleParty>
</sml:contact>
```


## Representing feature type in `GetObservation` ##
Link: http://code.google.com/p/ioostech/issues/detail?id=21

IOOS-compliant SOS server shall represent FeatureType (e.g., timeSeries, point, profile, etc)in GetObservation response as follows (this representation keeps the SWE elements the same between all FeatureTypes):

```
<om:featureOfInterest>
  <gml:FeatureCollection>
    <gml:metaDataProperty>
      <gml:name codeSpace="http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#discrete-sampling-geometries">timeSeries</gml:name>
    </gml:metaDataProperty>
    <gml:location>
      ...
    </gml:location>
  </gml:FeatureCollection>
</om:featureOfInterest>
```

Each unique CF feature type (discrete-sampling-geometries) shall be encoded in a separate `<om:member>/<om:Observation>` block that may contain multiple stations. Conversely, all stations corresponding to one feature type shall be returned in a single `<om:member>/<om:Observation>` block. The encoding of the reference to the CF feature type shall be done within `</om:ObservationCollection>/<om:member>/<om:Observation>/<om:featureOfInterest>/<gml:FeatureCollection>`:

```
<gml:metaDataProperty>
	<gml:name codeSpace="http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#discrete-sampling-geometries">timeSeries</gml:name>
</gml:metaDataProperty>
```


## Definition of station and sensor IDs in `GetObservation` ##
Link: http://code.google.com/p/ioostech/issues/detail?id=22

In the `<om:result>` block of the GetObservation response, the `<swe2:Text>` element rather than `<swe2:Category’> shall be used to define _stationID_ or _sensorID_, as shown below:
```
<om:result>
    <swe2:DataStream>
        <swe2:elementType name="components">
            <swe2:DataRecord>
                <swe2:field name="stationID">
                    <swe2:Text definition="http://mmisw.org/ont/ioos/definition/stationID">
                        <swe2:value>urn:ioos:station:wmo:41001</swe2:value>
                    </swe2:Text>
                </swe2:field>
                <swe2:field name="sensorID">
                    <swe2:Text definition="http://mmisw.org/ont/ioos/definition/sensorID"/>
                </swe2:field>
            </swe2:DataRecord>
        </swe2:elementType>
    </swe2:DataStream>
</om:result>
```


## Child procedures in `DescribeSensor` ##
Link: http://code.google.com/p/ioostech/issues/detail?id=23

The IOOS-compliant SOS service shall encode in the `<sml:component>` the child procedure ID (asset identifier) and link to the child's DescribeSensor response using `<xlink:title>` and `<xlink:href>` respectively; any further child information is optional:
```
<sml:components>
  <sml:ComponentList>
    <!-- sml:component with name and xlink:href to DescribeSensor is required -->  
    <sml:component name="component1" xlink:href="http://192.168.8.15:8080/sos?REQUEST=DescribeSensor&service=SOS&version=1.0.0&procedure=urn:ogc:object:feature:Sensor:IFGI:ifgi-sensor-1&outputFormat=text%2Fxml%3Bsubtype%3D%22sensorML%2F1.0.1%22 xlink:title="urn:ogc:object:feature:Sensor:IFGI:ifgi-sensor-1"/>
    <sml:component name="component2" xlink:href="http://192.168.8.15:8080/sos?REQUEST=DescribeSensor&service=SOS&version=1.0.0&procedure=urn:ogc:object:feature:Sensor:IFGI:ifgi-sensor-2&outputFormat=text%2Fxml%3Bsubtype%3D%22sensorML%2F1.0.1%22 xlink:title="urn:ogc:object:feature:Sensor:IFGI:ifgi-sensor-2"/>
     <!-- any further summary sml:System info is optional -->
     <sml:System gml:id="station-bb0101">
        <gml:description>OSTEP2</gml:description>
        <sml:identification xlink:href="urn:ioos:station:NOAA.NOS.CO-OPS:bb0101" />
        <sml:location>
          <gml:Point srsName="urn:ogc:def:crs:epsg::4326" gml:id="LOCATION-bb0101">
            <gml:coordinates>36.8572 -76.30833</gml:coordinates>
          </gml:Point>
        </sml:location>
      </sml:System>
    </sml:component>
  ...
  </sml:ComponentList>
</sml:components>
```

## XML header and namespace references ##
Link: http://code.google.com/p/ioostech/issues/detail?id=25

The IOOS-compliant SOS service shall conform to the following specific patterns for the namespace references in the GetCapabilities and GetObservation response XML headers:
  1. In GetCapabilities, the `<swe:>` namespace definition may be omitted.
  1. In GetObservation, the `<swe:>` and `<swe2:>` namespace definitions shall be included, and shall refer to versions 1.0.1 and 2.0 respectively (for additional information look [here](SOSGuidelines#Versions_of_SOS,_SWE_and_O&M.md)).
  1. In both GetCapabilities and GetObservation, the `<gml:>` namespace definition may omit reference to a version number (because the O&M 1.0 schema already defines GML 3.1.1 as the version used).

## Station offerings in `GetCapabilities` and `GetObservation` ##
Link: http://code.google.com/p/ioostech/issues/detail?id=26

In GetCapabilities, the `<sos:ObservationOffering>` element for a network offerings shall contain just a single `<sos:procedure>` element with `<xlink:href="NETWORK ID URN">` attribute, whereas the individual station procedures encompassed by the network offering shall be obtained via a DescribeSensor request.

A GetObservation request to IOOS-compliant SOS server shall include **ONLY** one offering, but may include multiple procedures.

A GetObservation response shall conform to the following rules:
  * The network offering URN shall be displayed just once, outside the `<om:Observation>` elements, as the content of a `<om:ObservationCollection>/<gml:name>` element. For single station offerings, the `<om:ObservationCollection>/<gml:name>` may indicate the station URN.
The `<om:ObservationCollection>/<om:member>/<om:Observation>/<gml:name>` shall follow the naming pattern <OFFERING ASSET URN>-<FEATURE TYPE>, e.g.:
```
<gml:name>urn:ioos:network:noaa.nws.ndbc:all-timeSeries</gml:name>
```
  * The single `<om:procedure>` element shall list all the station URN's corresponding to the `<om:Observation>` feature type, and the station URNs shall be placed into individual `<gml:member>` elements within `<om:procedure>` as follows:
```
<om:procedure>
  <om:Process>
    <gml:member xlink:href="urn:ioos:station:wmo:41001" />
    <gml:member xlink:href="urn:ioos:station:wmo:41002" />
  </om:Process>
</om:procedure>
```


## Representation of platform/sensor horizontal coordinates ##
Link: http://code.google.com/p/ioostech/issues/detail?id=27

Link: http://code.google.com/p/ioostech/issues/detail?id=28

Link: http://code.google.com/p/ioostech/issues/detail?id=19


The IOOS SOS implementation treats `<om:featureOfInterest>` as the single container for all geospatial and feature-type response metadata (i.e., all information that is outside the `<om:result>` block). As the station location information is one such element, it shall be placed in the `<om:featureOfInterest>/<gml:FeatureCollection>` block of the GetObservation response; that allocation validates with the Oxygen XML Editor, so it's just as valid as placing geospatial metadata outside `<om:featureOfInterest>` as was previously done (i.e. at the same hierarchy level as `<om:procedure>`, `<om:samplingTime>`, etc.).

Despite having been “deprecated” (i.e., "not recommended to use") since GML 3.1.0, the `<gml:location>` remains the least complex and all-sufficient structure among many options of reporting station position. In addition, the use of “location” structure provides the pragmatic advantage of identical location encoding in GetObservation (`<gml:location>`) and DescribeSensor (`<sml:location>`).

The following rules encompass the geospatial metadata representation in IOOS-compliant GetObservation and DescribeSensor responses:

  * The `<om:featureOfInterest>/<gml:FeatureCollection>/<gml:location>/<gml:Point>` structure shall be used to represent station location metadata in a single-station GetObservation response (EXAMPLE 1 below).

  * The `<om:featureOfInterest>/<gml:FeatureCollection>/<gml:location>/<gml:MultiPoint>` structure shall be used to represent station location metadata in a multi-station GetObservation response (EXAMPLE 2 below).

  * The `<sml:SensorML>/<sml:member>/<sml:System>/<sml:location>/<gml:Point>` structure shall be used to represent station location metadata in a single-station DescribeSensor response (EXAMPLE 3 below).

  * The `<gml:Point>/<gml:name>` element shall be used to associate the _stationID_ with the station coordinates in both multi-station and single-station GetObservation, and in single-station DescribeSensor responses.

  * The `<gml:boundedBy>` element shall be used to represent geospatial metadata in a multi-station (i.e. “network-al”) DescribeSensor response, where the `<gml:envelope>` coordinates shall define an actual rectangle(EXAMPLE 4 below).

EXAMPLE 1 (single-station GetObservation):
```
<gml:location>
  <gml:Point srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
    <gml:name>urn:ioos:station:wmo:41001</gml:name> 
    <gml:pos>34.7 -72.73</gml:pos>
  </gml:Point>
</gml:location>
```

EXAMPLE 2 (multi-station GetObservation):
```
<gml:location>
  <gml:MultiPoint srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
    <gml:pointMembers>
      <gml:Point>
        <gml:name>urn:ioos:station:wmo:41001</gml:name> 
        <gml:pos>34.7 -72.73</gml:pos>
      </gml:Point>
          <gml:Point>
        <gml:name>urn:ioos:station:wmo:41004</gml:name> 
        <gml:pos>32.5 -79.09</gml:pos>
      </gml:Point>
      <gml:Point>
        <gml:name>urn:ioos:station:wmo:41008</gml:name> 
        <gml:pos>31.4 -80.87</gml:pos>
      </gml:Point>
    </gml:pointMembers>
  </gml:MultiPoint>
</gml:location>
```

EXAMPLE 3 (single-station DescribeSensor):
```
<sml:location>
  <gml:Point srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
    <gml:name>urn:ioos:station:wmo:41001</gml:name> 
    <gml:pos>34.7 -72.73</gml:pos>
  </gml:Point>
</sml:location>
```

EXAMPLE 4 (“network-all” DescribeSensor):
```
<sml:location>
  <gml:boundedBy>
    <gml:Envelope srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
      <gml:lowerCorner>-90.0 -180.0</gml:lowerCorner>
      <gml:upperCorner>90.0 180.0</gml:upperCorner>
    </gml:Envelope>
  </gml:boundedBy>
</sml:location>
```


## Representation of platform/sensor vertical coordinate ##
Link: http://code.google.com/p/ioostech/issues/detail?id=16


The description of the sensor position in `GetObservation` response consists of 3 parts: (1) a 3D Compound CRS for use as a global Reference Frame; (2) description of the Local Frame for a platform; and (3) description of the sensor position relative to the platform Local Frame:

1. **3D Compound CRS**:
  * the GML definition of the 3D Compound CRS looks as follows:

```
<gml:CompoundCRS xmlns:gml="http://www.opengis.net/gml"
    xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.opengis.net/gml http://schemas.opengis.net/gml/3.1.1/base/gml.xsd" gml:id="IOOS_Buoy_CRS">
    <gml:srsName>3D Compound CRS 4326 2D geographic + vertical height referenced to instantaneous water level </gml:srsName>
    <gml:validArea>
        <gml:description> World wide for any floating sensor or platform </gml:description>
    </gml:validArea>
    <gml:includesCRS xlink:href="urn:ogc:def:crs:EPSG::4326" xlink:title="WGS 84 Geoid"/>
    <gml:includesCRS xlink:href="urn:ogc:def:crs:EPSG::5829" xlink:title=" Instantaneous Water Level height "/>
</gml:CompoundCRS> 
```

  * for floating, surface buoys, IOOS has specified a 3D CRS with EPSG::4326 (WGS84 Geoid) for the horizontal reference frame (latitude/longitude), and EPSG::5829 (Instantaneous water level uncorrected for tide with vertical axis upward direction) for the vertical reference;
  * for a tide gauge or a station at a fixed location relative to the Geoid (MSL), the 3D CRS should be EPSG::4979
  * if both horizontal and vertical CRSs are registered with the EPSG Register, the Compound CRS shall be resolved via single URI by the OGC CRS resolver; for example, the IOOS 3D Compound CRS defined above, shall use the following URI (the axes order shall be exact):

```
http://www.opengis.net/def/crs-compound?1=http://www.opengis.net/def/crs/EPSG/0/4326&2=http://www.opengis.net/def/crs/EPSG/0/5829
```

2. **Platform Local Frame** - the coordinate vector is specified that describes the station location in the 3D CRS Reference Frame:

```
      <om:result>
        <swe2:DataStream>
          <swe2:elementType name="components">
            <swe2:DataRecord>
[…]
              <swe2:field name="stationID">
                <swe2:Text definition="http://mmisw.org/ont/ioos/definition/stationID">
                  <swe2:value>urn:ioos:station:wmo:41001</swe2:value>
                </swe2:Text>
              </swe2:field>
              <swe2:field name="platformLocation">
                <swe2:Vector
                  definition="http://www.opengis.net/def/property/OGC/0/PlatformLocation"
                  referenceFrame=http://www.opengis.net/def/crs-compound?1=http://www.opengis.net/def/crs/EPSG/0/4326&2=http://www.opengis.net/def/crs/EPSG/0/5829
                  <!-- For a tide gauge the referenceFrame="http://www.opengis.net/def/crs/EPSG/0/4979" -->
                  localFrame="#PlatformFrame">
                  <swe2:coordinate name="latitude">
                    <swe2:Quantity definition="http://mmisw.org/ont/cf/parameter/latitude" axisID="Lat">
                      <swe2:uom code="deg"/>
                      <swe2:value>32.5</swe2:value>
                    </swe2:Quantity>
                  </swe2:coordinate>
                  <swe2:coordinate name="longitude">
                    <swe2:Quantity definition="http://mmisw.org/ont/cf/parameter/longitude" axisID="Lon">
                      <swe2:uom code="deg"/>
                      <swe2:value>-78.5</swe2:value>
                    </swe2:Quantity>
                  </swe2:coordinate>
                  <swe2:coordinate name="height">
                    <swe2:Quantity definition="http://mmisw.org/ont/cf/parameter/height" axisID="Z">
                      <swe2:uom code="m"/>
                      <swe2:value>0</swe2:value>
                    </swe2:Quantity>
                  </swe2:coordinate>
                </swe2:Vector>
              </swe2:field>
[…]
            </swe2:DataRecord>
          </swe2:elementType>
[…]
        </swe2:DataStream>
      </om:result>
```

3. **description of the sensor position** relative to the platform Local Frame specifying a height/depth:
  * sensor’s position should always be reported as height (vertical upward);
  * sensor’s position below the water surface should be reported as height with _**negative**_ value;
  * zero height is at water level in the 3D CRS

```
      <om:result>
        <swe2:DataStream>
          <swe2:elementType name="components">
            <swe2:DataRecord>
[…]
              <swe2:field name="sensorData">
                <swe2:DataChoice>
                  <swe2:item name="sensor1">
                    <swe2:DataRecord>
                      <swe2:field name="sensorID">
                        <swe2:Text definition="http://mmisw.org/ont/ioos/definition/sensorID">
                          <swe2:value>urn:ioos:station:wmo:41001:sensor1</swe2:value>
                        </swe2:Text>
                      </swe2:field>
                      <swe2:field name="height">
                        <swe2:Quantity definition="http://mmisw.org/ont/cf/parameter/height" referenceFrame="#PlatformFrame">
                          <swe2:uom code="m"/>
                          <swe2:value>5</swe2:value>
                        </swe2:Quantity>
                      </swe2:field>
[…]
                    </swe2:DataRecord>
                  </swe2:item>

                  <swe2:item name="sensor2">
                    <swe2:DataRecord>
                      <swe2:field name="sensorID">
                        <swe2:Text definition="http://mmisw.org/ont/ioos/definition/sensorID">
                          <swe2:value>urn:ioos:station:wmo:41001:sensor2</swe2:value>
                        </swe2:Text>
                      </swe2:field>
                      <swe2:field name="height">
                        <swe2:Quantity definition="http://mmisw.org/ont/cf/parameter/height" referenceFrame="#PlatformFrame">
                          <swe2:uom code="m"/>
                          <swe2:value>-5</swe2:value>
                        </swe2:Quantity>
                      </swe2:field>
                  </swe2:item>
[…]
                </swe2:DataChoice>                
              </swe2:field>
            </swe2:DataRecord>
          </swe2:elementType>
```


## Lower Camel Case Names ##
Link: http://code.google.com/p/ioostech/issues/detail?id=31

Names, titles, gml ids, and other attribute values in SOS XML documents meant as human readable labels should use lower camel case (ex. sensorLocation). An exception is made for labels containing the short version of an identifier or definition URI that contains underscores (e.g. air\_temperature, station\_12, etc). Another exception is made for network-all. This rule does not apply to identifier values and terms from established vocabularies (e.g. http://mmisw.org/ont/cf/parameter/air_temperature or urn:ioos:station:xoos:the\_station). Text containing acronyms should treat the acronym component as a normal word for readability (e.g. bprLocation instead of BPRLocation).


## Observation values TextEncoding separators ##
Link: http://code.google.com/p/ioostech/issues/detail?id=34

Use XML entities in GetObservation `<swe:TextEncoding>` to represent special characters. Use of standard CSV separators is strongly recommended:
```
<swe2:TextEncoding decimalSeparator="." tokenSeparator="," blockSeparator="&#10"/>
```

Use unencoded separators (e.g. actual line feeds) in the values block, example:
```
25.41,10.23,320
25.43,10.23,300
25.39,11.51,310
```

## WMO IDs ##
Link: http://code.google.com/p/ioostech/issues/detail?id=41

Station WMO IDs should be specified (when available) in the identifier section of a DescribeSensor response as follows:
```
<sml:identifier name="wmoID">
    <sml:Term definition="http://mmisw.org/ont/ioos/definition/wmoID">
        <sml:value>41001</sml:value>
    </sml:Term>
</sml:identifier>
```
The _wmoID_ should be specified as a separate identifier even if the main _stationID_ URN uses the WMO authority.

## Platform Vocabularies ##
Platform vocabulary development is continuing but is not yet ready for publication.  The 1.0 templates will be completed before the vocabulary is published.  In the interim, please use the location reproduced below in the DS template to publish the platform name.  You may choose your own vocabulary or wait until the official vocabulary is published (by end of March). The link to MMI is active, but does not yet contain the vocabulary.
```
 <sml:classifier name="platformType">
   <sml:Term definition="http://mmisw.org/ont/ioos/definition/platformType">
     <sml:codeSpace xlink:href="http://mmisw.org/ont/ioos/platform"/>
     <sml:value>buoy</sml:value>
   </sml:Term>
  </sml:classifier>
```


## Sponsorship ##
There has been a request by some of the RA Directors to have a metadata field that contains sponsorship of platforms.  Please insert all sponsoring parties (zero-many) in the DS field below:

```
<sml:classifier name="sponsor">
  <sml:Term definition="http://mmisw.org/ont/ioos/definition/sponsor">
    <sml:codeSpace xlink:href="http://mmisw.org/ont/ioos/organization"/>
    <sml:value>ACE</sml:value>
  </sml:Term>
</sml:classifier>
```

IOOS-supported platforms should be attributed with a sponsor entry that includes: `<sml:value>IOOS</sml:value>`  This way, the asset inventory can identify IOOS-sponsored platforms, and use this information.  In practice, there are probably few assets 100% supported by IOOS, so having IOOS as a sponsor can safely be interpreted as Partial IOOS support.


## The proper use of `<sml:validTime>` in `DescribeSensor` response ##

Link: http://code.google.com/p/ioostech/issues/detail?id=48

The `<sml:validTime>` shall not be used to represent the time range of observations for a procedure but only to specify a time period, in which this specific sensor description is valid. The validity period may be different for various sensors on the same platform (station) if any of them had limited functionality due to some incident. When such incident occurs, a new DescribeSensor document shall be created with a validity period going from the date of that incident to the date of the next one (or "now" if there were no more incidents), while the old document shall be archived with a validity period ending at the date of the incident.

To support discovery and search the time bounds of the data provided in an offering is encoded into the GetCapabilities response in the ObservationOffering element.  For example, from NDBC

```
<sos:ObservationOffering gml:id="station-23020">
<gml:description>Red Sea</gml:description>
<gml:name>urn:ioos:station:wmo:23020</gml:name>
<gml:srsName>http://www.opengis.net/def/crs/EPSG/0/4326</gml:srsName>
<gml:boundedBy>
   <gml:Envelope srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
      <gml:lowerCorner>22.161 38.501</gml:lowerCorner>
      <gml:upperCorner>22.161 38.501</gml:upperCorner>
   </gml:Envelope>
</gml:boundedBy>
<sos:time>
   <gml:TimePeriod>
      <gml:beginPosition>2009-05-14T14:50:00Z</gml:beginPosition>
      <gml:endPosition>2010-12-17T03:50:00Z</gml:endPosition>
   </gml:TimePeriod>
</sos:time>
<sos:procedure xlink:href="urn:ioos:station:wmo:23020"/>
<sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/waves"/>
<sos:featureOfInterest xlink:href="urn:cgi:Feature:CGI:EarthOcean"/>
<sos:responseFormat>text/xml;subtype="om/1.0.0"</sos:responseFormat>
<sos:responseFormat>text/csv</sos:responseFormat>
<sos:responseFormat>text/tab-separated-values</sos:responseFormat>
<sos:responseFormat>application/vnd.google-earth.kml+xml</sos:responseFormat>
<sos:responseFormat>text/xml;schema="ioos/0.6.1"</sos:responseFormat>
<sos:responseFormat>application/ioos+xml;version=0.6.1</sos:responseFormat>
<sos:resultModel>om:ObservationCollection</sos:resultModel>
<sos:responseMode>inline</sos:responseMode>
</sos:ObservationOffering>
```

## Specifying missing/out of range values in `GetObservation` ##

Link: http://code.google.com/p/ioostech/issues/detail?id=45

Although specifying the missing or out of range values is completely optional, it shall follow the SWECommon standard requirements. In general, a `<swe:quantity>` may contain any number of `<swe:nilValue>` elements for any nilValue reason:


```
<swe:Quantity>
  ...
  <swe:nilValues>
    <swe:NilValues>
      <swe:nilValue reason="http://www.opengis.net/def/nil/OGC/0/BelowDetectionRange">-9999</swe:nilValue>
      <swe:nilValue reason="http://www.opengis.net/def/nil/OGC/0/AboveDetectionRange">9999</swe:nilValue>
      <swe:nilValue reason="http://www.opengis.net/def/nil/OGC/0/OutOfService">-1</swe:nilValue>
      <swe:nilValue reason="http://www.opengis.net/def/nil/OGC/0/missing">8888</swe:nilValue>
      
    </swe:NilValues>
  </swe:nilValues>
  ...
</swe:Quantity>
```