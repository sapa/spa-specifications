---
layout: page
title: Actors
---

Entities that "have the potential to perform intentional actions of kinds for which someone may be held responsible" for CIDOC-CRM are instances of `E39 Actor` while RiC calls them `E4 Agent`. Here both classes are used as actors/agents are one point where the scope of both models overlap. CIDOC-CRM further distinguishes further between 
`E21 Person`, `E74 Group` and `E40 Legal Body` as subclasses. As RiC so far does not provide any further classification [a custom vocabulary](https://sapa.github.io/spa-vocabulary/#http://vocab.performing-arts.ch/agenttype) is used via `ric:P32_Type` in analogy with the CIDOC-CRM subclasses.

The following examples are not complete as documentation of the implementations of `E82 Actor Appellation`, `E52 Time-Span` etc. is not repeated here.

### Persons

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.
@prefix ric: <http://yet-to-be-defined-ric-implementation/>.
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/643827> a crm:E21_Person, ric:E4_Agent ;
	ric:P32_Type spav:agenttype-person ;
	rdfs:label "Firstname Lastname" ;
	crm:P1_is_identified_by [ a crm:E82_Actor_Appellation ] ;
	ric:P33_Identity_Type spav:identitytype-given ;
	crm:P98i_was_born [ a crm:E67Birth ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ] ;
		crm:P7_took_place_at <http://data.performing-arts.ch/p/009321>
	] ;
	crm:P100i_died_in [ a crm:E69_Death ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ] ;
		crm:P7_took_place_at <http://data.performing-arts.ch/p/762881>
	] ;
	owl:sameAs <http://www.wikidata.org/entity/Q123>, 
	<https://d-nb.info/gnd/123456789>, 
	<http://tls.theaterwissenschaft.ch/wiki/Firstname_Lastname> ;
	ric:R210_is_subject_of <http://data.performing-arts.ch/r/789664> .
```

### Groups and Legal Bodies

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.
@prefix ric: <http://yet-to-be-defined-ric-implementation/>.
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/638821> a crm:E40_Legal_Body, ric:E4_Agent ;
	ric:P32_Type spav:agenttype-legalbody ;
	crm:P2_has_type spav:grouptype-producer ;
	rdfs:label "Theatre ABC" ;
	crm:P1_is_identified_by [ a crm:E82_Actor_Appellation ] ;
	ric:P33_Identity_Type spav:identitytype-given ;
	crm:P95i_was_formed_by [ a crm:E66_Formation ] ;
	crm:P99i_was_dissolved_by [ a crm:E68_Dissolution ] ;
	ric:R273_is_successor_of <http://data.performing-arts.ch/a/354227> ;
	ric:R269_is_predecessor_of <http://data.performing-arts.ch/a/921648> ;
	crm:P107_has_current_or_former_member <http://data.performing-arts.ch/a/539818> ;
	crm_P76_has_contact_point [ a crm:E45_Address ;
		rdf:value "Street, Place, Country" ;
		crm_P2_has_type spav:contactpoint-address
	] ;
	crm_P76_has_contact_point [ a crm:E51_Contact_Point ;
		rdf:value <http://www.theatre-abc.ch> ;
		crm_P2_has_type spav:contactpoint-website
	] ;
	crm:P74_has_current_ or_former_residence [ a crm:Place ;
		crm:P87_is_identified_by [ a crm:E45_Address ;
			rdf:value "Street, Place, Country" ;
			crm_P2_has_type spav:contactpoint-address
		] ;
		crm:P89_falls_within <http://data.performing-arts.ch/p/763919>
	] ;
	crm:P14i_performed [ a crm:E7_Activity ;
		crm:P2_has_type spav:genre-spokentheatre
	] ;
	crm:P14i_performed [ a crm:E7_Activity ;
		crm:P2_has_type spav:activity-stagemanagement ;
		crm:P16_used_specific_object <http://data.performing-arts.ch/o/165290> ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ]

	] ;
	ric:R210_is_subject_of <http://data.performing-arts.ch/r/456> .
```

<!-- TODO: How to represent the temporalities of memberships? -->
<!-- TODO: How to represent that one actor/agent controls another? -->
<!-- TODO: Change the two identical blank node addresses into into one entity with URI? -->

