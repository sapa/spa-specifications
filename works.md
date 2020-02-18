---
layout: page
title: Works
---

[FBBRoo](https://www.ifla.org/publications/node/11240) as a bibliographical model distinguishes between `F1 Work`, `F2 Expression`, `F3 Manifestation` and `F5 Item` as different levels of abstractions for describing literature. This allows to represent the relations between different versions, editions and physical manifestations of literary works. Analog to the first three of these classes FRBRoo also provides classes to describe performative works: `F20 Performance Work`, `F25 Performance Plan` and `F31 Performance`. This allows us to relate productions to their individual performances on the one side and the abstract concepts that stand above original productions and re-stagings on the other side. (See [Doerr, M., Bekiari, C., LeBoeuf, P., & nationale de France, B. (2008). FRBRoo, a conceptual model for performing arts. In 2008 Annual Conference of CIDOC, Athens](http://ftp.ics.forth.gr/_publications/drfile.2008-06-42.pdf))

As a general system each production in the database is represented as work, plan and performance with the plan as the main entity. This hierarchy is also reflected in the URIs:

* `F25 Performance Plan`: `http://data.performing-arts.ch/w/UUID`
* `F20 Performance Work`: `http://data.performing-arts.ch/w/UUID/w`
* `F31 Performance`: `http://data.performing-arts.ch/w/UUID/p`

In the case of a re-staging the plan refers to the work instance of the original production. The default performance (`/w/UUID/p`) is an abstract entity that holds information that all performances share. Specific performances such as the premiere are then parts of the default performance with subordinate URIs (`/w/UUID/p/UUID`).

### Levels of a Production <a id="production-levels"></a>

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1/> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" ;

<http://data.performing-arts.ch/w/UUID1/w> a frbroo:F20_Performance_Work ;
    rdfs:label "Die Grönholm-Methode" ;
    crm:P2_has_type spav:mnawx ;
    frbroo:R12_is_realised_in <http://data.performing-arts.ch/w/UUID1> .

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
    frbroo:R25_performed <http://data.performing-arts.ch/w/UUID1> ;
    crm:P9_consists_of <http://data.performing-arts.ch/w/UUID1/p/UUID2> .
    
<http://data.performing-arts.ch/w/UUID1/p/UUID2> a frbroo:F31_Performance  ;
    crm:P2_has_type spav:hlosp ;
    crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "5.4.2017" ;
			crm:P82a_begin_of_the_begin "2017-04-05"^^xsd:date ;
			crm:P82b_end_of_the_end "2017-04-05"^^xsd:date .
		] .

spav:mnawx a crm:E55_Type, skos:Concept ;
        skos:prefLabel "performance art"@en .

spav:hlosp a crm:E55_Type, skos:Concept ;
        skos:prefLabel "German language premiere"@en .
```

<!-- TODO: crm:P9_consists_of or frbroo:has_part ?-->

### Activities <a id="activities"></a>

FRBRoo and CIDOC-CRM provide two ways to connect the individual performance works and plans, either directly as shown above with `R12 is realised in` or through an activity. The latter option is needed to provide further information about when and by whom the act of translation was done. All activities that are needed to create the `F25 Performance Plan` (production, direction, stage design etc.) are then parts of this `F28 Expression Creation`. Activities that only take place in relation to an actual performance are parts of one of the performances depending on whether they are general or only happened as part of single performances.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" .

<http://data.performing-arts.ch/w/UUID1/w> a frbroo:F20_Performance_Work ;
	rdfs:label "Die Grönholm-Methode" ;
    frbroo:R12_is_realised_in <http://data.performing-arts.ch/w/UUID1> .

<http://data.performing-arts.ch/x/UUID3> a frbroo:F28_Expression_Creation ;
	frbroo:R19_created_a_realisation_of <http://data.performing-arts.ch/w/UUID1/w> ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID1> ;
	crm:P9_consists_of [ a crm:E7_Activity ;
    	crm:P2_has_type spav:muwgo ;
    	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID5> . ] ,
    	[ a crm:E7_Activity ;
    	crm:P2_has_type spav:mutnt ;
    	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID5> . ] .

<http://data.performing-arts.ch/a/UUID5> a crm:E40_Legal_Body  ;
	rdfs:label "Theater Matte" .

<http://data.performing-arts.ch/a/UUID6> a crm:E21_Person  ;
	rdfs:label "Oliver Stein" .

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
    frbroo:R25_performed <http://data.performing-arts.ch/w/UUID1> ;
	crm:P9_consists_of [ a crm:E7_Activity ;
    	crm:P2_has_type spav:munib ;
    	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID7> . ]

<http://data.performing-arts.ch/a/UUID7> a crm:E21_Person  ;
	rdfs:label "Markus Maria Enggist" .

spav:muwgo a crm:E55_Type, skos:Concept ;
    skos:prefLabel "production"@en .

spav:mutnt a crm:E55_Type, skos:Concept ;
    skos:prefLabel "stage direction"@en .

spav:munib a crm:E55_Type, skos:Concept ;
    skos:prefLabel "acting"@en .
```

<!-- TODO: role and order -->

The usage of activities is necessary to provide certain information but as this information might not be relevant in all cases the direct connection between `F20 Performance Work` and `F25 Performance Plan` is also used. The same applies to sources (such as literary works) and documentations (such as video recordings) as they are also rendered as FRBRoo individuals.

All contributions to performing arts productions are rendered as instances of `E7 Activity` and classified with the [SPA vocabulary](https://sapa.github.io/spa-vocabulary/). Alternative designations for an activity are preserved with an optional `rdfs:label`.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/x/UUID1> a frbroo:F28_Expression_Creation ;
        crm:P9_consists_of [ a crm:E7_Activity ;
	        crm:P2_has_type spav:mutnt ;
    	    rdfs:label "installation" ;
        	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID2> .
        ] .

<http://data.performing-arts.ch/a/UUID2> a crm:E21_Person ;
	rdfs:label "William Forsythe" .

spav:mutnt a crm:E55_Type, skos:Concept ;
    skos:prefLabel "stage design"@en .
```

In the above example, William Forsythe has a credit for "installation" which is preserved additionally to the classification of his contribution as stage design.


### Additional Information <a id="additional-information"></a>

<!-- TODO: acts and scenes  act_count, scene_count / spa:number_of_acts, spa_number_of_scenes xsd:int -->

The [venue](venues) is linked with the default performance.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
	crm:P8_took_place_ on_or_within <http://data.performing-arts.ch/o/UUID2>

<http://data.performing-arts.ch/o/UUID2> a crm:E22_Man-Made_Object ;
    rdfs:label "Theater Matte" ;
    crm:P2_has_type spav:dwmkn .

spav:dwmkn a crm:E55_Type, skos:Concept ;
    skos:prefLabel "venue"@en .
```

The spoken language and possible subtitles are defined as properties of the `frbroo:F20_Performance_Work`.

```ttl
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix schema: <http://schema.org/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1/w> a frbroo:F20_Performance_Work ;
	schema:inLanguage spav:lgita ;
    schema:subtitleLanguage spav:lgdeu .

spav:lgita a crm:E55_Type, skos:Concept ;
    skos:prefLabel "Italian"@en .

spav:lgdeu a crm:E55_Type, skos:Concept ;
    skos:prefLabel "German"@en .
```


### Sources <a id="sources"></a>

FRBRoo is also used to describe the literary reference of a production.

<!-- TODO: Store all sources temporality in one entity? -->
<!-- TODO: Extend vocabulary. -->

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" ;
    frbroo:R14_incorporates <http://data.performing-arts.ch/w/UUID2> .

<http://data.performing-arts.ch/w/UUID2> a frbroo:F22_Self-Contained_Expression ;
	rdfs:label "Die Grönholm-Methode" ;
	crm:P2_has_type spav:WORK-ADAPTION ;
    frbroo:R14_incorporates <http://data.performing-arts.ch/w/UUID5> .

<http://data.performing-arts.ch/x/UUID3> a frbroo:F28_Expression_Creation  ;
	crm:P2_has_type spav:mudcw ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID2> ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID4> .

<http://data.performing-arts.ch/a/UUID4> a crm:E21_Person  ;
	rdfs:label "Corinne Thalmann" .

<http://data.performing-arts.ch/w/UUID5> a frbroo:F22_Self-Contained_Expression ;
	rdfs:label "Die Grönholm-Methode" ;
	crm:P2_has_type spav:WORK-TRANSLATION ;
    frbroo:R14_incorporates <http://data.performing-arts.ch/w/UUID8> .

<http://data.performing-arts.ch/x/UUID6> a frbroo:F28_Expression_Creation  ;
	crm:P2_has_type spav:muwyo ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID5> ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID7> .

<http://data.performing-arts.ch/a/UUID7> a crm:E21_Person  ;
	rdfs:label "Stefanie Gerhold" .

<http://data.performing-arts.ch/w/UUID8> a frbroo:F22_Self-Contained_Expression ;
	rdfs:label "El mètode Grönholm" .
	crm:P2_has_type spav:WORK-ORIGINAL .

<http://data.performing-arts.ch/x/UUID9> a frbroo:F28_Expression_Creation  ;
	crm:P2_has_type spav:muiuk ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID8> ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID10> .

<http://data.performing-arts.ch/a/UUID10> a crm:E21_Person  ;
	rdfs:label "Jordi Galceran" .

spav:mudcw a crm:E55_Type, skos:Concept ;
    skos:prefLabel "adaption"@en .

spav:muwyo a crm:E55_Type, skos:Concept ;
    skos:prefLabel "translation"@en .

spav:muiuk a crm:E55_Type, skos:Concept ;
    skos:prefLabel "authorship"@en .
```

While each `F22 Self-Contained Expression` according to FRBRoo comes with a `F1 Work`, the rendering of the letter is omitted for the sake of reducing complexity.

<!-- TODO: add vocab for texts types -->

### Documentation <a id="documentation"></a>

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" ;
    frbroo:R14_incorporates <http://data.performing-arts.ch/w/UUID2> .

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
    frbroo:R25_performed <http://data.performing-arts.ch/w/UUID1> ;
    crm:P9_consists_of <http://data.performing-arts.ch/w/UUID1/p/UUID2> .

<http://data.performing-arts.ch/w/UUID1/p/UUID2> a frbroo:F31_Performance  ;
    crm:P4_has_time-span [ a crm:E52_Time-Span ;
        rdfs:label "5.4.2017" .
    ] .

<http://data.performing-arts.ch/w/UUID3> a frbroo:F29_Recording_Event  ;
    frbroo:R20_recorded <http://data.performing-arts.ch/w/UUID1/p/UUID2> ;
	crm:P9_consists_of <http://data.performing-arts.ch/w/UUID4> .

<http://data.performing-arts.ch/w/UUID4> a crm:E7_Activity ;
	crm:P2_has_type spav:mujig ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID5> ;
	frbroo:R22_realised <http://data.performing-arts.ch/w/UUID6> .

<http://data.performing-arts.ch/a/UUID5> a crm:P21_Person ;
	rdfs:label "NN" .

<http://data.performing-arts.ch/w/UUID6> a frbroo:F21_Recording_Work  .

spav:mujig a crm:E55_Type, skos:Concept ;
    skos:prefLabel "camera operation"@en .
```

<!-- TODO: add identifier to recording work -->
