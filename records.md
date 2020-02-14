---
layout: page
title: Records
---

Records and record sets wil be described according to [Records in Context](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context") (RiC). However, as there is no official ontology for RiC yet, classes and properties for the time being may be substituted with equivalents from other ontologies such as [PREMIS](http://id.loc.gov/ontologies/premis.html), [PROV](http://www.w3.org/TR/prov-overview/) and [RDA](http://www.rdaregistry.info). Also, some information might be stored as literal values instead of structured links to other entities as a result of the migration from legacy databases. Such data might be restructured at a later time together with a refined data model.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix dct: <http://purl.org/dc/terms/> .
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID2> a rico:RecordSet ;
    dc:title "Klainguti, Battista" ;
    dc:indentifier "123-KB" ;
    dc:type spav:qekqz ;
    dc:description "press clippings"
    dc:date "2001-2009" ;
    rdfs:comment "some comment" ;
    dc:extent [
    	a dct:SizeOrDuration ;
    	rdf:value "2 R <Sammelcouvert>" .
    ] ;
    rico:isPartOf <http://data.performing-arts.ch/r/UUID1> .

```

* `spav:qekqz`= "file"