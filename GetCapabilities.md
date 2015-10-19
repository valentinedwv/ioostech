

# Introduction #

GetCapabilities provides summary information about the service and about the platforms for which it provides data.

  * Go over guidelines, rules, and minimum requirements needed for ows:ServiceIdentification, ows:ServiceProvider, ows:OperationsMetadata, and sos:Contents
  * patterns and guides for title, keywords, and maybe abstract

# Request #

Issuing the request: bla bla bla

Example request: http://sdf.ndbc.noaa.gov/sos/server.php?request=GetCapabilities&service=SOS

**FROM OOSTETHYS GET DOCUMENT:**

The parameters rules for the GetCapabilities operation are taken from table 3 and table 5 of [OGC 06-121r3](http://portal.opengeospatial.org/files/?artifact_id=20040)

Example: http://host[:port]/path?request=GetCapabilities&service=SOS&version=1.0.0

| **Parameter Name** | **Definition** | **Data type and Values** | **Multiplicity and Use of the Parameter** |
|:-------------------|:---------------|:-------------------------|:------------------------------------------|
| request            | Operation name | GetCapabilities          | One (mandatory)                           |
| service            | Service type identifier | SOS                      | One (mandatory)                           |
| _**AcceptFormats**_ | Comma-separated prioritized sequence of zero or more response formats desired by client, with preferred formats listed first | text/xml                 | One (mandatory). When omitted or not supported by server, return service metadata document using MIME type "text/xml" .|
| _**AcceptVersions**_ | Prioritized sequence of one more specification versions accepted by client, with preferred versions listed first | 1.0.0 has format X.Y.Z   | Zero or more (optional).                  |
| **Sections**       | Select GetCap section to return | GetCapabilities          | optional?                                 |

  * **Recommendation:** Request should implement **'Sections'** parameter, for easier and lighter metadata parsing, like this: http://host[:port]/path?request=GetCapabilities&service=SOS&version=1.0.0&sections=OperationsMetadata .  Here's a NANOOS example: http://habu.apl.washington.edu/pyws/sos.py?service=SOS&request=GetCapabilities&sections=OperationsMetadata
  * https://wiki.52north.org/bin/view/Sensornet/GetCapabilities

# Response #

The GetCapabilities response is an XML document with four sections:
  * [ServiceIdentification](#ServiceIdentification_Section.md) provides a brief summary description of the service and the type of data it offers.
  * [ServiceProvider](#ServiceProvider_Section.md) provides information about the operator of the service.
  * [OperationsMetadata](#OperationsMetadata_Section.md) provides detail URL endpoints and allowed parameters for each operation.
  * [Contents](#Contents_Section.md) provides a detailed listing of the observations offered by the SOS.

Sample GetCapabilities responses:
  * [NDBC Operational SOS](http://code.google.com/p/ioostech/downloads/detail?name=ndbc_sos_GetCap.xml)
  * [NOS/COOPS Operational SOS](http://code.google.com/p/ioostech/downloads/detail?name=noscoops_sos_GetCap.xml)

## ServiceIdentification Section ##

```
<ows:ServiceIdentification>
  <ows:Title>NANOOS Sensor Observation Service (SOS)</ows:Title>
  <ows:Abstract>Sensor Observation Service (SOS) Server for NANOOS, blah-blah.</ows:Abstract>
  <ows:Keywords>
    <ows:Keyword>NANOOS</ows:Keyword>
    <ows:Keyword>Air Temperature</ows:Keyword>
    <ows:Keyword>Chlorophyll</ows:Keyword>
    <ows:Keyword>Salinity</ows:Keyword>
    <ows:Keyword>Water Temperature</ows:Keyword>
    <ows:Keyword>Pacific Northwest</ows:Keyword>
    <ows:Keyword>Oregon</ows:Keyword>
  </ows:Keywords>
  <ows:ServiceType codeSpace="http://opengeospatial.net">OGC:SOS</ows:ServiceType>
  <ows:ServiceTypeVersion>1.0.0</ows:ServiceTypeVersion>
  <ows:Fees>NONE</ows:Fees> 
  <ows:AccessConstraints>NONE</ows:AccessConstraints>
</ows:ServiceIdentification>
```

## ServiceProvider Section ##

```
<ows:ServiceProvider>
  <ows:ProviderName>NANOOS - Northwest Association of Networked Ocean Observing Systems</ows:ProviderName>
  <ows:ProviderSite xlink:href="http://www.nanoos.org"/>
  <ows:ServiceContact>
    <ows:IndividualName>Emilio Mayorga</ows:IndividualName>
    <ows:ContactInfo>
      <ows:Phone>
        <ows:Voice>206-543-6431</ows:Voice>
      </ows:Phone>
      <ows:Address>
        <ows:DeliveryPoint></ows:DeliveryPoint>
        <ows:City>Seattle</ows:City>
        <ows:AdministrativeArea>WA</ows:AdministrativeArea>
        <ows:PostalCode>98195</ows:PostalCode>
        <ows:Country>USA</ows:Country>
        <ows:ElectronicMailAddress>mayorga@apl.washington.edu</ows:ElectronicMailAddress>
      </ows:Address>
    </ows:ContactInfo>
  </ows:ServiceContact>
</ows:ServiceProvider>
```

## OperationsMetadata Section ##

  * ows:OperationsMetadata/ows:Operation@[name=GetObservation]
    * What should be listed under ows:Parameter@[name=offering]/ows:AllowedValues ?
      * Each and every offering actually available, including both asset/platform and network offerings?
      * Full urn's, unqualified (naked) values, or both? My recommendation: Only full urn's?
      * But in sos:Contents/sos:ObservationOfferingList, sos:ObservationOffering@[gml:id] is specified as the naked unqualified station value, not full urn! eg: gml:id="station-ORCA\_Hansville"
    * What should be listed under ows:Parameter@[name=observedProperty]/ows:AllowedValues ? Full urn's, unqualified (naked) values, or both? My reccommendation: Only full urn's
  * ows:OperationsMetadata/ows:Operation@[name=DescribeSensor]
    * What should be listed under ows:Parameter@[name=procedure]/ows:AllowedValues? Do 'network' procedures complicate this? Full urn's, unqualified (naked) values, or both? My recommendation: Only full urn's?
  * ows:Parameter@[name=service] and ows:Parameter@[name=version]. Currently NDBC and NOS are placing them in different elements. Which one is correct?

## Contents Section ##

The Contents section of Capabilities XML is a list of one or more observation offerings; each offering corresponds to a single platform or a network of platforms. The following information is provided for each offering:

### Example response for an offering (from NANOOS) ###
```
<sos:ObservationOffering gml:id="station-APL_NPB2Carr">
  <gml:description>LSG NPB-2 Profiling Buoy at Carr Inlet. APL-UW Buoy asset (NANOOS: APL_NPB2Carr)</gml:description>
  <gml:name>urn:ioos:station:nanoos:APL_NPB2Carr</gml:name>
  <gml:srsName>urn:ogc:def:crs:epsg::4326</gml:srsName>
  <gml:boundedBy>
    <gml:Envelope srsName="urn:ogc:def:crs:epsg::4326">
      <gml:lowerCorner>47.2800 -122.7300</gml:lowerCorner>
      <gml:upperCorner>47.2800 -122.7300</gml:upperCorner>
    </gml:Envelope>
  </gml:boundedBy>
  <sos:time>
    <gml:TimePeriod> 
        <gml:beginPosition>2012-01-08T05:20:51Z</gml:beginPosition>
        <gml:endPosition indeterminatePosition="now"/>
    </gml:TimePeriod>
  </sos:time>
  <sos:procedure xlink:href="urn:ioos:station:nanoos:APL_NPB2Carr"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/wind_speed"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/wind_speed_of_gust"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/wind_from_direction"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/surface_air_pressure"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/air_temperature"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/sea_water_salinity"/>
  <sos:observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/sea_water_temperature"/>
  <sos:featureOfInterest xlink:href="urn:cgi:Feature:CGI:EarthOcean"/>
  <sos:responseFormat>text/csv</sos:responseFormat>
  <sos:responseFormat>text/plain</sos:responseFormat>
  <sos:responseFormat>application/xml</sos:responseFormat>
  <sos:resultModel>om:Observation</sos:resultModel>
  <sos:responseMode>inline</sos:responseMode>
</sos:ObservationOffering>
```

### Offering (platform) general description ###

#### gml:id ####
_Role:_ Brief attribute which is required by the XML schema rules but is not the official platform identifier.<br>
<i>Content:</i> IOOS convention has been to use gml:id values starting with 'station-' for individual platforms and 'network-' for networks of platforms, with additional characters derived from the actual IOOS identifier (see gml:name).<br>
<i>Example:</i> station-21401.<br>
<i>Note:</i> XML rules permit a gml:id to be random string of letters and characters as long as it is unique within the file. Do not rely on the gml:id value remaining constant for a given offering.<br>
<br>
<h4>gml:name</h4>
<i>Role:</i> The official IOOS identifier for the platform or network.<br>
<i>Content:</i> A Uniform Resource Name (URN) that obeys the IOOS URN convention described at <a href='Fill.md'>in URL</a>.<br>
<i>Example:</i> urn:ioos:station:wmo:21401.<br>
<i>Note:</i> gml:name is now redundant with procedure. There has been discussion of using gml:name for the station name information now found in gml:description.<br>
<br>
<h4>gml:description</h4>
<i>Role:</i> The name of the station assigned by the data provider. This is sometimes more descriptive than the IOOS identifier.<br>
<i>Content:</i> A human-readable string at the discretion of the provider.<br>
<i>Example:</i> 250NM Southeast of Iturup Island.<br>
<i>Note:</i> If the Name information is moved to gml:name (see above), this field could be either eliminated or used for additional description of the platform type.<br>
<br>
<h3>Spatial Information</h3>

<h4>gml:boundedBy</h4>
<i>Role:</i> The location or bounding box of the platform or network.<br>
Content: A gml:Envelope providing coordinate values and a spatial reference system (SRS) identifier (see srsName). IOOS uses latitude/longitude coordinates in decimal degrees. The coordinates are given as a lower corner (southwest) and an upper corner (northeast). For fixed platforms, both values are the same. For moored buoys with a nominal location and watch radius, the nominal location is provided. For moving sensors, the overall bounding box of the trajectory is provided. For a network of sensors, the overall bounds of the network are provided.<br>
<i>Example:</i>
<pre><code>&lt;gml:boundedBy&gt;<br>
  &lt;gml:Envelope srsName="urn:ogc:def:crs:epsg::4326"&gt;<br>
    &lt;gml:lowerCorner&gt;42.617 152.583&lt;/gml:lowerCorner&gt;<br>
    &lt;gml:upperCorner&gt;42.617 152.583&lt;/gml:upperCorner&gt;<br>
  &lt;/gml:Envelope&gt;<br>
&lt;/gml:boundedBy&gt;<br>
</code></pre>

<h4>srsName</h4>
<i>Role:</i> States the spatial reference system (a.k.a. coordinate reference system) used by geographic locations.<br>
<i>Content:</i> A URN defined by OGC based on the European Petroleum Survey Group (EPSG) database of coordinate reference systems. IOOS uses decimal latitude/longitude in the World Geodetic System 1984 (WGS84), as identified by the value in the example.<br>
<i>Example:</i> urn:ogc:def:crs:epsg::4326<br>
<i>Note:</i> srsName appears redundantly in two places: inside gml:boundedBy (as an attribute of the gml:Envelope) and as a separate gml:srsName. If may be permitted to eliminate gml:srsName -- some investigation is required.<br>
<br>
<h3>Temporal Information</h3>

<h4>time</h4>
<i>Role:</i> States the time period for which data are available from this offering.<br>
<i>Content:</i> a gml:TimePeriod providing a beginPosition and an endPosition. Time values are always Universal Time in ISO 8601 format (yyyy-mm-ddThh:mm:ssZ). If the offering remains in operation, then the end time has not yet been defined so the value indeterminatePosition="now" is specified.<br>
<i>Example:</i>
<pre><code>&lt;time&gt;<br>
  &lt;gml:TimePeriod&gt;<br>
    &lt;gml:beginPosition&gt;2010-11-15T18:15:00Z&lt;/gml:beginPosition&gt;<br>
    &lt;gml:endPosition indeterminatePosition="now"/&gt;<br>
  &lt;/gml:TimePeriod&gt;<br>
&lt;/time&gt;<br>
</code></pre>
<i>Note:</i> The overall start and end times do not indicate whether data gaps exist. If an offering comprises multiple sensors, each with different start or end times (for example, a new sensor was added at a later date), the start and end times indicate the overall period during which at least some data are available.<br>
<br>
<h3>Other Information</h3>

<h4>procedure</h4>
<i>Role:</i> The official IOOS identifier for the platform or network. The value of this identifier can be used in DescribeSensor requests for additional metadata and in GetObservation requests for actual data.<br>
Content: A Uniform Resource Name (URN) that obeys the IOOS URN convention described at <a href='Fill.md'>in URL</a>.<br>
<i>Example:</i> urn:ioos:station:wmo:21401.<br>
<i>Note:</i> Previously, IOOS used multiple procedures per offering (one per sensor); SOS 2.0 allows only one procedure, which is now redundant with gml:name. There has been discussion of using gml:name for the station name information now found in gml:description.<br>
<br>
<h4>observedProperty (1 or more)</h4>
<i>Role:</i> A list of one or more quantities observed by this offering. The observedProperty identifier is used in GetObservation requests to obtain actual data.<br>
<i>Content:</i> A URL from the Marine Metadata Interoperability (MMI) project corresponding to a Climate and Forecast (CF) Standard Name.<br>
<i>Example:</i> <a href='http://mmisw.org/ont/cf/parameter/sea_floor_depth_below_sea_surface'>http://mmisw.org/ont/cf/parameter/sea_floor_depth_below_sea_surface</a>

<h1>Other Issues</h1>
<h3>Multiple Observed Properties and Compound Phenomena</h3>
Conventions for creating and referencing compound phenomena.<br>
<br>
Links to resources: <a href='http://www.w3.org/2005/Incubator/ssn/wiki/images/4/46/O%26M_Property_Dictionary.pdf'>http://www.w3.org/2005/Incubator/ssn/wiki/images/4/46/O%26M_Property_Dictionary.pdf</a>

Links to discussions on this wiki: