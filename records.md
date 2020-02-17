---
layout: page
title: Records
---

Records and record sets are described according to [Records in Context](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context") (RiC). However, these decriptions will evolve slowly with the amount of migrated data and in consideration of emerging RiC conventions. Also, some information might be stored as literal values instead of structured links to other entities as a result of the migration from legacy databases. Such data will be restructured at a later time together with a refined data model.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix ric-rst: <https://www.ica.org/standards/RiC/vocabularies/recordSetTypes#> .
@prefix dc: <http://purl.org/dc/elements/1.1/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID2> a rico:RecordSet ;
    rico:name "Klainguti, Battista" ;
    rico:identifier "123-KB" ;
    rico:hasRecordSetType ric-rst:File ;
    rico:hasDocumentaryFormType spav:dffop ;
    dc:date "2001-2009" ;
    rico:recordResourceExtent "2 R <Sammelcouvert>" ;
    rico:descriptiveNote "some comment" ;
    rico:isPartOf <http://data.performing-arts.ch/r/UUID1> .

```

* `spav:dffop`= "clippings"