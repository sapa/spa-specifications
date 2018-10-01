---
layout: page
title: Time
---

In the CIDOC-CRM any statement about time is at the end a statement about a time-span, which can be defined in regard to is maximum and minimum boundaries. Here only two properties are used to describe a `E52 Time-Span`: `crm:P82a_begin_of_the_begin` and `crm:P82b_end_of_the_end`. Additionally, `rdfs:label` is used to provide an easier access.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .

[ a crm:E52_Time-Span ;
	rdfs:label "1999" ;
	crm:P82a_begin_of_the_begin "1999-01-01"^^xsd:date ;
	crm:P82b_end_of_the_end "1999-12-31"^^xsd:date
]
```

As instances of `E52 Time-Span` are never re-used and only accessed through a specific actor, object or activity they belong to, they are both rendered as conceptual blank nodes, i.e. with x-based URIs. The only exceptions are theatre seasons.

A `E52 Time-Span` is used for both defining a point in time like a specific date or a longer period. <!-- TODO: Do I actually have use cases for time periods? --> However, if two events mark the beginning and the end of such a time period, there are two simple `E52 Time-Span` instances like in the formation and dissolution of a legal body.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .

<http://data.performing-arts.ch/a/UUID1> a crm:E40_Legal_Body ;
	crm:P95i_was_formed_by [ a crm:E66_Formation ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "1961" ;
			crm:P82a_begin_of_the_begin "1961-01-01"^^xsd:date ;
			crm:P82b_end_of_the_end "1961-12-31"^^xsd:date
		]
	] ;
	crm:P99i_was_dissolved_by [ a crm:E68_Dissolution ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "1989" ;
			crm:P82a_begin_of_the_begin "1989-01-01"^^xsd:date ;
			crm:P82b_end_of_the_end "1989-12-31"^^xsd:date
		]
	] .
```

<!-- TODO: Model a person with a year/day of birth. Needs a birth event! -->

<!-- TODO: Model the temporal validity of a name. Difficult ... -->

<!-- TODO: model a theatre season -->

