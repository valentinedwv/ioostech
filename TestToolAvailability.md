



# Test tool availability #

| **Test** | **Required** | **Tested by OGC tool** | **Comments**|
|:---------|:-------------|:-----------------------|:------------|
| GetCapabilities, GET method| yes          | yes                    |             |
| GetCapabilities, POST method| yes          | no                     | [various options available for 52North](https://wiki.52north.org/bin/view/SensorWeb/SosTutorial) |
| DescribeSensor, GET method | yes          | no                     |             |
| DescribeSensor, POST method | yes          | yes                    | [test available for 52North](http://sensorweb.demo.52north.org/52nSOSv3.2.1) |
| GetObservation, GET method | ?            | no                     |             |
| GetObservation, POST method | yes          | yes                    | [various options available for 52North](http://sensorweb.demo.52north.org/52nSOSv3.2.1) |
| GetObservation with "result" parameters/filters | yes          | no                     | [various options available for 52North](http://sensorweb.demo.52north.org/52nSOSv3.2.1) |
| DescribeFeatureType | ?            | no                     |             |
| DescribeObservationType | ?            | no                     |             |
| DescribeResultModel | no           | no                     |             |
| GetObservationById | no           | no                     |             |
| GetResult | no           | no                     |             |
| GetFeatureOfInterest | no           | no                     |             |
| GetFeatureOfInterestTime | no           | no                     |             |
| InsertObservation | no           | no                     |             |
| RegisterSensor | no           | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |
|          |              | no                     |             |



## List of OGC SOS v1.0 [r6](https://code.google.com/p/ioostech/source/detail?r=6) tests ##

### OWS Common Tests ###

  * owsTests:ows-main
    * Assertion: Run test group for GetCapabilities requests using the GET method.
  * owsTests:ows-OWS.GetCapabilities.1
    * Assertion: The GET method request must be supported (using HTTP GET). Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root element matches the provided root element.
  * owsTests:ows-OWS.ContentType.1
    * Assertion: A response message containing an entity body must contain a Content-Type entity header field that correctly indicates the media type of the message body. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document matches the root element name; (3) the response Content-Type header must be "text/xml" for XML entities.
  * owsTests:ows-OWS.GetCapabilities-Exceptions.1
    * Assertion: In the event that a GetCapabilities request cannot be processed for any reason, the response entity shall include an exception report. The exception code must be one of those listed in Table 5 in the specification document. GetCapabilities with no _**service**_ parameter and _**version**_ parameter equal to 1.0.0.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue" exception code; (4) theExceptionReport @locator value shall be that of the missing parameter.
  * owsTests:ows-OWS.GetCapabilities-Exceptions.2
    * Assertion: In the event that a GetCapabilities request cannot be processed for any reason, the response entity shall include an exception report. The exception code must be one of those listed in Table 5. GetCapabilities with a bogus _**service**_ parameter value (ADSF), and _**version**_ parameter equal to 1.0.0.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the 'InvalidParameterValue' exception code; (4) theExceptionReport @locator value shall be that of the invalid parameter.
  * owsTests:ows-OWS.GetCapabilities-Exceptions.3
    * Assertion: In the event that a GetCapabilities request cannot be processed for any reason, the response entity shall include an exception report. The exception code must be one of those listed in Table 5. GetCapabilities with _**service**_ parameter SOS, _**version**_ parameter 1.0.0, and bogus AcceptVersions parameter value “2000-01-01”.
  * owsTests:ows-OWS.GetCapabilities-Exceptions.5
    * Assertion: In the event that a GetCapabilities request cannot be processed for any reason, the response entity shall include an exception report. The exception code must be one of those listed in Table 5. GetCapabilities with an incorrect KVP query string `http://SOS-server-URL/sos?request~GetCapabilities!service~!SOS`, triggering the missing parameter value exception.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue" exception code, for both the request and service.
  * owsTests:ows-OWS.CaseInsensitiveKvpNames.1
    * Assertion: Parameter names in KVP strings shall be handled in a case-insensitive manner. GetCapabilities with the KVP parameter names in all uppercase, lower-case and mixed-case.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root element matches the provided root element.
  * owsTests:ows-OWS.GetCapabilities-AcceptVersions.1
    * Assertion: If AcceptVersion is not specified, the service must respond with highest supported version. GetCapabilities with no version and service of "SOS". Without AcceptVersion, using version negotiation, sends latest copy.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an sos:SOS\_Capabilities document; (3) the response version must be what was requested
  * owsTests:ows-OWS.GetCapabilities-AcceptVersions.2
    * Assertion: Version negotiation using _**AcceptVersions**_ parameter (preference ordering) must return service metadata corresponding to the most preferred version that is supported. If none of the requested versions are supported, the server must generate an exception with code 'VersionNegotiationFailed'. GetCapabilities with no version and service of "SOS".  With AcceptVersion, expecting one of the versions listed $acceptVersions.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an sos:SOS\_Capabilities document; (3) the response version must be what was requested. The AcceptVersion element is used with a number of versions, one is expected to return ('1.1.0').
  * owsTests:ows-OWS.GetCapabilities-AcceptVersions.3
    * Assertion: Version negotiation using AcceptVersions parameter (preference ordering) must return service metadata corresponding to the most preferred version that is supported. If none of the requested versions are supported, the server must generate an exception with code 'VersionNegotiationFailed'. GetCapabilities with no _**version**_, _**service**_ of "SOS", and bogus _**AcceptVersion**_ number "2000-01-01" `http://SOS-server-URL/sos?request=GetCapabilities&service=SOS&acceptversions=2000-01-01`. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "VersionNegotiationFailed" exception code.
  * owsTests:ows-OWS.GetCapabilities-Sections.1
    * Assertion: The response to a GetCapabilities request that includes a sections parameter with NO VALUE provided shall include an abbreviated capabilities document that omits all optional sections `http://SOS-server-URL/sos?service=SOS&request=GetCapabilities&sections=`. Pass if the response is schema valid and omits all optional top-level elements.
  * owsTests:ows-OWS.GetCapabilities-Sections.2
    * Assertion: The response to a GetCapabilities request that includes a sections parameter listing optional elements _**ServiceIdentification**_ and _**OperationsMetadata**_ shall include only the requested elements in the response entity `http://SOS-server-URL/sos?service=SOS&request=GetCapabilities&sections=ServiceIdentification,OperationsMetadata`. Pass if the response is schema valid and includes only the requested optional elements.
  * owsTests:ows-OWS.GetCapabilities-AcceptFormats.1
    * Assertion: The response to a GetCapabilities request containing an _**AcceptFormats**_ parameter specifying a supported format must include a response entity that corresponds to the requested media type. Examples: (1)`http://SOS-server-URL/sos?service=SOS&request=GetCapabilities&acceptformats=text/xml` and (2)`http://SOS-server-URL/sos?service=SOS&request=GetCapabilities&acceptformats=application/zip`. Pass if the response is schema valid and _**Content-Type**_ equals requested media type.


### General SOS Tests ###

  * sos:general-SOS.General-InvalidRequest.1
    * Assertion: Sending a POST request that is non-conformant to a schema associated with an SOS operation (with “test” in the body) causes the server to return a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue" exception code.
  * sos:general-SOS.General-ValidResponse.1
    * Assertion: A response is a valid response for the SOS. This general assertion is tested by all other tests, so there is nothing specific to test now.


### Core SOS Tests ###

A request for a valid capabilities document is made with the optional "version" parameter omitted, and a response is validated with the schema. Further tests are performed on the GetCapabilities response only if the response passes schema validation.

#### `GetCapabilities Tests` ####

  * getCapabilities:core-SOS.GetCapabilities-KVPRequestParameterHandling.1
    * Assertion: GetCapabilities request with missing mandatory parameters _**service**_ and _**version**_ returns a valid error report message.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue" exception code.
  * getCapabilities:core-SOS.GetCapabilities-KVPRequestServiceParameterHandling.1
    * Assertion: GetCapabilities request with no _**version**_ parameter and a bogus _**service**_ parameter value of “XYZ” returns a valid error report message.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the " InvalidParameterValue" exception code.
  * getCapabilities:core-SOS.GetCapabilities-KVPRequestRequestParameterHandling.1
    * Assertion: Request with no _**version**_ parameter and a bogus _**request**_ parameter value of “GetMeASandwich” returns a valid error report message.  Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the " InvalidRequest" exception code.
  * getCapabilities:core-SOS.GetCapabilities-OperationsMetadataMandatoryOperations.1
    * Assertion: The OperationsMetadata section of the GetCapabilities response lists the mandatory operations of the SOS.
  * getCapabilities:core-SOS.GetCapabilities-OperationsMetadaOptionalOperations.1
    * Assertion: Any non-mandatory operations advertised in the OperationsMetadata section of the GetCapabilities response have valid SOS method names.
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidTime.1
    * Assertion: The values in the _**time**_ element for each ObservationOffering are valid time values (ISO 8601) or are valid named times (i.e. indeterminate, now, etc.).  If a time period is specified, then the “beginTime” value must come before the “endTime” or be equal to the “endTime” value.
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidProcedure.1
    * Assertion: The values in the _**procedure**_ element(s) for each ObservationOffering contain a value and are valid URNs.
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidObservedProperty.1
    * Assertion: The values in the _**observedProperty**_ element(s) for each ObservationOffering contain a value and are valid URNs, or valid URLs, e.g. for CF/MMI phenomenon names (see document OGC 05-010 for correct formatting of definition URN).
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidResponseFormat.1
    * Assertion: The values in the _**responseFormat**_ element(s) for each ObservationOffering contain a value and are valid MIME types.
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidResultModel.1
    * Assertion: If an ObservationOffering provides the _**resultModel**_ element, then the _**resultModel**_ element must be in the om:Observation substitution group and is typically om:Observation or a specialized extension.  Value must be namespace-qualified.
  * getCapabilities:core-SOS.GetCapabilities-ResponseContentsValidResponseMode.1
    * Assertion: If an ObservationOffering provides the _**responseMode**_ element, then the _**responseMode**_ element contains a value that is one of the valid responseMode values.

#### `DescribeSensor Tests` ####

  * describeSensor:core-SOS.DescribeSensor-RequestInvalidMIMEType.1
    * Assertions: A DescribeSensor request with no _**outputFormat**_ parameter as well as with a bogus _**outputFormat**_ parameter value that is not advertised in the capabilities document (e.g. “text/xml;subtype="sensorML/A.B.C"”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue " exception code for missing _**outputFormat**_; (4) the ExceptionReport shall have the "InvalidParameterValue" exception code for bogus _**outputFormat**_ value.
  * describeSensor:core-SOS.DescribeSensor-RequestInvalidProcedure.1
    * Assertion: A DescribeSensor request with no _**procedure**_ parameter as well as with a bogus _**procedure**_ parameter value that is not advertised in the capabilities document (e.g. “urn:ogc:object:procedure:CITE:NFL:AstroDome”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "MissingParameterValue " exception code for missing _**procedure**_; (4) the ExceptionReport shall have the "InvalidParameterValue" exception code for bogus _**procedure**_ value.
  * describeSensor:core-SOS.DescribeSensor-ResponseMatchingResponseFormat.1
    * Assertion: The format of the response document matches the _**outputFormat**_ specified in the request and is valid according to the _**outputFormat**_ schema.
  * describeSensor:core-SOS.DescribeSensor-ResponseMatchingProcedure.1
    * Assertion: The unique identifier in the response document matches the procedure URN specified in the request.

#### `GetObservation Tests` ####

All GetObservation tests use the "Post" method at the URL obtained from the GetCapabilities response.

  * getObservation:core-SOS.GetObservation-RequestInvalidSRSName.1
    * Assertion: A GetObservation request with a bogus _**srsName**_ parameter value that is not advertised in the capabilities document (e.g. “urn:ogc:def:crs:EPSG:9999”) produces a valid error message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidOffering.1
    * Assertion: A GetObservation request with a bogus _**offeringId**_ parameter value that is not advertised in the capabilities document (e.g. “softliness\_of\_jello”) produces a valid error message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidEventTime.1
    * Assertion: A GetObservation request with an invalid _**eventTime**_ parameter (e.g. bogus _**timePosition**_ parameter value of “scooby”) produces a valid error message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidProcedure.1
    * Assertion: A GetObservation request with a bogus _**procedure**_ parameter value that is not advertised in the capabilities document (e.g. “urn:ogc:object:procedure:CITE:WeatherService:ThisIsInvalid”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidFeatureOfInterest.1
    * Assertion: A GetObservation request with one or more invalid _**featureOfInterest**_ values that are not advertised in the capabilities document (e.g. “urn:ogc:def:object:feature:TheInvalidFeature”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidObservedProperty.1
    * Assertion: A GetObservation request with one or more invalid _**observedProperty**_ values that are not advertised in the capabilities document (e.g. “urn:ogc:def:phenomenon:OGC:TheInvalidObservedProperty”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidResult.1
    * Assertion: A GetObservation request with an invalid _**result**_ parameter (e.g. using the comparison operator "ogc:PropertyIsEqualTo" with no value) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidResponseFormat.1
    * Assertion: A GetObservation request with a bogus _**responseFormat**_ parameter value that is not advertised in the capabilities document (e.g. “text/xml;subtype="XX"”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidResultModel.1
    * Assertion: A GetObservation request with a bogus _**resultModel**_ parameter value that is not advertised in the capabilities document (e.g. “TheBogusOne”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-RequestInvalidResponseMode.1
    * Assertion: A GetObservation request with a bogus _**responseMode**_ parameter value that is not advertised in the capabilities document (e.g. “NotValid”) produces a valid error report message. Pass if all of the following conditions are true: (1) the response is schema valid; (2) the root document is an ows:ExceptionReport document; (3) the ExceptionReport shall have the "InvalidParameterValue" exception code.
  * getObservation:core-SOS.GetObservation-ResponseMatchingSRSData.1
    * Assertion: If an _**srsName**_ parameter is supplied in the request, then the _**srsName**_ value of the response data is valid according to the format specified by the requested _**srsName**_.
  * getObservation:core-SOS.GetObservation-ResponseMatchingProcedureData.1
    * Assertion: GetObservation requests made for each _**procedure**_ element advertised in the capabilities document produce the responses with _**procedure**_ values that match or are a subset of the _**procedure**_ values specified in the requests.
  * getObservation:core-SOS.GetObservation-ResponseMatchingObservedPropertyData.1
    * Assertion: GetObservation requests made for each _**observedProperty**_ element advertised in the capabilities document produce the responses with _**observedProperty**_ values that match or are a subset of the _**observedProperty**_ values specified in the requests.
  * getObservation:core-SOS.GetObservation-ResponseAdvertisedEventTimeData.1
    * Assertion: A valid GetObservation request made for each offering advertised in the capabilities document with the advertised _**eventTime**_ for the requested offering returns one or more observations.
  * getObservation:core-SOS.GetObservation-ResponseMatchingEventTimeData.1
    * Assertion: A valid GetObservation request made for each offering advertised in the capabilities document with the _**eventTime**_ value that is off the advertised range for the requested offering (e.g. is before the earliest advertised _**beginPosition**_) returns no observations.
  * getObservation:core-SOS.GetObservation-ResponseMatchingFeatureOfInterestData.1
    * Assertion: A valid GetObservation request made for each _**featureOfInterest**_ advertised in the capabilities document produces the response with _**featureOfInterest**_ values that match or fall within the spatial extent identified in the _**featureOfInterest**_ value specified in the request.
  * getObservation:core-SOS.GetObservation-ResponseMatchingResultData.1
    * Assertion: If a valid filter value is supplied in the result parameter of the request, then the response O&M data is valid for that filter.
  * getObservation:core-SOS.GetObservation-ResponseMatchingResponseFormatData.1
    * Assertion: The format of the response data matches the format supplied in the _**responseFormat**_ parameter of the request.