---
layout: page
title: SPA Specifications
exclude_from_nav: 'true'
---

The future database of the [Foundation SAPA](https://www.sapa.swiss "Swiss Archive of the Performing Arts") will be published as linked data and build on the conceptual models [CIDOC-CRM](http://www.cidoc-crm.org), [FBBRoo](https://www.ifla.org/publications/node/11240) and [RiC](https://en.wikipedia.org/wiki/Records_in_Contexts "Records in Context"). As RiC doesn't have an official ontology yet, its classes and properties for the time being are substituted with equivalents from [ORE](http://www.openarchives.org/ore/1.0/vocabulary), [PREMIS](http://id.loc.gov/ontologies/premis.html), [PROV](http://www.w3.org/TR/prov-overview/) and [RDA](http://www.rdaregistry.info).

The implementation of these models is guided by the following ideas:

* Classes and properties come from the three reference ontologies.
* They are further specified by a domain-specific [vocabulary](https://sapa.github.io/spa-vocabulary/).
* There is distinction between core entities (such as persons or works) represent IRL phenomena and should be linkable and entities that serve primarily auxiliary functions. The latter may be represented as blank nodes without an URI.
* Make individual decisions when complexity is actually needed. If this is the case, think about providing a reduced version of the same information in a simple way. (Names are a good example here. They can be pretty complicated but sometimes you just need a simple label.)

### Basic Concepts <a id="basic-concepts"></a>

The documentation is structured along the following basic concepts:

* [Actors/Agents](actors) (individual persons, groups, institutions)
* Works (performing arts works and their originals such as written plays or musical compositions)
* Objects (incl. [Venues](venues))
* [Places](places)
* Records

The documentation tries to avoid redundancy. An object that appears in relation to an agent is not further described there.

###  General Concepts <a id="general-concepts"></a>

Some concepts apply to more or less to all entities:

* [Identities (types, identifiers, appellations)](identities)
* [Time](time)
* Spatial Coordinates
* Dimension

RDF sample code is in turtle syntax and covers only the aspects that are relevant in the respective context.