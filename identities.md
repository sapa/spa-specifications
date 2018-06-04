## Identities

Before any statements are made about an entity, it should be identified. Such identifications are happening on three different levels: by attributing a type, by assigning one or more identifiers and by documenting real world appellations used in regard to the entity.

### Types

Standard classes as defined by CIDOC-CRM, FRBRoo and RiC are used. Own class-like categories from the [Swiss Performing Arts vocabulary](https://sapa.github.io/spa-vocabulary/) are attributed trough `crm:P2_has_type`. On both levels more that one classification can be used.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.
@prefix ric: <http://yet-to-be-defined-ric-implementation/>.
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

<!-- TODO: Do the categories need separate prefixes or can the ids simply start with the category letter? a-id -->

Inventory numbers are stored according to CIDOC and RiC.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.
@prefix ric: <http://yet-to-be-defined-ric-implementation/>.
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/o/123456> a crm:E24_Physical_Man-Made_Thing ;
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

The CIDOC-CRM has one main class (`E41 Appellation`) and several subclasses (`E35 Title`, `E35 Title`, `E44 Place Appellation`, `E82 Actor Appellation`, ...) to document appellations. Here the subclasses are used in respect to the type of entity that is described. However, in all cases the structure is the same and as appellations are never used for more than one entity, they are modeled as blank nodes.

`rdfs:Label` is additionally used for the most common appellation in order to facilitate database requests that are not primarily interested in appellations.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.
@prefix ric: <http://yet-to-be-defined-ric-implementation/>.
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/123456> rdfs:label "Konzert Theater Bern" ;
	crm:P1_is_identified_by [ a crm:E82_Actor_Appellation ;
		rdf:value = "Konzert Theater Bern" ;
		crm:P2_has_type spav:appellation-officialname ;
		crm:P139_has_alternative_form [ a crm:E82_Actor_Appellation ;
			rdf:value "KTB" ;
			crm:P2_has_type spav:appellation-abbreviation
		]
	] ;
	crm:P67_is_referred_to_by [ a crm:E33_Linguistic_Object ;
		rdf:value "Beschreibung des Theaters" ;
		crm:P2_has_type spav:appellation-description
	] .
```

<!-- TODO: provide example with times -->

<!-- TODO: How to handle different languages? -->

<!-- TODO: Other examples, e.g. for work titles? -->

