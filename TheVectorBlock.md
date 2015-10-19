# Introduction #

Inside of the CSV response block, we may need to return position information (x,y,z). SWE defined the `<swe:Vector>` block for this purpose.

```
<swe:field name="location">
  <swe:Vector definition="urn:ogc:def:data:LocationVector" referenceFrame="urn:ogc:def:crs:EPSG::4326">
    <swe:coordinate name="lon">
      <swe:Quantity definition="urn:ogc:def:property:OGC:GeodeticLongitude" axisCode="X" axisID="Long">
        <gml:description>Longitude of the observation</gml:description>
        <gml:name>Longitude</gml:name>
        <swe:uom code="deg"/>
      </swe:Quantity>
    </swe:coordinate>
    <swe:coordinate name="lat">
      <swe:Quantity definition="urn:ogc:def:property:OGC:GeodeticLatitude" axisCode="Y" axisID="Lat">
        <gml:description>Geodetic latitude of the observation</gml:description>
        <gml:name>Latitude</gml:name>
        <swe:uom code="deg"/>
      </swe:Quantity>
    </swe:coordinate>
    <swe:coordinate name="alt">
      <swe:Quantity definition="urn:ogc:def:property:OGC:AltitudeAboveMSL" axisCode="Z" axisId="Altitude">
        <gml:description>Altitude of the observation above mean sea level</gml:description>
        <gml:name>Altitude above MSL</gml:name>
        <swe:uom code="m"/>
      </swe:Quantity>
    </swe:coordinate>
  </swe:Vector>
</swe:field>
```

```
<swe:values>
  30.5,-76.5,1
  30.5,-76.5,2
  30.5,-76.5,3
  30.5,-76.5,4
  30.5,-76.5,5
  30.5,-76.5,6
  32.5,-74.5,1
  32.5,-74.5,2
  32.5,-74.5,3
  32.5,-74.5,4
  32.5,-74.5,5
  32.5,-74.5,6
</swe:values>
```