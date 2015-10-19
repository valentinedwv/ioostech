# Notes and To-Do's for SOS Reference Implementation, Summer 2012 #

## urn conventions, identifiers ##

We've made several changes and updates to the previously published (in draft form) IOOS naming conventions for station and sensor id urn's. That documentation will be updated, but for now, here are pointers to the main, relevant ioostech Issues:
  * [Issue 3: URN vs URL](http://code.google.com/p/ioostech/issues/detail?id=3)
  * [Issue 5: URN syntax for platform/stations identifiers](http://code.google.com/p/ioostech/issues/detail?id=5)
  * [Issue 24: Change "NOAA" in def:identifier, def:classifier urn's to "IOOS"](http://code.google.com/p/ioostech/issues/detail?id=24)
  * [ioostech\_dev discussion: Standardizing sensor asset urn component text?](https://groups.google.com/d/topic/ioostech_dev/Qj6hBy52FPU/discussion)

Related discussions on the ioostech\_dev list and on other Issues are mentioned and linked from there.


---

**OLD. Will update/remove eventually**

# Introduction #

This is my main public brain dump, to help me guide the crafting of more organized wiki contents (including other pages) addressing a range of issues relevant to the IOOS DMAC Reference Implementation focus. Most of this material will be based on recent or ongoing discussions, and in challenges and solutions that have come up in the development of the [new NANOOS "NVS" SOS service](NANOOSNVSPythonSOS.md).

# To-Do's #

  1. IOOS conventions we've re-discovered or agreed on recently, including links to important documents (eg, [IOOS Conventions for CSV Encoding](http://code.google.com/p/ioostech/downloads/detail?name=IOOS_Conventions_for_CSV_Encoding_v101.doc), [IOOS Conventions for Asset Identifiers (including station & sensor urn conventions)](http://code.google.com/p/ioostech/downloads/detail?name=IOOS_Conventions_for_Asset_Identifiers_2011-01-21_dps.docx), adoption of CF names for measurements)
  1. Semantics of GetObservations requests: meaning and usage of _offering, procedure, observedProperties_, etc
  1. Development of a reasonable but unofficial DescribeSensor SensorML response
  1. Mention and link to Ted Habermann's ISO XML metadata created dynamically via XSL mapping from the GetCapabilities response.

# My other wiki pages #

Other ioostech wiki pages I've created and manage. I've also [assigned them the 'NANOOS' tag](http://code.google.com/p/ioostech/w/list?q=label:NANOOS), but this index here makes it easier to track them.

  * [NANOOSNVSPythonSOS](NANOOSNVSPythonSOS.md)
  * [EmilioControlledVocabs](EmilioControlledVocabs.md) Some pointers, links and initial thoughts on Controlled Vocabularies, including ones for platform or station types in SensorML
  * [CanadianAssetsIOOSNDBC](CanadianAssetsIOOSNDBC.md)