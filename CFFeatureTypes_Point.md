# point #



## CDL ##
```
dimensions:
	obs = 100 ;
variables:
	double lat(obs) ;
		lat:units = "degrees_north" ;
		lat:long_name = "latitude of the observation" ;
		lat:standard_name = "latitude" ;
	double lon(obs) ;
		lon:units = "degrees_east" ;
		lon:long_name = "longitude of the observation" ;
		lon:standard_name = "longitude" ;
	double alt(obs) ;
		alt:units = "m" ;
		alt:positive = "up" ;
		alt:axis = "Z" ;
		alt:standard_name = "height" ;
	int time(obs) ;
		time:long_name = "time" ;
		time:standard_name = "time" ;
		time:units = "seconds since 1990-01-01 00:00:00" ;
	double temperature(obs) ;
		temperature:long_name = "Water Temperature" ;
		temperature:standard_name = "sea_water_temperature" ;
		temperature:units = "Celsius" ;
		temperature:coordinates = "time lat lon alt" ;
	double humidity(obs) ;
		humidity:long_name = "Humidity" ;
		humidity:standard_name = "specific_humidity" ;
		humidity:units = "Percent" ;
		humidity:coordinates = "time lat lon alt" ;

	// global attributes:
		:CF\:featureType = "point" ;
```



## SWE ##

```
<DataStream>
  <elementCount>
    <Count definition="urn:def:ogc:data:OGC:ArrayDimension" axisCode="obs">
      <value>1234</value>
    </Count>
  <elementCount>
  <elementType name="station_data">
    <DataRecord>
      <field name="time">
        <Time definiton="urn:ogc:def:property:OGC:SamplingTime" referenceTime="1970-01-01T00:00:00Z">
          <uom code="d"/>
        </Time>  
      </field>
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
              <gml:name>Latitude</gml:name>
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
</DataStream>
```