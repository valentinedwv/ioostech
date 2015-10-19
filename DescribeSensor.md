


# Request #

The attributes of the DescribeSensor request are detailed in the Table 3 of the Sensor Observation Service specification 1.0 ([OGC 06-009r6](https://portal.opengeospatial.org/files/?artifact_id=26667)).

| **Parameter** | **Name** | **Definition	Data type and Values** | **Multiplicity and Use of the Parameter** |
|:--------------|:---------|:------------------------------------|:------------------------------------------|
|request        |	Operation name|	DescribeSensor                      |	One (mandatory)                           |
|procedure      |	Is the process or sensor system, for which the description is to be returned. It could be an observing system, platform or a simple device, such as a bin. This value must match the value advertised in the xlink:href attribute of a procedure element advertised in the SOS GetCapabilities response. In the SOS specification it is referred as SensorID (Table 3). |	anyURI	One (mandatory)              |
|service        |	Service type identifier |	SOS                                 |	One (mandatory)                           |
|version        |	Specification version of the SOS accepted by client	|1.0.0 has format X.Y.Z               |	One (mandatory)                           |
|outputFormat   |	Specifies the desire output format.|	text/xml;subtype=sensorML/1.0.1	    | One (mandatory)                           |


# Response #

The following templates show very DRAFT examples of desirable sensor/platform/network descriptions.  These templates are not finalized.

  * Sensor description [DescribeSensor-Sensor.xml](http://code.google.com/p/ioostech/source/browse/trunk/templates/1.0/DescribeSensor/DescribeSensor-Sensor.xml)
  * Network description [DescribeSensor-Network.xml ](http://code.google.com/p/ioostech/source/browse/trunk/templates/1.0/DescribeSensor/DescribeSensor-Network.xml)
  * Platform description (time series at a point) [DescribeSensor-TimeSeries.xml](http://code.google.com/p/ioostech/source/browse/trunk/templates/1.0/DescribeSensor/DescribeSensor-TimeSeries.xml)
  * Platform description (trajectory from a glider) [DescribeSensor-Trajectory.xml](http://code.google.com/p/ioostech/source/browse/trunk/templates/1.0/DescribeSensor/DescribeSensor-Trajectory.xml)

# Examples #
  * IOOS Examples or Guidance [DescribeSensorMetadataForIOOSSOS](DescribeSensorMetadataForIOOSSOS.md)
  * Oostethys Examples http://code.google.com/p/oostethys/source/browse/trunk/component/server/perl/difDescribeSensor.xml?r=517
  * OGC Resources http://www.ogcnetwork.net/search/node/sensorml
  * OGC Resources https://portal.opengeospatial.org/files/?artifact_id=45897

## Q2O: QARTOD to OGC ##

Project home page is here.  http://q2o.whoi.edu/  One key idea relevant to the SensorML discussion is that Q2O has separated the platform/sensor metadata into two or more hierarchies based on the time scale in which the metadata is updated.  They can be referenced from within through xlinks.  For example, the _OEM_ file, or Original Equipment Manufacturer file, contains static metadata for a sensor that represents metadata that a) never changes and/or b) represents the factory defaults (these may change through time).  A second file, is a time dependent _Deployment_ file that contains metadata relevant to a particular deployment of the sensor in the environment.  I think this is an idea worth pursuing.

## Marine Metadata Initiative ##

Go to http://marinemetadata.org and search sensorml, there are many resources.

Additionally, Carlos Rueda at MMI has been working on a web service to create SensorML documents.  I don't know how capable it is but according to his comments on the SensorML mailing list he has been working on it lately (Oct 2011).  I hope this means that he's willing to engage if we have questions and possibly even respond to requests.  http://mmisw.org/smlmor/