Intro
-----------------------------------------
Sparqly is a small python library for querying SPARQL endpoints. It can be used from the command line or as a module in other python applications. 

The idea is to make it easy to access sparql endpoints, in a pythonic way. 

The main file is a genetic wrapper for any sparql endpoints, providing 4 main methods:
- `query`: accepts a generic query as a string
- `ontology`: queries for all owl:Classes
- `describe`: a describe query for a specific URI
- `alltriples`: a query that returns all the triples mentioning a specific URI

Furthemore, there are two specializations of the main sparql wrapper: nature.py and dbpedia.py. 
These are like 'plugins' that embed special behaviour for specific endpoints.

####Dependencies:
Sparqly relies on sparql-wrapper, which itseld depends on rdflib. Install both of them using `easy_install`.

- http://sparql-wrapper.sourceforge.net/
- https://github.com/RDFLib


####Credits: 
Sparqly main library is based on code found here: http://terse-words.blogspot.co.uk/2012/01/get-real-data-from-semantic-web.html
I just added a few more methods for sparql queries, parametrized the format for the results set etc..





Todo:
-----------------------------------------
- keep on adding queries specific to nature...
- check support for RDF/XML, TURTLE, N3..








ChangeLog:
-----------------------------------------

####7/2/13

- added command line handlers
- added a parameter for convert() [by defaults it's True]
- Added support for JSON and XML formats.











Example
-----------------------


	In [1]: from sparqly import *

	In [2]: s = SparqlEndpoint("http://data.nature.com/sparql")

	In [3]: q = "select ?x where {?x a owl:Class}"

	In [4]: results = s.query(q)
	PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	PREFIX owl: <http://www.w3.org/2002/07/owl#>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	PREFIX void: <http://rdfs.org/ns/void#>
	PREFIX dcterms: <http://purl.org/dc/terms/>
	PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
	PREFIX dc: <http://purl.org/dc/elements/1.1/>
	select ?x where {?x a owl:Class} 


	In [5]: print results
	{u'head': {u'vars': [u'x']}, u'results': {u'bindings': [{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Graph'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Catalog'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Citation'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/ProductGroup'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Term'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Subject'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Contributor'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Article'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/ProductFamily'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Product'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Publication'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/DataCitation'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Coverage'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Technique'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Interest'}}, {u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Speciality'}}]}}

	In [6]: for x in results['results']['bindings']:
	   ...:     print x
	   ...:     
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Graph'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Catalog'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Citation'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/ProductGroup'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Term'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Subject'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Contributor'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Article'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/ProductFamily'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Product'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Publication'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/DataCitation'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Coverage'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Technique'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Interest'}}
	{u'x': {u'type': u'uri', u'value': u'http://ns.nature.com/terms/Speciality'}}

	In [7]: results = s.query(q, "XML")
	PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	PREFIX owl: <http://www.w3.org/2002/07/owl#>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	PREFIX void: <http://rdfs.org/ns/void#>
	PREFIX dcterms: <http://purl.org/dc/terms/>
	PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
	PREFIX dc: <http://purl.org/dc/elements/1.1/>
	select ?x where {?x a owl:Class} 


	In [8]: print results
	<xml.dom.minidom.Document instance at 0x105333c20>

	In [9]: print results.toxml()
	<?xml version="1.0" ?><sparql xmlns="http://www.w3.org/2005/sparql-results#">
	<head>
	 <variable name="x"/>
	</head>
	<results>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Graph</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Catalog</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Citation</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/ProductGroup</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Term</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Subject</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Contributor</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Article</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/ProductFamily</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Product</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Publication</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/DataCitation</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Coverage</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Technique</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Interest</uri></binding>
	</result>
	<result>
	 <binding name="x"><uri>http://ns.nature.com/terms/Speciality</uri></binding>
	</result>
	</results></sparql>

	In [10]: results = s.query(q, convert=False)
	PREFIX foaf: <http://xmlns.com/foaf/0.1/>
	PREFIX owl: <http://www.w3.org/2002/07/owl#>
	PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
	PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
	PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
	PREFIX void: <http://rdfs.org/ns/void#>
	PREFIX dcterms: <http://purl.org/dc/terms/>
	PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
	PREFIX dc: <http://purl.org/dc/elements/1.1/>
	select ?x where {?x a owl:Class} 



	In [11]: type(results)
	Out[11]: instance

	In [12]: print results
	<SPARQLWrapper.Wrapper.QueryResult instance at 0x10588ee18>

	In [13]: for x in results:
	   ....:     print x
	   ....:     
	{ "head": {"vars": [

	 "x"

	] },

	"results": {

	"bindings": [

		{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Graph"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Catalog"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Citation"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/ProductGroup"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Term"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Subject"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Contributor"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Article"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/ProductFamily"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Product"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Publication"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/DataCitation"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Coverage"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Technique"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Interest"

			}

		},{

			"x": {

			 "type": "uri",

			 "value": "http://ns.nature.com/terms/Speciality"

			}

		}

	] } }


	In [14]: results.info()
	Out[14]: 
	{'connection': 'close',
	 'content-length': '1541',
	 'content-type': 'application/sparql-results+json',
	 'date': 'Thu, 07 Feb 2013 16:35:51 GMT',
	 'server': 'Jetty(6.1.26)',
	 'set-cookie': 'BIGipServerjetty-external=rd1o00000000000000000000ffff0a0101cbo80; expires=Thu, 07-Feb-2013 17:35:51 GMT; path=/',
	 'x-cerberus-query-processing-time': '0.282',
	 'x-cerberus-version-number': '1.4.0'}

