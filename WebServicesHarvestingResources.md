# IOOS Portal Parsing Tools #
| **Service** | **Info URL** | **Service URL** | **Developer** | **Examples or code repo** |
|:------------|:-------------|:----------------|:--------------|:--------------------------|
| Hydrometeorological Design Studies Center (HADS)  | http://dipper.nws.noaa.gov/hdsc/pfds/ | http://amazon.nws.noaa.gov/nexhads2/servlet/DecodedData |               |                           |
| NOAA Center for Operational Oceanographic Products and Services (CO-OPS)  | http://tidesonline.nos.noaa.gov/ | http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/ |               |                           |
| NOAA National Data Buoy Center (NDBC)  | http://www.ndbc.noaa.gov/  | http://sdf.ndbc.noaa.gov/sos |               |                           |
| NOAA Weather  | http://www.nws.noaa.gov/ | http://www.nws.noaa.gov/data/obhistory/ |               |                           |
| Remote Automatic Weather Stations (RAWS)  | http://www.raws.dri.edu/ | http://www.raws.dri.edu/cgi-bin/wea_list2.pl |               |                           |
| Snow telemetry (SNOTEL)  | http://www.wcc.nrcs.usda.gov/ | http://www.wcc.nrcs.usda.gov/nwcc/site |               |                           |
| U.S. Geological Survey water (USGS Water/NWIS)  | http://waterdata.usgs.gov/ak/nwis/uv | http://waterservices.usgs.gov/nwis/iv |               |                           |
| NERRS       |              | e.g. http://cdmo.baruch.sc.edu/QueryPages/realtime.cfm?Station_Code=hudfsmet | MARACOOS/ASA  |                           |
| HRECOS      | http://www.hrecos.org/joomla/ |                 | MARACOOS/ASA  |                           |
| Drifters (NEFSC only) | http://www.nefsc.noaa.gov/drifter/  |                 | MARACOOS/ASA  |                           |
| Ships and drifting buoys from MADIS | http://madis.noaa.gov/madis_sfc.html |                 |               |                           |
| HFRadar ground stations | http://maracoos.org/hfradar |                 |               |


# 52North Data Injectors #
| **Service** | **Info URL** | **Service URL** | **Developer** | **Examples or code repo** |
|:------------|:-------------|:----------------|:--------------|:--------------------------|
| Hydrometeorological Design Studies Center (HADS)  | http://dipper.nws.noaa.gov/hdsc/pfds/ | http://amazon.nws.noaa.gov/nexhads2/servlet/DecodedData | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester  |
| NOAA Center for Operational Oceanographic Products and Services (CO-OPS)  | http://tidesonline.nos.noaa.gov/ | http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/ | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |
| NOAA National Data Buoy Center (NDBC)  | http://www.ndbc.noaa.gov/  | http://sdf.ndbc.noaa.gov/sos `[1]` | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |
| NOAA Weather  | http://www.nws.noaa.gov/ | http://www.nws.noaa.gov/data/obhistory/ | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester  |
| Remote Automatic Weather Stations (RAWS)  | http://www.raws.dri.edu/ | http://www.raws.dri.edu/cgi-bin/wea_list2.pl | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |
| Snow telemetry (SNOTEL)  | http://www.wcc.nrcs.usda.gov/ | http://www.wcc.nrcs.usda.gov/nwcc/site | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |
| U.S. Geological Survey water (USGS Water/NWIS)  | http://waterdata.usgs.gov/ak/nwis/uv | http://waterservices.usgs.gov/nwis/iv | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |
| NERRS       |http://cdmo.baruch.sc.edu/webservices.cfm  | http://cdmo.baruch.sc.edu/webservices2/requests.cfc?wsdl | AOOS/Axiom    | https://github.com/axiomalaska/sensor-web-harvester |

`[1]` AOOS' sensor-web-harvester currently uses http://www.ndbc.noaa.gov/to_station.shtml and http://www.ndbc.noaa.gov/data/5day2/ for NDBC sensors because these endpoints tend to be more up-to-date and complete.

# URN Authorities #
| **Source** | **URL** | **Authority** |
|:-----------|:--------|:--------------|
| Chugach Nation Forest Avalanche Information Center | http://www.cnfaic.org | cnfaic        |
| Hydrometeorological Design Studies Center (HADS) | http://dipper.nws.noaa.gov/hdsc/pfds | gov.noaa.nws.hads |
| NOAA Weather | http://www.nws.noaa.gov/ | gov.noaa.nws  |
| Remote Automatic Weather Stations (RAWS) | http://www.raws.dri.edu/ | edu.dri.raws  |
| Snow telemetry (SNOTEL) | http://www.wcc.nrcs.usda.gov/ | gov.usda.nrcs.wcc.snotel |
| U.S. Geological Survey water (USGS Water/NWIS) | http://waterdata.usgs.gov/ak/nwis/uv | gov.usgs.waterdata |
| NERRS      | http://cdmo.baruch.sc.edu/webservices.cfm | cdmo.nerrs    |
| Micro specialties Inc | http://www.micro-specialties.com/ | com.micro-specialties |
| Circum-Arctic Lakes Observation Network | http://datagarrison.com/users/300234011204340/300234011204340/plots.php | nsf.aon.calon |
| Alaska Department of Transportation | http://www.dot.state.ak.us/iways/roadweather/forms/IndexForm.html | alaska.dot    |
| USGS Climate Monitoring | http://data.usgs.gov/climateMonitoring/main/home | gov.usgs.climate-monitoring |
| NOAA Water | http://water.weather.gov/ahps/index.php | gov.noaa.water |
| AOOS       | http://www.aoos.org/ | aoos          |
| US Climate Reference Network (USCRN) | http://www.ncdc.noaa.gov/crn/ | gov.noaa.uscrn |
| NOAA PMEL Carbon Program | http://www.pmel.noaa.gov/co2/ | gov.noaa.pmel |
| Water and Environmental Research Center | http://ine.uaf.edu/werc/ | edu.uaf.werc  |



## Sensor Web Harvester ##
https://github.com/axiomalaska/sensor-web-harvester

This Scala project harvests sensor data from web sensor sources (SOS, html pages, etc) and inserts the data into SOS. This project uses the [SOS Observation Injecter toolkit](https://github.com/axiomalaska/sos-injection) (below) to inject observations into the SOS. The current sources that it pulls observations from are: HADS, NDBC, NOAA NOS CO-OPS, NOAA Weather, RAWS, SnoTel, USGS Water, and NERRS.

This project can be used by just downloading the pre-built jar from Github. Goto [Github project](https://github.com/axiomalaska/sensor-web-harvester) to learn more.

## SOS Observation Injector ##
https://github.com/axiomalaska/sos-injection

The SOS Observation Injector is a Java toolkit that can be used to enter sensor observations into an SOS. This project takes as input Source, Station, Sensor, and Phenomenon objects and adds the needed XML formating to allow the data to be placed in an SOS. Users can use this toolkit to create Java or Scala programs that retrieve sensor data from databases, files, web services, or any other source and insert that data into an SOS server.

Go to [Github project](https://github.com/axiomalaska/sos-injection) to learn more.