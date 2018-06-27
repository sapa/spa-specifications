---
layout: page
title: Identities
---

Before any statements are made about an entity, it should be identified. Such identifications are happening on three different levels: by attributing a type, by assigning one or more identifiers and by documenting real world appellations used in regard to the entity.

### Types

Standard classes as defined by CIDOC-CRM, FRBRoo and RiC are used. Own class-like categories from the [Swiss Performing Arts vocabulary](https://sapa.github.io/spa-vocabulary/) are attributed trough `crm:P2_has_type`. On both levels more that one classification can be used.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix ric: <http://yet-to-be-defined-ric-implementation/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/123456> a crm:E40_Legal_Body, ric:E4_Agent ;
	crm:P2_has_type spav:XXX ;
	ric:P32_Type spav:XXX ;
	ric:P33_Identity_Type spav:XXX .
```

<!-- TODO: Rethink RiC types. -->

### Internal identifiers

The primary identifier is the URI of a resource. URIs are structured according to the five basic categories:

* Actors: `http://data.performing-arts.ch/a/<ID>`
* Works: `http://data.performing-arts.ch/w/<ID>`
* Objects: `http://data.performing-arts.ch/o/<ID>`
* Places: `http://data.performing-arts.ch/p/<ID>`
* Records: `http://data.performing-arts.ch/r/<ID>`

Entities that are only used once in regard to other instances (such as appellations or descriptions) are conceptually seen as blank nodes and in this specification are described as such. However, for technical reasons they are effectively rendered as URIs of specific category: `http://data.performing-arts.ch/x/<ID>`.

Inventory numbers are stored according to CIDOC-CRM and RiC.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix ric: <http://yet-to-be-defined-ric-implementation/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/o/123456> a crm:E24_Physical_Man-Made_Thing, ric:E1_Record ;
	crm:P1_is_identified_by [ a crm:E42_Identifier ;
		rdf:value "E-123456" ;
		crm:P2_has_type spav:specific-identifier .
	] ;
	ric:P2_Local_Identifier "E-123456" .
```

### Links to external identifiers

Links to other databases such as Wikidata are considered to be objective and stable. Therefore instead of the CIDOC-CRM's elaborate options to describe identifiers, a simple `owl:sameAs` is used.

```ttl
<http://data.performing-arts.ch/a/123456> owl:sameAs <http://www.wikidata.org/entity/Q807427>, 
	<https://d-nb.info/gnd/1102238422>, 
	<http://tls.theaterwissenschaft.ch/wiki/Barbara_Frey> .
```

<!-- TODO: This does not allow to look for external identifiers based on categories easily. Provide SPARQL code to show all Wikidata-Entries? Or use `42 Identifier` with type Wikidata? -->

### Appellations

The CIDOC-CRM has one main class (`E41 Appellation`) and several subclasses to document appellations. Here subclasses are only used if they express a specific form of appellation in respect to the type of entity that is described (`E35 Title`, `E48 Place Name`). However, in all cases the structure is the same and as appellations are never used for more than one entity, they are modeled as blank nodes.

`rdfs:Label` is additionally used for the most common appellation in order to facilitate database requests that are not primarily interested in appellations.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix ric: <http://yet-to-be-defined-ric-implementation/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/123456> rdfs:label "Konzert Theater Bern" ;
	crm:P1_is_identified_by [ a crm:E41_Appellation ;
		rdf:value "Konzert Theater Bern" ;
		crm:P2_has_type spav:appellation-officialname ;
		crm:P139_has_alternative_form [ a crm:E41_Appellation ;
			rdf:value "KTB" ;
			crm:P2_has_type spav:appellation-abbreviation
		]
	] ;
	crm:P67_is_referred_to_by [ a crm:E33_Linguistic_Object ;
		rdf:value "Beschreibung des Theaters" ;
		crm:P2_has_type spav:appellation-description
	] .
```

Any literal value such as `rdfs:label` or `rdf:value` may be used with language tags.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix ric: <http://yet-to-be-defined-ric-implementation/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/452987> a crm:E21_Person, ric:E4_Agent ;
	ric:P32_Type spav:agenttype-person ;
	rdfs:label "Fyodor Mikhaylovich Dostoyevsky"@en ;
	rdfs:label "Fjodor Michailowitsch Dostojewski"@de ;
	rdfs:label "Fiodor Mikhaïlovitch Dostoïevski"@fr ;
	rdfs:label "Fëdor Michajlovič Dostoevskij"@it ;
	crm:P1_is_identified_by [ 
		a crm:E41_Appellation ;
		rdf:value "Fyodor Mikhaylovich Dostoyevsky"@en ;
		rdf:value "Fjodor Michailowitsch Dostojewski"@de ;
		rdf:value "Fiodor Mikhaïlovitch Dostoïevski"@fr ;
		rdf:value "Fëdor Michajlovič Dostoevskij"@it
	] .
```

<!-- TODO: Other examples, e.g. for work titles? -->

