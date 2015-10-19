# TimeEncodings #

## Inside GetObservation ##

### Inside Observation ###
```
<om:samplingTime>
  <gml:TimePeriod gml:id="DATA_TIME">
    <gml:beginPosition>2009-05-23T00:00:00Z</gml:beginPosition>
    <gml:endPosition>2009-05-23T02:00:00Z</gml:endPosition>
  </gml:TimePeriod>
</om:samplingTime>
```
### Inside DataRecord ###

```
<swe:field name="time">
  <swe:Time definition="http://www.opengis.net/def/property/OGC/0/SamplingTime">
    <swe:uom xlink:href="http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"/>
  </swe:Time>
</swe:field>
```


```
<swe:field name="time">
  <swe:Time definiton="urn:ogc:def:property:OGC:SamplingTime" referenceTime="1970-01-01T00:00:00Z">
    <swe:uom code="d"/>
  </swe:Time>  
</swe:field>
```