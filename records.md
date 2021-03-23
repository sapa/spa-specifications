---
layout: page
title: Records
---

Records and record sets are described according to [Records in Context](https://www.ica.org/en/egad-ric-conceptual-model "Records in Context") (RiC). However, these decriptions will evolve over time with adaptions of the data to the emerging RiC conventions. So, some information might be stored as literal values instead of structured links to other entities as a result of the migration from legacy databases and will be restructured at a later time together with a refined data model. An own ontology (`spao`) is used to complement missing classes and properties but condsidered to be temporary.

### Record Sets <a id="recordsets"></a>

Record sets must be identified by `rico:name` while `rico:identifier` and `spao:legacyIdentifier` are optional. The type of each record set is also specified via `rico:hasRecordSetType` with a controlled vocabulary that is based on `rico:RecordSetType`. Each record set must have a parent record set (`rico:isOrWasIncludedIn`) with the exception of the main record set that represents the archive as such. `olo:index` is used as an optional property to ensure a specific sorting.

```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix spao: <http://ontology.performing-arts.ch/> .
@prefix olo: <http://purl.org/ontology/olo/core#> .

<http://data.performing-arts.ch/r/UUID2> a rico:RecordSet ;
    rico:identifier "1027-2-17" ;
    spao:legacyIdentifier "ABC-123", "DEF-456" ;
    rico:name "Johansson, Ronny" ;
    rdfs:label "Johansson, Ronny" ;
    rico:hasRecordSetType spav:rsfil ;
    olo:index 12 ;
    rico:isOrWasIncludedIn <http://data.performing-arts.ch/r/UUID1> .

<http://data.performing-arts.ch/a/UUID1> a rico:Agent .

```

* `spav:rsfil` = `ric-rst:File` = "File"


### Records <a id="records"></a>

The identification and description of records is mostly identical to that of record sets and they are connected to their record sets with `rico:isOrWasIncludedIn`. Additionally, they may have one or more subordinate record parts or instantiations.

```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .

<http://data.performing-arts.ch/r/UUID3> a rico:Record ;
    rico:identifier "1027-6-1-2-3" ;
    rico:name "Portrait de Sigurd Leeder" ;
    rdfs:label "Portrait de Sigurd Leeder" ;
    rico:isOrWasIncludedIn <http://data.performing-arts.ch/r/UUID2> ;
    rico:hasInstantiation <http://data.performing-arts.ch/o/UUID4> .

<http://data.performing-arts.ch/r/UUID2> a rico:RecordSet .
<http://data.performing-arts.ch/o/UUID4> a rico:Instantiation .

```

### Record Parts <a id="record-parts"></a>

RiC allows to describe parts of records. This is only used here when the record is a video tape or film reel that contains several videos or films. Record parts use a subset of the properties of records e.g. for content descriptions. They are also used to link to instantiations like digital files that contain not the entire record.

```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .

<http://data.performing-arts.ch/r/UUID1> a rico:Record ;
    rico:identifier "215-7" ;
    rico:name "Baumfee / Mermaid" ;

<http://data.performing-arts.ch/r/UUID2> a rico:RecordPart ;
    rico:identifier "215-7-1" ;
    rico:name "Baumfee" ;
    olo:index 0 ;
    rico:isOrWasConstituentOf <http://data.performing-arts.ch/r/UUID1> ;
    rico:hasInstantiation <http://data.performing-arts.ch/o/UUID4> .

<http://data.performing-arts.ch/r/UUID3> a rico:RecordPart ;
    rico:identifier "215-7-2" ;
    rico:name "Mermaid" ;
    olo:index 1 ;
    rico:isOrWasConstituentOf <http://data.performing-arts.ch/r/UUID1> .
    rico:hasInstantiation <http://data.performing-arts.ch/o/UUID5> .

<http://data.performing-arts.ch/o/UUID4> a rico:Instantiation .
<http://data.performing-arts.ch/o/UUID5> a rico:Instantiation .

```

### Content description <a id="content-description"></a>

The description on the content still uses several properties that derive from legacy fields and need to be consolidated: `spao:isRelatedTo`, `spao:seeAlso`, `spao:hasNote`, and `spao:hasInternalNote`. For record sets RiC specifies the usage of `rico:hasOrHadAllMembersWithDocumentaryFormType` instead of `rico:hasDocumentaryFormType`.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix ric-rst: <https://www.ica.org/standards/RiC/vocabularies/recordSetTypes#> .
@prefix spav: <http://vocab.performing-arts.ch/> .
@prefix frbroo: <http://iflastandards.info/ns/fr/frbr/frbroo/> .

<http://data.performing-arts.ch/r/UUID3> a rico:Record ;

    rico:hasCreator <http://data.performing-arts.ch/a/UUID1> ;
    rico:hasDocumentaryFormType spav:dfwox ;
    rico:hasOrHadLanguage spav:lgfra, spav:lgita ;
    rico:hasOrHadSubject <http://data.performing-arts.ch/w/UUID3> ;
    spao:isRelatedTo "1047-1-4-38-5" ;
    spao:seeAlso <http://data.performing-arts.ch/r/UUID2> ;
    rico:descriptiveNote "some comment" ;
    spao:hasNote "some public note" ;
    spao:hasInternalNote "some internal note";
    rico:isAssociatedWithPlace <http://data.performing-arts.ch/p/UUID8> ;
    rico:isAssociatedWithDate [
    	a rico:DateRange ;
    	rico:hasBeginningDate [
            a rico:SingleDate ;
            rico:normalizedDateValue "1954-09-12" ;
            rico:dateStandard "ISO 8601" 
        ] ;
    	rico:hasEndDate [
            a rico:SingleDate ;
            rico:normalizedDateValue "1954-09-12" ;
            rico:dateStandard "ISO 8601" 
        ] .
    ] .

<http://data.performing-arts.ch/a/UUID1> a rico:Agent .
<http://data.performing-arts.ch/a/UUID2> a rico:Record .
<http://data.performing-arts.ch/w/UUID3> a a frbroo:F25_Performance_Plan .
<http://data.performing-arts.ch/p/UUID5> a spao:ArchivalPlace .
<http://data.performing-arts.ch/p/UUID8> a rico:Place .

```

* `spav:dfwox` = "correspondence"
* `spav:lgfra` = "French"
* `spav:lgita` = "Italian"



### Archival processing <a id="archival-processing"></a>

 Temporarily, some information from a legacy database was stored in an own, informal ontology (`spoa`). These properties should later to transfered into RiC, once the standard is finalized.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix ric-rst: <https://www.ica.org/standards/RiC/vocabularies/recordSetTypes#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID2> a rico:RecordSet ;
    rico:hasProvenance <http://data.performing-arts.ch/a/UUID1> ;
    rico:isAssociatedWithEvent [
    	a rico:Event ;
    	rico:hasEventType spav:etdon .
    ] ;
    rico:history "Digitized by the Swiss Institute for the Conservation of Photography (ISCP)." ;
    spao:cassation "Records in very poor technical condition were not archived." ;
    spao:hasDoublets "2" ;
    spao:hasPacking spav:pkba4 ;
    rico:hasExtent [
        a rico:RecordResourceExtent ;
        rico:quantity "1" ;
        rico:hasUnitOfMeasurement spav:umbox 
    ] ;
    spao:hasProcessingConvention "ISAD/G" ;
    spao:hasProcessingDate [
        a rico:SingleDate ;
        rico:expressedDate "2011-11" ;
        rico:normalizedDateValue "2011-11" ;
        rico:dateStandard "ISO 8601" .
    ]
    spao:hasResponsibleEmployee "Employee name" .

    rico:isOrWasIncludedIn <http://data.performing-arts.ch/r/UUID1> .

<http://data.performing-arts.ch/a/UUID1> a rico:Agent .

```

* `spav:etdon` = "donation"
* `spav:pkba4` = "box A4"
* `spav:umbox` = "boxes"

### Rights and permissions <a id="rights-permissions"></a>

Also contains lecagy fields but mostly with controlled vocabularies that should be transfered into the final version of RiC.

```ttl
@prefix rico: <https://www.ica.org/standards/RiC/ontology#> .
@prefix ric-rst: <https://www.ica.org/standards/RiC/vocabularies/recordSetTypes#> .
@prefix spav: <http://vocab.performing-arts.ch/> .

<http://data.performing-arts.ch/r/UUID3> a rico:Record ;
    rico:conditionsOfAccess "Accès libre selon le règlement de SAPA." ;
    rico:conditionsOfUse "Nutzung gemäss dem Reglement der Stiftung SAPA." ;
    spao:hasAccessibility spav:acpbc ;
    spao:hasCopyrightDeclaration spav:cpyes ;
    spao:hasCredit "SAPA, Fonds Sigurd Leeder." ;
    spao:hasPermission spav:pmarc ;
    spao:hasPhysicalUsability spav:pures ;
    spao:hasProtectionDuration "0" ;
    spao:hasTermsOfProtection spav:tpunk ;
    spao:hasUsageRightsStill spav:blyes ;
    spao:hasUsageRightsStreaming spav:blyes ;
    schema:copyrightNotice "© Foto Kiehl, Berlin" .

```

* `spav:acpbc` = "public"
* `spav:cpyes` = "yes"
* `spav:pmarc` = "archivist"
* `spav:pures` = "restricted"
* `spav:tpunk` = "unknown"
* `spav:pures` = "restricted"
* `spav:blyes` = "yes"

