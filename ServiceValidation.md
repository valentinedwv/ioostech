


The US IOOS is developing and deploying the DMAC standards in order to ensure interoperable, quality-controlled ocean data that comes from various sources such as academia, federal agencies, private sector industries, or local governments. The standards shall be applied to the IOOS partners within the framework of the partners’ offerings quality verification process that should finally result in formal certification.
Both federal and non-federal partners’ offerings need to be verified for compliance with DMAC standards in order for the provided data to be included into the US IOOS system. Non-federal partners may use the DMAC compliance for civil liability protection or just to ensure interoperability, and the formal certification process may be an identified means of verifying compliance.

# Scope #

The DMAC service development is in progress, and is almost completed. The implementations are about to start. This regimen is intended to examine the service and content of the DMAC implementation.
The service validation seems to be an all-sufficient task, and can be done irrespective of other IOOS activity; however, since IOOS has carried out a development and implementation of the IOOS Registry, which among other functions is supposed to periodically probe partners’ services and harvest offered data, it would be highly beneficial to coordinate all testing activities (and especially any development of test tools) with IOOS Registry developers.
Formal verification of interoperability of data offerings is the core part of the compliance certification. The verification applies to both federal (NDBC, CO-OPS) and non-federal (RAs) partners, and includes series of tests of the partners’ offerings, as follows:

_TODO: Add text describing the differences between tests that are specific to OGC requiremenst and hence may be carried out by the OGC CITE tools and tests that are specific to IOOS requirements (e.g. use of vocabularies or use of correct identifier scheme).  Create another page for contributions of IOOS specific test._

  * **Data access service conformance** – verifies compliance with the OGC specification for SOS, SensorML, SWECommon, WMS, WCS, and OPeNDAP specification for DAP access service (it is assumed that both 52North and ncSOS varieties should be tested with the same tool):
    1. _SOS, WCS, WMS, and SensorML_ – test engine and scripts developed by the OGC Compliance and Interoperability Testing Initiative (CITE); currently goes through an extensive modification and enhancement process; its growing popularity results in a rapid errors and bugs identification and correction. The CITE scripts [do not test all features of the services](http://cite.opengeospatial.org/te2/about/sos/1.0.0/web); thus, more [test tool development](TestToolAvailability.md) is needed to fully cover the IOOS services functionality.<br>The following is list of currently available tests and their status:<br>
<table><thead><th> <b>Specification</b> </th><th> <b>Version</b> </th><th> <b>Revision</b> </th><th> <b>Status</b> </th></thead><tbody>
<tr><td>Geography Markup Language (GML)</td><td>3.2.1           </td><td>3.2.1-<code>r2</code> </td><td>Beta           </td></tr>
<tr><td>Sensor Model Language (SensorML)</td><td>1.0.1           </td><td><code>r2</code>  </td><td>Beta           </td></tr>
<tr><td>Sensor Observation Service (SOS)</td><td>1.0.0           </td><td><code>r6</code>  </td><td>Final          </td></tr>
<tr><td>Sensor Observation Service (SOS)</td><td>2.0             </td><td><code>r1</code>  </td><td>Beta           </td></tr>
<tr><td>Web Coverage Service (WCS)</td><td>1.0.0           </td><td><code>r5</code>  </td><td>Final          </td></tr>
<tr><td>Web Coverage Service (WCS)</td><td>1.1.1           </td><td><code>r1</code>  </td><td>Final          </td></tr>
<tr><td>Web Coverage Service (WCS)</td><td>2.0.1           </td><td><code>r2</code>  </td><td>Beta           </td></tr>
<tr><td>Web Coverage Service - Earth Observation Profile</td><td>1.0 (pending)   </td><td><code>r2</code>  </td><td>Beta           </td></tr>
<tr><td>Web Map Server (WMS) - Client</td><td>1.3.0           </td><td><code>r2</code>  </td><td>Beta           </td></tr>
<tr><td>Web Map Service (WMS) </td><td>1.1.1           </td><td><code>r3</code>  </td><td>Final          </td></tr>
<tr><td>Web Map Service (WMS) </td><td>1.3.0           </td><td><code>r4</code>  </td><td>Final          </td></tr></li></ul></li></ul></tbody></table>

No OGC CITE test for SWECommon is currently available, and probably will not been developed any time soon.<br>
<br>
<blockquote>2. <i>OPeNDAP</i> – no standard tests are available; verification may be done with simple tools like <a href='http://www.opendap.org/faq2#testMyServers'>Web browser and telnet client</a>.</blockquote>

<ul><li><b>Metadata conformance</b> – verifies compliance of metadata included in or accompanying requested datasets (files) with the IOOS endorsed standards (e.g. ISO-19115/19119/19139, CF Conventions, SensorML, vocabularies, etc.):<br>
<ol><li>observations and model results in netCDF<br>
<ul><li>visual analysis vs. <a href='http://www.nodc.noaa.gov/data/formats/netcdf/'>NODC templates</a> for each featureType;<br>
</li><li>threddsISO or ncISO service (rubric)<br>
</li><li><a href='http://puma.nerc.ac.uk/cgi-bin/cf-checker.pl'>CF-Convention Compliance Checker</a>;<br>
</li><li>else?<br>
</li></ul></li><li>observations in SWECommon (SOS Response)<br>
<ul><li>visual comparison with <a href='https://code.google.com/p/ioostech/source/browse/#svn%2Ftrunk%2Ftemplates%2FMilestone1.0%253Fstate%253Dclosed'>IOOS SOS templates Milestone 1.0</a>;<br>
</li><li>validation against <a href='https://code.google.com/p/ioostech/source/browse/#svn%2Ftrunk%2Ftemplates%2FMilestone1.0%2FSchemas%253Fstate%253Dclosed'>formal XML schemas</a> using XML Editor like Oxygen or specially developed validator;<br>
</li><li><a href='https://www.ngdc.noaa.gov/metadata/published/NOAA/IOOS/iso/index-secure.html'>rubric service at NGDC</a> or IOOS RCV<br>
</li><li>else?<br>
</li></ul></li><li>MMI-hosted ontology – proper ontology test tool (?); possibly just visual observation of the data samples and comparison with the vocabularies<br>
</li></ol></li><li><b>Data quality</b> – methods and test tools are not clear at the moment</li></ul>


<h1>Relevant documents and specifications</h1>

For the purposes of this testing, the controlling documents for the DMAC services are (the list is open):<br>
<ul><li>OGC SOS 1.0.0 Specification<br>
</li><li>OGC SOS 2.0 Specification (for Milestone 2.0)<br>
</li><li>OGC Observation & Measurement Specification<br>
</li><li>OGC Web Services Common Specification, Version 1.1.0 <code>[OGC 06-121r3]</code>
</li><li>OGC SensorML v1.0 Specification<br>
</li><li>OGC SWECommon Data Model v2.0 (mostly for Milestone 2.0)<br>
</li><li>OGC OWS, O&M, SOS, etc. XML schemas<br>
</li><li>Ontologies (vocabularies, definitions, etc.) (<a href='http://mmisw.org/orr/#b-http://mmisw.org/orr/'>http://mmisw.org/orr/#b-http://mmisw.org/orr/</a> and <a href='https://marinemetadata.org/references/ioosparameter-https://marinemetadata.org/references/ioosparameter'>https://marinemetadata.org/references/ioosparameter-https://marinemetadata.org/references/ioosparameter</a>)<br>
</li><li>SOS response templates (Milestone 1.0):<br>
<ul><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/OM-GetObservation.xml'>OM-GetObservation.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SML-DescribeSensor-Network.xml'>SML-DescribeSensor-Network.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SML-DescribeSensor-Station.xml'>SML-DescribeSensor-Station.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SOS-GetCapabilities.xml'>SOS-GetCapabilities.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-MultiStation-TimeSeries.xml'>SWE-MultiStation-TimeSeries.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-MultiStation-TimeSeries_QC.xml'>SWE-MultiStation-TimeSeries_QC.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-SingleStation-SingleProperty-TimeSeries.xml'>SWE-SingleStation-SingleProperty-TimeSeries.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-SingleStation-TimeSeriesProfile.xml'>SWE-SingleStation-TimeSeriesProfile.xml</a>
</li><li><a href='http://code.google.com/p/ioostech/source/browse/trunk/templates/Milestone1.0/SWE-SingleStation-TimeSeriesProfile_QC.xml'>SWE-SingleStation-TimeSeriesProfile_QC.xml</a>
</li></ul></li><li><a href='https://code.google.com/p/ioostech/source/browse/#svn%2Ftrunk%2Ftemplates%2FMilestone1.0%2FSchemas%253Fstate%253Dclosed'>IOOS XML Schemas for SOS Milestone 1.0 responses</a>
</li><li>List of entry points, and schedule of IOOS SOS implementation at the National Data Buoy Center (NDBC), Center for Operational Oceanographic Products and Services (CO-OPS), and 11 regions.</li></ul>


<h1>Test goals</h1>

The US IOOS test entity will use test tools – either standard and publicly available, or specifically developed for IOOS – to send requests to the services. The NBDC, CO-OPS, and RAs will be consulted to ensure that requests are reasonable and appropriate within the context of the DMAC Milestone 1.0.<br>
<br>
Service requests and responses will be documented and analyzed in order to demonstrate the consistency, or lack thereof, of the responses from the services.<br>
<br>
The following is the list of questions that validation should provide answers to, and available options of doing so. The list is by no means explicit, and should be revised and altered as needed:<br>
<ol><li>Service state, i.e. “Is the service online and sending out products?”<br>
<ul><li>OGC CITE standard test<br>
</li></ul></li><li>Service reaction to correct/incorrect requests, i.e. “To what degree is the service compliant with the OGC specification?”<br>
<ul><li>OGC CITE standard test (<a href='http://cite.opengeospatial.org/te2/about/sos/1.0.0/web/'>some requests are not tested</a>)<br>
</li></ul></li><li>Syntactic validity of the service response, i.e. “Does the service response contain all expected elements and attributes in the order that is prescribed by the OGC specification <b>AND</b> IOOS Milestone 1.0 templates?”<br>
<ul><li>OGC CITE standard test (<a href='http://cite.opengeospatial.org/te2/about/sos/1.0.0/web/'>some operations are not tested</a>)<br>
<ul><li>Visual comparison between IOOS SOS XML response document and respective Milestone 1.0 template, or<br>
</li><li>Validation of IOOS SOS XML response document with the respective XML Schema document (Schematron document?) – either manually with XML editor (e.g. Oxygen) or automatically with some scripts<br>
</li></ul></li></ul></li><li>Semantic validity of the service response, i.e. “Does the response metadata conform to standards, conventions, vocabularies, definitions, etc.?”<br>
<ul><li>Visual evaluation of the response<br>
</li><li>Rubric tool at <a href='https://www.ngdc.noaa.gov/metadata/published/NOAA/IOOS/iso/index-secure.html'>NGDC</a> or IOOS RCV (?)<br>
</li><li>else?<br>
</li></ul></li><li>Validity of data provided by the service, i.e. “Are the quantitative values retrieved from the service and their distribution as expected (believable), and comparable to values from other services (if applicable)?”<br>
<ul><li>Manual analysis of the “result” section of the GetObservation response<br>
</li><li>Automatic analysis (no automatic tool is available at the moment) (?)<br>
</li></ul></li><li>Data missing values provided by the service, i.e. “Does the data in response products contain missing values, and do the count and geographic distribution of these values match what is expected (original data product)?”<br>
<ul><li>Manual analysis of the “result” section of the GetObservation response, or<br>
</li><li>Automatic analysis (no automatic tool is available at the moment) (?)<br>
</li></ul></li><li>else?</li></ol>


<h1>Immediately Possible Test Activities</h1>

<ol><li>Run OGC SOS compliance <a href='TestToolAvailability.md'>test scripts</a>
</li><li>In addition, run 52North SOS <a href='http://sensorweb.demo.52north.org/52nSOSv3.2.1'>test tool</a> (assumed that this tool will work on either ncSOS or 52North implementations).<br>
</li><li>Perform validation of IOOS SOS responses using the <a href='http://code.google.com/p/ioostech/source/browse/#svn%2Ftrunk%2Ftemplates%2FMilestone1.0%2FSchemas'>schemas</a> developed from the Milestone 1.0 templates.<br>
</li><li>If possible, determine how real data offerings match data advertisement - use GetCapabilities and GetObservation responses - and then query the DMAC coordinator if that matches their intent.<br>
</li><li>If the RA is running both 52N and ncSOS, verify that both services behave the same way