---
layout: page
title: Venues
---

Venues are the sites where a performance is actually happening. What makes their representation intricate is that CIDOC-CRM distinguishes between location (`P53 Place`) and infrastructure (`E18 Physical Thing` or `E22 Man-Made Object`), i.e. a building and its stage(s). In order to described such sites comprehensively here both aspects are combined.

Buildings (`spav:dwvhk`) and their venues (`spav:dwmkn`) are properly identified with URIs while an abstract place is attached to the building only to provide the option to add required data such as an address or the specific city a building is located in.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .

<http://data.performing-arts.ch/o/31552> a crm:E22_Man-Made_Object ;
    rdfs:label "Kaserne Basel" ;
    crm:P2_has_type spav:dwvhk ;
    crm:P1_is_identified_by [ crm:E41_Appellation ] ;
    crm:P156_occupies [ a crm:P53_Place ;
        crm:P168_place_is_defined_by [ a crm:E94_Space_Primitive ] ;
        crm:P87_is_identified_by [ a crm:E45_Address ;
             rdf:value "Klybeckstrasse 1b, 4057 Basel, CH" ] ;
        crm:P89_falls_within <http://data.performing-arts.ch/o/23456>
    ] ;
    crm:P46_is_composed of <http://data.performing-arts.ch/o/88630> ;
    crmP16i_was_used_for [ a crm:E7_Activity ;
    	crm:P2_has_type spav:management ;
    	crm:P14_carried_out_by <http://data.performing-arts.ch/a/52776>
    ] .
    
<http://data.performing-arts.ch/a/52776> a crm:E40_Legal_Body, ric:E4_Agent ;
	rdfs:label "Kaserne Basel" .

<http://data.performing-arts.ch/o/88630> a crm:E22_Man-Made_Object ;
    rdfs:label "Reithalle" ;
    crm:P2_has_type spav:dwmkn ;
    crm:P8i_witnessed <!-- TODO: add performance --> .

<http://data.performing-arts.ch/w/09371> a frbr:F31_Performance  ;
	rdfs:label "Worst Case Szenarios" .

<http://data.performing-arts.ch/p/76529> a crm:P53_Place ;
    rdfs:label "Basel" .
```

