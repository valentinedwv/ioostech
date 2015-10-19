# Introduction #

Options to consider for how to represent RA affiliation and other metadata in DescribeSensor responses.


# SensorML Specification Discussion #

OGC SensorML spec doesn't restrict the naming of _identifier_ or _classifier_ elements within the SensorML 'Metadata Group' section.  More info, see SensorML spec (section 10.5.1): http://portal.opengeospatial.org/files/?artifact_id=21273.

The  _identifier@name_ or _classifier@name_ can be any value, currently those in use for _identifier_ (from CO-OPS) include 'Station ID', 'Short Name', and 'Long Name'.  For classifier, they include (CO-OPS) 'Parent Network', 'System Type Name', 'System Type Identifier', and (NANOOS/NDBC) 'Platform Type'.

SensorML defines sub-elements of _identifier_ and _classifier_ a _Term_ element with an optional _@definition_ attribute.  _Term_ contains a _value_ element to represent the actual value.  _Term_ can optionally include a _codeSpace_ element to reference a dictionary or ontology to constrain the choices for the _value_ element.  The same is true for the _KeywordList_ element, which optionally includes a _@codespace_ attribute and can include unconstrained _keyword_ sub-elements or a constrained set of keywords defined within an ontology or dictionary referenced by _@codespace_.

## Use of _classifier_ and _keywords_ in IOOS SOS Services ##

Presently, the _@codespace_ restriction is used by CO-OPS and NANOOS for the 'System Type Identifier' classifier to refer to the Marine Metadata Initiative 'platform' ontology at http://mmisw.org/ont/mmi/platform.

Example:
```
<sml:classifier name="System Type Identifier">
<sml:Term definition="urn:ioos:def:classifier:NOAA::systemTypeID">
        <sml:codeSpace xlink:href="http://mmisw.org/ont/mmi/platform/"/>
	<sml:value>Platform</sml:value>
</sml:Term>
</sml:classifier>
```

Example of _KeywordList_ using _@codeSpace_ GCMD ontology/dictionary reference from CO-OPS:

```
<sml:keywords>
	<sml:KeywordList codeSpace="http://gcmd.nasa.gov/Resources/valids/archives/keyword_list.html">
		<sml:keyword>OCEAN PLATFORMS</sml:keyword>
		<sml:keyword>Oceans > Tides > Tidal Currents</sml:keyword>
	</sml:KeywordList>
</sml:keywords>
```

I don't think any validation is provided against any ontologies or dictionaries referenced in _KeywordList_ or _Term_ elements in SensorML (the GCMD codeSpace referenced above in the CO-OPS response is not a structured document), however creating a dictionary (or codeList in ISO terminology) might have some value in solving issues of identifying RA or other affiliation within DescribeSensor SensorML responses.  At least if they were accessible by URL they could be referenced by clients in parsing DescribeSensor responses to obtain a list of valid values.


# Suggested Solution: #

**_(comments welcome)_**

If the working group could define a set of classifiers (ie _@name_ s) to use for IOOS SOS services and a list of acceptable values, and this could be hosted at an appropriate web host (ie ioos.gov), the DescribeSensor responses could uniformly refer to this dictionary.  Or, where appropriate, extending or working within the Marine Metadata Interoperability ontology platform to use established ontologies for classifiers.

Based on the SensorML spec, and also for easier parsing, I'd recommend using camelCase _@name_ attributes for both _classifier_ and _identifier_ elements.

Examples:

```
<identifier name=”stationID”>
<identifier name=”shortName”>
<identifier name=”longName”>
...

<classifier name=”parentNetwork”>
<classifier name=”owner”>
<classifier name=”operator”>
<classifier name=”publisher”>
<classifier name=”platformType”>
<classifier name=”systemTypeIdentifier”>
<classifier name=”systemTypeName”>
… … 
```

Detail:
```
<sml:classifier name="parentNetwork">
      <sml:Term definition="urn:ioos:def:classifier:NOAA:parentNetwork">
            <sml:codeSpace xlink:href="http://ioos.gov/ont/ra_abbrev/"/>
            <sml:value>AOOS</sml:value>
      </sml:Term>
</sml:classifier>
```


These values might be used in conjunction with the _contact_ elements in SensorML, which have more options for providing detailed contact info following roughly the ISO 19115 _ResponsibleParty_, _Person_, and _ContactList_ models.  I don't know the best way to go about making this association, because the contact element can only be qualified by using the existing 'xlink:role' URN attribution currently used across the IOOS SOS services.