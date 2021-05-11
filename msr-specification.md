---
titlepage: true
toc-own-page: true
title: "Service Specification of Maritime Service Registry (MSR)"
author: [MCC]
date: "2021-04-21"
keywords: [Service registry]
logo: "materials/mcplogo.png"
titlepage-text-color: "476E7D"
footer-center: "G1128 Service Specification"
...

<!-- Hey it is comment! This should be invisible. -->

# WARNING: WORKING DOCUMENT! - Service Specification of Maritime Service Registry (MSR)

## Introduction
In IMO resolution MSC.467(101) ‘guidance on the definition and harmonization of the format and structure of maritime services in the context of e-navigation’, IMO defines Maritime Services and Technical Services in the context of e-navigation. In the resolution the Maritime Services are on the highest level, describing a service in an entirely non-technical manner. One or more Technical Services are associated with a Maritime Service, and these Technical Services are the ones defining the actual information exchange needed to take place in order to carry our a Maritime Service.

Maritime Service Registry, MSR for short, takes a place of a registry for Technical Service and a reference point to information and an end-point of registered services and thus to improve the accessibility of available services in the maritime domain.

The Technical Services in the resolution are also defined on three levels following the same structure as G1128, where MSR supervises all service providers to describe their service in the format of G1128.



### Purpose
The main tasks of MSR are registration of services by service provider and a discovery service for registered services, so any service consumer can identify available services and gain access. MSR registration needs to be able to register all relevant e-Navigation and e-Maritime services, commercial and non-commercial, authorized and non-authorized, for free and against payment.
MSR needs to allow service consumers to discover available services and enable the use of the services through given end-points.
It can be seen as a sophisticated yellow pages phone book.
A registry can be searched using a number of different criteria including coverage area.

MSR is an implementation of service management concept which was given from the IALA's G1128 specification.

![service management concept](materials/msr-specification-erd-local.png)

*Service management concept (from the IALA's G1128 specification)*

### Intended readership

This service specification is primarily intended to be read by architects, system engineers and developers in charge of developing and operating a MSR instance.
Furthermore, this service specification is intended to be read by enterprise architects, service architects, information architects, system engineers and developers in pursuing architecting, design and development activities of related maritime services.

### Inputs from other sources
The service management concept originally given from the IALA's G1128 specification was given and implemented throughout previous projects such as EfficienSea2 and Sea Traffic Management.

## Service identification
A unique identification of the service is given below.

Attribute | Content
--- | ---
Name | Maritime Service Registry (MSR)
ID | urn:mrn:mcp:service:mcc:mcc:specification:msr
Version | 1.1.0
Description | a service registry and a reference point to provide information of registered services and thus to improve the visibility and accessibility of available information and services in the maritime domain.
Keywords | service registry, service discoverability, service specification, G1128, technical services
Architect(s) | MCC MSR WG
Status | Released

## Operational context

In the operational context of MSR, it is mostly contexts of service consumers and providers that make interactions with. MSR acts as a trustworthy information provider of service to service consumers where they can get the list of services with certain search parameters. For service provider MSR facilitates the dissemination of their service information and an access point when the relevant information is successfully registered. More detailed descriptions are given below.

#### Service discoverability
Following aspects need to be satisfied:

* Only organisations that are registered in a MIR instance (see details on “Vetting procedure for organisations joining MCP instances”; Document ID: MCP Gen 5) are allowed to submit service descriptions (any level, i.e. service specifications, service designs, and service instances) to a MSR. I.e. a submitter needs to authenticate itself using MIR.
* MSR needs to be open for queries/searches without authentication.
* Endpoints in Service Instances needs to point to active services that are in production (not test services). This is of course only the case if the MSR itself is a production environment.
* Requirements on service provider authentication and service consumer authentication is entirely up to the service provider.

#### Service registration
With regard to service registration, the MSR instances work nearly independent of each other. a MSR instance provider will only accept services to be registered using identities from MIR instances it chooses.

With regard to service registration, the MSR instance provider naturally only has an obligation to it's own users that it allows to register services in its registry. So, SLA and accountability is only towards its own users.

Some services registered to a MSR will be local, i.e. will only be discoverable in that specific MSR instance. Other services should be globally discoverable across all MSR instances and when such a service is registered in the MSR, the searchable parameters must be added to the distributed ledger of maritime services. Thus, the MSR instance provider needs to run a node in the ledger.

##### Requirement on service registration
Services registered in a MSR must follow the IALA guideline on e-navigation technical services (G1128). In this guideline services are described on three levels:

* Service specification
* Service technical design
* Service instance

The service specification is the highest level, giving a high level description and containing the data model of the service. This data model may be a reference to an IHO product specification - or it could define a different data model.
A service specification will have one or more associated technical designs. Each technical design describes how the service can be implemented using a specific technology. Although the technologies in principle can be anything (even a phone number), the MCC promotes the use of web-services and services using the MMS.
For each technical design that will be one or more service instances that provides information of concrete service providers. The most important information is the endpoint of the service, but other significant information includes a geographical coverage of the service.

##### MRN of service documents for identification
At the time of registration of service, a service provider should be exposed to the MRN scheme for the identification of service documents. The G1128 clearly stated MRN as an unique identifier scheme. A service provider should follow the MRN scheme of the MCP identity service provider (who operates a MIR) that they are belonging. There is a possibility of having more than one MRN of a service document for the identification.

In MSR, the primary identification MRN needs to be aligned with the MCP MRN scheme, defined in 'MCC Identity Management and Security Identity Management' as follows:

```
<MCP-MRN> ::= "urn" ":" "mrn" ":" "mcp" ":" <MCP-TYPE> ":" <IPID> ":" <IPSS>  
<MCP-TYPE> ::= "device" | "org" | "user" | "vessel" | "service" | "mir" | "mms" | "msr"
<IPID> ::= <CountryCode> | (alphanum) 0*20(alphanum / "-") (alphanum)
<IPSS> ::= pchar *(pchar / "/")
```

More detailed description of the syntax is given in the referenced document.

Here the MRN syntax of <IPSS> for a service document is given:

```
<MSR-IPSS> ::= <ORG> ":" <G1128-TYPE> ":" <SERVICE-NAME>
<ORG> ::= pchar *(pchar / "/")
<G1128-TYPE> ::= "instance" | "specification" | "design"
<SERVICE-NAME> ::= pchar *(pchar / "/")
```
where <ORG> represents an organization ID assigned by <IPID>, <G1128-TYPE> represents the type of the documentation, i.e., specification, design, and instance, and <SERVICE-NAME> can be any specific string representing an unique identifier of a service. <ORG> together with <IPID> represents the identity of the service provider, an organization or a company registered to a specific MIR.

Governance of MRN of service documents is a responsibility of a MSR provider and thus the uniqueness of a MRN at the database level.

### Functional and non-functional requirements

#### Functional requirements
Requirement Id | Requirement Name | Requirement Text | References
--- | --- | --- | ---
MSR-FR001 | something | something | something
MSR-FR002 | something | something | something
MSR-FR003 | something | something | something

##### Requirement definitions - MSR-FR001
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - MSR-FR002
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - MSR-FR003
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

#### Non-functional requirements
Requirement Id | Requirement Name | Requirement Text | References
--- | --- | --- | ---
MSR-NFR001 | something | something | something
MSR-NFR002 | something | something | something
MSR-NFR003 | something | something | something

##### Requirement definitions - MSR-NFR001
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - MSR-NFR002
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - MSR-NFR003
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

### Other constraints
To be written

#### Relevant industrial standards
There are no such relevant industrial standards found.

#### Operational nodes
To be written

##### Operational nodes providing MSR service
Operational Node | Remarks
--- | ---
something | something

##### Operational nodes consuming MSR service
Operational Node | Remarks
--- | ---
something | something

#### Operational activities (Optional)
To be written

## Service overview
This section aims at providing an overview of the main elements of the service. The elements in this view are all usually created by an UML modelling tool.

### Service interfaces
Describe the interfaces of the service including the selected Message Exchange Pattern (MEP) by using an UML diagram5 that illustrates the service interfaces definitions and operations and in tabular form.
It is also recommended to describe the considerations resulting in the selection of a certain message exchange pattern.
A service interface supports one or several service operations. Depending on the message exchange pattern, service operations are either to be implemented by the service provider (e.g. in a Request/Response MEP, query operations are provided by the service provider – the service consumer uses them in order to submit query requests to the service provider), or by the service consumer (e.g. in a Publish/Subscribe MEP, publication operations are provided by the service consumer – the service provider uses them to submit publications to the service consumer). This distinction shall be clearly visualised in a service interface table (see example below): for each service interface, it shall be stated whether it is either provided or used by the Service. A service provides at least one service interface.
An example diagram and corresponding table is given below.

## Service data model

### Data models
```json
  Design:
    type: object
    properties:
      comment:
        type: string
      designAsDoc:
        $ref: '#/definitions/Doc'
      designAsXml:
        $ref: '#/definitions/Xml'
      designId:
        type: string
      docs:
        type: array
        items:
          $ref: '#/definitions/Doc'
      id:
        type: integer
        format: int64
      implementedSpecificationVersion:
        $ref: '#/definitions/SpecificationTemplate'
      lastUpdatedAt:
        type: string
      name:
        type: string
      organizationId:
        type: string
      publishedAt:
        type: string
      specifications:
        type: array
        items:
          $ref: '#/definitions/Specification'
      status:
        type: string
      version:
        type: string
    description: Holds a description of a technical design.A design can be compatible to one or morespecification templates.It has at least a technical representation of thedescriptiion in form of an XML and a filled out templateas e.g. word document.
  Doc:
    type: object
    properties:
      comment:
        type: string
      filecontent:
        type: string
        format: byte
      filecontentContentType:
        type: string
      id:
        type: integer
        format: int64
      mimetype:
        type: string
      name:
        type: string
    description: 'A doc represents a human readable document that can be attached to various objects.This could be an office document containing guidelines linked,to a service specification, or a Getting Started PDF attached toan service instance.'
  Instance:
    type: object
    properties:
      comment:
        type: string
      compliant:
        type: boolean
      designId:
        type: string
      docs:
        type: array
        items:
          $ref: '#/definitions/Doc'
      endpointType:
        type: string
      endpointUri:
        type: string
      geometry:
        $ref: '#/definitions/JsonNode'
      geometryContentType:
        type: string
      id:
        type: integer
        format: int64
      imo:
        type: string
      implementedSpecificationVersion:
        $ref: '#/definitions/SpecificationTemplate'
      instanceAsDoc:
        $ref: '#/definitions/Doc'
      instanceAsXml:
        $ref: '#/definitions/Xml'
      instanceId:
        type: string
      keywords:
        type: string
      lastUpdatedAt:
        type: string
      mmsi:
        type: string
      name:
        type: string
      organizationId:
        type: string
      publishedAt:
        type: string
      serviceType:
        type: string
      specificationId:
        type: string
      status:
        type: string
      unlocode:
        type: string
      version:
        type: string
    description: Holds a description of an service instance.An instance can be compatible to one or more specification templates. It has at least a technical representation of thedescriptiion in form of an XML and a filled out templateas e.g. word document.
  JsonNode:
    type: object
    properties:
      array:
        type: boolean
      bigDecimal:
        type: boolean
      bigInteger:
        type: boolean
      binary:
        type: boolean
      boolean:
        type: boolean
      containerNode:
        type: boolean
      double:
        type: boolean
      float:
        type: boolean
      floatingPointNumber:
        type: boolean
      int:
        type: boolean
      integralNumber:
        type: boolean
      long:
        type: boolean
      missingNode:
        type: boolean
      nodeType:
        type: string
        enum:
          - ARRAY
          - BINARY
          - BOOLEAN
          - MISSING
          - 'NULL'
          - NUMBER
          - OBJECT
          - POJO
          - STRING
      'null':
        type: boolean
      number:
        type: boolean
      object:
        type: boolean
      pojo:
        type: boolean
      short:
        type: boolean
      textual:
        type: boolean
      valueNode:
        type: boolean
  Specification:
    type: object
    properties:
      comment:
        type: string
      docs:
        type: array
        items:
          $ref: '#/definitions/Doc'
      id:
        type: integer
        format: int64
      implementedSpecificationVersion:
        $ref: '#/definitions/SpecificationTemplate'
      keywords:
        type: string
      lastUpdatedAt:
        type: string
      name:
        type: string
      organizationId:
        type: string
      publishedAt:
        type: string
      specAsDoc:
        $ref: '#/definitions/Doc'
      specAsXml:
        $ref: '#/definitions/Xml'
      specificationId:
        type: string
      status:
        type: string
      version:
        type: string
    description: Holds a logical description of a service. A specification can be compatible to one or morespecification templates.It has at least a technical representation of the servicedescriptiion in form of an XML and a filled out service templateas e.g. word document.
  SpecificationTemplate:
    type: object
    properties:
      comment:
        type: string
      docs:
        type: array
        items:
          $ref: '#/definitions/Doc'
      guidelineDoc:
        $ref: '#/definitions/Doc'
      id:
        type: integer
        format: int64
      name:
        type: string
      templateDoc:
        $ref: '#/definitions/Doc'
      type:
        type: string
        enum:
          - SPECIFICATION
          - DESIGN
          - INSTANCE
      version:
        type: string
      xsds:
        type: array
        items:
          $ref: '#/definitions/Xsd'
    description: 'A SpecificationTemplate contains information on how to define a aspects ofa service.It has a type do differentiate between e.g. logical definitions andconcrete service instances.Templates will evolve, that''s why they have a version.'
  Xml:
    type: object
    properties:
      comment:
        type: string
      content:
        type: string
      contentContentType:
        type: string
      id:
        type: integer
        format: int64
      name:
        type: string
    description: A technical way to describe aspects if a service.The Xml should validate against a XSD from a SpecificationTemplate.
  Xsd:
    type: object
    properties:
      comment:
        type: string
      content:
        type: string
        format: byte
      contentContentType:
        type: string
      id:
        type: integer
        format: int64
      name:
        type: string
    description: 'A schema for describing aspects of a service in a XML document.        '
```
## Service interface specifications

### Service interface <INTERFACE NAME>

#### Operation

## Service dynamic behaviour

## Service provisioning

A service management concept with MSR is visualised as below. Both, service specifications as well as information about service instances can be published in a service registry. A service registry can be a collection of documents, or could be realised as a service itself that would have an Application Programming Interface (API) for automatic interfacing to the registry (lookup, updating, deleting etc.). This concept is implemented as MSR within MCP (formerly called the Maritime Cloud), see https://maritimeconnectivity.net/.

This section shall describe the way services are planned to be provided and consumed. It is labelled optional since one of the key aspects of service-orientation is to increase flexibility of the overall system by separating the definition of services from their implementation. This means that a service can be provided in several different contexts that are not necessarily known at the time, when the service is designed.

## Definitions
Most of terms in the context of MCP can be found in the terminology page of the online documentation of MCP (https://docs.maritimeconnectivity.net/en/latest/terminology.html).

### Terminology
Term | Definition
--- | ---
MSR | Maritime Service Registry
MIR | Maritime Identity Registry
MRN | Maritime Resource Name

## References
1. IALA Guideline - G1128 THE SPECIFICATION OF e-NAVIGATION TECHNICAL SERVICES
2. MSR Requirements v0.1.5
3. Vetting procedure for organisations joining MCP instances
4. MCC Identity Management and Security Identity Management
