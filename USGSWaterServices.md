# Alaska (AOOS) #
# Caribbean (CaRA) #
# Central and Northern California (CeNCOOS) #
# Gulf of Mexico (GCOOS) #
# Great Lakes Observing System (GLOS) #
# Mid-Atlantic (MARACOOS) #
# Northwest Pacific (NANOOS) #
Ingesting USGS data for [NVS](http://nvs.nanoos.org) with Python, by using the WaterML 1.1 encoding option from the USGS water services. Done via the [CUAHSI HIS catalog](http://hiscentral.cuahsi.org/) and its SOAP services, but could also do this directly from the USGS REST WaterML web services.

# Northeastern Atlantic (NERACOOS) #
# Pacific Islands (PacIOOS) #
# Southern California (SCCOOS) #
# Southeast Atlantic (SECOORA) #

Still using the earlier NWIS service(like http://waterdata.usgs.gov/nwis/ ...) documented at

http://nautilus.baruch.sc.edu/twiki_dmcc/bin/view/Main/CarolinasCoastGetData#USGS

# OOI #
> ## Java ##
> The implementation is all wrapped up in the overall EOI Agent codebase - but the majority of the code for actually dealing with the USGS services is here: https://github.com/ooici-eoi/eoi-agents/blob/develop/src/net/ooici/eoi/datasetagent/impl/UsgsAgent.java

# CUAHSI HIS #
> ## "WaterML" XML encoding and "WaterOneFlow" web services ##
> Folks at the [Texas Water Development Board, TWDB](http://www.twdb.state.tx.us/) have developed [a comprehensive Python package (pyHIS)](https://github.com/swtools/pyhis) to ingest WaterML data using [HIS web services ("WaterOneFlow")](http://his.cuahsi.org/). The TWDB team lead for this project is Dharhas Pothina; [Dharhas will give a webinar on pyHIS on 2011/11/15](http://www.cuahsi.org/his-webinars.html) that will be recorded and be available afterwards.