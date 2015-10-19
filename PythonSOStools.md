

# Python SOS Data Services #

We're in the [Year of the Water Snake](http://en.wikipedia.org/wiki/Snake_%28zodiac%29) (Feb 2013 on). Big things are bound to happen in the world of Python services for [marine](http://en.wikipedia.org/wiki/Sea_serpent) and [hydrological](http://en.wikipedia.org/wiki/Giant_anaconda) data.

## Recent or upcoming events and opportunities ##

  * We'll try to set up an IOOS DMAC call focused on these Python-oriented topics
  * [SciPy 2013, Austin, June 24-29](http://conference.scipy.org/scipy2013/).
    * Great meeting! Several sessions were relevant and attended by a relevant crowd. Massimo Di Stefano (RPI/WHOI?) has [a nice overview and links](http://tw.rpi.edu/web/event/SciPy/2013/report), from a related perspective.
    * I organized a small, brief Birds of a Feather: [Data access and munging tools for oceanographic and hydrological applications](http://conference.scipy.org/scipy2013/bof_detail.php?id=50), attended mainly by Rich Signell, Alex Crossby, Dharhas Pothina, Andy Wilson, Philip Elson and Chris Barker. I wrote a [summary of the great discussions that focused on pyoos, ulmo, iris/cartopy and pagean](https://groups.google.com/d/msg/ioos_tech/ztzB5qEPpTc/SG2Uowoo_OQJ).
  * [4th Symposium on Advances in Modeling and Analysis Using Python, 2014 AMS Annual Meeting, Atlanta, 2-6 Feb 2014](http://annual.ametsoc.org/2014/index.cfm/programs-and-events/conferences-and-symposia/fourth-symposium-on-advances-in-modeling-and-analysis-using-python/). (abstract deadline has already passed). Follow-up to previous AMS (American Meteorological Society) symposia with great presentations, [including the 2013 one in Austin](http://annual.ametsoc.org/2013/index.cfm/programs-and-events/conferences-and-symposia/third-symposium-on-advances-in-modeling-and-analysis-using-python/).

## Key "high-level" libraries & code ##

Roughly ordered from higher to lower level, in focus.

  * [NANOOS SOS](NANOOSNVSPythonSOS.md). Server software.
  * [WOFpy/ulmo/pyhis group](https://github.com/twdb/). Based in Austin. Centered around the CUAHSI HIS stack (WOF/WaterML), though not exclusively.
    * [WOFpy](https://github.com/swtools/WOFpy). Server software, for CUAHSI HIS water data services: WaterML 1.0 + WaterOneFlow (WOF) 1. Note that WOFpy implements HTTP GET requests (REST-like, but using parameter-argument pairs), unlike the original WOF 1 specifications and most implementations out there. [FYI, USGS also has a GET WOF 1 implementation.](http://waterservices.usgs.gov/)
    * [ulmo](https://github.com/twdb/ulmo). Client software. (Replaces the now-deprecated "pyhis" package, developed by the same group)
  * [istSOS](http://code.google.com/p/istsos/). Server software.
  * [pyoos](https://github.com/asascience-open/pyoos). Client software.
  * [OWSLib](http://geopython.github.com/OWSLib/). Mostly client. Thanks to Kyle Wilcox (ASA), it now includes SOS & SensorML requests and parsing, and WaterML 1.0/1.1 parsing.
  * [netcdf4-python](http://code.google.com/p/netcdf4-python/). Mostly client.
  * [Pydap](http://pydap.org). Server/Client.
  * [cf-python](http://cfpython.bitbucket.org/). Package that implements the CF data model for reading, writing and processing of data and its metadata. Installation also deploys these two shell utilities (built on cf-python) for inspecting and combining datasets: _cfdump_ (view CF fields) and _cfa_ (create aggregated CF datasets). [Derrick mentioned these tools on an ioos\_tech email from 4/24/2013.](https://groups.google.com/d/msg/ioos_tech/yNSDQw1vWkA/h8JuEhjiOzgJ)


## Mailing lists and groups ##

  * [pywaterdata email list](http://librelist.com/browser/pywaterdata/). Limited to the WOFpy/ulmo/pyhis group. Deprecated in favor of an [ulmo-focused Google Group](https://groups.google.com/forum/?hl=en#!forum/ulmo) in Aug. 2013, but the list archive is still available and is still useful.
  * [Water Python Google Code group](http://code.google.com/p/waterpython/). Never really got off the ground after a bit of enthusiasm back in early 2010 (Chris Barker, Rob Hetland, etc). But could be repurposed....
  * [oceanpython.org](http://oceanpython.org/), from OTN


# Sketch of a Code Architecture for a Python SOS server #

Initial goal is to support only the mandatory _core_ operations (GetCapabilities, DescribeSensor and GetObservation). Additional data-consumer oriented _enhanced_ requests may be targeted in the future, particularly GetFeatureOfInterest, GetResult and DescribeResultModel. There are no plans to support _transactional_ operations (RegisterSensor and InsertObservation).

## Core elements ##
  * [pycsw](http://pycsw.org/) can serve as the template and pattern for building an OWSLib-based SOS server. pycsw already supports GET (KVP), POST (XML) and SOAP requests. [An overview of the pycsw code architecture is available](https://github.com/geopython/pycsw/wiki/Code-Architecture).
  * [WOFpy](https://github.com/swtools/WOFpy). In collaboration with WOFpy/ulmo TWDB group, support WaterML 1.x (and WOF services) and WaterML 2.0 + SOS 2.
  * [paegan](https://github.com/asascience-open/paegan) "attempts to fill the need for a high level common data model (CDM) library for array based met/ocean data". (See [this](http://www.unidata.ucar.edu/software/netcdf-java/CDM/) and [that](http://www.unidata.ucar.edu/projects/THREDDS/CDM/CDM-TDS.htm) for info on the CDM).
  * [NANOOS Python SOS](NANOOSNVSPythonSOS.md) server software. Currently it has a limited scope and is not highly generalizable, but it will provide guidance (and some code) for how all the components should come together.
  * [istSOS](http://code.google.com/p/istsos/). What can we learn or borrow from it?
  * [OWSLib](http://geopython.github.com/OWSLib/). pycsw already uses OWSLib "for CSW client and metadata parser". [SOS 1.0 and 2.0 (SWE/SensorML) parsing and encoding is already included in OWSLib.](http://geopython.github.io/OWSLib/#sos)
  * [SQLAchemy](http://www.sqlalchemy.org/) for database bindings. Both pycsw and WOFpy already rely on SQLAlchemy.


# Other relevant, but somewhat tangential efforts #

  * [Scitools](http://scitools.org.uk). Run by the UK Met Office. Python libraries intended to interact with CF datasets (Iris package) and generate commonly needed oceanographic data plots more readily (Cartopy package). Very cool stuff. [Here's a 4/12/2013 thread on ioos\_tech list, where Derrick mentioned this](https://groups.google.com/d/topic/ioos_tech/91VLT0GLXKE/discussion).