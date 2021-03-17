---
layout: page
title: Venues
---

Venues are the sites where a performance is actually happening. What makes their representation intricate is that CIDOC-CRM distinguishes between location (`P53 Place`) and infrastructure (`E18 Physical Thing` or `E22 Man-Made Object`). In order to described such sites comprehensively here both aspects are combined. They are primarily understood and identified as a `E22 Man-Made Object` that always comes with a specific but unidentified `P53 Place`. These places optionally come with a `crm:E94_Space_Primitive` and a `crm:E45_Address`.

Venues can contain each other in that sense that a building can contain one or more specifc stages, which are connected with `crm:P46_is_composed_of`. The stages then do not come with individual places as theit location is already defined through the building they are part of.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/o/UUID1> a crm:E22_Man-Made_Object, rico:Thing ;
    rdfs:label "Kaserne Basel" ;
    crm:P2_has_type spav:dwmkn ;
    crm:P102_has_title [ a crm:E35_Title ;
        rdf:value "Kaserne Basel" .
    ] ;
    crm:P156_occupies [ a crm:P53_Place ;
        crm:P168_place_is_defined_by [ a crm:E94_Space_Primitive ] ;
        crm:P87_is_identified_by [ a crm:E45_Address ;
             rdf:value "Klybeckstrasse 1b, 4057 Basel, CH" ] ;
        crm:P89_falls_within <http://data.performing-arts.ch/p/UUID2>
    ] ;
    crm:P46_is_composed_of <http://data.performing-arts.ch/o/UUID3> ;
    rico:hasBeginningDate [ a rico:Date ;
        rico:normalizedDateValue "1980" ;
        rico:dateStandard "ISO 8601" .
    ] ;
    rico:hasEndDate [ a rico:Date ;
        rico:normalizedDateValue "1999" ;
        rico:dateStandard "ISO 8601" .
    ] .
    
<http://data.performing-arts.ch/a/UUID4> a crm:E40_Legal_Body, rico:CorporateBody ;
    rdfs:label "Kaserne Basel" .

<http://data.performing-arts.ch/o/UUID3> a crm:E22_Man-Made_Object, rico:Thing ;
    rdfs:label "Reithalle" ;
    crm:P2_has_type spav:dwmkn ;
    crm:P8i_witnessed <http://data.performing-arts.ch/w/UUID5> .

<http://data.performing-arts.ch/w/UUID5> a frbroo:F31_Performance ;
    rdfs:label "Worst Case Szenarios" .

<http://data.performing-arts.ch/p/UUID2> a crm:P53_Place ;
    rdfs:label "Basel" .
```

* `spav:dwmkn`= "venue"
* `spav:mujfv`= "management"
