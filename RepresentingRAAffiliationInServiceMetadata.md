# Introduction #

We have a need to have each service in IOOS (SOS, THREDDS/OPeNDAP, ERDDAP etc) self documented in such a way that their affiliation with one of the Regional Associations and/or Federal Partners is clear and machine readable.  We need to do this in such a way as to allow a many to many relationship between a server and a region/federal partner.

_**Question**:  Is the statement above (many to many) true? Are there cases where a server belongs to both a region and a federal or other type of entity?  The example that comes to mind is NERRS and SECOORA but there may be others.  Jeremy/Vembu?_

One use case for this need is having the [IOOS Data Catalog](DataCatalog.md) regularly harvest service metadata from a server and properly attribute the server to a region for plotting or another summary purpose.  Finally, an intermediate term goal for all of us is to have the Annual Non-Federal Observation Asset Inventory automated.  [Requirement](Requirement.md).

This idea was further discussed in a thread on the ioostech\_dev group list.  https://groups.google.com/d/topic/ioostech_dev/hTMaCJtkcWo/discussion

# SOS Capabilities XML #
In the `<ServiceIdentification>` section of the SOS capabilities response, include the following keyword markup.

```
<ows:Keywords>
  <ows:Keyword>aoos</ows:Keyword>
  <ows:Keyword>IOOS</ows:Keyword>
  <ows:Keyword>Alaska</ows:Keyword>
  <ows:Keyword>ocean</ows:Keyword>
  <ows:Keyword>observing</ows:Keyword>
  <ows:Keyword>...</ows:Keyword>
</ows:Keywords>
```

The RA acronym should appear as one of the keywords and each keyword should appear as a separate `<ows:Keyword></ows:Keyword>` element.  Also, the acronym IOOS must appear as one of the keywords.  This will enable several metadata aggregation engines like ESRI Geoportal to be searched for IOOS related services.  The DataCatalog will parse the keywords list looking for the 11 RA acronyms and select other acronyms like IOOS, NDBC, CO-OPS.

_Ideally the RA acronym would be the first keyword but that is not necessary.  This search is not case sensitive.  (**Comment from EMILIO**: I don't think there should be any expectation about the order in which the RA acronym appears; that's an unnecessary burden, that's probably only handy for **people** reading the GetCapabilities XML response directly. Also, while the search indeed should be case insensitive, we should recommend that the acronym be entered as all-uppercase so it does look like an acronym.)_

# SensorML Example #

See discussion here: [DescribeSensorMetadataForIOOSSOS](DescribeSensorMetadataForIOOSSOS.md)

# ISO 19119/19139 Service Metadata #
The ISO service metadata describes geospatial web services.  It is general and can encompass many of the elements in the SOS capabilities XML as well as many more elements capabilities XML cannot describe.  Currently (circa 2011) it is most often used in IOOS to describe servers which have the ability to automatically provide ISO service metadata through ncISO ([Google Group](https://groups.google.com/forum/#!forum/ncisometadata), [Home page](http://www.ngdc.noaa.gov/eds/tds/)).  This plugin can be enabled in any THREDDS server newer than v 4.2.8 although 4.2.9 is preferred.  Additionally, both Hyrax and ERDDAP are working on porting the ncISO plugin to their environments.  ncISO can be run as a command line client tool in addition to a server side plugin.

## Mapping from NetCDF to ISO via ncISO ##

Unidata Attribute Conventions for Dataset Discovery (ACDD) ([ACDD on the GEO-IDE wiki](https://geo-ide.noaa.gov/wiki/index.php?title=NetCDF_Attribute_Convention_for_Dataset_Discovery))

### Mapping from within THREDDS Catalogs ###
The following shows how a publisher element in THREDDS catalog metadata can be used to identify the publisher of the service.
http://www.ngdc.noaa.gov/thredds/ncisoExamplesCatalog.xml and http://www.ngdc.noaa.gov/thredds/ncisoExamplesCatalog.html?dataset=oceanSitesAntaresImprovedTDS

```
<dataset name="OceanSITES Antares Improved TDS Metadata" ID="oceanSitesAntaresImprovedTDS" urlPath="oceansites/OS_ANTARES-1_200509_D_CTDImprovedTDS.nc">
<serviceName>allMetadata</serviceName>
<documentation type="Rights">These data were collected and made freely available by the OceanSITES project and the national programs that contribute to it.</documentation>
<contributor role="Principal Investigator">Christian Tamburini</contributor>
<project>EuroSITES</project>
<publisher>
	<name vocabulary="">EuroSITES</name>
	<contact url="http://www.noc.soton.ac.uk" email="postmaster@noc.soton.ac.uk"/>
</publisher>
</dataset>
```

Questions:
  * Where is this mapped to in the ISO?
  * What is the `vocabulary` attribute and how should we use it?
  * Are there other "roles" we should use?
http://www.unidata.ucar.edu/projects/THREDDS/tech/catalog/v1.0.2/InvCatalogSpec.html
https://geo-ide.noaa.gov/wiki/index.php?title=NetCDF_Attribute_Convention_for_Dataset_Discovery#Determining_an_Order_of_Precedence


### Using netCDF global attributes ###
```
variable.attribute = 'AOOS'
```
What goes above exactly?

See also: https://geo-ide.noaa.gov/wiki/index.php?title=NetCDF_and_ISO_Metadata

## Writing ISO directly ##

TODO: Give a better example here.

https://geo-ide.noaa.gov/wiki/index.php?title=ISO_Components#CI_ResponsibleParty

NOTE: The link above only shows the ISO element that we should use, it does not necessarily show the right implementation for this purpose nor does it show where to put it in the overall document.  Need a full XPath.