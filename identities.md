---
layout: page
title: Identities
---

Before any statements are made about an entity, it should be identified. Such identifications are happening on three different levels: by attributing a type, by assigning one or more identifiers and by documenting real world appellations used in regard to the entity.

### Types <a id="types"></a>

Standard classes as defined by CIDOC-CRM, FRBRoo and RiC are used. Own class-like categories from the [Swiss Performing Arts vocabulary](https://sapa.github.io/spa-vocabulary/) are attributed trough `crm:P2_has_type`. On both levels more that one classification can be used.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID1> a crm:E40_Legal_Body, rico:CorporateBody ;
    crm:P2_has_type spav:abcde .
```

### Identifiers <a id="identifiers"></a>

The primary identifier is the URI of a resource. URIs are structured according to the five basic categories:

* Actors: `http://data.performing-arts.ch/a/<UUID>`
* Works: `http://data.performing-arts.ch/w/<UUID>`
* Objects: `http://data.performing-arts.ch/o/<UUID>`
* Concepts: `http://data.performing-arts.ch/c/<UUID>`
* Places: `http://data.performing-arts.ch/p/<UUID>`
* Records: `http://data.performing-arts.ch/r/<UUID>`
* Seasons: `http://data.performing-arts.ch/s/<YEAR1>-<YEAR2>`

Some properties of actors such as gender or nationality are rendered by CIDOC-CRM als group memberships. These groups are identified as `http://data.performing-arts.ch/g/<TYPE>/<VALUE>`, where `<TYPE>` stands for groups types (`gender`, `nation`) and `<VALUE>` for the respective group identities (`f`, `m`, and `d` for gender and ISO 3166-1 country codes for nationality). For the time being Swiss nationality is the only one that is mapped in order to avoid the complexity of historicizing nationalities and because this is satisfactory in regard to our collection policy.

Entities that are only used once in regard to other instances (such as appellations or descriptions) are conceptually seen as blank nodes and in this specification are described as such. However, for technical reasons they are effectively rendered as URIs of a special category: `http://data.performing-arts.ch/x/<UUID>`.

Entities that are considered to be not yet identified also have a separate name space: `http://data.performing-arts.ch/u/<UUID>`.

Inventory numbers are stored according to CIDOC-CRM and RiC/PREMIS.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix premis: <http://www.loc.gov/premis/rdf/v1#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/o/UUID2> a crm:E22_Man-Made_Object, rico:Thing ;
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

The CIDOC-CRM has one main class (`E41 Appellation`) and several subclasses in respect to the type of entity that is described (`E82 Actor Appellation`, `E35 Title`, `E48 Place Name`). In all cases the usage is the same and as appellations are never used for more than one entity, they are modeled as blank nodes.

`rdfs:label` is additionally used for the most common appellation in order to facilitate database requests that are not primarily interested in appellations.

#### Groups

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID4> rdfs:label "Konzert Theater Bern" ;
    crm:P131_is_identified_by [
    	a crm:E82_Actor_Appellation ;
        rdf:value "Konzert Theater Bern" ;
        crm:P2_has_type spav:yanuj
    ] ;
    crm:P131_is_identified_by [
    	a crm:E82_Actor_Appellation ;
        rdf:value "KTB" ;
        crm:P2_has_type spav:yamqk
    ] ;
    crm:P67_is_referred_to_by [
    	a crm:E33_Linguistic_Object ;
        rdf:value "Beschreibung des Theaters" ;
        crm:P2_has_type spav:eoept
    ] .
```

* `spav:yanuj` = "official name"
* `spav:yamqk` = "acronym"
* `spav:eoept` = "description"

#### Persons

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID5> a crm:E21_Person, rico:Person ;
	rdfs:label "Lilli Palmer" ;
    crm:P131_is_identified_by [
    	a crm:E82_Actor_Appellation ;
        rdf:value "Lilli Palmer" ;
        crm:P2_has_type spav:yatcx ;
        crm:P2_has_type spav:yaajh
    ] ;
    crm:P131_is_identified_by [
    	a crm:E82_Actor_Appellation ;
        rdf:value "Lilli Marie Peiser" ;
        crm:P2_has_type spav:yadpx
    ] .
```

* `spav:yatcx` = "common name"
* `spav:yadpx` = "birth name"
* `spav:yaajh` = "pseudonym"

Any literal value such as `rdfs:label` or `rdf:value` may be used with language tags.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID6> a crm:E21_Person, rico:Person ;
    rdfs:label "Fyodor Mikhaylovich Dostoyevsky"@en ;
    rdfs:label "Fjodor Michailowitsch Dostojewski"@de ;
    rdfs:label "Fiodor Mikhaïlovitch Dostoïevski"@fr ;
    rdfs:label "Fëdor Michajlovič Dostoevskij"@it ;
    crm:P131_is_identified_by [ 
        a crm:E82_Actor_Appellation ;
        rdf:value "Fyodor Mikhaylovich Dostoyevsky"@en ;
        rdf:value "Fjodor Michailowitsch Dostojewski"@de ;
        rdf:value "Fiodor Mikhaïlovitch Dostoïevski"@fr ;
        rdf:value "Fëdor Michajlovič Dostoevskij"@it
    ] .
```

<!-- TODO: Other examples, e.g. for work titles? -->

