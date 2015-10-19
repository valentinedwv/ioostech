### Musings on identifying IOOS Assets using GC, DS, GC ###

<b>Situation:</b> Asset owned by RA1<br>
<b>Anticipated Result:</b> operatorSector in DS is...?<br>
<b>Resolution:</b> We allow the RAs to choose their sector, whether it is a non-profit or academic?<br>
<br>
<b>Situation:</b> Asset located in RA1, but data provided through RA2 and RA1<br>
<b>Anticipated Result:</b> For the RA2 responses, keyword in GC is RA2.  parentNetwork in DS is also RA2.  Does a field contain RA1?<br>
<b>Resolution:</b> We encourage that RA2 also puts RA1 in the parentNetwork<br>
<br>
<b>Situation:</b> Asset owned by ACE, operated by SCRIPPS, provided by RA1<br>
<b>Anticipated Result:</b> Keyword in GC is RA1, operatorSector in DS is academic, publisher in DS is RA1.  Where is ACE listed?<br>
<b>Resolution:</b> We require that the RA includes any federal affiliation in the parentNetwork.<br>
<br>
<b>Situation:</b>  Asset owned/operated by SCRIPPS, data provided by NDBC<br>
<b>Anticipated Result:</b> operatorSector in DS is academic.  Publisher is likely listed as NDBC, parentNetwork may be SCRIPPS and RA and NDBC.<br>
<b>Resolution:</b> For any re-served data, we require that the original data providers and the RA are listed in the parentNetwork.<br>
<br>
<i>Note:</i> Do we want to include PlatformMobility and PlatformEnvironment in the DS templates?  Ideally the PlatformEnvironment could be derived from the PlatformType, but the PlatformMobility maybe cannot.  This is probably for v1.1<br>
<br>
<i>Note:</i> Not sure if I should be surprised by this, but the gml:id in GC is not specified using a URN.  Yet, the sml:id in DS is specified using a URN.  Conversely, the gml:name in GC and DS is specified using a URN and the sml:name in DS is not necessarily specified using a URN.<br>
<br>
<i>Note:</i> Where do we include information about the QA/QC for certification, in addition to other reasons?  This is probably for v1.1<br>
<br>
<i>Note:</i> Do we need a seasonal flag or a non-real time sensor flag?<br>
<br>
<i>Note:</i> I think we need a placeholder for the WMO ID<br>
<br>
<i>Note:</i> I'll be starting an asset inventory page with requirements, metadata fields, mappings to SOS, etc in the days to come.<br>
<br>
<br>
<h3>Useful Reports Generated From NGDC ISO Metadata in the Service Registry</h3>

A record in the registry is one dataset for DAP services but a service endpoint (containing multiple datasets) for SOS services.  Will need a way of combining DAP datasets when creating summary reports<br>
<br>
<br>
<h3>Musings on Platform Vocabularies</h3>

One issue is that many shore stations contain water measurements and met measurements, such as the Puerto Rico Seismic Network which takes water levels and met obs. How do we classify these stations?