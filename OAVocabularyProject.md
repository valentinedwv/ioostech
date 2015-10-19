# Inter-agency Ocean Acidification parameter vocabulary #



## Goal: ##
Our goal is to create an inter-agency ocean acidification parameter list, which will be shared by all participating agencies, to facilitate OA data sharing.

## Parameter submission form: ##
Please <a href='https://docs.google.com/a/noaa.gov/spreadsheet/viewform?formkey=dG1jN1RUY2xxSGxkMUdobzNvMkZ1d1E6MQ#gid=0'>click here</a> to submit your parameters.

This interface enables you to submit new ocean acidification parameters to us. Once approved, the new parameters will be added to the Interagency Ocean Acidification Parameter List in the MMI. Before you submit any new parameters, we strongly recommend you to check against the <a href='http://mmisw.org/orr/#http://mmisw.org/ont/ioos/OA'>Interagency Ocean Acidification Parameter list</a> first, to make sure the parameters you are submitting are not already in the list.

After the submission is completed, please send an email to `<ioos_nodc_chemical_vocabulary@googlegroups.com>`. This will start the review process.

## Repository of submitted parameters ##
Please <a href='https://docs.google.com/a/noaa.gov/spreadsheet/ccc?key=0AkOD4kCLqux_dG1jN1RUY2xxSGxkMUdobzNvMkZ1d1E#gid=0'>click here</a> to check out the parameters that are just submitted.

Your will need to sign in using your official NOAA mail or your personal Gmail if your work email is not Gmail based. Newly submitted parameters will be stored here temporarily before they are approved into the Interagency Ocean Acidification Parameter List in the MMI.

## Proposed bylaws: ##
  * Committee members have up to two weeks to raise comments or objections on a submitted parameter. After that time, silence assumes consent.
  * After approval, the parameters will be published into the inter-agency OA parameter list that resides in MMI.

## Inter-agency Ocean Acidification Parameter List ##
The approved ocean acidification parameters will be published in the [Interagency Ocean Acidification Parameter list](http://mmisw.org/ont/ioos/OA), which resides in MMI's website.

## Current committee members: ##
  * Rob Ragsdale (IOOS)
  * Hassan Moustahfid (IOOS)
  * Emilio Mayoga (NANOOS/Univ. of Washington)
  * Sara Haines (SECOORA/UNC - CH)
  * Don Collins (NODC)
  * Hernan Garcia (NODC)
  * Liqing Jiang (NODC)
  * Alex Kozyr (CDIAC)
  * Cyndy Chandler (BCO-DMO)
  * Dwight Gledhill (OAP)
  * Leticia Barbero (AOML)
  * Cathy Cosca (PMEL)
  * Simone Alin (PMEL)

## Discussion ##

### Emilio Mayorga 21 January 2013 ###

- The Google spreadsheet needs an attribute for term name in the
vocabulary; this is not a name intended primarily for people, but
rather one that follows naming conventions that are appropriate for
computers. The CF parameter name is a great example. For example, it
probably should be limited to lower case (and of course, no blank
spaces). I think Sara and Rob have sent out some proposed naming
conventions for IOOS parameter terms; that and CF rules would be a
good place to start.

- In the parameter Google spreadsheet, Sara (or someone else?) added
this comment: "How should we deal with acronyms or chemical terms in
the term ID on MMI??  Initially, acronyms and chemical formulas were
frowned upon.  I can't remember the thinking.  Open to suggestions,
and comments." That's a very appropriate question to ask, to come up
with naming rules. Personally, I think forbidding molecular formulas
would be too limiting, and would create the nightmare of huge names
that CF has with many chemical parameters. Same goes for a variable as
widespread and widely known as pH. BTW, a few months ago I looked at
what variables existed for pH or acidity in CF and the IOOS parameter
vocabulary. I'd be happy to forward what I found if there's interest.

- We should start thinking of an MMI vocabulary mapping for OA. Some
OA terms will be taken from CF, some from existing terms on the IOOS
parameter vocabulary, and some will be added to the latter. The
vocabulary mapping brings it all together in a convenient way. We
could create a new one, or build on top of one of the mappings Sara
has set up for IOOS. I think I gave examples of this I few months ago
on an email. Something may already exist, I forget.

### Emilio Mayorga 18 November 2012 ###

#1. That sounds reasonable. How about having as an additional
requirement for submission, a brief email to a list (existing or new
and dedicated list?) arguing for the inclusion? If the vocabulary
doesn't include anything like that term, the argument may be simple.
But if there is potential overlap with an existing term, the argument
may need to be more well thought out. Also, requests may involve
rethinking existing terms, not just additions, right?

#2. The first option (like SeaVOX) sounds good.

#4. I'm not sure I understand what you're proposing here.

**Liqing’s response # 4) is about the format of the shared parameter list. It could be the current IOOS list (provided IOOSdoes not mind to expand the scope of their list significantly), or a separate list built on top of theIOOS list (preferred by Hernan).**

#5. Member of the group will need to be decided on. We can set up a
wiki page that lists these members, for transparency. I assume the
list won't be no larger than the cc list on this thread.

### Liqing Jiang 06 November 2012 ###

I just had a brief meeting with Rob and John Ten Hoeve this Monday
(11/5). To move things forward, below are some of our shared thinking
(suggested Terms of Reference for consideration):

1) We need a mechanism to let people submit terms they want to be
added to the shared parameter list that resides at MMI. Google Form
will be one option. The back-side Google spreadsheet (with all the
inputs) will be shared with all of us (list to be defined). Users do
not need to have a Google account to input terms to Google Form, but
you will need a Google account, if you want to read and edit the
shared spreadsheet.

2) Once the terms are in, the reviewing and approving mechanisms could be:

> - either, requiring you to add your comments or objections next to
the terms within two weeks after the terms are submitted (any terms
after two weeks of their submission are automatically assumed to be
good to go).  This is the approach used at SeaVOX and it works well.

> - or, having monthly or quarterly meetings to approve new terms to
be added to MMI.

3) Once a term is approved, we need a person to move the term from
Google spreadsheet into MMI. Rob has volunteered to do this. Do we
need an alternate person, in case Rob is on travel?

4) The MMI list probably should be a generic list unless the present
IOOS list has no limitations as to what terms can be added or
modified.

5. Membership: Who are the members of this group?

### Liqing Jiang 09 October 2012 ###

Several comments:

1) It sounds like a great idea to divide pH into several parameters
based on their scales, considering that missing pH scales had been
such a big problem in the past. If we keep pH\_total scale as a
separate variable, should we do the same thing for pH\_seawater, which
is also a very commonly used scale? Maybe for NBS, and free scale as
well?

2) When it comes to carbon dioxide, I have a slightly different view
(compared to pH). I am not sure if we need to specify whether the
carbon dioxide is reported as pCO2, or fCO2. Can we simply say carbon
dioxide-seawater and carbon dioxide-air? The reason is because
researchers know how to convert them to the term that they prefer, and
we do not want them to only get a portion of the carbon dioxide data
when they do the search. Plus, sometimes only xCO2 is reported.
Anyway, I do not have a strong opinion on this and am ok with either
way.

Technically speaking, pCO2-air is incorrect. It should be xCO2-air.
This is another reason, carbon dioxide-air is better.

I do not know what Nisumaa et al. (2010) are referring to when they
say 'CO2'. Do they mean concentration of carbon dioxide (after Henry
Constant conversion) in the unit of mol/kg or mol/L? That is usually
an intermediate term for calculation of other carbon species, and it
is not very often reported. The same is true for HCO3, and CO3. They
are usually calculated, instead of measured.

3) I second your opinion on units.

4) These are not Tier one terms, but they are important carbon related
parameters that are not in the IOOS list as well:
Silicate
Apparent Oxygen Utilization
Dissolved Organic Nitrogen
CFC-11
CFC-12
CFC113
Carbon 13
Carbon 14
Oxygen18

### Emilio Mayorga 04 October 2012 ###

I should've included this, directly from Table 2 of Nisumaa et al (2010):
NISUMAA ET AL. 2010. EPOCA/EUR-OCEANS data compilation on the
biological and biogeochemical responses to ocean acidification. Earth
Syst. Sci. Data, 2, 167–175, 2010, doi:10.5194/essd-2-167-2010
http://www.earth-syst-sci-data.net/2/167/2010/



 Table 2. R package seacarb (Lavigne and Gattuso, 2010) computes the
following carbonate system variables.
Short variable name Long variable name and unit

---

S Salinity
T Temperature (oC)
P Pressure (bar)
pH pHT (total scale)**CO2 Carbon dioxide concentration (mol kg-1)
pCO2 Carbon dioxide partial pressure (µatm)
fCO2 Carbon dioxide fugacity (µatm)
HCO3 Bicarbonate concentration (mol kg-1)
CO3 Carbonate ion concentration (mol kg-1)
CT Dissolved inorganic carbon concentration (mol kg-1)
AT Total alkalinity (mol kg-1)
OmegaAragonite Aragonite saturation state
OmegaCalcite Calcite saturation state
  * The definition of pH is implicitly based on a concentration
unit for hydrogen ion,
although the pH value itself has the dimension 1. The concentration
unit for hydrogen
ion used here in mol kg-1.

---

NISUMAA ET AL. 2010. EPOCA/EUR-OCEANS data compilation on the
biological and biogeochemical responses to ocean acidification. Earth
Syst. Sci. Data, 2, 167–175, 2010, doi:10.5194/essd-2-167-2010
http://www.earth-syst-sci-data.net/2/167/2010/

---**

04 October 2012

I completely agree with Sara's suggestion.

Liqing: At the call, I volunteered to send out the first version of
the OA Tier 1 parameters. Your email didn't mention this. Clearly
you're way too nice :) Never let someone who volunteers to do
something get away with forgetting about it!

Here's the OA Tier 1 parameter list I compiled from Nisumaa et al
(2010, EPOCA carbonate variables calculations), with some additions:
Direct carbonate system and acidity/buffering variables:
pH\_T, pH, CO2, pCO2, fCO2, H2CO3, HCO3, CO3, TA, TCO2/DIC, pCO2\_air
Other basic variables strongly tied to these:
water temperature, salinity, pressure, dissolved oxygen, DOC

I'm not suggesting **at all** that we use these spellings as is.
Spellings should follow a naming & syntax convention that's
appropriate for the vocabulary hosting the terms. We can talk about
this later.

Hernan and Liqing: I'm also not suggesting that pH parameter names
should be separated into ones measured on the total scale, vs "all
others". As I mentioned at the call, I think we should separate the
parameter (concept) name from the method reference; I'm glad to hear
that Donald agrees!

I'm also attaching the two slides I put together for the IOOS DMAC
meeting a month ago. Hernan: Feel free to grab text from here to start
drafting the "terms of reference"! I have other text I've copied and
pasted from other emails and documents that could be very useful.

CF and the IOOS Parameter Vocabularies already include some of these
variables. Sara has also created some mappings among these variables,
and vs. the IOOS 26 Core Variables. I'm listing them below at the
bottom of my message, as MMI parameter URL's, with indentation
reflecting the mappings already built in (some of the looser mappings
may have been removed by now). The two relevant parameters already on
the IOOS Parameter Vocabulary are called "acidity" and "pCO2". We're
**not** stuck with those names as is. I personally don't like them, for
a number of reasons. We should take ownership of these terms and edit
them to reflect a clearer scope and more consistent naming convention.

Finally, here's the URL for the IOOS Vocabularies wiki page. It's not
quite final, but close:
http://code.google.com/p/ioostech/wiki/ControlledVocabularies
Its scope is broader than observed-properties vocabularies. At the end
you'll find a reference and link to the paper Sara wrote recently
(with help from several of us), providing more background and
discussions. Here's the reference and link to the pdf:
Haines, S., V. Subramanian, E. Mayorga, D. Snowden, R. Ragsdale, C.
Rueda and M. Howard. Submitted. IOOS vocabulary and ontology strategy
for observed properties. Proc. MTS/IEEE Oceans 2012, Hampton Roads,
VA.
http://ioostech.googlecode.com/files/IOOSVocabPaper_MTSOceans2012_HainesEtal_Final_copyrighted.pdf

### Sara Haines 04 October 2012 ###

Comment to Liqing Jiang 04 October 2012 Discussion)

Another option is to do these in a less formal way, as mentioned by Sarah.
Maybe we could just send a list of terms that we want to be included in the
general list to either Sarah, Rob or Derick, and they can check them against
the CF list, correct errors, and take care of it.

Just to clarify, my suggestion is to pass around the list of terms for Tier 1 objective (approx 25 maybe) amongst those of you (or others that should be) on this list to edit comment or add terms, perhaps provide definitions if there is concern about getting started.  This gets it started.  Then with some blessing of the group concerned in the list of terms place it on ORR either under IOOS. Don't let the lack of formal mechanisms stop you from getting your work done.  But doing something, we will be able to provide input for a formal mechanism.

### Liqing Jiang 04 October 2012 ###

Kick off discussion summary

We all agreed:
1) to build a shared general list that everyone can link their own
vocabulary list to, based on the IOOS parameter list on the MMI;
2) the scope of the list will be broader than what IOOS currently covers;
3) using CF vocabulary, as well as SeaDataNet, as primary references
for new inputs;
3) to start with the Tier 1 Ocean Acidification list as a test bed;
4) Rob will be the person who input new terms;
5) there is a need to hammer out mechanisms for inputting new terms.

As a next step, we need to work on details of the
mechanisms/procedures for inputting new terms. I am going to start off
the discussion by offering some wild suggestions:
1) to create a new MMI list, serving as an intermediate repository for
new input terms. The list should be editable by at least one
representative from IOOS, University of Washington, and NODC, etc.
2) to appoint members to a committee that is responsible for approving
new terms, and to elect a chair for the committee. Volunteers please?
3) to decide on a mechanism to approve terms, e.g., by adding comments
next to the yet-to-be-approved terms in the list as mentioned above,
by meeting regularly over telecon, or by exchanging emails, etc.
4) to come up with a time frame, after which the new terms are assumed
to be automatically approved by everyone.