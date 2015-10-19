# 52North #

[52North](http://52north.org/communities/sensorweb/) Sensor Web Community (Servers and clients)

  * Web-based Thin Client: http://52north.org/communities/sensorweb/clients/Thin_SWE_Client/index.html
    * demo: http://sensorweb.demo.52north.org/ThinSweClient2.0/Client.html
    * Another demo (via Shane): http://sensorweb.demo.52north.org/sensorwebclient-webapp-3.0.0-rc.2/ Don't know if this is simply a newer version of the demo listed above.

Provide map-view of sensor locations, interactive graphing, and data export capabilities, work with pre-provided SOS services, however not with services above, probably require specific response formats (?)

# Applied Science Associates #

  * EDC (Environmental Data Connector):
    * [ASA Environmental Data Connector](https://github.com/asascience-open/EDC) - Desktop (Java) based EDC
    * [ftp://ftp.oilmap.com/EDC/Standalone/sos_wg/edcstore.zip](ftp://ftp.oilmap.com/EDC/Standalone/sos_wg/edcstore.zip) (use a real FTP client)
    * Or from ERD at: http://www.pfeg.noaa.gov/products/EDC/
    * [ASA EDC-Web](http://ec2-72-44-60-22.compute-1.amazonaws.com/edc/) - Web based EDC

  * pyoos (Python-based client; still early in the development):
    * https://github.com/asascience-open/pyoos

# NGDC #

XSL translations


# IOOS Modeling Testbed tools #

Eric Bridgers javascript library hosted at Oostethys google code site http://code.google.com/p/oostethys/downloads/list


# Proteus #

"[IAI's Proteus](http://www.i-a-i.com/proteus/) offers a convenient way to discover sensor data from SOS standardized by OGC. Proteus can visualize service contents on a map to quickly give an overview of sensor locations. Sensor data can then be viewed in a time series and exported for further processing." Currently (Sept. 2012) at Beta stage.


# SECOORA #
http://code.google.com/p/xenia/source/browse/trunk/python/xeniatools/ioosDif.py
and for that matter, many useful things at
http://code.google.com/p/xenia/source/browse/trunk/python/

## GetCapabilities survey ##

An initial perl script to get the GetCapabilites document and had to manually tweak some of the response xml namespace info at the document beginning to get around some odd things which the version of LibXML I'm using doesn't handle well.

The perl script is at http://neptune.baruch.sc.edu/xenia/ioos/get_sos.pl and the resultant GetCapabilities documents and processed files are at http://neptune.baruch.sc.edu/xenia/ioos/out

Each organization in the current array list below like 'secoora' has a 'latest.txt.secoora' response corresponding to the getCapabilites response a summary file 'out\_secoora' which is listed in a way for further post-processing - including platform locations and obs types, summary platform and observation type counts and kml/kmz file like 'secoora.kml' 'secoora.kmz' showing the platform locations and obs types at each location.


# Thoughts on Needs for Clients #

Mostly excerpted from [an email](https://groups.google.com/d/msg/ioostech_dev/Z5smNTb9yQc/zqK5PRRcbggJ) from Mohamed C at CO-OPS.

_I think we should encourage the development of software components that are specialized in solving one piece of this puzzle and have those available for all. Examples of such components would be client software to parser SOS responses in various languages and flavors. Others would be translation clients that read in one format and output another. Also, other examples would be components that can be used by the data providers to tackle areas of developing SOS services. Validation .. etc_

As a starting point we may need a survey for such stand alone components, where the most need is? what was developed so far? , and we can all pitch in or at least encourage all entities to write code on the identified areas in such a way that can be reused by others with minimum changes if any.