---
layout: page
title: Places
---

<!-- TODO: also use RiC -->

According to the CIDOC-CRM place are "extents in space, in particular on the surface of the earth, in the pure sense of physics: independent from temporal phenomena and matter". We distinguish between three kinds of places:

* Official administrative entities such as municipalities, districts, canton, and countries.
* Places that are recognized as such in common knowledge but lack the status to be an administrative entity. These can be villages, which are administrated as regional groups, or city districts, which have lost their autonomy at some point.
* Specific sites that are needed to define the residence of an actor or the location of an object. These are identified by an address rather than a name.

The first two receive p-based URIs, while the third kind is identified by a x-based URI here represented by with blank nodes.

A legal body in the city of Bern:

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .

<http://data.performing-arts.ch/a/UUID1> a crm:E40_Legal_Body ;
    crm:P74_has_current_or_former_residence [ a crm:E53_Place ;
        crm:P89_falls_within <http://data.performing-arts.ch/p/UUID2> ;
        crm:P87_is_identified_by [ a crm:E45_Address ;
            rdf:value "Some Street, 3001 Bern"
        ]
    ]

<http://data.performing-arts.ch/p/UUID2> a crm:E53_Place ;
    rdfs:label "Bern"@de, "Berne"@fr, "Berna"@it, "Bern"@en ;
    crm:P87_is_identified_by <http://data.performing-arts.ch/p/UUID2/a> ;
    owl:sameAs <http://www.wikidata.org/entity/Q70>, <http://d-nb.info/gnd/4005762-8>, <http://geonames.org/2661552/>, <http://classifications.data.admin.ch/municipality/351> .

<http://data.performing-arts.ch/p/UUID2/a> a crm:E48_Place_Name ;
    rdf:value "Bern"@de, "Berne"@fr, "Berna"@it, "Bern"@en .
```

Names of places are given in four languages as `crm:E48_Place_Name` and are repeated as `rdfs:label` for easier usage. The URI of the `crm:E48_Place_Name` is the same as that of the `crm:E53_Place` with an additional `/a`. Therefore, each place may only have a single name in each language. For the sake of brevity this notation is abridged in the following examples.

Relations between places:

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .

<http://data.performing-arts.ch/p/UUID3> a crm:E53_Place ;
    rdfs:label "Altstetten" ;
    crm:P87_is_identified_by [ a crm:E48_Place_Name ;
        rdf:value "Altstetten"
    ] ;
    owl:sameAs <http://geonames.org/6295513/>,
        <http://www.wikidata.org/entity/Q445711> ;
    crm:P89_falls_within <http://data.performing-arts.ch/p/UUID4> .

<http://data.performing-arts.ch/p/UUID4> a crm:E53_Place ;
    rdfs:label "Zürich" ;
    crm:P87_is_identified_by [ a crm:E48_Place_Name ;
        rdf:value "Zürich"
    ] ;
    owl:sameAs <http://geonames.org/6295513/>,
        <http://www.wikidata.org/entity/Q72>,
        <http://d-nb.info/gnd/4068038-1>,
        <http://viaf.org/viaf/185144783004419863241>,
        <http://classifications.data.admin.ch/municipality/261> ;
    crm:P89_falls_within <http://data.performing-arts.ch/p/UUID5> .

<http://data.performing-arts.ch/p/UUID5> a crm:E53_Place ;
    rdfs:label "Kanton Zürich" ;
    crm:P87_is_identified_by [ a crm:E48_Place_Name ;
        rdf:value "Kanton Zürich"
    ] ;
    owl:sameAs <http://geonames.org/2657895/>,
        <http://www.wikidata.org/entity/Q11943>,
        <http://d-nb.info/gnd/4068041-1>,
        <http://viaf.org/viaf/140174177>,
        <http://classifications.data.admin.ch/canton/ZH> ;
    crm:P89_falls_within <http://data.performing-arts.ch/p/UUID36> .

<http://data.performing-arts.ch/p/UUID6> a crm:E53_Place ;
    rdfs:label "Schweiz" ;
    crm:P87_is_identified_by [ a crm:E48_Place_Name ;
        rdf:value "Schweiz"
    ] ;
    owl:sameAs <http://geonames.org/2658434/>,
        <http://www.wikidata.org/entity/Q39>,
        <http://d-nb.info/gnd/4053881-3>,
        <http://viaf.org/viaf/154323889> .
```

Places in Switzerland are described by a maximum of four levels. The example above defines Altstetten, a place that 1934 became a district of the city of Zurich. Zurich as a current Swiss municipality represents the next (and most relevant) level. Municipalities fall within districts, which are omitted here. Instead each municipality is directly assigned to a canton. All cantons then are part of Switzerland as a state.

Foreign places are only represented with two levels, i.e. Paris is a place in France.

