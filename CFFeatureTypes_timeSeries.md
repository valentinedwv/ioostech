# timeSeries #



Data may be taken over periods of time at a set of discrete point, spatial locations called stations (see also discussion in CF 1.6 section 9.1).  The set of elements at a particular station is referred to as a timeSeries feature.

## CDL ##

### Single Station ###



### Multiple Stations ###

#### Incomplete-Multidimensional ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/timeSeries-Incomplete-MultiDimensional-MultipleStations-H.2.2)

#### Orthogonal-Multidimensional ####

["Sample Files"](https://github.com/asascience-open/CFPointConventions/tree/master/timeSeries-Orthogonal-Multidimenstional-MultipleStations-H.2.1)

## SWE ##

### Sample ###

Hmm.. I don't know where I got this from?  OGC Spec, NDBC, or a combination of both.

```
<DataArray>
  <elementCount>
    <Count gml:id="STATION_DIMENSION" definition="urn:ogc:def:data:OGC:ArrayDimension">
      <value>23</value>
    </Count>
  </elementCount>
  <elementType name="StationData">
    <DataRecord>
      <field name="location"> 
        <Vector definition="urn:ogc:def:data:LocationVector" referenceFrame="urn:ogc:def:crs:EPSG:6.7:4979">
          <coordinate name="lon">
            <Quantity definition="urn:ogc:def:property:OGC:Longitude" axisCode="X">
              <gml:description>Longitude of the observation</gml:description>
              <gml:name>Longitude</gml:name>
              <uom code="deg"/>
            </Quantity>
          </coordinate>
          <coordinate name="lat">
            <Quantity definition="urn:ogc:def:property:OGC:GeodeticLatitude" axisCode="Y">
              <gml:description>Geodetic latitude of the observation</gml:description>
              _<gml:name>Latitude</gml:name>_
              <uom code="deg"/>
            </Quantity>
          </coordinate>
          <coordinate name="alt">
            <Quantity definition="urn:ogc:def:property:OGC:AltitudeAboveMSL" axisCode="Z">
              <gml:description>Altitude of the observation above mean sea level</gml:description>
              <gml:name>Altitude above MSL</gml:name>
              <uom code="m"/>
            </Quantity>
          </coordinate>
        </Vector>
      </field>
      <field name="ObservationCount">
        <Count gml:id="OBS_DIMENSION" definition="urn:ogc:def:data:OGC:ArrayDimension"/>
      </field>
      <field name="ObservationArray">
        <DataArray>
          <elementCount ref="OBS_DIMENSION"/>
          <elementType>
            <DataRecord>
              <field name="time">
                <Time definiton="urn:ogc:def:property:OGC:SamplingTime" referenceTime="1970-01-01T00:00:00Z">
                  <uom code="d"/>
                </Time>  
              </field>             
              <field name="humidity">
                <Quantity definition="urn:ogc:def:property:OGC:SpecificHumidity">
                  <gml:name>Specific Humidity</gml:name>
                  <uom code="%"/>
                </Quantity>
              </field>
              <field name="temp">
                <Quantity definition="urn:ogc:def:property:OGC:AirTemperature">
                  <gml:name>Temperature</gml:name>
                  <uom code="Cel"/>
                </Quantity>
              </field>
            </DataRecord> 
          </elementType>
        </DataArray>
      </field>
    </DataRecord>
  </elementType>
</DataArray>
```

### Single Block ###

I came up with this, pulling in ideas from many different places and the SWE spec.

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
      <om:featureOfInterest xlink:href="TIMESERIES_COLLECTION"/>
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
            </swe:Vector>
          </swe:field>
          <swe:elementType name="message">
            <swe:DataChoice>
              <swe:item name="TimeSeries_1">
                <swe:DataRecord>
                  <swe:label>First TimeSeries (TimeSeries_1)</swe:label>
                  <swe:field name="temp">
                    <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
                      <swe:uom code="Cel"/>
                    </swe:Quantity>
                  </swe:field>
                </swe:DataRecord>
              </swe:item>
              <swe:item name="TimeSeries_2">
                <swe:DataRecord>
                  <swe:label>Second TimeSeries (TimeSeries_2)</swe:label>
                  <swe:field name="temp">
                    <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
                      <swe:uom code="Cel"/>
                    </swe:Quantity>
                  </swe:field>
                  <swe:field name="air_pressure">
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
            2009-05-23T00:00:00Z,30.5,-76.5,TimeSeries_1,15.4
            2009-05-23T00:00:00Z,32.5,-78.5,TimeSeries_2,16.6,1016.4
            2009-05-23T01:00:00Z,30.5,-76.5,TimeSeries_1,15.8
            2009-05-23T01:00:00Z,32.5,-78.5,TimeSeries_2,16.1,1018.3
            2009-05-23T02:00:00Z,30.5,-76.5,TimeSeries_1,15.4
            2009-05-23T02:00:00Z,32.5,-78.5,TimeSeries_2,16.2,1017.6
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```

### Multiple Block ###

I came up with this, pulling in ideas from many different places and the SWE spec.

Since we are giving each timeSeries location (i.e. a station) it's own data block, we can leave out the latitude and longitude in the CSV block. It is represented in the `<gml:boundedBy>` section inside of `<om:Observation>`. If the profile is moving, it is not a timeSeries! I have left them in there for reference.

```
<?xml version="1.0" encoding="UTF-8"?>
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <gml:description>TimeSeries 1</gml:description>
      <gml:name>TimeSeries_1</gml:name>
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
            </swe:Vector>
          </swe:field>
          <swe:field name="temp">
            <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_temperature">
              <swe:uom code="Cel"/>
            </swe:Quantity>
          </swe:field>
          <swe:field name="air_pressure">
            <swe:Quantity definition="http://mmisw.org/ont/cf/parameter/air_pressure">
              <swe:uom code="hPa"/>
            </swe:Quantity>
          </swe:field>
          <swe:encoding>
            <swe:TextEncoding blockSeparator="\n" tokenSeparator=","/>
          </swe:encoding>
          <swe:values>
            2009-05-23T00:00:00Z,32.5,-78.5,16.6,1016.4
            2009-05-23T01:00:00Z,32.5,-78.5,16.6,1016.2
            2009-05-23T02:00:00Z,32.5,-78.5,16.6,1016.1
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
  <om:member>
    <om:Observation>
      <gml:description>TimeSeries 2</gml:description>
      <gml:name>TimeSeries_2</gml:name>
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
            2009-05-23T00:00:00Z,30.5,-76.5,15.1
            2009-05-23T01:00:00Z,30.5,-76.5,15.3
            2009-05-23T02:00:00Z,30.5,-76.5,16.1
          </swe:values>
        </swe:DataStream>
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>

```