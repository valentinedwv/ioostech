Please if possible provide information on how the SOS you are using was developed or its origins(Oostethys,NDBC,etc)  If your SOS is altered from a reference implementation(Oostethys,NDBC,52 North,etc) please describe or provide documentation link(s) to how and why it is different(additional features,work with existing skills/environment,etc).

I've listed a GetCapabilities link from the earlier SOS endpoint listing document - if there are additional GetCapabilities,DescribeSensor,GetObservation sample links you would like to share or documentation links, please feel free to add those also.

The goal is to develop hopefully a small handful of SOS implementation references and function/feature profiles that can be the source of possible updates or changes discussion.


# Alaska (AOOS) #

Documentation link(52 North)
https://docs.google.com/document/d/15qKOfJSS3t9JTFZFUsU5ssVNGQxcWYivH9j0XE1puq0/edit?hl=en_US

http://svc.axiomalaska.com:8080/sos2/sos?request=GetCapabilities&service=SOS

# Caribbean (CaRA) #

not working?

# Central and Northern California (CeNCOOS) #

http://204.115.180.244/sos/server.php?request=GetCapabilities&service=SOS

# Gulf of Mexico (GCOOS) #

http://data.gcoos.org/sos/sos_server.php?request=GetCapabilities&service=SOS

# Great Lakes Observing System (GLOS) #

http://michigan.glin.net/glos/sos/sos.php?request=GetCapabilities&service=SOS

# Mid-Atlantic (MARACOOS) #

http://www.weatherflow.com/sos/sos.pl?request=GetCapabilities&service=SOS

# Northwest Pacific (NANOOS) #

http://data.stccmop.org/ws/util/sos.py?request=GetCapabilities&service=SOS

and a second service documented [here](NANOOSNVSPythonSOS.md)

# Northeastern Atlantic (NERACOOS) #

Oostethys.  There are actually two versions demonstrating the OOSTethsy Perl Toolkit.  SWE and DIF.
### SWE ###
http://www.neracoos.org/cgi-bin/sos/V1.0/oostethys_sos.cgi?request=GetCapabilities&service=SOS
### DIF ###
http://www.neracoos.org/cgi-bin/sos/V1.0/oostethys_sos_dif.cgi?request=GetCapabilities&service=SOS

# Pacific Islands (PacIOOS) #

http://oos.soest.hawaii.edu/oostethys/sos?request=GetCapabilities&service=SOS

# Southern California (SCCOOS) #

http://sccoos-obs0.ucsd.edu/sos/server.php?request=GetCapabilities&service=SOS

# Southeast Atlantic (SECOORA) #

Documentation link
http://code.google.com/p/xenia/wiki/VMwareProducts#SOS

We have an older(2009) Oostethys version and a 'DIF' version which is a copied response format of the initial NDBC DIF SOS version.

http://neptune.baruch.sc.edu/cgi-bin/oostethys_sos.cgi?request=GetCapabilities&service=SOS

Xenia: Relational Database Schema used by SECOORA
Link to Google Code page: http://code.google.com/p/xenia/


# NDBC #

Documentation link
http://sdf.ndbc.noaa.gov/sos/

Production server:
http://sdf.ndbc.noaa.gov/sos/server.php?request=GetCapabilities&service=SOS

Test server:
http://sdftest.ndbc.noaa.gov/sos/server.php?request=GetCapabilities&service=SOS


# CO-OPS #
Documentation Link
http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/


http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/SOS?request=GetCapabilities&service=SOS

Documentation Link for test server

http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos-test/

http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos-test/SOS?request=GetCapabilities&service=SOS



# ACE #

http://sos.usace.army.mil/oracle_server.php?request=GetCapabilities&service=SOS