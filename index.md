## SPA Specifications

The future database of the [Foundation SAPA](https://www.sapa.swiss "Swiss Archive of the Performing Arts") will be published as linked data and build on the conceptual models [CIDOC-CRM](http://www.cidoc-crm.org), [FBBRoo](https://www.ifla.org/publications/node/11240) and [RiC](https://en.wikipedia.org/wiki/Records_in_Contexts "Records in Context").

The implementation of these models is guided by the following ideas:

* Classes and properties come from the three reference ontologies.
* They are further specified by a domain-specific [vocabulary](https://sapa.github.io/spa-vocabulary/).
* There is distinction between core entities (such as persons or works) represent IRL phenomena and should be linkable and entities that serve primarily auxiliary functions. The latter may be represented as blank nodes without an URI.

### Basic Concepts

The documentation is structured along the following basic concepts:

* Actors/Agents (individual persons, groups, institutions)
* Works (performing arts works and their originals such as written plays or musical compositions)
* Objects
* Places
* Records

The documentation tries to avoid redundancy. An object that appears in relation to an agent is not further described there.

###  General Concepts

Some concepts to more or less to all entities:

* [Identities (types, identifiers, appellations)](identities.html)
* Time
* Spatial Coordinates
* Dimension

RDF sample code is in turtle syntax and covers only the aspects that are relevant in the respective context.