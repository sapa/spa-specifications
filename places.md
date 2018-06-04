---
layout: page
title: Places
---

According to the CIDOC-CRM place are "extents in space, in particular on the surface of the earth, in the pure sense of physics: independent from temporal phenomena and matter". We distinguish between three kinds of places:

* Official administrative entities such as municipalities, districts, canton, and countries.
* Places that are recognized as such in common knowledge but lack the status to be an administrative entity. These can be villages, which are administrated as regional groups, or city districts, which have lost their autonomy at some point.
* Specific sites that are needed to define the residence of an actor or the location of an object. These are identified by an address rather than a name.

The first two receive URIs, while the third kind is represented with blank nodes.

A legal body in the city of Bern:

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.

<http://data.performing-arts.ch/a/12345> a crm:E40_Legal_Body ;
	crm:P74_has_current _or_former_residence [ a crm:E53_Place ;
		crm:P89_falls_within <http://data.performing-arts.ch/p/12345> ;
		crm:P87_is_identified_by [ a crm:E45_Address ;
			rdf:value "Some Street, 3001 Bern"
		]
	]

<http://data.performing-arts.ch/p/12345> a crm:E53_Place ;
	rdfs:label "Bern";
	crm:P87_is_identified_by [ a crm:E44_Place_Appellation ;
		rdf:value "Bern"
	] ;
	owl:sameAs <http://www.wikidata.org/entity/Q70>, <http://d-nb.info/gnd/4005762-8>, <http://geonames.org/2661552>, <http://classifications.data.admin.ch/municipality/351> .
```

<!-- TODO: add geo data -->

<!-- TODO: Should the address be machine readable? -->

Currently, places and their relations to other entities are only represented according to the CIDOC-CRM as RiC does not provide additional depth of information and may be inferred later.