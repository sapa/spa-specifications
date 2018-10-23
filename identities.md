---
layout: page
title: Identities
---

Before any statements are made about an entity, it should be identified. Such identifications are happening on three different levels: by attributing a type, by assigning one or more identifiers and by documenting real world appellations used in regard to the entity.

### Types <a id="types"></a>

Standard classes as defined by CIDOC-CRM, FRBRoo and RiC (respectively its alternatives) are used. Own class-like categories from the [Swiss Performing Arts vocabulary](https://sapa.github.io/spa-vocabulary/) are attributed trough `crm:P2_has_type`. On both levels more that one classification can be used.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID1> a crm:E40_Legal_Body, prov:Agent ;
	crm:P2_has_type spav:abcde .
```

### Identifiers <a id="identifiers"></a>

The primary identifier is the URI of a resource. URIs are structured according to the five basic categories:

* Actors: `http://data.performing-arts.ch/a/<UUID>`
* Works: `http://data.performing-arts.ch/w/<UUID>`
* Objects: `http://data.performing-arts.ch/o/<UUID>`
* Places: `http://data.performing-arts.ch/p/<UUID>`
* Records: `http://data.performing-arts.ch/r/<UUID>`

<!-- TODO: Do I have to distinguish here between works and performances? -->

Entities that are only used once in regard to other instances (such as appellations or descriptions) are conceptually seen as blank nodes and in this specification are described as such. However, for technical reasons they are effectively rendered as URIs of a special category: `http://data.performing-arts.ch/x/<UUID>`.

Entities that are considered to be not yet identified also have a separate name space: `http://data.performing-arts.ch/u/<UUID>`.

Inventory numbers are stored according to CIDOC-CRM and RiC/PREMIS.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix premis: <http://www.loc.gov/premis/rdf/v1#> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/o/UUID2> a crm:E24_Physical_Man-Made_Thing, prov:Entity ;
	crm:P1_is_identified_by [ a crm:E42_Identifier ;
		rdf:value "E-123456" ;
		crm:P2_has_type spav:wayst .
	] ;
	premis:hasIdentifier "E-123456" .
```

* `spav:wayst` = "signature"

### Links to external identifiers <a id="external-identifiers"></a>

Links to other databases such as Wikidata are considered to be objective and stable. Therefore instead of the CIDOC-CRM's elaborate options to describe identifiers, a simple `owl:sameAs` is used.

```ttl
<http://data.performing-arts.ch/a/UUID3> owl:sameAs <http://www.wikidata.org/entity/Q807427>, 
	<https://d-nb.info/gnd/1102238422>, 
	<http://tls.theaterwissenschaft.ch/wiki/Barbara_Frey> .
```

<!-- TODO: This does not allow to look for external identifiers based on categories easily. Provide SPARQL code to show all Wikidata-Entries? Or use `42 Identifier` with type Wikidata? -->

### Appellations <a id="appellations"></a>

The CIDOC-CRM has one main class (`E41 Appellation`) and several subclasses to document appellations. Here subclasses are only used if they express a specific form of appellation in respect to the type of entity that is described (`E35 Title`, `E48 Place Name`). However, in all cases the structure is the same and as appellations are never used for more than one entity, they are modeled as blank nodes.

`rdfs:label` is additionally used for the most common appellation in order to facilitate database requests that are not primarily interested in appellations.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID4> rdfs:label "Konzert Theater Bern" ;
	crm:P1_is_identified_by [ a crm:E41_Appellation ;
		rdf:value "Konzert Theater Bern" ;
		crm:P2_has_type spav:yanuj ;
		crm:P139_has_alternative_form [ a crm:E41_Appellation ;
			rdf:value "KTB" ;
			crm:P2_has_type spav:yamqk
		]
	] ;
	crm:P67_is_referred_to_by [ a crm:E33_Linguistic_Object ;
		rdf:value "Beschreibung des Theaters" ;
		crm:P2_has_type spav:eoept
	] .
```

* `spav:yanuj` = "official name"
* `spav:yamqk` = "acronym"
* `spav:eoept` = "description"


Any literal value such as `rdfs:label` or `rdf:value` may be used with language tags.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID5> a crm:E21_Person, prov:Agent ;
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

