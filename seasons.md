---
layout: page
title: Seasons
---

Performing arts productions are usually organized in annual seasons lasting from one summer until the next. The attribution of an individual production to a general season happens by defining the production's `F28 Expression Creation ` as part of a `E4 Period` that is the respective season. This season is the same for all producers. However, the productions also falls into a directorship that is responsible for the program of several seasons at a specific theater. Such a directorship is carried out by one or more persons and the theater as an institution.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbr: <http://www.cidoc-crm.org/frbr/> .
@prefix spav: <http://vocab.performing-arts.ch/> .
@prefix wd: <http://www.wikidata.org/entity/> .

<http://data.performing-arts.ch/w/UUID1> a frbr:F25_Performance_Plan ;
    rdfs:label "Hello, Mister MacGuffin!" .

<http://data.performing-arts.ch/x/UUID2> a frbr:F28_Expression_Creation  ;
    frbr:R17_created <http://data.performing-arts.ch/w/UUID1> ;
    crm:P10_falls_within <http://data.performing-arts.ch/e/UUID3> ,
        <http://data.performing-arts.ch/e/UUID4> .

<http://data.performing-arts.ch/e/UUID3> a crm:E4_Period ;
    rdfs:label "Season 2017/18" .

<http://data.performing-arts.ch/e/UUID4> a crm:E7_Activity ;
    rdfs:label "Directorship Barbara Frey, Schauspielhaus Zürich" ;
    crm:P4_has_time-span [ a crm:E52_Time-Span ;
        rdfs:label "1.8.2009 -" ;
        crm:P82a_begin_of_the_begin "2009-08-01"^^xsd:date .
    ] ;
    crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID5> ,
        <http://data.performing-arts.ch/a/UUID5> .

<http://data.performing-arts.ch/a/UUID5> a crm:E40_Legal_Body  ;
    rdfs:label "Schaupielhaus Zürich" .

<http://data.performing-arts.ch/a/UUID6> a crm:E21_Person  ;
    rdfs:label "Barbara Frey" .
```