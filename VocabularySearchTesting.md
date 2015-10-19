

# Introduction #

Most catalog services provide some search mechanisms of the metadata fields.  However, these tend to be limited to exact matches or specific fields but not able to find data that is somewhat related or same data that is labeled differently.  Searching for like or similar terms is an important step towards improving the search capability within data catalogs like THREDDS or geoportal catalog services.  In this section, IOOS is testing automated search capabilities and discovery of terms based on relationships established in mapping vocabulary.  This is an attempt to create a tunnel or mechanism by which more intelligent searches can be made.

But what is returned is only as good as the SPARQL query and the mappings in the vocabulary.

# SPARQL Endpoint #

Numerous examples exist in PERL, Python, and HTML Forms that illustrate how to issue SPARQL queries to vocabulary search services.  SPARQL Endpoints can return the data in different formats (HTML, JSON, CSV, RDF, N3), but accessing all these formats is not always obvious.  Of the Python code, [SparqlWrapper](http://sparql-wrapper.sourceforge.net/) seems to be the most robust [(note: a github fork is also available)](https://github.com/tatiana/SPARQLWrapper). The MMI Endpoint returns XML, CSV, JSON, and HTML.

As a proof-of-concept, python script examples were created to show how to submit a SPARQL query with a JSON return, being the easiest format of response to work with python.

> ## SPARQL-Python Examples ##
    * [using urllib2 (example\_sparql\_urllib2.ipynb)](http://nbviewer.ipython.org/urls/raw.github.com/nccoos/ioos-vocabulary-search/master/examples/example_sparql_urllib2.ipynb)
    * [using SPARQLWrapper (example\_sparql\_wrapper.py)](http://nbviewer.ipython.org/urls/raw.github.com/nccoos/ioos-vocabulary-search/master/examples/example_sparql_wrapper.ipynb)

> ## CSW-Python Examples ##
    * [Using OWSLIB-CSW to access NGDC Geoportal CSW (example\_csw\_ngdc\_geoportal.ipynb)](http://nbviewer.ipython.org/urls/raw.github.com/nccoos/ioos-vocabulary-search/master/examples/example_csw_ngdc_geoportal.ipynb)


# Visualizing Vocabularies, Mappings, and Search Results #

Developing recipes for geoportal programmers to issue SPARQL queries to MMI ORR is one key to demonstrating how MMI ORR can enhance catalog search.  Another key to this development is to visualize what the search results are. Visualizing the terms and their mappings will be the next step in making registered vocabs on MMI ORR more useful.

