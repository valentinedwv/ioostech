# Introduction #

NDBC has added the new SWE [GetObservation](GetObservation.md) response formats to its public test site.  This site may be reached at http://sdftest.ndbc.noaa.gov/sos/.

# Issues/Questions #

  1. The templates do not include placeholders for station id and sensor id.  These ids/URNs are useful in making [DescribeSensor](DescribeSensor.md) calls to obtain metadata.  The NDBC responses do include these fields, but feedback on proper usage is invited.
  1. How should composite phenomena be handled?  NDBC has coded the fields into the SWE record definitions within the responses similar to what CO-OPS has done in their sample templates and how NDBC has coded these responses in the past.  Do we have valid property names for these composite phenomena?  Any guidance would be helpful.
  1. How to code quality flags in SWE the response?  NDBC uses two types of flags - Environmental Quality Control (EQC) flags (or hard flags) which prohibit the release of data to the GTS and Data Quality Analyst (DQA) flags (or soft flags) which simply warn the data analysts of potential problems.  These flags are listed at http://sdftest.ndbc.noaa.gov/sos/qcflags.shtml.  There may be zero or one EQC flags present with the data, however, there may be zero or more DQA flags present.  How should the possible multiple DQA flags be handled in the SWE response?  Additional information on NDBC quality control may be found at http://www.ndbc.noaa.gov/NDBCHandbookofAutomatedDataQualityControl2009.pdf.
  1. Do we code station elevation and sensor elevation in the response?  Or does sensor elevation belong in [DescribeSensor](DescribeSensor.md) response?  If we code both, then can sensor elevation be a simple offset (defined as http://mmisw.org/ont/cf/parameter/height) from the station elevation?

# Progress #

The initial SWE changes were implemented into the NDBC public test at http://sdftest.ndbc.noaa.gov/sos/ on March 15, 2012.