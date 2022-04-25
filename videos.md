---
layout: page
title: Videos
---

Original videos may be analog, physical objects or born digital. All these archival masters are converted into preservation copies and usually also dissemenation copies. All of them are instantiations of a single record. If a carrier like a video tape contains several works, each of them is described as a `rico:RecordPart` to allow connections of separate instantiations.

Videos are described from three perspectives and by using three ontologies:

* as archival entities with [RiC](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context")
* as digital objects with [PREMIS](http://id.loc.gov/ontologies/premis.html)
* and as videos with [EBUCore](https://tech.ebu.ch/MetadataEbuCore)

Therefore, they always two class types:

* Videos tapes and films are at the same time a `rico:Instantiation` and a `ebucore:MediaResource`.
* Digital videos are `rico:Instantiation`/`premis:Representation` plus one or more `premis:File`/`ebucore:MediaResource`.

Videos are also described as [objects](objects).

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix premis: <http://www.loc.gov/premis/rdf/v1#> .
@prefix ebucore: <https://www.ebu.ch/metadata/ontologies/ebucore#> .
@prefix cryptographicHashFunctions: <http://id.loc.gov/vocabulary/preservation/cryptographicHashFunctions> .
@prefix spav: <http://vocab.performing-arts.ch/> .
@prefix spao: <http://ontology.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID1> a rico:Record ;
	rico:identifier "207-9" ;
	rico:name "umwege" ;
	rico:hasInstantiation <http://data.performing-arts.ch/o/UUID2>, <http://data.performing-arts.ch/o/UUID3>, <http://data.performing-arts.ch/o/UUID4>, <https://vimeo.com/123456> .

<http://data.performing-arts.ch/o/UUID2> a rico:Instantiation, ebucore:MediaResource ;
	rico:identifier "207-9-VHS-MAS" ;
	spao:hasArchivalStatus spav:asarm ;
	rico:hasOrHadLocation <http://data.performing-arts.ch/p/UUID7> ;
	rico:hasCarrierType spav:fvywh ;
	rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID3> a rico:Instantiation, premis:Representation ;
	rico:identifier "207-9-DIG-SKD" ;
	spao:hasArchivalStatus spav:aspcd ;
	rico:hasOrHadLocation <http://data.performing-arts.ch/p/UUID8> ;
	rico:hasCarrierType spav:fvdgf ;
	rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID4>, <https://vimeo.com/123456> .

<http://data.performing-arts.ch/o/UUID5> a premis:File, ebucore:MediaResource ;
	premis:isIncludedIn <http://data.performing-arts.ch/o/UUID3> ;
	premis:originalName "207-9-DIG-SKD.mkv" .

<http://data.performing-arts.ch/o/UUID4> a rico:Instantiation, premis:Representation ;
	rico:indentier "207-9-DIG-NK" ;
	spao:hasArchivalStatus spav:asdcd ;
	rico:hasOrHadLocation <http://data.performing-arts.ch/p/UUID8> ;
	rico:hasCarrierType spav:fvdgf .

<http://data.performing-arts.ch/o/UUID6> a premis:File, ebucore:MediaResource ;
	premis:inIncludedIn <http://data.performing-arts.ch/o/UUID4> ;
	premis:originalName "207-9-DIG-SKD.mkv" .

<https://vimeo.com/123456> a rico:Instantiation ;
	rico:hasCarrierType spav:fvonl .

<http://data.performing-arts.ch/p/UUID7> a spao:ArchivalLocation .

<http://data.performing-arts.ch/p/UUID8> a spao:ArchivalLocation .

```

* `spav:asarm` = "archival master"
* `spav:aspcd` = "preservation copy digital"
* `spav:asdcd` = "dissemination copy digital"
* `spav:fvywh` = "VHS"
* `spav:fvdgf` = "digital file"
* `spav:fvonl` = "online"

### PREMIS and EBUCore properties <a id="premis"></a>

The implemenation of [PREMIS](http://id.loc.gov/ontologies/premis.html) is limited to only a few classes and property and might be extended later.

Analog videos and video files are both defined as a `ebucore:MediaResource` and use respective properties.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix premis: <http://www.loc.gov/premis/rdf/v1#> .
@prefix ebucore: <https://www.ebu.ch/metadata/ontologies/ebucore#> .
@prefix cryptographicHashFunctions: <http://id.loc.gov/vocabulary/preservation/cryptographicHashFunctions> .
@prefix spav: <http://vocab.performing-arts.ch/> .
@prefix spao: <http://ontology.performing-arts.ch/> .

<http://data.performing-arts.ch/o/UUID2> a rico:Instantiation, ebucore:MediaResource ;
	rico:identifier "207-9-VHS-MAS" ;
	rdau:P60558 spav:clmul ;
	ebucore:aspectRatio spav:arfsc ;
	ebucore:channels "2" ;
	ebucore:duration "0:33:07" ;
	ebucore:hasStandard spav:bspal ;
	rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID3> a rico:Instantiation, premis:Representation ;
	rico:identifier "207-9-DIG-SKD" ;
	rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID4>, VIMEO .

<http://data.performing-arts.ch/o/UUID5> a premis:File, ebucore:MediaResource ;
	premis:inIncludedIn <http://data.performing-arts.ch/o/UUID3> ;
	premis:originalName "207-9-DIG-SKD.mkv" ;
	premis:compositionLevel "0" ;
	premis:size "26994251513" ;
	premis:fixity [
		a cryptographicHashFunctions:md5 ;
		rdf:value "8fc77dad889c207233af066d2df03b7e"
	] ;
	rdau:P60558 spav:clmul ;
	ebucore:hasFormat spav:cfmkv, spav:vfffv1v34, spav:afflac ;
	ebucore:duration "0:33:07" ;
	ebucore:hasStandard spav:bspal ;
	ebucore:frameRate "25" ;
	ebucore:height "576" ;
	ebucore:width "720" ;
	ebucore:aspectRatio spav:arfsc ;
	ebucore:scanningFormat spav:sfint ;
	ebucore:scanningOrder spav:sotop ;
	ebucore:channels "2" ;
	ebucore:samplingRate "48000" .

```

* `spav:clmul` = "color"
* `spav:arfsc` = "full screen"
* `spav:bspal` = "PAL"
* `spav:cfmkv` = "Matroska"
* `spav:vfffv1v34` = "FFV1 Version 3.4"
* `spav:afflac` = "FLAC"
* `spav:sfint` = "interlaced"
* `spav:sotop` = "top"
