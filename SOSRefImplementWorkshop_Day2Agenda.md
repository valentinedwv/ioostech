

[Day 1](SOSRefImplementWorkshop_Day1Agenda.md) |
[Day 2](SOSRefImplementWorkshop_Day2Agenda.md) |
[Day 3](SOSRefImplementWorkshop_Day3Agenda.md)


# Day Two #

## Day One Wrap Up ##

Emilio will lead a [short wrap up of Day 1 activities](SOSRefImplementWorkshop_Day1Agenda.md).

## Common Data Model (CF/SWE/O&M) ##

(Kyle) Part 1: [O&M / SWE Common encoding for the scientific feature types defined by CF conventions / the Common Data Model.](CFFeatureTypes.md)

### Requirements ###

  * Output format needs to be useable by the community
    * IOOS GML was not the solution, too verbose
    * CSV has has positive reception
    * Need to add metadata block to CSV output so it is completely self describing.
  * Should we be able to translate the SWE output into a Binary NetCDF output fairly easily?

  * Support multiple observedProperties and offerings, even if offerings are on different frequencies.  How should we represent the different offerings?
    * MultipleBlocks
      1. Less fill values.  Each offering only has to return the observedProperties that apply to itself, not all of them that are requested.
      1. Multiple CSV blocks means more output parsing and POTENTIALLY more verbose output.
      1. Offerings are **usually** on a common frequency, resulting in even less fill values.
    * SingleBlock
      1. Less description metadata since it is all encompassed in one block.
      1. More fill values for offerings that do not support all requested observedProperties.
      1. Offerings on different reporting frequencies can further increase the verbosity of the output.


### Can we simplify the FeatureTypes into just a few outputs? ###

  * Can point and timeSeries be represented as a timeSeriesProfile with less data?  Is this acceptable?
  * Can trajectory and trajectoryProfile be represented in the same output format?

### The Time Block ###

[How to describe times in the responses.](TheTimeBlock.md)


### Identifying the FeatureType ###

See: IdentifyingTheFeatureType


### How and Where to describe the Geometry ###

  * timeSeriesProfile
    * location
    * depths (if not varying by time)

```
      <om:featureOfInterest>
        <gml:FeatureCollection>
          <gml:location>    
              <gml:Point>
                <gml:pos>-76.3 45</gml:pos>
              </gml:Point>
          </gml:location>
        </gml:FeatureCollection>
      </om:featureOfInterest>
```

  * trajectoryProfile
    * the trajectory path
    * should we include the time and depth associated with each trajectory point here?

```
      <om:featureOfInterest>
        <gml:FeatureCollection>
          <gml:location>
            <gml:MultiPoint>
            <gml:srsName>EPSG_URN</gml:srsName>
              <gml:pointMembers>
                <gml:Point>
                  <gml:pos>-76.3 45 8</gml:pos>
                </gml:Point>
              </gml:pointMembers>
            </gml:MultiPoint>
          </gml:location>
        </gml:FeatureCollection>
      </om:featureOfInterest>
```

### The Position Vector Block ###

[How to describe the position of an asset](TheVectorBlock.md) inside of `<om:result>` block.

Which featureTypes need position information inside of the result block?
  * timeSeries[Profile](Profile.md) - point location will need to be represented elsewhere, so why repeate the location in each line of CSV?
  * trajectory[Profile](Profile.md) - depending on where we are listing the actual path (geometry), we **may** not need to verbosely list each position.