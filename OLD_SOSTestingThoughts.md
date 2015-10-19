


The material here was moved from the SOSTesting page once the Milestone 1.0 Test Plan was put there.

[SOS Validator Tool](https://github.com/axiomalaska/ioos-sos-validator)  Shane can make it run all the tests suggested by Alex:
# OGC compliance
  1. Test output files for template compliance
# "Rules" from [wiki](SOSGuidelines#Rules.md) (We need to determine the mandatory/optional tests.)
# For automation, how do we know which services to test?  Shane prefers to get SOS endpoints from the Service Registry via CSW, but may not be possible.  May need to manually populate a list of services to be tested.  Shane would have to be in the loop to add/delete services.
# Need to document Tool Requirements in the following form: [of Test](Name.md) [of element](xpath.md) [type](feature.md) [Request](Request.md) [outcome](expected.md) [of failure](severity.md)
  1. List of tests should be a google spreadsheet with the fields defined above.
  1. Only IOOS-specific tests need to be in this spreadsheet (not OGC stuff)
  1. Also need to define format/location of Test Report.  Probably just a list of tests and pass/fail.  If fail, what severity of failure.
  1. Wiki will maintain the list of tests that are to be executed with the validator.

Material below to be reworked.
# Introduction #

Initial testing is designed more towards a survey of existing SOS GetCapabilities, DescribeSensor and GetObservation services that have been submitted to the CatalogEndpoints document/spreadsheet.  For initial purposes, just looking at one (hopefully representative) SOS from each RA or other agency.  Also for initial purposes only considering single in-situ representations and not profiles or trajectories.

[See discussion\_thread\_1](#discussion_thread_1.md)

An initial simple perl script was setup to read submitted SOS endpoints and detail the number of platforms and observation types and their locations based on the GetCapabilities document.  The script also parses based on whether full xml namespaces are used and reports the vocabulary prefix in effect and provides a kml file of the platform locations.

This script can be used along with Eric Bridger's similar browser application which provides similar information at http://www.google.com/url?sa=D&q=http://dev.neracoos.org/IOOSCatalog3/SOSTester/catalog_end_points.html&usg=AFQjCNGG65xpqLiu3iCdtNebN2NxlQX_BA

[See discussion thread 2](#discussion_thread_2.md)

In addition to the above summary SOS information, creating a xsd(xml schema document) from a provided xml was used (the 'trang' tool) to compare existing schema/element differences between the existing SOS GetCapabilities documents.

Testing and categorization/compliance would be broken into 3 parts
  * a survey and categorization step to identify,categorize and describe existing SOS services to a known or new reference
    * see CatalogEndpoints spreadsheet and [SOSVersions](SOSVersions.md)
  * differences in schema  - xsd reference and differences
    * see 'discussion thread 2' below
  * differences in vocabulary - the listing/range of possible element/prefix terms and differences

This script can be used along with Eric Bridger's similar browser application which provides similar information at http://dev.neracoos.org/IOOSCatalog3/SOSTester/catalog_end_points.html  (starfish/starfish)

See also [SOSSurvey](SOSSurvey.md) and [SOSVersions](SOSVersions.md)

# SOS Assessment #

Summary of the current level of services and possibilities for evaluation, in an effort to identify requirements or problems to solve.

## Criteria for Comparison ##

  1. Does the service support compound offerings such as vector data (e.g. `observedProperty=winds` actually returns three or four scalar quantities such as wind\_gust, wind\_speed, wind\_direction etc)?
  1. Collections (e.g. `offering=network-all` returns all buoys in the network) and multiple observed properties (`observedProperty=sea_water_temperature,sea_water_salinity` returns data from both variables with one call)?
  1. Correct usage of vocabularies?
  1. Are the terms referenced by vocabularies, actually part of the voacabularies?  e.g. `<observedProperty xlink:href="http://mmisw.org/ont/cf/parameter/winds"/>`, winds is not actually part of the CF Standard Name vocabulary despite the URL.
  1. How are resource IDs implemented in the response types?  (This questions is trying to ge at the unique ID problem but isn't stated well.)
  1. Which SOS responses are supported?  DescribeSensor? SOS Core Profile, Transactional Profile or Full Profile?
  1. Are you eating your own dog food or is this just for “IOOS compliance”?  Do you or any customers you know of actually use your SOS service?  If not, do you know the chief complaint?
  1. What is the length of data available from each service (full time series from a ten year record or just the last month or year or whatever)?
  1. Are data available on the service representative of the entire RA inventory?  If not, why?  Are these decisions related to technology impediments that we can solve?

## Questions/Comments about the assessment ##
Let's make sure each question has a purpose.  What we're envisioning here is a survey where all members of the team will need to spend time answering a questionnaire.  This is potentially non-trivial so let's make it worthwhile. How will we collect and/or compile the information?
  * A template wiki page with questions?  Then copy/paste onto a new wiki page for each respondent?
  * A linked spreadsheet?

Place holder for the work Jeremy started: ["Thanks for posting the Catalog service endpoints document, from that I went through and tried to choose one SOS from each of the 11 RA's and federal backbone (ndbc,coop,ace) to start some analysis on. Worked up an initial perl script to get the GetCapabilites document... "](https://groups.google.com/d/topic/ioostech_dev/rnngO1AK0Ug/discussion).


# Discussion Threads #

## discussion thread 1 ##

from initial thread http://groups.google.com/group/ioostech_dev/browse_thread/thread/ae79e03b500ad148

Thanks for posting the Catalog service endpoints document, from that I went through and tried to choose one SOS from each of the 11 RA's and federal backbone(ndbc,coop,ace) to start some analysis on.

Worked up an initial perl script to get the GetCapabilites document and had to manually tweak some of the response xml namespace info at the document beginning to get around some odd things which the version of LibXML I'm using doesn't handle well.

The perl script is at http://neptune.baruch.sc.edu/xenia/ioos/get_sos.pl
and the resultant GetCapabilities documents and processed files are at
http://neptune.baruch.sc.edu/xenia/ioos/out

Each organization in the current array list below like 'secoora' has
a 'latest.txt.secoora' response corresponding to the getCapabilites
response a summary file 'out\_secoora' which is listed in a way for further post-processing - including platform locations and obs types, summary platform and observation type counts and kml/kmz file like 'secoora.kml' 'secoora.kmz' showing the platform
locations and obs types at each location.

I wanted to start also processing a sample getObservation from each RA and Fed SOS to start profiling common points and differences similarly - if there is a spreadsheet of getObservation links for each provider and associated documentation or we can build one, let me know.

Let me know if this type of analysis is helpful towards some kind of
validation testing or if it overlaps with something already in place - I was also looking into perl or unix command-line tools for validating
response xml's against an xml schema - xmllint and LibXML provide a basic pass/fail option towards this, but not sure if they work well in practice or provide enough useful detail on errors.

In developing the perl script, the following differences were noted in the
code below:
##########################################
#differences between sos's
```
my $sos_ns_prefix = 'sos:'; 
if ($org eq 'gcoos' || $org eq 'macoora' || $org eq 'coop') { 
  $sos_ns_prefix = ''; 
} 

##### 
my $vocab_delimiter = '#'; 
if ($org eq 'gcoos' || $org eq 'cencoos' || $org eq 'pacioos' || $org eq 
'coop' || $org eq 'ace' || $org eq 'ndbc') { 
  $vocab_delimiter = '/'; 
} 

if ($org eq 'neracoos' || $org eq 'aoos') { 
  $vocab_delimiter = ':'; 
} 

##### 
#uri vocab prefixes 
#pacioos,cencoos,ndbc,coop,ace 
#http://mmisw.org/ont/cf/parameter/ 
#gcoos 
#http://mmisw.org/ont/gcoos/parameter/ 
#nanoos,sccoos,macoora,glos 
# 
http://www.csc.noaa.gov/ioos/schema/IOOS-DIF/IOOS/0.6.1/dictionaries/... 
#neracoos 
#urn:ogc:def:phenomenon:mmisw.org:cf: 
#aoos 
#urn:ogc:def:phenomenon:OGC:1.0.30:SwellPeriod 
#secoora 
#http://carolinasrcoos.org/cf# 
```

## discussion thread 2 ##

from http://groups.google.com/group/ioostech_dev/browse_thread/thread/f07d530a07fbf708

Posted some samples(will copy post to upcoming 'testing' wiki page
also) some examples of the generated xsd files(secoora\_sos.xsd,ndbc\_sos.xsd,...) for SOS GetCapabilities
documents using the 'trang' tool at http://neptune.baruch.sc.edu/xenia/sos/ioos/out/xsd

Using NDBC's GetCapabilities as a base reference - doing a difference
with the other xsd were almost same except for a few minor differences
in the the following organizations - secoora,neracoos,maracoos,aoos,pacioos - each of which has a `*_diff`
file to highlight the differences(like secoora\_diff)

Plan to go through this xsd generation and diff comparison for the
DescribeSensor and GetObservations documents as well.

I used a basic perl regex substitution script
http://neptune.baruch.sc.edu/xenia/sos/ioos/out/filter/convert.sh to
apply full 'sos:' namespaces to documents which didn't have them - and
had to mess around with the namespace declarations, setting
xmlns:sos="http://blah.org" to get trang to create a correct xsd file.