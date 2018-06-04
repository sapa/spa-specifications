---
layout: page
title: Time
---

<!-- TODO: Can we call this a date, when CIDOC-CRM suggest a different understanding of that term? -->

CIDOC-CRM provides various and complex ways to represent times. Here only two classes are used: `E52 Time-Span` and `E61 Time Primitive`. The combination of these solves the main issue encountered when trying to make human definitions of points in time machine-readable as they provide a method to add precise (although idealized) time-stamps.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.

[ a crm:E52_Time-Span ;
	rdfs:label "1999" ;
	crm:P81_ongoing_throughout [ a crm:E61_Time_Primitive ;
		rdf:value "1999-01-01"^^xsd:date;
	], [ a crm:E61_Time_Primitive ;
		rdf:value "1999-12-31"^^xsd:date;
	]
]
```
<!-- TODO: Do I need two `E61 Time Primitive`s here? -->

A `E52 Time-Span` provides the opportunity to be defined by values that either refer to the minimum or maximum temporal extend. Here only the property for minimum extends (`P81_ongoing_throughout`) are used.

As instances of both classes are never re-used and only accessed through a specific actor, object or activty they belong to, they are both rendered as blank nodes. The only exceptions are theatre seasons.

A `E52 Time-Span` is used for both defining a point in time like a specific date or a longer period. <!-- TODO: Do I actually have use cases for time periods? --> However, if two events mark the beging and the end of such a time period, there are two simple `E52 Time-Span` instances like in the formation and dissolution of a legal body.

```ttl
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/>.

<http://data.performing-arts.ch/a/123456> a crm:E40_Legal_Body ;
	crm:P95i_was_formed_by [ a crm:E66_Formation ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "1961" ;
			crm:P81_ongoing_throughout [ a crm:E61_Time_Primitive ;
				rdf:value "1961-01-01"^^xsd:date;
			], [ a crm:E61_Time_Primitive ;
				rdf:value "1961-12-31"^^xsd:date;
			]
		]
	] ;
	crm:P99i_was_dissolved_by [ a crm:E68_Dissolution ;
		crm:P4_has_time-span [ a crm:E52_Time-Span ;
			rdfs:label "1989" ;
			crm:P81_ongoing_throughout [ a crm:E61_Time_Primitive ;
				rdf:value "1989-01-01"^^xsd:date;
			], [ a crm:E61_Time_Primitive ;
				rdf:value "1989-12-31"^^xsd:date;
			]
		]
	] .
```

<!-- TODO: Model a person with a birthyear/day. Needs a birth event! -->

<!-- TODO: Model the temporal validity of a name. Difficult ... -->

<!-- TODO: model a theatre season -->

