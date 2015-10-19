# Profile #



A series of connected observations along a vertical line, like an atmospheric or ocean sounding, is called a profile. For each profile, there is a single time, lat and lon.  There are data values for X parameters and Y depths.

The SWE encoding will need to support single and multiple profiles per request.  Each profile may measure at different depths, times, and locations, and also measure different variables.  This makes using a flat CSV output very inefficient.

We need to think about how a user would want to see the data presented to them.  It may be better to seperate each PROFILE in the output as its own om:Observation block rather than combining them.  We could also use the DataChoice element to designate which profile belongs to which row, and each Profile will get its own description block (see below).

I present two options in the SWE section.  One with different Observation blocks for each Profile, and one in which Profiles are combined into one Observation block using the DataChoice element.

## CDL ##

There are **four** ways to represent profile data in NetCDF files using the CF 1.6 convention.  These should all be mapped to a common SWE encoding.

### Multidimensional ###

#### Orthogonal ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/profile-Orthogonal-MultiDimensional-MultipleProfiles-H.3.1)

#### Incomplete ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/profile-Incomplete-MultiDimensional-MultipleProfiles-H.3.2)

### Ragged ###

#### Indexed ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/profile-Indexed-Ragged-MultipleProfiles-H.3.5)

#### Contiguous ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/profile-Contiguous-Ragged-MultipleProfiles-H.3.4)


## SWE ##

There are basic examples.  The request that was made was for TWO profiles and TWO variables (temperature and salinity).

### Multiple Blocks ###
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
          <gml:endPosition>2009-05-23T00:00:00Z</gml:endPosition>
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
          <gml:endPosition>2009-05-23T00:00:00Z</gml:endPosition>
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
            2009-05-23T00:00:00Z,30.5,-76.5,1,15.4
            2009-05-23T01:00:00Z,30.5,-76.5,2,15.8
            2009-05-23T02:00:00Z,30.5,-76.5,3,15.4
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```

### Single Block ###

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
          <gml:endPosition>2009-05-23T00:00:00Z</gml:endPosition>
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
            2009-05-23T00:00:00Z,30.5,-76.5,1,PROFILE_1,15.4
            2009-05-23T00:00:00Z,32.5,-78.5,1,PROFILE_2,16.6,1016.4
            2009-05-23T00:00:00Z,30.5,-76.5,2,PROFILE_1,15.8
            2009-05-23T00:00:00Z,32.5,-78.5,2,PROFILE_2,16.1,1018.3
            2009-05-23T00:00:00Z,30.5,-76.5,3,PROFILE_1,15.4
            2009-05-23T00:00:00Z,32.5,-78.5,3,PROFILE_2,16.2,1017.6
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```


Alternatively see section 9.2.6 in the [SWE 2.0 specification](http://portal.opengeospatial.org/files/?artifact_id=41157)