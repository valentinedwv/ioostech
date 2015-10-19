# timeSeriesProfile #



A series of connected observations along a vertical line, like an atmospheric or ocean sounding, is called a profile. For each profile, there is a single time, lat and lon. There are data values for X parameters and Y depths.

When profiles are taken repeatedly at a station, one gets a time series of profiles (see also section H.2 in the CF 1.6 specification for discussion of stations and time series). The resulting collection of profiles is called a timeSeriesProfile.

The SWE encoding will need to support single and multiple profiles per request. Each profile may measure at different depths, times, and locations, and also measure different variables. This makes using a flat CSV output very inefficient.

We need to think about how a user would want to see the data presented to them. It may be better to seperate each PROFILE in the output as its own om:Observation block rather than combining them. We could also use the DataChoice element to designate which profile belongs to which row, and each Profile will get its own description block (see below).

I present two options in the SWE section. One with different Observation blocks for each timeSeriesProfile, and one in which Profiles are combined into one Observation block using the DataChoice element.

## CDL ##

### Single Station ###

#### Multidimensional (SS) ####

["Multidimensional (SS)"](https://github.com/asascience-open/CFPointConventions/blob/master/timeSeriesProfile-Multidimensional-SingleStation-H.5.2)

#### Ragged (SS) ####

["Ragged (SS)"](https://github.com/asascience-open/CFPointConventions/tree/master/timeSeriesProfile-Ragged-SingleStation-H.5.3)

### Multiple Station ###

#### Multidimensional (MS) ####

["Multidimensional (MS)"](https://github.com/asascience-open/CFPointConventions/tree/master/timeSeriesProfile-Orthogonal-Multidimensional-MultipeStations-H.5.1)

#### Ragged (MS) ####

["Ragged (MS)"](https://github.com/asascience-open/CFPointConventions/tree/master/timeSeriesProfile-Ragged-MultipeStations-H.5.3)


## SWE ##

### Single Block ###

I came up with this, pulling in ideas from many different places and the SWE spec.

The `<gml:boundedBy>` element contains all of the locations of the profiles included in the output.

The `<om:samplingTime>` includes the time range of all profiles.

```
<?xml version="1.0" encoding="UTF-8"?>
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <gml:description>Empty Description</gml:description>
      <gml:name>Empty Description</gml:name>
      <gml:boundedBy>
        <gml:Envelope srsName="urn:tds:station.sos:ID_1">
          <gml:lowerCorner>-78.5 30.5 0</gml:lowerCorner>
          <gml:upperCorner>-76.5 32.5 0</gml:upperCorner>
        </gml:Envelope>
      </gml:boundedBy>
      <om:samplingTime>
        <gml:TimePeriod gml:id="DATA_TIME">
          <gml:beginPosition>2009-05-23T00:00:00Z</gml:beginPosition>
          <gml:endPosition>2009-05-23T02:00:00Z</gml:endPosition>
        </gml:TimePeriod>
      </om:samplingTime>
      <om:procedure xlink:href="FILE OR DATASET LOCATION"/>
      <om:observedProperty xlink:href="http://marinemetadata.org/cf#temperature"/>
      <om:featureOfInterest xlink:href="PROFILE_COLLECTION"/>
      <om:result>
        <swe:DataStream>
          <swe:field name="time">
            <swe:Time definition="http://www.opengis.net/def/property/OGC/0/SamplingTime">
              <swe:uom xlink:href="http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"/>
            </swe:Time>
          </swe:field>
          <swe:field name="location">
            <swe:Vector definition="http://www.opengis.net/def/property/OGC/0/PlatformLocation" referenceFrame="http://www.opengis.net/def/crs/EPSG/0/4979">
              <swe:coordinate name="lat">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Latitude" axisID="Lat">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="lon">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Longitude" axisID="Long">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="alt">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceExtent.owl#Altitude" axisID="h">
                  <swe:uom code="m"/>
                </swe:Quantity>
              </swe:coordinate>
            </swe:Vector>
          </swe:field>
          <swe:elementType name="message">
            <swe:DataChoice>
              <swe:item name="PROFILE_1">
                <swe:DataRecord>
                  <swe:label>First Profile (PROFILE_1)</swe:label>
                  <swe:field name="temp">
                    <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
                      <swe:uom code="Cel"/>
                    </swe:Quantity>
                  </swe:field>
                </swe:DataRecord>
              </swe:item>
              <swe:item name="PROFILE_2">
                <swe:DataRecord>
                  <swe:label>Second Profile (PROFILE_2)</swe:label>
                  <swe:field name="temp">
                    <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
                      <swe:uom code="Cel"/>
                    </swe:Quantity>
                  </swe:field>
                  <swe:field name="salinity">
                    <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_pressure">
                      <swe:uom code="hPa"/>
                    </swe:Quantity>
                  </swe:field>
                </swe:DataRecord>
              </swe:item>
            </swe:DataChoice>
          </swe:elementType>
          <swe:encoding>
            <swe:TextEncoding blockSeparator="\n" tokenSeparator=","/>
          </swe:encoding>
          <swe:values>
            2009-05-23T00:00:00Z,30.5,-76.5,5,PROFILE_1,15.4
            2009-05-23T00:00:00Z,32.5,-78.5,5,PROFILE_2,16.6,1016.4
            2009-05-23T01:00:00Z,30.5,-76.5,5,PROFILE_1,15.8
            2009-05-23T01:00:00Z,32.5,-78.5,5,PROFILE_2,16.1,1018.3
            2009-05-23T02:00:00Z,30.5,-76.5,5,PROFILE_1,15.4
            2009-05-23T02:00:00Z,32.5,-78.5,5,PROFILE_2,16.2,1017.6
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```

### Multiple Blocks ###

I came up with this, pulling in ideas from many different places and the SWE spec.

Since we are giving each profile location (i.e. a station) it's own data block, we can leave out the latitude and longitude in the CSV block.  It is represented in the `<gml:boundedBy>` section inside of `<om:Observation>`.  If the profile is moving, it is not a timeSeriesProfile!  I have left them in there for reference.

The `<gml:boundedBy>` element contains the actual location of each profile.

The `<om:samplingTime>` includes the time range of a single profile.

```
<?xml version="1.0" encoding="UTF-8"?>
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <gml:description>Profile 1</gml:description>
      <gml:name>PROFILE_1</gml:name>
      <gml:boundedBy>
        <gml:Envelope srsName="urn:tds:station.sos:ID_1">
          <gml:lowerCorner>-78.5 32.5 0</gml:lowerCorner>
          <gml:upperCorner>-78.5 32.5 0</gml:upperCorner>
        </gml:Envelope>
      </gml:boundedBy>
      <om:samplingTime>
        <gml:TimePeriod>
          <gml:beginPosition>2009-05-23T00:00:00Z</gml:beginPosition>
          <gml:endPosition>2009-05-23T02:00:00Z</gml:endPosition>
        </gml:TimePeriod>
      </om:samplingTime>
      <om:procedure xlink:href="FILE OR DATASET LOCATION"/>
      <om:observedProperty xlink:href="http://marinemetadata.org/cf#temperature"/>
      <om:featureOfInterest xlink:href="ID_1"/>
      <om:result>
        <swe:DataStream>
          <swe:field name="time">
            <swe:Time definition="http://www.opengis.net/def/property/OGC/0/SamplingTime">
              <swe:uom xlink:href="http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"/>
            </swe:Time>
          </swe:field>
          <swe:field name="location">
            <swe:Vector definition="http://www.opengis.net/def/property/OGC/0/PlatformLocation" referenceFrame="http://www.opengis.net/def/crs/EPSG/0/4979">
              <swe:coordinate name="lat">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Latitude" axisID="Lat">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="lon">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Longitude" axisID="Long">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="alt">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceExtent.owl#Altitude" axisID="h">
                  <swe:uom code="m"/>
                </swe:Quantity>
              </swe:coordinate>
            </swe:Vector>
          </swe:field>
          <swe:field name="temp">
            <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
              <swe:uom code="Cel"/>
            </swe:Quantity>
          </swe:field>
          <swe:field name="salinity">
            <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_pressure">
              <swe:uom code="hPa"/>
            </swe:Quantity>
          </swe:field>
          <swe:encoding>
            <swe:TextEncoding blockSeparator="\n" tokenSeparator=","/>
          </swe:encoding>
          <swe:values>
            2009-05-23T00:00:00Z,32.5,-78.5,1,16.6,1016.4
            2009-05-23T00:00:00Z,32.5,-78.5,2,16.1,1018.3
            2009-05-23T00:00:00Z,32.5,-78.5,3,16.2,1017.6
            2009-05-23T01:00:00Z,32.5,-78.5,1,16.6,1016.2
            2009-05-23T01:00:00Z,32.5,-78.5,2,16.1,1018.3
            2009-05-23T01:00:00Z,32.5,-78.5,3,16.2,1017.9
            2009-05-23T02:00:00Z,32.5,-78.5,1,16.6,1016.1
            2009-05-23T02:00:00Z,32.5,-78.5,2,16.1,1018.2
            2009-05-23T02:00:00Z,32.5,-78.5,3,16.2,1017.5
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
  <om:member>
    <om:Observation>
      <gml:description>Profile 2</gml:description>
      <gml:name>PROFILE_2</gml:name>
      <gml:boundedBy>
        <gml:Envelope srsName="urn:tds:station.sos:ID_2">
          <gml:lowerCorner>-76.5 30.5 0</gml:lowerCorner>
          <gml:upperCorner>-76.5 30.5 0</gml:upperCorner>
        </gml:Envelope>
      </gml:boundedBy>
      <om:samplingTime>
        <gml:TimePeriod>
          <gml:beginPosition>2009-05-23T00:00:00Z</gml:beginPosition>
          <gml:endPosition>2009-05-23T02:00:00Z</gml:endPosition>
        </gml:TimePeriod>
      </om:samplingTime>
      <om:procedure xlink:href="FILE OR DATASET LOCATION"/>
      <om:observedProperty xlink:href="http://marinemetadata.org/cf#temperature"/>
      <om:featureOfInterest xlink:href="ID_2"/>
      <om:result>
        <swe:DataStream>
          <swe:field name="time">
            <swe:Time definition="http://www.opengis.net/def/property/OGC/0/SamplingTime">
              <swe:uom xlink:href="http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"/>
            </swe:Time>
          </swe:field>
          <swe:field name="location">
            <swe:Vector definition="http://www.opengis.net/def/property/OGC/0/PlatformLocation" referenceFrame="http://www.opengis.net/def/crs/EPSG/0/4979">
              <swe:coordinate name="lat">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Latitude" axisID="Lat">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="lon">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceCoordinates.owl#Longitude" axisID="Long">
                  <swe:uom code="deg"/>
                </swe:Quantity>
              </swe:coordinate>
              <swe:coordinate name="alt">
                <swe:Quantity definition="http://sweet.jpl.nasa.gov/2.0/spaceExtent.owl#Altitude" axisID="h">
                  <swe:uom code="m"/>
                </swe:Quantity>
              </swe:coordinate>
            </swe:Vector>
          </swe:field>
          <swe:field name="temp">
            <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
              <swe:uom code="Cel"/>
            </swe:Quantity>
          </swe:field>
          <swe:encoding>
            <swe:TextEncoding blockSeparator="\n" tokenSeparator=","/>
          </swe:encoding>
          <swe:values>
            2009-05-23T00:00:00Z,30.5,-76.5,1,15.1
            2009-05-23T00:00:00Z,30.5,-76.5,2,17.1
            2009-05-23T00:00:00Z,30.5,-76.5,3,12.4
            2009-05-23T01:00:00Z,30.5,-76.5,1,15.3
            2009-05-23T01:00:00Z,30.5,-76.5,2,15.9
            2009-05-23T01:00:00Z,30.5,-76.5,3,14.5
            2009-05-23T02:00:00Z,30.5,-76.5,1,16.1
            2009-05-23T02:00:00Z,30.5,-76.5,2,15.2
            2009-05-23T02:00:00Z,30.5,-76.5,3,15.4
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```