# Introduction #


One thing the group has been trying to figure out (Shane, you probably missed this discussion) is a good way to distinguish in the GetObservation responses which Featuretype is actually being returned.  As far as I can tell, we will need 6 different outputs.

  * PointCollection - although seldom used
  * ProfileCollection -although seldom used
  * TimeSeriesCollection
  * TimeSeriesProfileCollection
  * TrajectoryCollection
  * TrajectoryProfileCollection

But how should we represent that?  I didn't include it in my SWE examples, because frankly I wasn't happy enough with any of the options.

Since the contents of the `<om:Observation>` block will be different depending on the type, we need to include it there (at the top level) and can't just include it in the `<om:result>` section (the meat).

Crosswalk between the various vocabularies used to describe these feature types.  These are just approximate matches.

| CSML[(1)](#Footnotes.md) | Climate and Forecast[(2)](#Footnotes.md) | Unidata CDM [(3)](#Footnotes.md) | THREDDS [(4)](#Footnotes.md) |
|:-------------------------|:-----------------------------------------|:---------------------------------|:-----------------------------|
| Point                    | point                                    | Point                            |                              |
| PointSeries              | timeSeries                               |Station time series               | Station                      |
| Trajectory               | trajectory                               | Trajectory                       | Trajectory                   |
| Profile                  | profile                                  | Profile                          |                              |
| ScanningRadar            |                                          |Radial                            | Swath ???                    |
| Swath                    | Grid                                     | Grid                             | Swath                        |
| Grid                     | Grid                                     | Grid                             | Grid                         |
| ProfileSeries            | timeSeriesProfile                        | Station Profile                  |                              |
| Section                  | trajectoryProfile                        | Section                          |                              |
| GridSeries               |                                          | Grid                             | Grid                         |
|                          |                                          |                                  | Image ???                    |
|                          |                                          |                                  |                              |


**[Unidata CDM Definitions](http://www.unidata.ucar.edu/software/netcdf-java/reference/FeatureDatasets/PointFeatures.html)**
  1. **Point feature**: one or more parameters measured at one point in time and space.
  1. **Station time series feature**: a time-series of data points all at the same location, with varying time.
  1. **Profile feature**: a set of data points along a vertical line.
  1. **Station Profile feature**: a time-series of profile features at a named location.
  1. **Trajectory feature**: a set of data points along a 1D curve in time and space.
  1. **Section feature**: a collection of profile features which originate along a trajectory.



# Options #


## A ##

In the `<gml:description>` tag.  So simple.  This field should probably be better used for other metadata... but this is so easy!

```
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <gml:description>TimeSeriesProfileCollection</gml:description>
      ...
      <om:result>
        ...
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>
```

## B ##

Inside of the `<om:procedure>` block.  The `codeSpace` for the `<gml:name>` should be better defined here.

```
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <om:procedure>
        <om:Process>
          <gml:FeatureCollection>
            <gml:name codeSpace="http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#discrete-sampling-geometries">profile</gml:name>
          </gml:FeatureCollection>
        </om:Process>
      </om:procedure>
      ...
      <om:result>
        ...
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>
```

## C ##

Inside of the `<om:featureOfInterest>` block. The codeSpace for the `<gml:name>` should be better defined here.

```
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <om:featureOfInterest xlink:role="cf:featureType:profile" xlink:href="urn:ogc:def:nil:OGC:unknown" />
      ...
      <om:result>
        ...
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>
      
```

## D ##



In the `<om:metadata>` block.

```
<om:ObservationCollection xmlns:om="http://www.opengis.net/om/1.0" xmlns:gml="http://www.opengis.net/gml" xmlns:swe="http://www.opengis.net/swe/1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" gml:id="ID_1" xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd">
  <om:member>
    <om:Observation>
      <om:metadata>
        <gml:name codeSpace="http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#discrete-sampling-geometries">timeSeries</gml:name>
      </om:metadata>
      ...
      <om:result>
        ...
      </om:result>
    </om:Observation>
  </om:member>
</om:ObservationCollection>
      
```

## E ##

Alternate implementation of the above, but with the actual geometry described inline as opposed to strictly using a reference to a vocabulary.  I've also heard of this reference being made using a link to a WFS server which handles the details of the feature description.  Though more complicated than in [IdentifyingTheFeatureType#C](IdentifyingTheFeatureType#C.md) this has the advantage of not giving us another vocabulary to manage.

The example below comes from the example files Mike Botts developed, copies of which are on this wiki at: [ObservationSeries-2011-12-20.xml](http://code.google.com/p/ioostech/source/browse/ObservationSeries-2011-12-20.xml)
```
<!--=============================================================
        feature of interest carries the sampling geometry of the observation
 ==============================================================-->
    <om:featureOfInterest>
        <sams:SF_SpatialSamplingFeature gml:id="SamplingPoint1">
            <sf:type xlink:href="http://www.opengis.net/def/samplingFeatureType/OGC-
                OM/2.0/SF_SamplingPoint"/>
            <sf:sampledFeature xsi:nil="true"/>
            <sams:shape>
                <gml:Point gml:id="UOMlocation">
                    <gml:pos srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
                        52.87 7.78</gml:pos>
                </gml:Point>
            </sams:shape>
        </sams:SF_SpatialSamplingFeature>
    </om:featureOfInterest>
```

NOTE: some of the elements used above come from version 2.0 of O&M.  We had intended to stick with 1.0 for all of the relevant specifications so this may be a problem.  A 1.0 version of the above concepts hasn't been developed yet.  TBD

# Footnotes #
> <sup>(1)</sup> http://csml.badc.rl.ac.uk/

<sup>(2)</sup> http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html#discrete-sampling-geometries

> <sup>(3)</sup>  http://www.unidata.ucar.edu/software/netcdf-java/reference/FeatureDatasets/PointUML.html, http://www.unidata.ucar.edu/software/netcdf-java/reference/FeatureDatasets/PointFeatures.html

> <sup>(4)</sup>  [http://www.unidata.ucar.edu/projects/THREDDS/tech/catalog/InvCatalogSpec.html#dataType ]