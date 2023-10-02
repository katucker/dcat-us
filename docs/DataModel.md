```mermaid
  classDiagram

    class adms:Identifer

    class dcat:Catalog {
      dcterms:title title
      dct:description description
      dct:publisher publisher
      foaf:homepage homepage
      dct:language language
      dct:license license
      dct:issued releaseDate
      dct:rights rights
      dct:spatial spatial
      dct:modified modificationDate
      dct:conformsTo schemaVersion
      dct:creator creator
      dct:accessRights accessRights
    }

    class dcat:DataService {
      URL endpoint
      dct:license license
      dcat:keyword keyword
    }

    class dcat:Dataset {
      dcterms:title title
      dct:description description
      dcterms:identifier identifer
      dct:spatial spatial
      dct:modified modificationDate
      dct:publisher publisher
      dct:accessRights accessRights
    }

    class dcat:DatasetSeries {
      dcterms:title title
      dct:description description
    }

    class dcat:Distribution {
      URL accessURL
      dct:license license
      dct:format format
    }

    class dcat:CatalogRecord
    class dcat:Resource
    class dcat:Relationship
    class dcat:Distribution
    class dcat:Role

    class dcat-us:AccessRestriction {
      RestrictionStatus restrictionStatus
      Organization restrictionAuthority
      String restrictionNote
    }
    class dcat-us:CUIRestriction
    class dcat-us:GeographicBoundingBox
    class dcat-us:Investment
    class dcat-us:LiabilityStatement
    class dcat-us:Program
    class dcat-us:UseRestriction

    class dct:LicenseDocument
    class dct:Location
    class dct:MediaType
    class dct:PeriodOfTime
    class dct:ProvenanceStatement
    class dct:RightsStatement
    class dct:Standard

    class dqv:Metric
    class dqv:QualityMeasurement

    class foaf:Agent {
      foaf:name name
      dcterms:type type
      foaf:mbox email
      foaf:phone phone
      foaf:workplaceHomepage URL
      locn:address address
      org:memberof memberOf
    }
    class foaf:Document
    class foaf:Person

    class locn:Address

    class org:Organization

    class prov:Activity
    class prov:Attribution {
      prov:agent agent
      dcat:hadRole role
    }

    class skos:Concept
    class skos:ConceptScheme

    class spdx:Checksum

    class vcard:Address
    class vcard:Contact


Catalog "1" *-- "1..n" Dataset
Catalog "1" *-- "0..n" DataService
Dataset "1" *-- "0..n" Distribution
DataService --> Dataset : serves
DatasetSeries o-- "0..n" Dataset
```
