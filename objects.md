---
layout: page
title: Objects
---

Records in Context distinguishes between [records](records) as archival entities and instantiations as their material (both physical and digital) expressions. Thus a digitized photograph is described as one record with two instantiations - the original print and the digital file. Each additional version like a copy of the file on the IIIF server is an additional instantiation. All information that is independent of the materiality like creator, content, or copyright belongs to the record, all other information like format, size, or location belongs to the insantiations.

Digital instantiations are primarily described with [PREMIS](http://id.loc.gov/ontologies/premis.html). Therefore, each of them is a `rico:Instantiation` and a `premis:Representation`. The representation stands for the record as a whole and may consists of several files, e.g. a series of still images and a sound file that are the result of digitizing an analog film. Some objects (like letters or costumes) are only represented as records without explicit instantiations. Instantiation property such as `rico:hasLocation` then are used with the record itself.

### Example of a digitized photograph

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix premis: <http://www.loc.gov/premis/rdf/v1#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID1> a rico:Record ;
    rico:identifier "1027-9-3-41" ;
    rico:hasInstantiation <http://data.performing-arts.ch/o/UUID2>, <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID2> a rico:Instantiation ;
    rico:hasCarrierType spav:fvbrm ;
    rico:hasExtent [
        a rico:InstantiationExtent ;
        rico:quantity "9x6.5" ;
        rico:hasUnitOfMeasurement spav:umcm
    ] ;
    rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID3> a rico:Instantiation, premis:Representation ;
    rico:hasCarrierType spav:fvdgf .

<http://data.performing-arts.ch/o/UUID4> a premis:File ;
    premis:isIncludedIn <http://data.performing-arts.ch/o/UUID3> ;
    premis:originalName "1027-9-3-41.tiff" .
```

* `spav:fvbrm`= "photo negative"
* `spav:fvdgf`= "digital file"
* `spav:umcm`= "cm"

### Preservation and handling <a id="preservation"></a>

Object preservations are described either with [RiC](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context") or [PREMIS](http://id.loc.gov/ontologies/premis.html) for digital objects. Temporarily, some information from a legacy database was stored in an own, informal ontology (`spoa`). These properties should later to transfered either into PREMIS or RiC, once the standard is finalized.

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
	rico:hasInstantiation <http://data.performing-arts.ch/o/UUID2>, <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID2> a rico:Instantiation, ebucore:MediaResource ;
	rico:identifier "207-9-VHS-MAS" ;
	spao:hasArchivalStatus spav:asarm ;
	rico:hasOrHadLocation <http://data.performing-arts.ch/p/UUID7> ;
	rico:history "Reinigung der Bänder (von Schmutz und Abrieb) mit RTI-Reinigungsgerät durch Videokonservierung SAPA 17.05.2018. TC: A" ;
    spao:hasAccessibility spav:acpbc ;
    spao:hasCondition spav:cdict ;
    spao:hasPermission spav:pmnon ;
    spao:hasPhysicalUsability spav:puurs ;
    spao:hasProtectionDuration "0" ;
    spao:hasTermsOfProtection spav:tpunk ;
    spao:lastControl [
        a rico:Singledate ;
        rico:normalizedDateValue "2018-06" ;
        rico:dateStandard "ISO 8601"
    ]
	rico:hasDerivedInstantiation <http://data.performing-arts.ch/o/UUID3> .

<http://data.performing-arts.ch/o/UUID3> a rico:Instantiation, premis:Representation ;
	rico:identifier "207-9-DIG-SKD" ;
	spao:hasArchivalStatus spav:aspcd ;
	rico:hasOrHadLocation <http://data.performing-arts.ch/p/UUID8> ;
    spao:hasAccessibility spav:acpbc ;
    spao:hasCondition spav:cdict ;
    spao:hasPermission spav:pmnon ;
    spao:hasPhysicalUsability spav:puurs ;
    spao:hasProtectionDuration "0" ;
    spao:hasTermsOfProtection spav:tpunk ;
    spao:preparationDate [
        a rico:Singledate ;
        rico:normalizedDateValue "2018-06" ;
        rico:dateStandard "ISO 8601"
    ] .

<http://data.performing-arts.ch/p/UUID7> a spao:ArchivalLocation .

<http://data.performing-arts.ch/p/UUID8> a spao:ArchivalLocation .

```

* `spav:asarm` = "archival master"
* `spav:acpbc` = "public"
* `spav:asdcd` = "dissemination copy digital"
* `spav:cdict` = "intact"
* `spav:fvdgf` = "digital file"
* `spav:pmnon` = "none"
* `spav:puurs` = "unrestricted"
* `spav:tpunk` = "unknown"
* `spav:pmnon` = "none"