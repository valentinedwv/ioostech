

# Overview and Test Plan Objectives #

The IOOS SOS software reference implementations based on [i52n-sos](http://ioos.github.io/i52n-sos/) and [ncSOS](https://github.com/asascience-open/ncSOS/wiki) are ready to be used, and other implementations are in progress.  IOOS data providers that serve in situ data are making plans to implement one or more of these solutions at their locations.  Once these services are installed within an IOOS data provider's domain, they will need to be tested to ensure the SOS responses and data formats conform to specifications.

**_For now, these tests are intended to be initial service deployment tests, and are not intended to be automated or recurring service validation tests.  Based on the results of these tests we may choose to build automated and/or recurring service validation tests._**

**_Further, this Test Plan will not be applied to the initial 'system test surrogate' installations. Rather, a series of more basic operations will be applied to determine whether that 'system testing' has passed._**

The objective of this test plan is to describe the overall testing strategy and to define how each data provider's service endpoint will be tested. This test plan will describe the following:

  * Scope of the tests to be conducted
  * Roles and responsibilities
  * Testing process, methods and required tools
  * Success criteria for each test performed
  * Methodology for reporting defects or anomalies
  * Methodology for configuration management and version control
  * Format and content of Test Reports

The final section of the plan is intended to be used as a repository for ideas for additional test tools, scripts, etc.  This section should be augmented during test execution, and will potentially be used as requirements for future tool development.


# Roles and Responsibilities #

| **Role** | **Responsible Org/Individual** |
|:---------|:-------------------------------|
|Test Authority|Derrick Snowden                 |
|Test Manager|Alex Birger                     |
|Tester    |Varies based on test, likely Alex Birger will do majority|
|Software-related Issues|52N-Shane, ncSOS-Kyle, python-Emilio|
|Installation or data-related Issues|RA or Fed DMAC POC              |
|Test Reports|Alex Birger                     |


# Process #

The general process is as follows:
  1. Data provider POC announces a service endpoint is ready for testing, supplies the following information:
    1. Endpoint URL
    1. Software release or version number
    1. Point of contact for test-related issues
  1. Tester(s) execute tests on service. Defects are identified and logged in defect reporting system ([Issues](https://code.google.com/p/ioostech/issues/list) portion of ioostech).
  1. Defects are investigated and addressed by appropriate individual.
  1. Software or system updates are performed as needed to correct issues identified during testing.
  1. Test Manager determines which tests need to be re-run, testing is re-done.
  1. Process continues until Test Manager determines:
    1. Service passed tests
    1. Service cannot be further tested
  1. Test results are documented in Test Report.
  1. Test Authority makes final determination of service Pass or Fail.


# SOS Service Test States #

Throughout the test process, services will transition through several states, as defined below.  The [Fielding Plan (dashboard)](RABuildout.md) will be updated weekly to reflect the latest state of each service.

| **State** | **Meaning** |
|:----------|:------------|
|Pending    |Service is not ready for testing|
|Ready for Test|Service is available for test, testing has not begun|
|In Progress|Testing is underway|
|Hold       |Testing identified defects; awaiting resolution before testing can continue|
|Complete-Success|Testing is complete and success criteria was met|
|Complete-Fail|Testing is complete, service did not meet success criteria|


# Test Methods and Success Criteria #

The sections below provide a high level description of the tests to be conducted.  A individual test is considered successful if the test outcome matches the Expected Result.


## Test 1: Service Registered in IOOS Service Registry ##

**Test Goal:** Verify that the service is registered in the IOOS Service Registry.

**Test Method:**  Find service in NGDC service registry using the existing web interface.

**Expected Result:** Service under test is in the service registry and can be harvested.


## Test 2: OGC Compliance ##

**Test Goal:** Ensure that the service is compliant with selected OGC specifications.

**Test Object:** All installations of the 52N software. The ncSOS installations are excluded from the OGC Compliance testing process because a variety of OGC test components use HTTP POST method for requests while ncSOS does not support HTTP POST binding.

**Test Method:** The following tests will be performed using the OGC CITE test scripts:
  * [OWS Common Tests](ListofTestsIOOSSOS#1.1_OWS_Common_Tests.md)
  * [General SOS Tests](ListofTestsIOOSSOS#2_General_SOS_Tests.md)
  * [GetCapabilities Tests](ListofTestsIOOSSOS#3.1_GetCapabilities_Tests.md)
  * [DescribeSensor Tests](ListofTestsIOOSSOS#3.2_DescribeSensor_Tests.md)
  * [GetObservation Tests](ListofTestsIOOSSOS#3.3_GetObservation_Tests.md)

**Expected Results:**
  * No catastrophic errors encountered
  * Tests marked as "IOOS Optional" may fail altogether.


## Test 3: IOOS SOS Convention (Profile) Compliance ##

**Test Goals:**

  * Validate that the service response is syntactically valid, i.e. the service response contain the expected elements and attributes in the order that is prescribed by the IOOS Milestone 1.0 templates as described in the [Web Services Description Document](https://ioostech.googlecode.com/files/IOOS%20SOS%20WSDD%20Draft%20v0.91.docx).
  * Validate that the service response semantically conforms to the IOOS SOS Convention, i.e. the meaning of variables, elements, attributes, etc. matches the description in the [CF Conventions v1.6](http://cf-pcmdi.llnl.gov/documents/cf-conventions/1.6/cf-conventions.html), [Web Services Description Document](https://ioostech.googlecode.com/files/IOOS%20SOS%20WSDD%20Draft%20v0.91.docx), and [IOOS Controlled Vocabularies](ControlledVocabularies.md).

**Test Method:**
For each SOS Milestone 1.0 implementation -
  1. Issue GetCapabilities, DescribeSensor, or GetObservation request and capture XML response document.
  1. Using Oxygen XML Editor (or similar tool), perform validation of the response document against the [IOOS XML Schema](https://code.google.com/p/ioostech/source/browse/#svn%2Ftrunk%2Ftemplates%2FMilestone1.0%2FSchemas%253Fstate%253Dclosed), and verify that the response passes a series of the syntactic and semantic [IOOS-specific tests for SOS Milestone 1.0](ListofTestsIOOSSOS.md).

**Expected Result:**
  * Output files validate against schema.
  * Output files pass the [IOOS-specific tests for SOS Milestone 1.0](ListofTestsIOOSSOS.md).

## Test 4: Quantity of Offerings ##

**Test Goal:** Verify that the service contains an appropriate quantity of a data provider's _in situ_ data offerings.  The goal is to have 80% of available offerings accessible from the service.

**Test Method:** Execute GetCapabilities operation on the service to determine how many datasets are served.  Report results to the appropriate DMAC coordinator and determine percentage of offerings that are served through the SOS.

**Expected Result:** At least 80% of data provider's offerings are served through the SOS.


# Defect Reporting #

Any issues encountered during testing will be logged in the Issues section of the [wiki](https://code.google.com/p/ioostech/issues/list).

The defect list will be reviewed weekly by the Test Manager and IOOS DMAC personnel at the weekly DMAC Project Management meeting.

_How do we "assign" a defect to an individual?_
_Should we use Labels as a way to categorize the issues?_


# Configuration Management #

The software implementations have version numbers that are provided when the service endpoint is reported to be ready for test.  Testers will track software versions when running tests and reporting defects or issues.


# Test Report Format #

No standalone test reports are planned for this series of tests.  Existing reporting mechanisms will be used to report progress, including:
  * [Defect reports logged and tracked as wiki Issues](https://code.google.com/p/ioostech/issues/list)
  * The [SOS Buildout](https://sites.google.com/a/noaa.gov/ioos/collaboration-tools/dmac/fy2013/sosbuildout) status intranet page


# Future Test Tool Needs/Requirements #

Include here ideas for test tools, scripts, utilities, etc that would enhance or automate the testing process.


---
