```mermaid
  classDiagram

    class admsIdentifier["adms:Identifer"] {
        xsd:string notation[0..1]
        dcterms:Agent creator[0..1]
        rdfs:Literal schemaAgency[0..1]
        rdfs:Literal version[0..1]
        rdfs:Literal issued[0..1]
    }
    link admsIdentifier "https://doi-do.github.io/dcat-us/#properties-for-identifier" "This is based on the UN/CEFACT Identifier class."

    class dcatCatalog["dcat:Catalog"] {
        rdfs:Literal title[1..*]
        rdfs:Literal description[1..*]
        foaf:Agent publisher[1]
        foaf:Document homepage[0..1]
        dcterms::LinguisticSystem language[0..*]
        dcterms:LicenseDocument license[0..1]
        rdfs:Literal releaseDate[0..1]
        dcterms:RightsStatement rights[0..1]
        dcterms:Location geographicCoverage[0..*]
        skos:ConceptScheme themes[0..*]
        rdfs:Literal modificationDate[0..1]
        dcterms:Standard schemaVersion[0..1]
        dcterms:Agent creator[0..*]
        dcterms:RightsStatement accessRights[0..1]
        vcard:Contact contactPoint[0..*]
        rdfs:Literal keyword[0..*]
        dcat:Catalog hasPart[0..*]
        skos:Concept theme[0..*]
        rdfs:Literal identifier[0..*]
        foaf:Organization rightsHolder[0..1]
        skos:Concept subject[0..n<]
        dct:PeriodOfTime temporalCoverage[0..*]
        prov:Attribution qualifiedAttribution[0..*]
        skos:Concept category[0..1]
    }
    link dcatCatalog "https://doi-do.github.io/dcat-us/#properties-for-catalog" "A curated collection of metadata about resources (e.g., datasets and data services in the context of a data catalog)"
    dcatCatalog *-- "0..*" dcatCatalog
    dcatCatalog *-- dcatCatalog : "has part"
    dcatCatalog *-- "0..*" dcatCatalogRecord
    dcatCatalog *-- "0..*" dcatDataService
    dcatCatalog *-- "0..*" dcatDataset

    dcatCatalog "1" *-- "0..*" dcatDataService
    dcatDataset "1" *-- "0..*" dcatDistribution
    dcatDatasetSeries o-- "0..*" dcatDataset

    class dcatCatalogRecord["dcat:CatalogRecord"] {
        dct:Standard applicationProfile[0..1]
        skos:Concept changeType[0..1]
        rdfs:Literal description[0..*]
        dct:LinguisticSystem language[0..*]
        rdfs:Literal listingDate[0..*]
        rdfs:Literal modificationDate[1]
        rdfs:Literal title[0..*]
    }
    link dcatCatalogRecord "https://doi-do.github.io/dcat-us/#properties-for-catalog-record" "A record in a catalog, describing the registration of a single dcatResource.\nThis class is optional and not all catalogs will use it. It exists for catalogs where a distinction is made between metadata about a dataset or service and metadata about the entry in the catalog about the dataset or service. For example, the publication date property of the dataset reflects the date when the information was originally made available by the publishing agency, while the publication date of the catalog record is the date when the dataset was added to the catalog."
    dcatCatalogRecord --> "1" dcatResource : "primary topic"
    dcatCatalogRecord --> "0..1" dcatResource : "source metadata"

    class dcatDataService["dcat:DataService"] {
        rdfs:Resource endpointURL
        vcard:Contact contactPoint[1..*]
        foaf:Agent publisher[1]
        rdfs:Literal title[1..*]
        rdfs:Resource endpointDescription[0..*]
        dcterms:LicenseDocument license[0..1]
        rdfs:Literal keyword[0..*]
        xsd:decimal spatialResolutionInMeters[0..*]
        rdfs:Literal temporalResolution[0..*]
        skos:Concept theme[0..*]
        dct:RightsStatement accessRights[0..1<]
        dct:Standard conformsTo[0..*]
        rdfs:Literal creationDate[0..1]
        dcterms:Agent creator[0..*]
        rdfs:Literal description[O..*]
        rdfs:Literal identifier[0..*]
        dct:LinguisticSystem language[0..*]
        rdfs:Literal modificationDate[0..1]
        dct:RightsStatement rights[0..*]
        foaf:Organization rightsHolder[0..*]
        dcterms:Location geographicCoverage[0..*]
        dcterms:PeriodOfTime temporalCoverage[0..*]
        skos:Concept type[0..1]
        dqv:QualityMeasurement spatialResolution[0..*]
        odrl:Policy hasPolicy[0..*]
        prov:Attribution qualifiedAttribution[0..*]
        prov:Activity wasUusedBy[0..*]
        dcat-us:GeographicBoundingBox geographicBoundingBox[0..*]
    }
    link dcatDataService "https://doi-do.github.io/dcat-us/#properties-for-data-service" "A collection of operations that provides access to one or more datasets or data processing functions."
    dcatDataService --> "0..*" dcatDataset : serves

    class dcatDataset["dcat:Dataset"] {
        rdfs:Literal title[1..*]
        rdfs:Literal description[1..*]
        rdfs:Literal identifier[1..*]
        vcard:Contact contactPoint[0..*]
        dcat:Distribution datasetDistribution[0..*]
        dct:Location spatial[0..*]
        rdfs:Literal keyword[0..*]
        foaf:Document landingPage[0..*]
        rdfs:Literal modificationDate[0..1]
        foaf:Agent publisher[0..1]
        dcat-us:GeographicBoundingBox geographicBoundingBox[0..*]
        dct:PeriodOfTime temporalCoverage[0..*]
        skos:Concept theme[0..*]
        dct:RightsStatement accessRights[0..1]
        dct:Standard conformsTo[0..*]
        dct:Agent creator[0..*]
        foaf:Document documentation[0..*]
        dct:Frequency frequency[0..1]
        dcat:Dataset hasVersion[0..*]
        rdfs:Resource isReferencedBy[0..*]
        dct:LinguisticSystem language[0..*]
        adms:Identifier otherIdentifier[0..*]
        dct:ProvenanceStatement provenance[0..*]
        prov:Attribution qualifiedAttribution[0..*]
        dcat:Relationship qualifiedRelation[0..*]
        rdfs:Resource relatedResource[0..*]
        rdfs:Literal releaseDate[0..1]
        dcat:Distribution sample[0..*]
        dcat:Dataset source[0..*]
        dqv:QualityMeasurement qualityMeasurement[0..*]
        xsd:decimal spatialResolutionInMeters[0..*]
        rdfs:Literal temporalResolution[0..*]
        skos:Concept type[0..1]
        rdfs:Literal version[0..*]
        rdfs:Literal versionNotes[0..*]
        prov:Activity wasGeneratedBy[0..*]
        foaf:Agent attribution[0..*]
        dcat-us:Program program[0..*]
        dcat-us:Investment investment[0..*]
        dcat-us:Legislation applicationLegislation[0..*]
        dcat:Dataset supportedSchema[0..1]
        dcat:Distribution metadataDistribution[0..*]
        dcat-us:LiabilityStatement liabilityStatement[0..1]
        rdfs:Literal purpose[0..*]
        dct:Agent contributor[0..*]
        schema:url image[0..*]
        rdfs:Resource relatedResource[0..*]
    }
    link dcatDataset "https://doi-do.github.io/dcat-us/#properties-for-dataset" "A collection of data, published or curated by a single agent, and available for access or download in one or more representations."
    dcatDataset <|-- dcatCatalog
    dcatDataset <|-- dcatDatasetSeries
    dcatDataSet "1..*" <-- dcatDatasetSeries

    class dcatDatasetSeries["dcat:DatasetSeries"] {
        rdfs:Literal title[1..*]
        rdfs:Literal description[1..*]
        vcard:Kind contactPoint[0..*]
        dcat:Dataset first[0..1]
        dct:Location spatial[0..*]
        dcat:Dataset last[0..1]
        rdfs:Literal modificationDate[0..1]
        foaf:Agent publisher[0..1]
        dcat:Dataset seriesMember[0..1]
        dct:PeriodOfTime temporalCoverage[0..*]
        dct:Frequency frequency[0..1]
        rdfs:Literal releaseDate[0..1]
    }
    link dcatDatasetSeries "https://doi-do.github.io/dcat-us/#properties-for-dataset-series" "A collection of datasets that are published separately, but share some characteristics that group them."

    class dcatDistribution["dcat:Distribution"] {
        rdfs:Resource accessURL[1..*]
        dct:LicenseDocument license[1..1]
        skos:Concept[0..1]
        rdfs:Literal description[0..*]
        dct:MediaTypeOrExtent format[0..1]
        dct:RightsStatement Rights[0..1]
        dcat-us:AccessRestriction accessRestriction[0..*]
        dcat-us:UseRestriction useRestriction[0..*]
        dcat-us:CuiRestriction CUIRestriction[0..1]
        rdfs:Literal title[0..*]
        rdfs:Literal modificationDate[0..1]
        skos:Concept representationTechnique[0..1]
        skos:Concept status[0..*]
        dcterms:MediaType compressionFormat[0..1]
        xsd:decimal spatialResolutionInMeters[0..1]
        dct:RightsStatement accessRights[0..1]
        dcat:DataService accessService[0..*]
        xsd:decimal byteSize[0..1]
        spdx:Checksum checksum[0..1]
        LocationPeriodOrJurisdiction coverage[0..*]
        foaf:Document documentation[0..*]
        rdfs:Resource downloadURL[0..*]</td>
        rdfs:Literal identifier[0..1]
        schema:url image[0..3]
        dct:LinguisticSystem language[0..*]
        dct:Standard linkedSchemas[0..*]
        dct:MediaType mediaType[0..1]
        dcat:mediaType packagingFormat[0..1]
        rdfs:Literal releaseDate[0..1]
        xsd:duration temporalResolution[0..1]
    }
    link dcatDistribution "https://doi-do.github.io/dcat-us/#properties-for-distribution" "A specific representation of a dataset. A dataset might be available in multiple serializations that may differ in various ways, including natural language, media-type or format, schematic organization, temporal and spatial resolution, level of detail or profiles (which might specify any or all of the above)."

    class dcatResource["dcat:Resource"] {
        dcterms:RightsStatement accessRights[0..1]
        dcterms:Standard conformsTo[0..*]
        vcard:Contact contactPoint[0..*]
        foaf:Agent creator[0..*]
        rdfs:Literal description[1..*]
        rdfs:Literal title[1..*]
        rdfs:Literal releaseDate[0..1]
        rdfs:Literal modificationDate[0..1]
        dcterms:LinguisticSystem language[0..*]
        foaf:Agent publisher[0..1]
        rdfs:Literal identifier[1..*]
        skos:Concept theme[0..*]
        skos:Concept type[0..1]
        rdfs:Literal keyword[0..*]
        foaf:Document landingPage[0..*]
        dcterms:LicenseDocument license[0..1]
        dcterms:RightsStatement rights[0..1]
        rdfs:Literal version[0..*]
        rdfs:Literal versionNotes[0..*]
    }
    dcatResource -- dcatResource
    dcatResource *-- dcatResource : "has part"
    dcatResource <|-- dcatDataset
    dcatResource <|-- dcatDataService
    dcatResource --> "0..*" odrlPolicy : "has policy"
    dcatResource --> "0..*" provAttribution : "qualified attribution"
    
    class dcatRelationship["dcat:Relationship"] {
        dcat:Resource relation[1]
        dcat:Role role[1]
    }
    link dcatRelationship "https://doi-do.github.io/dcat-us/#properties-for-relationship" "An association class for attaching additional information to a relationship between DCAT Resources"
    dcatRelationship -- "2" dcatResource
    
    class dcatRole["dcat:Role"] {
        xsd:string preferredLabel[1..*]
        xsd:string alternateLabel[0..*]
        xsd:string definition[0..*]
        xsd:string notation[0..*]
    }
    link dcatRole "https://doi-do.github.io/dcat-us/#properties-for-role" "A role is the function of a resource or agent with respect to another resource, in the context of resource attribution or resource relationships."
    
    class dcat-usAccessRestriction["dcat-us:AccessRestriction"] {
        skos:Concept restrictionStatus[1]
        org:Organization specificRestriction[0..1]
        rdfs:Literal restrictionNote[0..1]
    }
    link dcat-usAccessRestriction "https://doi-do.github.io/dcat-us/#properties-for-access_restriction" "The AccessRestriction class used by NARA represents limitations placed on accessing specific records or information within their archives, ensuring controlled and responsible access based on legal, ethical, or security considerations."

    class dcat-usCUIRestriction["dcat-us:CUIRestriction"] {
        xsd:string cuiBannerMarking[1]
        xsd:string cuiDesignationIndicator[1]
        xsd:string requiredIndicatorPerAuthority[0..*]
    }
    link dcat-usCUIRestriction "https://doi-do.github.io/dcat-us/#properties-for-cui_restriction" "Represents Controlled Unclassified Information (CUI), which is information that requires safeguarding or dissemination controls in accordance with applicable laws, regulations, and government-wide policies but is not classified as confidential."

    class dcat-usGeographicBoundingBox["dcat-us:GeographicBoundingBox"] {
        xsd:decimal westBoundingLongitude[1]
        xsd:decimal eastBoundingLongitude[1]
        xsd:decimal southBoudingLatitude[1]
        xsd:decimal northBoundingLatitude[1]
    }
    link dcat-usGeographicBoundingBox "https://doi-do.github.io/dcat-us/#properties-for-geographic-bbox" "GeographicBoundingBox describes the spatial extent of domain of application of an resource and is standardized in WGS 84 Lat/Long coordinate system."

    class dcat-usInvestment["dcat-us:Investment"] {
        xsd:string title[1..*]
        xsd:string description[0..*]
        skos:Concept category[0..*]
        xsd:string identifier[0..*]
        xsd:string otherIdentifier[0..*]
        org:Organization agency[0..1]
    }
    link dcat-usInvestment "https://doi-do.github.io/dcat-us/#properties-for-investment" "TBD"
    
    class dcat-usLiabilityStatement["dcat-us:LiabilityStatement"] {
        rdfs:Literal liabilityStatementText[0..*]
    }
    link dcat-usLiabilityStatement "https://doi-do.github.io/dcat-us/#properties-for-liability_statement" "A formal declaration accompanying a dataset which outlines the responsibilities and limitations of the data provider in terms of the accuracy, completeness, and potential use of the data. It often serves to limit the legal exposure of the data provider by defining the scope of allowed uses and disclaiming warranties or guarantees."

    class dcat-usProgram["dcat-us:Program"] {
        xsd:string title[1..*]
        xsd:string description[0..*]
        skos:Concept category[0..*]
        xsd:string identifier[0..*]
        xsd:string otherIdentifier[0..*]
        org:Organization agency[0..1]

    }
    link dcat-usProgram "https://doi-do.github.io/dcat-us/#properties-for-program" "A class representing a governmental program."
    
    class dcat-usUseRestriction["dcat-us:UseRestriction"] {
        skos:Concept restrictionStatus[1]
        org:Organization restrictionAuthority[0..1]
        rdfs:Literal restrictionNote[0..1]
    }
    link dcat-usUseRestriction "https://doi-do.github.io/dcat-us/#properties-for-use-restriction" "A UseRestriction is a set of rules, guidelines, or legal provisions that dictate how a particular resource, asset, information, or object can be utilized. Use restrictions may encompass limitations on access, distribution, reproduction, modification, or sharing, and they are often put in place to protect privacy, intellectual property rights, security, or compliance with legal or ethical standards."

    class dctermsLicenseDocument["dcterms:LicenseDocument"] {
        rdfs:Literal licenseText[0..*]
    }
    link dctermsLicenseDocument "https://doi-do.github.io/dcat-us/#properties-for-licence-document" "A legal document giving official permission to do something with a resource." 

    class dctermsLocation["dcterms:Location"] {
        rdfs:Literal boundingBox[0..1]
        rdfs:Literal centroid[0..1]
        rdfs:Literal geographicIdentifier[0..*]
        locn:Geometry geometry[0..1]
        skos:ConceptScheme gazetteer[0..1]
        rdfs:Literal geographicName[1..*]
    }
    link dctermsLocation "https://doi-do.github.io/dcat-us/#properties-for-location" "A spatial region or named place. It can be represented using a controlled vocabulary or with geographic coordinates."

    class dctermsMediaType["dcterms:MediaType"] {
        xsd:string label[0..1]
    }
    link dctermsMediaType "https://doi-do.github.io/dcat-us/#properties-for-media-type" "A media type, e.g. the format of a computer file."

    class dctermsPeriodOfTime["dcterms:PeriodOfTime"] {
        xsd:date startDate[0..1]
        xsd:date endDate[0..1]
    }
    link dctermsPeriodOfTime "https://doi-do.github.io/dcat-us/#properties-for-period-of-time" "PeriodOfTime represents a period of time with a start date and an end."

    class dctermsProvenanceStatement["dcterms:ProvenanceStatement"] {
        xsd:string provenanceStatementText[0..*]
    }
    link dctermsProvenanceStatement "https://doi-do.github.io/dcat-us/#properties-for-provenance-statement" "Any changes in ownership and custody of a resource since its creation that are significant for its
            authenticity, integrity, and interpretation."

    class dctermsRightsStatement["dcterms:RightsStatement"] {
        rdfs:Literal label[0..*]
        rdfs:Literal attributionText[0..*]
    }
    link dctermsRightsStatement "https://doi-do.github.io/dcat-us/#properties-for-rights-statement" "A statement about the intellectual property rights (IPR) held in or over a resource, a legal document giving official permission to do something with a resource, or a statement about access rights."
    
    class dctermsStandard["dcterms:Standard"] {
        rdfs:Literal description[0..*]
        xsd:string identifier[0..*]
        xsd:date issued[0..1]
        rdfs:Literal title[0..*]
        skos:Concept type[0..*]
        xsd:string version[0..1]
        skos:ConceptScheme inScheme[0..1]
        xsd:date creationDate[0..1]
        xsd:date lastModified[0..1]
    }
    link dctermsStandard "https://doi-do.github.io/dcat-us/#properties-for-standard" "A standard or other specification to which a Dataset or Distribution conforms."
    
    class dqvMetric["dqv:Metric"] {
        dqv:Dimension inDimension[1]
        xsd:anySimpleType expectedDataType[1]
        rdfs:Literal definition[0..*]
    }
    link dqvMetric "https://doi-do.github.io/dcat-us/#properties-for-metric" "Represents a standard to measure a quality dimension. An observation (instance of dqv:QualityMeasurement) assigns a value in a given unit to a Metric."

    class dqvQualityMeasurement["dqv:QualityMeasurement"] {
        dqv:Metric isMeasurementOf[1]
        rdfs:Literal value[1]
        rdfs:Resource unitOfMeasure[0..1]
    }
    link dqvQualityMeasurement "https://doi-do.github.io/dcat-us/#properties-for-quality-measurement" "Represents the evaluation of a given dataset (or dataset distribution) against a specific quality
            metric."

    class foafAgent["foaf:Agent"] {
        xsd:string name[1]
        skos:Concept type[0..1]
    }
    link foafAgent "https://doi-do.github.io/dcat-us/#properties-for-agent" "An entity that acts on something (eg. person, group, software or physical artifact)."

    class foafDocument["foaf:Document"] {
        rdfs:Literal title[1..*]
        foaf:Person individualAuthor[0..*]
        org:Organization corporateAuthor[0..*]
        rdfs:Literal authorsAsLiteral[1]
        org:Organization publisherOrganization[1]
        rdfs:Literal publishersAsLiteral[1]
        rdfs:Literal identifier[0..1]
        rdfs:Literal publicationDate[1]
        rdfs:Literal bibliographicCitation[0..1]
        skos:Concept documentType[0..1]
        rdfs:Literal abstract[0..*]
        rdfs:Literal description[0..*]
        dct:Standard conformsTo[0..*]
        dct:MediaType mediaType[0..*]
    }
    link foafDocument "https://doi-do.github.io/dcat-us/#properties-for-document" "A publication - as a scientific paper, a technical report, a book, book chapter, but also a blog post."

    class foafPerson["foaf:Person"] {
        xsd:string name[1]
    }
    link foafPerson "https://doi-do.github.io/dcat-us/#properties-for-person" ""

    class locnAddress["locn:Address"] {
        rdfs:Literal administrativeArea[0..1]
        rdfs:Literal city[0..1]
        rdfs:Literal country[0..1]
        rdfs:Literal postalCode[0..1]
        rdfs:Literal streetAddress[0..1]
    }
    link locnAddress "https://doi-do.github.io/dcat-us/#properties-for-address-location" "The address of a location."

    class odrlPolicy["odrl:Policy"]

    class orgOrganization["org:Organization"] {
        xsd:string preferredLabel[1]
        xsd:string alternativeLabel[0..*]
        xsd:string notation[0..*]
    }
    link orgOrganization "https://doi-do.github.io/dcat-us/#properties-for-organization" "Represents a collection of people organized together into a community or other social, commercial or
            political structure. The group has some common purpose or reason for existence which goes beyond the set of
            people belonging to it and can act as an Agent. Organizations are often decomposable into hierarchical
            structures."

    class provActivity["prov:Activity"] {
        xsd:string label[1..*]
        skos:Concept category[0..1]
    }
    link provActivity "https://doi-do.github.io/dcat-us/#properties-for-activity" "An activity is something that occurs over a period of time and acts upon or with entities; it may include consuming, processing, transforming, modifying, relocating, using, or generating entities."

    class provAttribution["prov:Attribution"] {
        foaf:agent agent[1]
        dcat:role role[1]
    }
    link provAttribution "https://doi-do.github.io/dcat-us/#properties-for-attribution" "A responsibility of an Agent for a resource."

    class skosConcept["skos:Concept"] {
        rdfs:Literal alternateLabel[0..*]
        rdfs:Literal definition[0..*]
        xsd:string notation[0..*]
        rdfs:Literal preferredLabel[1..*]
    }
    link skosConcept "https://doi-do.github.io/dcat-us/#properties-for-concept" "A controlled vocabulary term used to classify Catalog, Dataset, or Data Service."

    class skosConceptScheme["skos:ConceptScheme"] {
        rdfs:Literal title[1..*]
        rdfs:Literal description[0..*]
        rdfs:Literal creationDate[0..1]
        rdfs:Literal publicationDate[0..1]
        rdfs:Literal modificationDate[0..1]
        xsd:string versionInfo[0..1]
    }
    link skosConceptScheme "https://doi-do.github.io/dcat-us/#properties-for-concept-scheme" "A concept collection (e.g. controlled vocabulary) in which a concept is defined."
    skosConceptScheme *-- skosConcept : "in scheme"

    class spdxChecksum["spdx:Checksum"]  {
        spdx:ChecksumAlgorithm algorithm[1]
        xsd:hexBinary checksumValue[1]
    }
    link spdxChecksum "https://doi-do.github.io/dcat-us/#properties-for-checksum" "A Checksum is a value that allows to check the integrity of the contents of a file. Even small changes to the content of the file will change its checksum. This class allows the results of a variety of checksum and cryptographic message digest algorithms to be represented."

    class vcardAddress["vcard:Address"] {
        rdfs:Literal administrativeArea[0..1]
        rdfs:Literal city[0..1]
        rdfs:Literal countryName[0..1]
        rdfs:Literal postalCode[0..1]
        rdfs:Literal streetAddress[0..1]
    }
    link vcardAddress "https://doi-do.github.io/dcat-us/#properties-for-address-contact_point" "Specify the components of the delivery address for an entity"

    class vcardContact["vcard:Contact"] {
        xsd:string formattedName[1]
        rdfs:Resource email[1]
        rdfs:Resource telephone[0..1]
        xsd:string organizationName[0..1]
        xsd:string familyName[0..1]
        xsd:string givenName[0..1]
        xsd:string positionTitle[0..1]
        vcard:Address address[0..*]
    }
    link vcardContact "https://doi-do.github.io/dcat-us/#properties-for-contact" "Point of Contact information"

```
