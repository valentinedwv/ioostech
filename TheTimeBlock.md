# Introduction #

Inside of the CSV response block, we may need to return time information. SWE defined the `<swe:Time>` block for this purpose.

Should we use ["ISO 8601"](http://en.wikipedia.org/wiki/ISO_8601)?

_Emilio Comment: I strongly vote for the use of ISO 8601 all across the SOS service (in requests and all responses). We already use ISO 8601, it's widely used in general, it's human readable (as opposed to Option C), and if we stick to some conventions it's easily parsed. I don't know what are the implications of Options A vs B in terms of the `<swe:field>` package, but I assume in both cases the values can be full ISO 8601 date-time strings, like `2009-05-23T00:00:00Z`? One of the main arguments I see for Option C is consistency with the netCDF world._

Guidance:

  * All datetime values are specified as iso8601 strings in UTC.

## A ##
```
<swe:field name="time">
  <swe:Time definition="urn:ogc:def:property:OGC::SamplingTime">
    <gml:name>Sampling Time</gml:name>
    <swe:uom xlink:href="urn:ogc:def:unit:ISO:8601"/>
  </swe:Time>
</swe:field>
```

```
<swe:values>
  2009-05-23T00:00:00Z
  2009-05-23T01:00:00Z
  2009-05-23T02:00:00Z
</swe:values>
```

## B ##
```
<swe:field name="time">
  <swe:Time definition="http://www.opengis.net/def/property/OGC/0/SamplingTime">
    <swe:uom xlink:href="http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"/>
  </swe:Time>
</swe:field>
```

```
<swe:values>
  2009-05-23
  2009-05-24
  2009-05-25
</swe:values>
```

## C ##
```
<swe:field name="time">
  <swe:Time definiton="urn:ogc:def:property:OGC:SamplingTime" referenceTime="1970-01-01T00:00:00Z">
    <swe:uom code="seconds"/>
  </swe:Time>  
</swe:field>
```


```
<swe:values>
  1243036800
  1243040400
  1243044000
</swe:values>
```