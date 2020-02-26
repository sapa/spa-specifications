---
layout: page
title: Actors
---

Entities that "have the potential to perform intentional actions of kinds for which someone may be held responsible" for CIDOC-CRM are instances of `E39 Actor` while RiC calls them `Agent`. Here both classes are used as actors/agents are one point where the scope of both models overlap. CIDOC-CRM further distinguishes further between `E21 Person`, `E74 Group` and `E40 Legal Body` as subclasses.

The following examples are not complete as documentation of the implementations of `E82 Actor Appellation`, `E52 Time-Span` etc. is not repeated here.

### Persons <a id="persons"></a>

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID1> a crm:E21_Person ,
	rico:Person ;
    rdfs:label "Firstname Lastname" ;
    rdfs:comment "profession" ;
    crm:P131_is_identified_by [ a crm:E82_Actor_Appellation ] ;
    crm:P98i_was_born [ a crm:E67_Birth ;
        crm:P4_has_time-span [ a crm:E52_Time-Span ] ;
        crm:P7_took_place_at <http://data.performing-arts.ch/p/UUID2>
    ] ;
    crm:P100i_died_in [ a crm:E69_Death ;
        crm:P4_has_time-span [ a crm:E52_Time-Span ] ;
        crm:P7_took_place_at <http://data.performing-arts.ch/p/UUID3>
    ] ;
    crm:P107i_is_current_or_former_member_of <http://data.performing-arts.ch/g/gender/X> ,
    	<http://data.performing-arts.ch/g/nation/XX>.
    owl:sameAs <http://www.wikidata.org/entity/Q123> ,
    <https://d-nb.info/gnd/123456789> , 
    <http://tls.theaterwissenschaft.ch/wiki/Firstname_Lastname> ;
```

Gender and nationality of a person are expressed as memberships in corresponding groups just as regular group memberships.

### Groups and Legal Bodies <a id="groups"></a>

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/a/UUID5> a crm:E40_Legal_Body ,
	rico:CorporateBody ;
    crm:P2_has_type spav:vrivu ;
    rdfs:label "Theatre ABC" ;
    crm:P131_is_identified_by [ a crm:E82_Actor_Appellation ] ;
    crm:P95i_was_formed_by [ a crm:E66_Formation ] ;
    crm:P99i_was_dissolved_by [ a crm:E68_Dissolution ] ;
    rico:isSuccessorOf <http://data.performing-arts.ch/a/UUID6> ;
    rico:controlledBy <http://data.performing-arts.ch/a/UUID7> ;
    crm:P107_has_current_or_former_member <http://data.performing-arts.ch/a/UUID8> ;
    crm:P76_has_contact_point [ a crm:E45_Address ;
        rdf:value "Street, Place, Country" ;
        crm_P2_has_type spav:ihtxc
    ] ;
    crm:P76_has_contact_point [ a crm:E51_Contact_Point ;
        rdf:value <http://www.theatre-abc.ch> ;
        crm_P2_has_type spav:ihctx
    ] ;
    crm:P74_has_current_ or_former_residence [ a crm:Place ;
        crm:P87_is_identified_by [ a crm:E45_Address ;
            rdf:value "Street, Place, Country" ;
            crm_P2_has_type spav:ihtxc
        ] ;
        crm:P89_falls_within <http://data.performing-arts.ch/p/UUID9>
    ] ;
    crm:P14i_performed [ a crm:E7_Activity ;
        crm:P2_has_type spav:mujfv ;
        crm:P16_used_specific_object <http://data.performing-arts.ch/o/UUID10> ;
        crm:P4_has_time-span [ a crm:E52_Time-Span ]
    ].

[
	a frbroo:F51_Pursuit ;
	crm:P14_carried_out_by <http://data.performing-arts.ch/a/UUID5> ;
	frbroo:R59_had_typical_subject spav:mneyg.
]

```

* `spav:vrivu`= "artistic professional producer with own venue"
* `spav:mneyg`= "spoken theatre"
* `spav:ihtxc`= "address"
* `spav:ihctx`= "website"
* `spav:mujfv`= "management"

A focus of a group on one or more genres is expressed as a `frbroo:F51_Pursuit`.

<!-- TODO: Change the two identical blank node addresses into into one entity with URI? -->

