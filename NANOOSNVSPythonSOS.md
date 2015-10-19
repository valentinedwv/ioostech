

# Python SOS for NANOOS NVS NRT in-situ Assets #

**_The new server was released publicly on Nov 18, 2011. Currently it provides access to 19 in-situ stations/assets._**

Documentation for the IOOS Python SOS server developed recently by [NANOOS](http://nanoos.org) (first by CMOP, then enhanced by APL-UW).

Our intent is to release the code, eventually, when we've cleaned it up and documented it just enough. I also intend to document conventions used (IOOS conventions), with links to where they're specified; when something seemed ambiguous, I'll try to describe the rationale behind decisions made.

## Defaults and minimalist, simplified requests ##

The NANOOS SOS makes extensive use of "defaults" to enable the simplest possible requests to be composed, making the service less complex and intimidating to users (including code, as these simplifications allow for simpler parsers). Many of these are illustrated in the [Sample requests and responses](#Sample_requests_and_responses.md) section.

  * DescribeSensor and GetObservation accept unqualified station values, and GetObservation accepts unqualified _observedProperty_ values. This is described in the [stations and observed properties](#stations_and_observed_properties.md) section.
  * In GetObservation, when the _eventTime_ key is ommitted, the latest observation is returned **(OOT)**. When the station and observed property are measured at multiple depths, the latest observation per depth is returned.
  * In GetObservation, when the _responseFormat_ key is ommitted, _text/plain_ is assumed. This is the same IOOS CSV data encoding as _text/csv_, except that a browser request result in an inline response rather than a file download. This is much more friendly to users and experimentation.

I'll describe all defaults and simplifications ... eventually.

## stations and observed properties ##

As illustrated below, this SOS service accepts both fully explicit and shorter, unqualified station (_procedure_ or _offering_, depending on request) and _observedProperty_ arguments; for example:
  * **station.** _procedure_ key in DescribeSensor and _offering_ key in GetObservation. Fully explicit urn: _urn:ioos:station:nanoos:ORCA\_Hoodsport_. Unqualified value: _ORCA\_Hoodsport_. RThe latter corresponds to the _NANOOS/NVS asset id_. **Rant:** BTW, this is a good place to remind ourselves that when dealing with horizontally fixed in situ stations, we're confronted with a confusing set of terms related to a station, depending on context: SWE/SOS use the abstract, ambiguous, overlapping terms _procedure_ and _offering_; in other contexts (eg, SensorML), _station_ and _platform_ are used. It's possible to use all 4 terms to refer to exactly the same thing!
  * **observedProperty.** Fully explicit urn: _http://mmisw.org/ont/cf/parameter/sea_water_temperature_. Unqualified value: _sea\_water\_temperature_. Only _CF names_ are currently accepted.

The use of NANOOS/NVS asset id's allows for direct URL-based linking to NVS, such as:
  * Go to the asset infowindow (pop up) on NVS: http://www.nanoos.org/nvs/nvs.php?section=NVS-Assets&infoWindow=action::auto_open||asset_class::siso||asset_id::ORCA_Hoodsport
  * Use the NVS light-weight JSON web services to request the asset's latest observations for all variables: http://www.nanoos.org/nvs/services/get_asset_info.php?opt=recent_values&asset_type=siso&asset_id=ORCA_Hoodsport&var_id=all&units_mode=v1 . These RESTful services are used by the NVS mobile apps and other NANOOS regional data-transport services.

## date-time (eventTime) requests in GetObservation ##

Usage descriptions, assumptions, and limitations.

  * Only UTC requests are currently accepted. The response timestamp is also in UTC.
  * [ISO 8601 date-time string formatting](http://en.wikipedia.org/wiki/ISO_8601) is used. Example: 2011-11-17T23:14Z
  * Minutes and seconds must be specified. A request that only specifies the date will return an error.
  * Request types:
    1. **Latest observations.** When the _eventTime_ key is omitted, the latest observation is returned **(OOT)**. When the station and observed property are measured at multiple depths, the latest observation per depth is returned.
    1. **Specified interval.** Example: eventTime=2011-11-15T00:00Z/2011-11-17T23:00Z
    1. **Specified instant.** Example: eventTime=2011-11-15T00:00Z. The requested timestamp is 'buffered' by 5 minutes on each end.

## Station time period begin-end conventions ##

The GetCapabilities response is very useful as an initial, sparse catalog of what's available on the SOS service, specially information about each station: location (lat & lon), measured parameters, and time period available. The station (ie, _offering_) time period is found in the XML node _sos:Contents/sos:ObservationOfferingList/sos:ObservationOffering/sos:time_. The most comon convention used in IOOS SOS endpoints is the one that, by not defining an explicit _endPosition_, implies that the station is still active and collecting observations:
```
<gml:TimePeriod>
    <gml:beginPosition>2011-10-24T17:58:31Z</gml:beginPosition>
    <gml:endPosition indeterminatePosition="now"/>
</gml:TimePeriod>
```
It's a safe bet that in many, if not most, cases, _gml:endPosition indeterminatePosition="now"_ is used even when the station has been offline for an extended period. I'm not aware of any IOOS guidelines about this.

In the NANOOS SOS only the previous 60 days of data are available, but even when a station or a parameter in a station has been offline for >60 days, the last observed value and its timestamp are retained and are also available. The NVS database supporting this SOS service also uses a manually set "OFFLINE" flag to indicate that a station is currently offline; the reason behind it and expected time to reactivation are not machine interpretable. Taking this context into account, the NANOOS SOS adopted a convention with four parts:
  1. **At least one sensor on the station is functioning normally and continues to return observations at the expected sampling rate:**
    * _gml:beginPosition_: an explicit value is used; this value is typically 60 days ago, the start of the data cache available (_not_ the deployment start, which is not available!)
    * _gml:endPosition_: left blank and attributed with _indeterminatePosition="now"_, as illustrated above, to indicate that observation is ongoing.
  1. **Station is currently offline (_OFFLINE_ flag is set), and the last observation was reported within the previous 60 days:**
    * _gml:beginPosition_: an explicit value is used; this value is typically 60 days ago.
    * _gml:endPosition_: as with _gml:beginPosition_, an explicit value is used, corresponding to the last timestamp when an observation was reported.
  1. **Station is currently offline (_OFFLINE_ flag is set), and the last observation was reported more than 60 days ago but within the previous 180 days:**
    * _gml:beginPosition_ and _gml:endPosition_ use explicit, identical values, corresponding to the last timestamp when an observation was reported.
  1. **Station is currently offline (_OFFLINE_ flag is set), and the last observation was reported more than 180 days ago:** In this case, it's assumed that the station has been removed permanently or not coming back any time soon, so it's excluded from the SOS service altogether.
## Data encodings available ##

GetObservation data responseFormat options: text/plain, text/csv, application/xml. Explain each, provide examples (links, in-line text) and relevant documentation (IOOS CSV doc).

## Sample requests and responses ##

All these examples are currently based on multi-depth (profiling) platforms. Explanations will be added later.

  1. **GetCapabilities**
    * Fully explicit request:  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&version=1.0.0&request=GetCapabilities
    * Minimalist version, with defaults:  http://habu.apl.washington.edu/pyws/sos.py
    * Request just the OperationsMetadata section of the GetCapabilities response:  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&request=GetCapabilities&sections=OperationsMetadata
  1. **DescribeSensor**
    * Fully explicit request:  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&version=1.0.0&request=DescribeSensor&procedure=urn:ioos:station:nanoos:ORCA_Hoodsport&outputFormat=text/xml;subtype="sensorML/1.0.1"
    * Minimalist version, with defaults and short names (not full urn's):  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&request=DescribeSensor&procedure=ORCA_Hoodsport
  1. **GetObservation**
    * Fully explicit request, for latest data:  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&version=1.0.0&request=GetObservation&offering=urn:ioos:station:nanoos:ORCA_Hoodsport&observedProperty=http://mmisw.org/ont/cf/parameter/sea_water_temperature&responseFormat=text/plain
    * Minimalist version, with defaults and short names (not full urn's):  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&request=GetObservation&offering=ORCA_Hoodsport&observedProperty=sea_water_temperature
    * Another Minimalist request, but specifying a time interval:  http://habu.apl.washington.edu/pyws/sos.py?service=SOS&request=GetObservation&offering=ORCA_Twanoh&observedProperty=mass_concentration_of_oxygen_in_sea_water&eventTime=2011-11-16T00:00Z/2011-11-18T23:00Z

# Miscellaneous Notes #

  * The NANOOS SOS GET requests are exhaustively case-insensitive. All keys and some values are case insensitive; eg, request=GetObservation and REQUEST=getobservation will both work. [See this email thread with Eric Bridger for context.](https://groups.google.com/forum/#!msg/ioostech_dev/xMp3zuXcLHQ/BwnMWRIu-BQJ)
  * The XML responses all use explicit namespace prefixes. Namespace defaults are never used.
  * This code has no direct relationship to the [older Python SOS server that was also developed by CMOP / NANOOS, around 2007/2008](http://www.oostethys.org/downloads/sos-cookbook-python/pysos-version-0.1); That code is basically orphaned, as far as we know.

## Limitations ##

  * An important current limitation has nothing to do with the code itself, but with the data store behind it: only the previous 60 days of data are available.
  * WMO Station ID's are not used at this time.
  * Only GET requests are implemented. POST requests are not implemented, and there are no near-term plans to do so.
  * Limitations of this SOS code are mainly related to GetObservation:
    * only one offering (1 station) and one observedProperty (measured parameter) can be requested at a time
    * BBOX parameter is not implemented
    * the only "standard" data encoding response available is the IOOS CSV specification
    * vector observedProperty requests (eg, Winds) are not implemented.

## Footnotes ##

**(OOT)** = An [OOSTethys](http://oostethys.org/) convention.