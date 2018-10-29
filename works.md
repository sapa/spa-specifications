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
@prefix frbroo: <http://erlangen-crm.org/efrbroo/> .
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
```

* `spav:mnawx`= "performance art"
* `spav:hlosp`= "German language premiere"


### Activities <a id="activities"></a>

FRBRoo and CIDOC-CRM provide two ways to connect the individual performance works and plans, either directly as shown above with `R12 is realised in` or through an activity. The latter option is needed to provide further information about when and by whom the act of translation was done. All activities that are needed to create the `F25 Performance Plan` (production, direction, stage design etc.) are then parts of this `F28 Expression Creation`. Activities that only take place in relation to an actual performance are parts of one of the performances depending on whether they are general or only happened as part of single performances.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://erlangen-crm.org/efrbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" ;

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
	rdfs:label "Theater Matte" ;

<http://data.performing-arts.ch/a/UUID6> a crm:E21_Person  ;
	rdfs:label "Oliver Stein" ;

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
    frbroo:R25_performed <http://data.performing-arts.ch/w/UUID1> ;
	crm:P9_consists_of [ a crm:E7_Activity ;
    	crm:P2_has_type spav:munib ;
    	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID7> . ]

<http://data.performing-arts.ch/a/UUID7> a crm:E21_Person  ;
	rdfs:label "Markus Maria Enggist" ;

```

<!-- TODO: role and order -->

* `spav:muwgo`= "production"
* `spav:mutnt`= "stage direction"
* `spav:munib`= "acting"


The usage of activities is necessary to provide certain information but as this information might not be relevant in all cases the direct connection between `F20 Performance Work` and `F25 Performance Plan` is also used. The same applies to sources (such as literary works) and documentations (such as video recordings) as they are also rendered as FRBRoo individuals.

All contributions to performing arts productions are rendered as instances of `E7 Activity` and classified with the [SPA vocabulary](https://sapa.github.io/spa-vocabulary/). Alternative designations for an activity are preserved as optional `RDFS:label`.


### Additional Information <a id="additional-information"></a>

<!-- TODO: acts and scenes -->
<!-- TODO: language rdau:P60099? wdt:P407? P72_has_language is only for E33_Linguistic_Object -->




### Source and Documentation <a id="source-documentation"></a>

FRBRoo is also used to describe the literary reference of a production and its documentation.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://erlangen-crm.org/efrbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" ;
    frbroo:R14_incorporates <http://data.performing-arts.ch/w/UUID2> .

<http://data.performing-arts.ch/w/UUID2> a frbroo:F22_Self-Contained_Expression ;
	rdfs:label "El mètode Grönholm" .

<http://data.performing-arts.ch/w/UUID2/w> a frbroo:F1_Work ;
	rdfs:label "El mètode Grönholm" ;
	frbroo:R12_is_realised_in <http://data.performing-arts.ch/w/UUID2> .

<http://data.performing-arts.ch/x/UUID3> a frbroo:F28_Expression_Creation  ;
	frbroo:R19_created_a_realisation_of <http://data.performing-arts.ch/w/UUID2/w> ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID2> ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID4> .

<http://data.performing-arts.ch/a/UUID4> a crm:E21_Person  ;
	rdfs:label "Jordi Galceran" .

<http://data.performing-arts.ch/w/UUID1/p> a frbroo:F31_Performance  ;
    frbroo:R25_performed <http://data.performing-arts.ch/w/UUID1> .

<http://data.performing-arts.ch/w/UUID3> a frbroo:frbroo:F26_Recording  ;
```

While here the performance plan is rendered to incorporate its literary source directly, in fact there may be several layers of translation and adaption in between.

<!-- TODO: Do we need types for works? -->

### Season

Performing arts production are usually organized in annual seasons lasting from one summer until the next. The attribution of an individual production to a general season happens by defining the production's `F28 Expression Creation ` as part of a `E4 Period` that is the respective season. This season is the same for all producers and all productions.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix frbroo: <http://erlangen-crm.org/efrbroo/> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/w/UUID1> a frbroo:F25_Performance_Plan ;
    rdfs:label "Die Grönholm-Methode" .

<http://data.performing-arts.ch/x/UUID3> a frbroo:F28_Expression_Creation  ;
	frbroo:R17_created <http://data.performing-arts.ch/w/UUID2> .

<http://data.performing-arts.ch/x/UUID4> a crm:E4_Period ;
	rdfs:label "Season 2016/17" ;
    crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "1.8.2016 - 31.7.2017" ;
			crm:P82a_begin_of_the_begin "2016-08-01"^^xsd:date ;
			crm:P82b_end_of_the_end "2017-07-31"^^xsd:date .
		] ;
	crm:P9_consists_of <http://data.performing-arts.ch/x/UUID3> .
```

<!-- TODO: Do we need a specific type? How does it relate to wd:Q40008090? -->

