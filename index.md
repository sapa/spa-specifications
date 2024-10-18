---
layout: page
title: SPA Specifications
exclude_from_nav: 'true'
---

The future database of the [SAPA Foundation](https://www.sapa.swiss "Swiss Archive of the Performing Arts") will be published as linked data and build on the conceptual models [CIDOC-CRM](http://www.cidoc-crm.org), [FBBRoo](https://www.ifla.org/publications/node/11240) and [RiC](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context"). As RiC is still in development, its classes and properties may be substituted with equivalents from [ORE](http://www.openarchives.org/ore/1.0/vocabulary), [PREMIS](http://id.loc.gov/ontologies/premis.html), [PROV](http://www.w3.org/TR/prov-overview/) and [RDA](http://www.rdaregistry.info) for the time being.

[SHACL](https://www.w3.org/TR/shacl/) : [http://shapes.performing-arts.ch](http://shapes.performing-arts.ch)

The implementation of these models is guided by the following ideas:

* Classes and properties come from the three reference ontologies.
* They are further specified by a domain-specific [vocabulary](http://vocab.performing-arts.ch/).
* There is a distinction between core entities (such as persons or works) that should be publicly addressable and entities (such as appellations) that serve primarily auxiliary functions. The latter are represented by special URIs and are shown here as blank nodes.
* Make individual decisions in which case complexity is actually needed. If this is the case, think about providing a reduced version of the same information in a simple way. (Names are a good example here. They can be pretty complicated but sometimes one just needs a simple label.)

### Basic Concepts <a id="basic-concepts"></a>

The documentation is structured along the following basic concepts:

* [Actors/Agents](actors) (individual persons, groups, institutions)
* [Records](records)
* Objects (incl. [venues](venues), archival [objects](objects) including [videos](videos))
* [Works](works) (performing arts works and their originals such as written plays or musical compositions)
* [Seasons](seasons)
* [Places](places)

###  General Concepts <a id="general-concepts"></a>

Some concepts apply to more or less to all entities:

* [Identities (types, identifiers, appellations)](identities)
* [Time](time)

RDF sample code is in turtle syntax and covers only the aspects that are relevant in the respective context.
