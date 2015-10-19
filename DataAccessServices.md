# OGC Sensor Observation Service #

## Interface Description for the IOOS SOS Profile ##
[SOSGuidelines](SOSGuidelines.md)

## Server Software ##
<dt></dt>
<dd>  </dd>


<dl>
<dt><b>52North</b></dt>
<dd>
<a href='http://www.52North.org'>52North</a> SOS modified by Axiom Consulting and Design to conform to the IOOS Profile <a href='SOS52North.md'>SOS52North</a></dd>

<dt><b>ncSOS</b></dt>
<dd><a href='http://www.unidata.ucar.edu/projects/THREDDS/'>THREDDS</a> plugin which provides an SOS interface to files served via the THREDDS data server v4.3 or greater.  The underlying files must conform to the CF Discrete Sampling Geometries.  <a href='ncSOS.md'>http://asascience-open.github.com/ncSOS/</a>  was written by <a href='http://www.asascience.com/'>Applied Science Associates</a></dd>

<dt><b>Python SOS</b></dt>
<dd>Python based server maintained by Emilio Mayorga from <a href='http://www.nanoos.org'>NANOOS</a> <a href='NANOOSNVSPythonSOS.md'>NANOOSNVSPythonSOS</a>.  Other related python tools can be found <a href='PythonSOStools.md'>here.</a>  </dd>

<dt><b>NDBC</b></dt>
<dd>PHP implementation of an SOS server written by the <a href='http://www.ndbc.noaa.gov'>National Data Buoy Center</a> and  <a href='http://sdf.ndbc.noaa.gov/sos/software/'>available here</a>.  The NDBC server implements the older DIF format and the current <a href='NDBC_SWE_Implementation.md'>SWE based observation response</a> </dd>

<dt><b>CO-OPS</b></dt>
<dd>CO-OPS has implemented SOS but their software implementation is not easy to distribute.  Nevertheless they have modern services compliant with the IOOS Profile v1.0 and the older DIF formats and they have extensive documentation and examples <a href='http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos-test/'>(test service)</a> <a href='http://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/'>(production service)</a>.  </dd>

</dl>


# OPeNDAP Based Services #

## THREDDS ##
http://www.unidata.ucar.edu/projects/THREDDS/

## ERDDAP ##
http://coastwatch.pfeg.noaa.gov/erddap/index.html

## PyDAP ##
http://www.pydap.org

## Hyrax ##
http://www.opendap.org