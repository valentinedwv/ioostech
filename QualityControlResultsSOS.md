# Introduction #

This page discusses how generic quality control tests could and/or should be recorded in the SOS responses.  This is a Milestone 1.0 issue and in no way depends on the results of QARTOD to address.


# Scenarios and QC Test Types #

## Referencing an external document ##

The simplest scenario for documenting QC is to reference an external document and give no specifics about the actual results of the test.  This is also useful for providing supplementary information.  It's a good practice overall.  See [Issue 49](https://code.google.com/p/ioostech/issues/detail?id=49) for discussion.

_AB: It is possible; see Option 1 or 2 in the encoding example below._

## One summary flag per data record ##

Mostly [Issue 15](https://code.google.com/p/ioostech/issues/detail?id=15).

_AB: This is possible; see Options 1 & 2 in the encoding example below._

## Multiple tests per data record ##

~~This may not be possible using just `<swe:quality>`.  It looks like the cardinality is 1.~~

~~See http://www.botts-inc.com/SensorML_1.0.1/schemaBrowser/SensorML_Boolean.html#Link1AB8BD20~~~~

_AB: That is not **exactly** right:_
  * _yes, the cardinality of `<swe:quality>` is `[0 … 1]` if it is a child element of `<swe:Boolean>`, `<swe:Time>` `<swe:TimeRange>` or `<swe:Category>`_
  * _but, the cardinality of `<swe:quality>` is `[0 … unbounded]` if it is a child element of `<swe:Count>`, `<swe:CountRange>`, `<swe:Quantity>` or `<swe:QuantityRange>`_

_See, for example, http://www.botts-inc.com/SensorML_1.0.1/schemaBrowser/SensorML_Count.html and Option 2 in the encoding example below._

## One summary flag per file or data set ##

_AB: Again, it seems possible using Option 1 (see below)_.

# References #
http://www.oceandatastandards.org/index.php?option=com_content&task=view&id=46&Itemid=0

# Investigative Example #
_I ran some investigation of the possible ways of indicating QC flags in SWECommon GetObservation response. For research, I used one of Janet Fredericks’ response templates referred by Sara Haines in [Issue 15](https://code.google.com/p/ioostech/issues/detail?id=15) (http://code.google.com/p/ioostech/issues/detail?id=15#c5). Here is the summary of my research:_

  * _It is possible to insert the QC information into a GO response at least in three different ways:_
    1. _in a form of the ISO 19115 Data Quality (DQ) package in the `<om:ObservationCollection>/<om:member>/<om:Observation>/<om:resultQuality>` (Option 1);_
    1. _in a form of unlimited number of `<swe:quality>` elements inside `<swe:DataArray>/<swe:elementCount>/<swe:count>` construct in the `<om:result>` section (Option 2);_
    1. _in a form of multiple number of `<swe:field>` elements in the `<om:result>` section (Option 3)._
  * _Option 1 allows providing a single QC record per observation record (general QC for the dataset, etc.); also, it allows reporting QC info in ISO 19115 format; however, in order to use this option, the `xmlns:gmd` namespace and reference to the `dataQuality.xsd` schema must be added to the declaration header._
  * _Option 2 (similar to Option 1) allows a single QC record for the whole dataset; at the same time it does not provide/require ISO format._
  * _Option 3 is the one that has been used by NDBC, it allows flexible reporting of the QC info that changes from one observation to another; however, in case that the QC is fixed, it results in unnecessary bloated `<swe:value>` section of the GO response._
_So, each option seems to have its own advantages and drawbacks, and perhaps IOOS should not concentrate on any single one of them._



_**ENCODING EXAMPLE:**_

```
<?xml version="1.0" encoding="UTF-8"?>
<om:ObservationCollection gml:id="ADCP_Observation" 
    xmlns:saxon="http://saxon.sf.net/" xmlns:xs="http://www.w3.org/2001/XMLSchema" 
    xmlns:gmi="http://www.isotc211.org/2005/gmi"
    xmlns:gco="http://www.isotc211.org/2005/gco"
    xmlns:gml="http://www.opengis.net/gml" 
    xmlns:gmd="http://www.isotc211.org/2005/gmd" 
    xmlns:om="http://www.opengis.net/om/1.0" 
    xmlns:swe="http://www.opengis.net/swe/1.0.1" 
    xmlns:xlink="http://www.w3.org/1999/xlink" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xsi:schemaLocation="http://www.opengis.net/om/1.0 http://schemas.opengis.net/om/1.0.0/observation.xsd 
    http://www.isotc211.org/2005/gmd http://schemas.opengis.net/iso/19139/20070417/gmd/dataQuality.xsd">
    
    
<!-- Observation name -->
    <gml:name>
        Data from ADCP profiler
    </gml:name>
    <om:member>
        <om:Observation>
<!-- Observation time -->
            <om:samplingTime>
                <gml:TimePeriod>
                    <gml:beginPosition>
                        2009-04-25T13:00:00Z
                    </gml:beginPosition>
                    <gml:endPosition>
                        2009-04-25T15:00:00Z
                    </gml:endPosition>
                </gml:TimePeriod>
            </om:samplingTime>
<!-- Sensor description (SensorML) -->
            <om:procedure xlink:href="http://mvcodata.whoi.edu/downloads/sensorML/v1.0/examples/sensors/ADCP_2.2/ADCP_System.xml"/>
<!-- Observation quality description (Option 1 - ISO 19115-2 DQ Package) -->
            <om:resultQuality>
                <gmd:DQ_DataQuality id="ID1">
                    <gmd:scope>
                        <gmd:DQ_Scope id="ID2">
                            <gmd:level></gmd:level>
                            <gmd:extent>
                                <gmd:EX_Extent id="ID3"></gmd:EX_Extent>
                            </gmd:extent>
                            <gmd:levelDescription></gmd:levelDescription>
                        </gmd:DQ_Scope>
                    </gmd:scope>
                    <gmd:report>
                        <gmd:DQ_TemporalValidity id="ID4">
                            <gmd:nameOfMeasure></gmd:nameOfMeasure>
                            <gmd:measureIdentification></gmd:measureIdentification>
                            <gmd:measureDescription></gmd:measureDescription>
                            <gmd:evaluationMethodType>
                                <gmd:DQ_EvaluationMethodTypeCode codeList="http://www.example.com/" codeListValue="http://www.example.com/">string</gmd:DQ_EvaluationMethodTypeCode>
                            </gmd:evaluationMethodType>
                            <gmd:evaluationMethodDescription></gmd:evaluationMethodDescription>
                            <gmd:evaluationProcedure></gmd:evaluationProcedure>
                            <gmd:dateTime></gmd:dateTime>
                            <gmd:result></gmd:result>
                        </gmd:DQ_TemporalValidity>
                    </gmd:report>
                    <gmd:lineage>
                        <gmd:LI_Lineage id="ID6">
                            <gmd:statement></gmd:statement>
                            <gmd:processStep></gmd:processStep>
                            <gmd:source>
                                <gmd:LI_Source id="ID7"></gmd:LI_Source>
                            </gmd:source>
                        </gmd:LI_Lineage>
                    </gmd:lineage>
                </gmd:DQ_DataQuality>
            </om:resultQuality>
<!-- Observable is a composite containing all data for now -->
            <om:observedProperty>
                <swe:CompositePhenomenon dimension="24" gml:id="ALL_OBSERVABLES">
                    <gml:description>
                        ALL Mesurements from ADCP_System including QC flags and bad data
                    </gml:description>
                    <gml:name>
                        ADCP measurements
                    </gml:name>
                    <swe:component xlink:href="urn:ogc:phenomenon:time:iso8601"/>
                    <swe:component xlink:href="urn:ogc:def:property:latitude"/>
                    <swe:component xlink:href="urn:ogc:def:property:longitude"/>
                    <swe:component xlink:href="urn:Q2O:def:property::depth"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/meanSeaWaterPressure"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/waveHeightFromPressure"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/wavePeriodFromPressure"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/loCutoffFrequency"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/hiCutoffFrequency"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/waveHeightAll"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/swell"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/windWaves"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/wavePeriodAll"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/swellPeriod"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/windPeriod"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/dominantWaveDirection"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/swellDirection"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/windWaveDirection"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/topBinHeight"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/properties/bottomBinHeight"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/qcflag/dataGapFlag"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/qcflag/aggregatePressureFlag"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/qcflag/echoIntensityFlag"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/qcflag/cMFlag"/>
                    <swe:component xlink:href="http://mmisw.org/ont/mvco/qcflag/aggregateVelocityFlag"/>
                </swe:CompositePhenomenon>
            </om:observedProperty>
<!-- Feature Of Interest -->
            <om:featureOfInterest xlink:href="urn:MVCO:location:MarthasVineyardCoastalObservatory"/>
            <om:parameter/>
<!-- Result Structure and Encoding -->
            <om:result>
                <swe:DataArray>
                    <swe:elementCount>
                        <swe:Count>
<!-- Observation quality description (Option 2 - multiple <swe:quality>) -->
                            <swe:quality xlink:title="dataGapFlag">
                                <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/dataGapFlag">
                                    <gml:metaDataProperty></gml:metaDataProperty>
                                    <gml:description></gml:description>
                                    <gml:name>dataGapFlag</gml:name>
                                        <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                    <swe:constraint>
                                        <swe:AllowedTokens>
                                            <swe:valueList></swe:valueList>
                                        </swe:AllowedTokens>
                                    </swe:constraint>
                                    <swe:quality/>
                                    <swe:value></swe:value>
                                </swe:Category>
                            </swe:quality>
                            <swe:quality xlink:title="aggregatePressureFlag">
                                <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/aggregatePressureFlag">
                                    <gml:metaDataProperty></gml:metaDataProperty>
                                    <gml:description></gml:description>
                                    <gml:name></gml:name>
                                    <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                    <swe:constraint>
                                        <swe:AllowedTokens>
                                            <swe:valueList></swe:valueList>
                                        </swe:AllowedTokens>
                                    </swe:constraint>
                                    <swe:quality></swe:quality>
                                    <swe:value></swe:value>
                                </swe:Category>
                            </swe:quality>
                            <swe:quality xlink:title="echoIntensityFlag">
                                <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/echoIntensityFlag">
                                    <gml:metaDataProperty></gml:metaDataProperty>
                                    <gml:description></gml:description>
                                    <gml:name></gml:name>
                                    <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                    <swe:constraint>
                                        <swe:AllowedTokens>
                                            <swe:valueList></swe:valueList>
                                        </swe:AllowedTokens>
                                    </swe:constraint>
                                    <swe:quality></swe:quality>
                                    <swe:value></swe:value>
                                </swe:Category>
                            </swe:quality>
                            <swe:quality xlink:title="cMFlag">
                                <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/cMFlag">
                                    <gml:metaDataProperty></gml:metaDataProperty>
                                    <gml:description></gml:description>
                                    <gml:name></gml:name>
                                    <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                    <swe:constraint>
                                        <swe:AllowedTokens>
                                            <swe:valueList></swe:valueList>
                                        </swe:AllowedTokens>
                                    </swe:constraint>
                                    <swe:quality></swe:quality>
                                    <swe:value></swe:value>
                                </swe:Category>
                            </swe:quality>
                            <swe:quality xlink:title="aggregateVelocityFlag">
                                <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/aggregateVelocityFlag">
                                    <gml:metaDataProperty></gml:metaDataProperty>
                                    <gml:description></gml:description>
                                    <gml:name></gml:name>
                                    <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                    <swe:constraint>
                                        <swe:AllowedTokens>
                                            <swe:valueList></swe:valueList>
                                        </swe:AllowedTokens>
                                    </swe:constraint>
                                    <swe:quality></swe:quality>
                                    <swe:value></swe:value>
                                </swe:Category>
                            </swe:quality>
                            <swe:value>
                                7
                            </swe:value>
                        </swe:Count>
                    </swe:elementCount>
                    <swe:elementType name="adcpObs">
                        <swe:DataRecord>
                            <swe:field name="sysInfo">
                                <swe:DataRecord>
                                     <swe:field name="time">
                                        <swe:Time definition="urn:ogc:phenomenon:time:iso8601"/>
                                    </swe:field>
                                    <swe:field name="lat">
                                        <swe:Quantity definition="urn:ogc:def:property:latitude">
                                            <swe:uom code="deg"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="lon">
                                        <swe:Quantity definition="urn:ogc:def:property:longitude">
                                            <swe:uom code="deg"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="depth">
                                        <swe:Quantity definition="urn:Q2O:def:property::depth">
                                            <swe:uom code="m"/>
                                        </swe:Quantity>
                                    </swe:field>
                                </swe:DataRecord>
                            </swe:field>
                            <swe:field name="pressure">
<!-- This is optional to ADCP systems -->
                                <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/meanSeaWaterPressure">
                                    <swe:uom code="cm"/>
                                </swe:Quantity>
                            </swe:field>
                            <swe:field name="pressureObsChainOutputs">
                                <swe:DataRecord>
                                    <swe:field name="waveHeightFromPressure">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/waveHeightFromPressure">
                                            <swe:uom code="cm"/>
                                            <swe:quality></swe:quality>
                                            <swe:quality></swe:quality>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="wavePeriodFromPressure">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/wavePeriodFromPressure">
                                            <swe:uom code="s"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="loCutoffFrequency">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/loCutoffFrequency">
                                            <swe:uom code="Hz"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="hiCutoffFrequency">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/hiCutoffFrequency">
                                            <swe:uom code="Hz"/>
                                        </swe:Quantity>
                                    </swe:field>
                                </swe:DataRecord>
                            </swe:field>
                            <swe:field name="velocityObsChainOutputs">
                                <swe:DataRecord>
                                    <swe:field name="waveHeightAll">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/waveHeightAll">
                                            <swe:uom code="cm"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="swell">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/swell">
                                            <swe:uom code="cm"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="windWaves">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/windWaves">
                                            <swe:uom code="cm"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="wavePeriodAll">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/wavePeriodAll">
                                            <swe:uom code="s"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="swellPeriod">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/swellPeriod">
                                            <swe:uom code="s"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="windPeriod">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/windPeriod">
                                            <swe:uom code="s"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="dominantWaveDirection">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/dominantWaveDirection">
                                            <swe:uom code="deg"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="swellDirection">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/swellDirection">
                                            <swe:uom code="deg"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="windWaveDirection">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/windWaveDirection">
                                            <swe:uom code="deg"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="topBinHeight">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/topBinHeight">
                                            <swe:uom code="cm"/>
                                        </swe:Quantity>
                                    </swe:field>
                                    <swe:field name="bottomBinHeight">
                                        <swe:Quantity definition="http://mmisw.org/ont/mvco/properties/bottomBinHeight">
                                            <swe:uom code="cm"/>
                                        </swe:Quantity>
                                    </swe:field>
                                </swe:DataRecord>
                            </swe:field>
<!-- Observation quality description (Option 3 - flags in <swe:field>) -->                  
                            <swe:field name="flags">
                                <swe:DataRecord>
                                    <swe:field name="dataGapFlag">
                                        <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/dataGapFlag">
                                            <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                        </swe:Category>
                                    </swe:field>
                                    <swe:field name="aggregatePressureFlag">
                                        <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/aggregatePressureFlag">
                                            <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                        </swe:Category>
                                    </swe:field>
                                    <swe:field name="echoIntensityFlag">
                                        <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/echoIntensityFlag">
                                            <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                        </swe:Category>
                                    </swe:field>
                                    <swe:field name="cMFlag">
                                        <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/cMFlag">
                                            <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                        </swe:Category>
                                    </swe:field>
                                    <swe:field name="aggregateVelocityFlag">
                                        <!-- ?? -->
                                        <swe:Category definition="http://mmisw.org/ont/mvco/qcflag/aggregateVelocityFlag">
                                            <swe:codeSpace xlink:href="http://mmisw.org/ont/mvco/flag"/>
                                        </swe:Category>
                                    </swe:field>
                                </swe:DataRecord>
                            </swe:field>
                        </swe:DataRecord>
                    </swe:elementType>
                    <swe:encoding>
                        <swe:TextBlock blockSeparator=" " decimalSeparator="." tokenSeparator=","/>
                    </swe:encoding>
<!-- Result Values -->
                    <swe:values>
                        2009-04-25T13:00:00,41.3366,-70.5564,0.0,1116.8,29.9,9,0.06,0.12,106.7,53.9,40.8,9,10,5,164.8,156.6,189.2,9.6,3.1,0,0,0,1,1
                        2009-04-25T13:20:00,41.3366,-70.5564,0.0,1107.4,25.3,9,0.06,0.12,86.5,44.4,40.5,6,10,5,188.4,156.2,199.9,9.6,3.1,0,0,0,1,1
                        2009-04-25T13:40:00,41.3366,-70.5564,0.0,1098.6,31.6,8,0.06,0.14,77.9,35.7,39.4,5,9,5,200.2,168.2,200.2,9.1,3.1,0,0,0,0,0
                        2009-04-25T14:00:00,41.3366,-70.5564,0.0,1090.3,29.1,9,0.06,0.14,77.2,31.9,40.6,5,9,5,196.9,169.8,192.3,9.1,3.1,0,0,0,0,0
                        2009-04-25T14:20:00,41.3366,-70.5564,0.0,1081.9,31.7,9,0.06,0.12,80.9,36.3,38.7,5,9,5,201.6,170.4,202.6,9.1,3.1,0,0,0,0,0
                        2009-04-25T14:40:00,41.3366,-70.5564,0.0,1074.4,35.2,10,0.06,0.12,79.0,34.7,35.8,4,9,5,246.2,161.1,155.9,9.1,3.1,0,0,0,0,0
                        2009-04-25T15:00:00,41.3366,-70.5564,0.0,1067.1,30.5,9,0.06,0.12,84.3,35.6,41.0,4,8,5,198.3,175.0,194.1,9.1,3.1,0,0,0,0,0 
                    </swe:values>
                </swe:DataArray>
            </om:result>
        </om:Observation>
    </om:member>
</om:ObservationCollection>
```