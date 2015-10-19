see also [SOSVersions](SOSVersions.md),[SOSAssessment](SOSAssessment.md),[SWECommonPlan](SWECommonPlan.md),[SWE Common Encoding Plan](https://docs.google.com/document/d/1czWdBFjPmAEtLe5T3_54fwk2cUdbILwWPkIDKPKFNvY/edit?hl=en_US)

**Please provide answers on this wiki(copy and paste to a new wiki page like SOSSurveySECOORA) or other means to the following questions in bold.**



# SOS development history #

**Please if possible provide information on how the SOS you are using was developed or its origins(Oostethys,NDBC,52 North,etc) If your SOS is altered from a reference implementation please describe or provide documentation link(s) to how and why it is different(additional features,work with existing skills/environment,etc).  This information can be used to cross-reference or cross-apply existing documentation or changes.**

**If you have SOS service usage documentation the same or similar to the below documentation, please provide links to that also.**

CO-OPS SOS request parameters http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/parameters.jsp

NDBC request parameters and example usage links http://sdf.ndbc.noaa.gov/sos/

See also discussion thread regarding 'IDD' (Interface Description Document) at http://groups.google.com/group/ioostech_dev/browse_thread/thread/85331a089b64716a/a32c8968617bdd41 http://waterservices.usgs.gov/rest/IV-Service.html#Service

# General rules #

**A listing of 'rules' which all SOS should follow - if disagree or would like to suggest additional common 'rules', please suggest below**

  * no case sensitivity - lowercase preference - request and response characters should not have any dependence on case
  * full namespaces in xml response elements, no default namespaces - 'sos:Contents' , not just 'Contents'
    * post requests also?(ndbc,co-ops)
      * post vs get - **Do you provide a POST method?  Is POST required by your users?**


---

# Request parameters #

## request= ##

request= GetCapabilities,DescribeSensor,GetObservation

**If you do not support the above request= types, please describe.**


---

## Defaults ##


---

### service=SOS ###

**Is service=SOS required or provided as a default?**


---

### version= ###

**Is version=??? required or provided as a default to the latest version?  If required, list accepted versions.**


---

### eventtime= ###

**Is eventtime always in full(including hours:minutes:seconds) ISO8601 format using GMT?**

**Does a missing eventtime parameter return the latest observation(s)?**


---

### outputformat= ###

_outputformat(DescribeSensor) vs responseformat(GetObservation) ?_

**Does a missing outputformat parameter return CSV?  Is the CSV response download or in-browser?**

**Additional outputformat= GML,TSV,KML,JSON... ?**


---

### qualified namespaces ###

**Do your offering,procedure or observedproperty parameters accept 'short' identifiers(like sea\_water\_temperature) or only fully qualified identifiers(like http://mmisw.org/ont/cf/parameter/sea_water_temperature )?**


---

### additional defaults ###
**Are there other additional default missing parameter conventions designed to make the service easier to use?**


---

## Required/Common ##


---

### offering vs procedure ###

**Are the parameters 'offering' and 'procedure' interchangeable in DescribeSensor and GetObservation requests?  If not, how do they differ?**


---

### platform vs sensor request ###

**Is a sensor request suffixed onto a platform request like below?  If not, what method is provided to access an individual sensor data feed?**

Platform procedure=urn:ioos:station:NOAA.NOS.CO-OPS:cb1301
<br />
Sensor procedure=urn:ioos:sensor:NOAA.NOS.CO-OPS:8454000:A1


---

### observedproperty= ###

**Does the observedproperty request support multiple observation requests?  If so, is it a comma-delimited list or some other vector identifier such as 'winds',etc?**


---

## Collections ##

### all ###

**Does your service support an 'all' type request like below?  If not implemented by featureofinterest or bbox parameter, please describe.**

offering=urn:ioos:network:noaa.nws.ndbc:all

### featureofinterest, bbox ###

**Does your service support a featureofinterest= or bbox= parameter like below?  Please describe.**

featureOfInterest=bbox:-177.3600,-46.9217,178.2700,71.3601
<br />
bbox=-177.3600,-46.9217,178.2700,71.3601
<br />
featureofinterest=urn:ioos:event:tsunami::geophysical:20090319\_tonga


---

## Additional parameters ##

**Does your SOS support additional parameters such as the examples in the link below regarding datum,sampling frequency or conversion of units or timezone?**

http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/parameters.jsp

  * result(datum)
  * unit
  * timezone
  * epoch(datum)
  * datatype(frequency)


---

## Error handling ##

**What error codes or responses are given by your SOS services - are the responses common to a standard or reference implementation?**


---

# Response #

## Service metadata ##

service identification keywords - RA name like SECOORA,etc
> http://code.google.com/p/ioostech/wiki/RepresentingRAAffiliationInServiceMetadata
> iso 19115, 19119

roles/responsibilites semantics/usage

**What ISO and contact type metadata implementation guidelines does your service reference?**

## Resource id's ##

redundancies? use same/close long/lat location to help identify overlaps?

**What's the method or authority(WMO,etc) for providing resource id's such as platform or sensor id's?**

## Data encoding ##

**What data encoding(s) does your GetObservation provide? SWE Common,GML,CSV,TSV,KML,JSON,... How is the schema and vocabulary of these various responses the same or different?(for example, same CSV headers/payload for both CSV and SWE Common? netCDF vocabulary,etc?)**


---

# Additional concerns #

## Vocabularies, UOM ##

http://code.google.com/p/ioostech/wiki/SOSTesting#discussion_thread_2

**What observedproperty and unit of measure(UOM) vocabulary prefix(s) and terms does your service reference?**

## Additional instrumentation/example types ##

> profiles,trajectories

> swe data arrays?

**Are there additional instrumentation types (other than single point in-situ) that your service provides(such as profiles,trajectories,...).  Please describe.**

## Usage and Performance ##

any usage of the sos service other than for ioos catalog - if so, one or many? user list and pattern of use(data types,amount,frequency)

usage/data,etc limits
  * holdings represented(type,time recency/window,period)
  * analysis & planned changes

performance
  * analysis & planned changes

### Clients/Testers ###
  * CITE
  * EDC
  * Eric
    * Registry http://dev.neracoos.org/IOOSCatalog3/Registry/
    * Tester http://dev.neracoos.org/IOOSCatalog3/SOSTester/
  * Jeremy
    * GetCapabilities http://code.google.com/p/ioostech/wiki/SOSTesting#discussion_thread_1
    * XML to XSD for schema comparison http://code.google.com/p/ioostech/wiki/SOSTesting#discussion_thread_2


---

# Additional comments #