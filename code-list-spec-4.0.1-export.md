# NIEM Code Lists Specification

- Version 4.0.1
- September 28, 2022
- NIEM Technical Architecture Committee (NTAC)

# Abstract

This document establishes methods for using code list artifacts with NIEM information exchange specifications. It provides for the use of Genericode documents, as well as for CSV code lists. It supports the use of code lists at schema definition time, via annotations for XML Schema documents that bind schema components to code lists. It supports the use of code lists at run time, via XML Schema components for use in XML documents that bind XML data to code lists. It also includes identifiers for well-known columns that have semantics needed across the NIEM community.

# Authors

NTAC

# Document Status

This document is a specification product of the NIEM Technical Architecture Committee (NTAC). This version of this document is normative for the conformance targets it defines.

Updates, revisions, and errata for this specification are posted to [https://github.com/NIEM/NIEM-Code-Lists-Spec](https://github.com/NIEM/NIEM-Code-Lists-Spec). Please submit comments on this specification as issues at [https://github.com/NIEM/NIEM-Code-Lists-Spec/issues](https://github.com/NIEM/NIEM-Code-Lists-Spec/issues).

# Table of Contents

- [1. Introduction](#introduction)

	- [1.1. Code list example](#code-list-example)
	- [1.2. Machine-readable format for a code list](#machine-readable-format-for-a-code-list)
	- [1.3. Identifiers for code lists](#identifiers-for-code-lists)
	- [1.4. Mechanism for resolving code lists](#mechanism-for-resolving-code-lists)
	- [1.5. Identifying a code list at run time](#identifying-a-code-list-at-run-time)
	- [1.6. Identifying a code list at schema time](#identifying-a-code-list-at-schema-time)

- [2. Terminology](#terminology)

	- [2.1. RFC 2119: Key words for use in RFCs to Indicate Requirement Levels](#rfc-2119:-key-words-for-use-in-rfcs-to-indicate-requirement-levels)
	- [2.2. RFC 3986: Uniform Resource Identifier (URI): Generic Syntax](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
	- [2.3. XML](#xml)
	- [2.4. XML Namespaces](#xml-namespaces)
	- [2.5. XML Information Set](#xml-information-set)
	- [2.6. XML Schema](#xml-schema)
	- [2.7. Conformance Targets Attribute Specification](#conformance-targets-attribute-specification)
	- [2.8. NIEM Naming and Design Rules](#niem-naming-and-design-rules)
	- [2.9. Code Lists](#code-lists)
	- [2.10. RFC 4180: Comma-separated values (CSV) files](#rfc-4180:-comma-separated-values-(csv)-files)
	- [2.11. XML Catalogs](#xml-catalogs)

- [3. Conformance targets](#conformance-targets)

	- [3.1. Code list document](#code-list-document)
	- [3.2. Genericode code list document](#genericode-code-list-document)
	- [3.3. CSV code list document](#csv-code-list-document)
	- [3.4. Code list-enabled schema document](#code-list-enabled-schema-document)
	- [3.5. Code list-enabled instance document](#code-list-enabled-instance-document)
	- [3.6. Code list validation set](#code-list-validation-set)

- [4. Binding XML content to code lists](#binding-xml-content-to-code-lists)

	- [4.1. Multiple bindings](#multiple-bindings)
	- [4.2. Binding by URI](#binding-by-uri)
	- [4.3. Definition of code list binding](#definition-of-code-list-binding)
	- [4.4. Run-time binding](#run-time-binding)

		- [4.4.1. Syntax for run-time code list binding](#syntax-for-run-time-code-list-binding)
		- [4.4.2. Run-time effective code list binding](#run-time-effective-code-list-binding)

	- [4.5. Schema-time binding](#schema-time-binding)

		- [4.5.1. Syntax for schema-time code list binding](#syntax-for-schema-time-code-list-binding)
		- [4.5.2. Simple binding of schema components](#simple-binding-of-schema-components)
		- [4.5.3. Complex binding of schema components](#complex-binding-of-schema-components)

	- [4.6. Matches for code list bindings](#matches-for-code-list-bindings)

- [5. Comma-separated values (CSV) code lists](#comma-separated-values-(csv)-code-lists)
- [6. Genericode code lists](#genericode-code-lists)
- [7. Well-known columns and references](#well-known-columns-and-references)

	- [7.1. Column: "code"](#column:-code)
	- [7.2. Column: "definition"](#column:-definition)
	- [7.3. Column: "subclass-of"](#column:-subclass-of)
	- [7.4. Column: "uri"](#column:-uri)
	- [7.5. Columns supporting ranges of values](#columns-supporting-ranges-of-values)

		- [7.5.1. Column: "minimum-inclusive"](#column:-minimum-inclusive)
		- [7.5.2. Column: "minimum-exclusive"](#column:-minimum-exclusive)
		- [7.5.3. Column: "maximum-inclusive"](#column:-maximum-inclusive)
		- [7.5.4. Column: "maximum-exclusive"](#column:-maximum-exclusive)

	- [7.6. Code list example using well-known columns](#code-list-example-using-well-known-columns)

- [Appendix A. References](#appendix-a-references)
- [Appendix B. XML Schema document for the code lists instance namespace](#appendix-b-xml-schema-document-for-the-code-lists-instance-namespace)
- [Appendix C. XML Schema document for the code list schema appinfo namespace](#appendix-c-xml-schema-document-for-the-code-list-schema-appinfo-namespace)
- [Appendix D. Example documents: Make–Model example](#appendix-d-example-documents:-make–model-example)

	- [Appendix D.1. Vehicle make and model code list](#appendix-d1-vehicle-make-and-model-code-list)
	- [Appendix D.2. Make–Model code list CSV file](#appendix-d2-make–model-code-list-csv-file)
	- [Appendix D.3. Make–Model code list Genericode file](#appendix-d3-make–model-code-list-genericode-file)
	- [Appendix D.4. XML instance with schema-time code list binding](#appendix-d4-xml-instance-with-schema-time-code-list-binding)
	- [Appendix D.5. Extension schema with schema-time code list binding](#appendix-d5-extension-schema-with-schema-time-code-list-binding)
	- [Appendix D.6. XML catalog for schema-time code list binding](#appendix-d6-xml-catalog-for-schema-time-code-list-binding)
	- [Appendix D.7. XML instance with run-time code list binding](#appendix-d7-xml-instance-with-run-time-code-list-binding)
	- [Appendix D.8. Extension schema with run-time code list binding](#appendix-d8-extension-schema-with-run-time-code-list-binding)
	- [Appendix D.9. XML catalog for run-time code list binding](#appendix-d9-xml-catalog-for-run-time-code-list-binding)

- [Appendix E. Index](#appendix-e-index)
- [Appendix F. Index of definitions](#appendix-f-index-of-definitions)
- [Appendix G. Index of rules](#appendix-g-index-of-rules)

# Table of Figures

- _Figure 1-1: An XML instance with run-time code list binding_
- _Figure 1-2: XML instance using schema-time code list binding_
- _Figure 1-3: XML schema defining a simple code list binding_
- _Figure 1-4: XML schema defining a complex code list binding_
- _Figure 7-1: Instance referencing range columns_
- _Figure 7-2: Definition of columns in Genericode_
- _Figure 7-3: Definition of columns in Genericode_
- _Figure 7-4: Distinct entries in Genericode_

# Table of Tables

- _Table 1-1: Example code list: vehicle makes and models_
- _Table 3-1: Codes representing conformance targets_
- _Table 7-1: Example code list: directions_
- _Table 7-2: Use of columns in a code list_
- _Table D-1: Vehicle make and model code list_

# Introduction

This document establishes methods for using code list artifacts with NIEM information exchange specifications. It provides for the use of Genericode documents, as well as for CSV code lists. It supports the use of code lists at schema definition time, via annotations for XML Schema documents that bind schema components to code lists. It supports the use of code lists at run time, via XML Schema components for use in XML documents that bind XML data to code lists. It also includes identifiers for well-known columns that have semantics needed across the NIEM community.

This specification supplements the use of XML Schema enumerations and simple types as a representation of code lists for information exchanges, which is sufficient for many use cases. The use of separate artifacts for code lists, along with annotations for XML Schema documents, has several goals and benefits, including include:

- Highly detailed and precise code lists, including:

	- Multiple columns may be used to carry additional information about a code, or about a concept represented by a code.
	- Multiple fields in an exchange may be validated against the same code list, enabling the use of composite keys composed of values from multiple columns of a code list. This supports use cases such as validation of both make and model of a vehicle, or state and county of a location.
	- Support for relationships between codes, via the "subclass-of" column, so that one entry in a code list can described as a specialization of another entry.
	- Support for multiple languages for code definitions and other information.

- Independent version management of code lists and XML schemas for information exchange. A single version of a code list may be used for multiple exchanges, and a single exchange specification may use multiple versions of a code list. As well, an exchange may support multiple versions of a code list simultaneously.
- Easy updating of code lists within schema sets and operational systems.
- A code list may be represented as a CSV spreadsheet document, enabling easy editing and importing of codes and supporting data.
- A code list may be represented as a Genericode XML document, supporting XML approaches to metadata management, and supporting the advanced features of Genericode, including version management and composite keys.
- Code lists may be specified at schema time, in which case code list identifiers may appear in XML Schema documents.
- Code lists may be specified at run time, in which case code list identifiers may appear in XML messages.
- Software for resolving code list identifiers to code list documents is included in many software platforms, via implementations of entity resolvers that use XML Catalogs.

This specification expands support for code lists, by enabling code lists to be managed independently of XML Schema documents, while still allowing them to support development of XML schemas and to be used for run-time validation. With the support of this specification, a single revision of a code list document may be used with multiple information exchange specifications. As well, a single information exchange specification may be used with multiple versions of a code list.

Features of this specification may be used in combination with other methods of representing code lists in exchanges, such as the use of enumerated values in simple types defined by XML Schema documents.

This specification describes an abstract model for code lists, and describes implementation of that model via Genericode and CSV files. Use of additional representations may be incorporated into future versions of this specification, as needed. In addition, the metadata and methods described by this document may support web service interactions for code list access, although such a mechanism is not described herein.

## Code list example

This section provides an example of a code list and how that code list can be integrated with XML Schemas to provide additional validation and meaning to messages. Take as an example a code list for vehicle makes and models:

### Table 1-1: Example code list: vehicle makes and models

| Make code | Make description | Model code | Model description | Class  |
| --------- | ---------------- | ---------- | ----------------- | ------ |
| FORD      | Ford             | FUS        | Fusion            | Auto   |
| HOND      | Honda            | CIV        | Civic             | Auto   |
| HOND      | Honda            | CRV        | CRV               | SUV    |
| DODG      | Dodge            | R15        | Ram 1500          | Pickup |
| NISS      | Nissan           | ALT        | Altima            | Auto   |
| FORD      | Ford             | F15        | F-150             | Pickup |
| TOYT      | Toyota           | COA        | Corolla           | Auto   |
| FORD      | Ford             | 500        | Five Hundred      | Auto   |
| HOND      | Honda            | ACC        | Accord            | Auto   |
| TOYT      | Toyota           | CAM        | Camry             | Auto   |
| CHEV      | Chevrolet        | SLV        | Silverado         | Pickup |
| MERZ      | Mercedes-Benz    | 500        | 500 Series        | Auto   |

To take the summary from [Section 2.9, _Code Lists_, below](#code-lists):

> To summarize, a _code list_ is a set of distinct entries with a corresponding set of columns. Each _distinct entry_ contains a set of code values. Each _code value_ corresponds to a distinct column in the code list. Each _column_ identifies and describes the code values within the distinct entries of the code list. A _code list identifier_ is a name for the code list as a whole, and a _column name_ is a name of a single column within a code list.

In this example:

- The _code list_ is the table.
- The _distinct entries_ are the rows (excluding the header) that start with "FORD", "HOND", etc.
- The _code values_ are the values of the individual table cells (excluding the header), including "FORD", "Ford", "FUS", "Fusion", etc.
- The code list _columns_ are the vertical stacks "Make code", "Make description", "Model code", "Model description", and "Class". Each column has a header and a slot within each distinct entry.

What we see above is a code list, but there are things missing; in order to make code lists and their uses machine-readable and verifiable, this specification provides:

1. **Machine-readable formats** for code lists. This specification provides for the use of Genericode (an XML representation) and CSV files to represent code lists. It also provides a foundation for other representations of code lists, to be identified and implemented later.
1. **Identifiers** for code lists. This specification defines that an _absolute URI_ is an identifier for a code list (as well, [Genericode](#Appendix-A-References) distinguishes between an identifier for a class of code lists and an identifier for a particular version of a code list). This specification also defines an _absolute URI_ as an identifier for a column, and a character string value as a name of a column within a code list.
1. Mechanism for **resolving** code lists. This specification leverages XML Catalogs to resolve code list identifier URIs into code list documents.
1. Mechanism for identifying the **use of a code list in an XML message**, such that it can be identified or specified by the exchanged message itself. This specification provides several XML attributes (in the _code lists instance namespace_) that label XML element content as corresponding to code values in a code list.
1. Mechanism for identifying **use of a code list in an XML Schema**, such that it can be determined at IEPD development time or system load time. This specification provides a small XML vocabulary (in the _code lists schema appinfo namespace_) that annotates XML Schema component definitions, to describe correspondences between XML content and code values in a code list.
1. **Matching values** in an XML instance document to code list distinct entries: This specification defines matches between a code list binding and a code list. Each code list binding may result in zero or more matches to _distinct entries_ in a _code list_.

## Machine-readable format for a code list

This specification provides for representing code lists using CSV files and Genericode files. The code list in _Table 1-1, _Example code list: vehicle makes and models_, above,_ may be represented as a CSV or Genericode document, as shown in [Appendix D.2, _Make–Model code list CSV file_, below,](#appendix-d2-make–model-code-list-csv-file) and [Appendix D.3, _Make–Model code list Genericode file_, below](#appendix-d3-make–model-code-list-genericode-file).

This specification also provides a framework for code lists that may be implemented using other formats. The syntax of code list bindings and code list use in instance documents may leverage formats other than CSV and Genericode. Future specifications may identify how other formats satisfy the code list framework defined by this document. 

## Identifiers for code lists

Consistent with [Genericode](#Appendix-A-References), this specification defines _absolute URIs_ as identifiers for code lists. Each code list may have any number of identifiers, each a URI. Genericode identifies several kinds of URIs that identify a code list.

This specification also provides for the identification of columns within a code list. It defines column names as strings, whereas Genericode defines column IDs of type `xs:ID`. The use of strings to carry identifiers allows CSV and other non-Genericode representations for code lists.

The use of identifiers for code lists and columns is shown in the examples:

- [Appendix D.3, _Make–Model code list Genericode file_, below,](#appendix-d3-make–model-code-list-genericode-file) shows URIs that identify the code list (one for the class of code list, another for the specific version of the code list). It also shows column definitions, each of which is provided an ID.
- [Appendix D.5, _Extension schema with schema-time code list binding_, below,](#appendix-d5-extension-schema-with-schema-time-code-list-binding) shows the use of code list URIs and column names to reference a code list from an XML Schema document.
- [Appendix D.7, _XML instance with run-time code list binding_, below,](#appendix-d7-xml-instance-with-run-time-code-list-binding) shows the use of code list URIs and column names to reference a code list from an XML instance document.
- [Appendix D.6, _XML catalog for schema-time code list binding_, below,](#appendix-d6-xml-catalog-for-schema-time-code-list-binding) and [Appendix D.9, _XML catalog for run-time code list binding_, below,](#appendix-d9-xml-catalog-for-run-time-code-list-binding) show the use of code list URIs to identify Genericode documents.

## Mechanism for resolving code lists

This specification uses the mechanism defined by [XML Catalogs](#Appendix-A-References) to describe the resolution of _code list identifier_ URIs into _code list documents_. Examples of this in use are shown in the _catalog entry files_ in [Appendix D.6, _XML catalog for schema-time code list binding_, below,](#appendix-d6-xml-catalog-for-schema-time-code-list-binding) and [Appendix D.9, _XML catalog for run-time code list binding_, below](#appendix-d9-xml-catalog-for-run-time-code-list-binding). Each of these catalog files resolves the _code list identifier_ "http://example.org/code-list/vehicle-make-model" to a locally available _resource_ "make-model.gc", a Genericode code list document. 

## Identifying a code list at run time

An XML document can connect its contents to code lists using attributes that appear in the instance. This is called a run-time binding, and connects the simple content of an element to a code value in a code list. The attributes that define this connection are in the _code lists instance namespace_. They are:

- Attribute `cli:codeListURI`: Carries an _absolute URI_ that acts as a _code list identifier_. It identifies a code list to which the value belongs.
- Attribute `cli:codeListColumnName`: Carries an `xs:string` that holds the name of a column within the code list, or a well-known column reference. The value of the element corresponds to a value in the identified column. This attribute may be optional; if it does not appear, the binding defaults to "#code", which is resolved to a code column, as specified for the class of code list document.
- Attribute `cli:codeListConstrainingIndicator`: carries an `xs:boolean` that indicates whether the binding to the code list defines a constraint on the validity of the message. This attribute is optional; if it does not appear, then the binding constrains message validity. Values are:

	- **true**: The message is valid only if the value of the element appears in the indicated column of the indicated code list. This is the default.
	- **false**: The validity of the message is not affected by the occurrence of the value within the code list. This allows a code list to be used as a source of meaningful values while allowing values not in the code list to be passed.

 _Figure 1-1, _An XML instance with run-time code list binding_, below,_ shows an example of run-time binding It uses the attribute `cli:codeListURI` to connect the value of element `ext:VehicleMakeCode` ("DODG") to the make–model code list, and the attribute `cli:codeListColumnName` to connect the value to the "make" column of that code list. It also connects the value of `ext:VehicleModelCode` ("R15") to the "model" column of the code list.

## Figure 1-1: An XML instance with run-time code list binding

```xml
<nc:Vehicle
   xmlns:cli="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
   xmlns:ext="http://example.org/namespace/extension-run-time"
   xmlns:nc="http://release.niem.gov/niem/niem-core/4.0/">
 <ext:VehicleMakeCode
     cli:codeListURI="http://example.org/code-list/vehicle-make-model"
     cli:codeListColumnName="make"
   >DODG</ext:VehicleMakeCode>
 <ext:VehicleModelCode
     cli:codeListURI="http://example.org/code-list/vehicle-make-model"
     cli:codeListColumnName="model"
   >R15</ext:VehicleModelCode>
</nc:Vehicle>
```

Advantages of this strategy include:

- The connection is established by the writer of the message, rather than the writer of the schema.
- The connection is established at run time, rather than at the time the schemas are defined.
- The connection to code lists is explicit in the XML instance document, rather than being defined in schemas that are not exchanged.

## Identifying a code list at schema time

This specification defines an annotation vocabulary, the _code lists schema appinfo namespace_, which allows connections between code lists and elements, attributes, and types that are defined in an XML Schema. This is managed with two annotation elements:

- `clsa:SimpleCodeListBinding`: a simple code list binding connects the simple content of an element or the value of an attribute to a code list. It is added to a schema component definition as an appinfo annotation. A simple code list binding may be attached to top-level attribute declarations, element declarations, simple type definitions, and complex type definitions. It has the following attributes:

	- Attribute `codeListURI` identifies the code list.
	- Attribute `columnName` identifies the code list column, or a well-known column reference.
	- Attribute `constrainingIndicator` indicates whether the existence (or absence) of a value in a code list impacts validity of the instance XML document.

- `clsa:ComplexCodeListBinding`: a complex code list binding on a complex type or element connects child elements to columns of a code list. Like a simple code list binding, it is added as a schema annotation on schema component definitions. It may be added to a top-level element declaration, or to a named complex type definition. It has the following parts:

	- Attribute `codeListURI` identifies the code list.
	- Attribute `constrainingIndicator` indicates whether the existence (or absence) of a value in a code list impacts validity of the instance XML document.
	- Element `clsa:ElementCodeListBinding` attaches child elements to columns of the code list. It has attributes:

		- Attribute `elementName` provides the name of an element whose value is connected to a code list.
		- Attribute `columnName` provides the name of a column of the code list, or a well-known column reference.

_Figure 1-2, _XML instance using schema-time code list binding_, below,_ shows an instance that uses schema-time binding. The instance does not carry any information about code lists; it does not have a code list identifier, nor does it have a column name. The instance is simple.

## Figure 1-2: XML instance using schema-time code list binding

```xml
<ext:Vehicle
 <ext:VehicleMakeCode>DODG</ext:VehicleMakeCode>
 <ext:VehicleModelCode>R15</ext:VehicleModelCode>
</ext:Vehicle>
```
The simple code list binding in _Figure 1-3, _XML schema defining a simple code list binding_, below,_ connects the content of VehicleMakeCode to the code list's "make" column.

## Figure 1-3: XML schema defining a simple code list binding

```xml
<xs:element name="VehicleMakeCode" type="niem-xs:token"
           substitutionGroup="nc:VehicleMakeAbstract">
 <xs:annotation>
   <xs:documentation>A code for a manufacturer of a vehicle.</xs:documentation>
   <xs:appinfo>
     <clsa:SimpleCodeListBinding
         codeListURI="http://example.org/code-list/vehicle-make-model"
         columnName="make"/>
   </xs:appinfo>
 </xs:annotation>
</xs:element>
```

The complex code list binding in _Figure 1-4, _XML schema defining a complex code list binding_, below,_ connects `nc:VehicleMake` and `nc:VehicleModel` child elements of element `Vehicle` to the code list:

- It connects the `nc:VehicleMake` element (or an element substitutable for `nc:VehicleMake`) to the column named "make".
- It connects the `nc:VehicleModel` element (or an element substitutable for `nc:VehicleModel`) to the column named "model".

## Figure 1-4: XML schema defining a complex code list binding

```xml
<xs:element name="Vehicle" type="nc:VehicleType"
           substitutionGroup="nc:Vehicle">
 <xs:annotation>
   <xs:appinfo>
     <clsa:ComplexCodeListBinding
         codeListURI="http://example.org/code-list/vehicle-make-model">
       <clsa:ElementCodeListBinding elementName="ext:VehicleMakeCode"
                                    columnName="make"/>
       <clsa:ElementCodeListBinding elementName="ext:VehicleModelCode"
                                    columnName="model"/>
     </clsa:ComplexCodeListBinding>
   </xs:appinfo>
 </xs:annotation>
</xs:element>
```
Advantages of this strategy include:

- Simplicity: Instance documents that don't specify code list bindings are simpler than those that do. When the schema defines the code list binding, the instance documents do not need to carry the code list connection attributes, making them much less verbose.
- Trust: connections to code lists are not defined by untrusted messages. The connections between the instances and code lists are defined as part of the schema of the message.
- Multiple bindings: a single value in an instance XML document be connected to multiple code lists in different ways. This is done by defining multiple code list bindings for elements, attributes, or types in the XML Schema that defines the value.
- Multiple columns: multiple child elements may be connected to multiple columns in a code list. For example, from [Appendix D.8, _Extension schema with run-time code list binding_, below,](#appendix-d8-extension-schema-with-run-time-code-list-binding) this annotation on a vehicle type connects the make and model fields of the vehicle to the make and model columns of a code list:

# Terminology

This document relies on terminology defined by other specifications and standards, as well as terminology specific to this specification. This section introduces many terms, and directs the reader to the external source definition of a term when appropriate. The following sections reflect the different sources and topics of this terminology:

- [Section 2.1, _RFC 2119: Key words for use in RFCs to Indicate Requirement Levels_](#rfc-2119:-key-words-for-use-in-rfcs-to-indicate-requirement-levels)
- [Section 2.2, _RFC 3986: Uniform Resource Identifier (URI): Generic Syntax_](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
- [Section 2.3, _XML_](#xml)
- [Section 2.4, _XML Namespaces_](#xml-namespaces)
- [Section 2.5, _XML Information Set_](#xml-information-set)
- [Section 2.6, _XML Schema_](#xml-schema)
- [Section 2.7, _Conformance Targets Attribute Specification_](#conformance-targets-attribute-specification)
- [Section 2.8, _NIEM Naming and Design Rules_](#niem-naming-and-design-rules)
- [Section 2.9, _Code Lists_](#code-lists)
- [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- [Section 2.11, _XML Catalogs_](#xml-catalogs)

## RFC 2119: Key words for use in RFCs to Indicate Requirement Levels

Within normative content (rules and definitions), the key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC2119](#Appendix-A-References).

## RFC 3986: Uniform Resource Identifier (URI): Generic Syntax

[RFC3986](#Appendix-A-References) defines uniform resource identifier (URI), which it describes as:

> A Uniform Resource Identifier (URI) is a compact sequence of characters that identifies an abstract or physical resource.

The term absolute URI is as defined by [RFC3986](#Appendix-A-References) [Section 4.3, _Absolute URI_](http://tools.ietf.org/html/rfc3986#section-4.3), identifying a uniform resource identifier that matches the grammar production `absolute-URI`.

The term resource is defined by [RFC3986](#Appendix-A-References) [Section 1.1, _Overview of URIs_](http://tools.ietf.org/html/rfc3986#page-5), which states:

> This specification does not limit the scope of what might be a resource; rather, the term "resource" is used in a general sense for whatever might be identified by a URI. Familiar examples include an electronic document, an image, a source of information with a consistent purpose (e.g., "today’s weather report for Los Angeles"), a service (e.g., an HTTP-to-SMS gateway), and a collection of other resources.

## XML

The term XML document is defined by [XML](#Appendix-A-References) [Section 2, _Documents_](http://www.w3.org/TR/2008/REC-xml-20081126/#dt-xml-doc), which states:

> A data object is an XML document if it is well-formed, as defined in this specification.

## XML Namespaces

This document uses XML Namespaces as defined by [XMLNamespaces](#Appendix-A-References).

The following namespace prefixes are used consistently within this specification. These prefixes are not normative; this document issues no requirement that these prefixes be used in any conformant artifact. Although there is no requirement for a schema or XML document to use a particular namespace prefix, the meaning of the following namespace prefixes have fixed meaning in this document.

- `xs` ("XML Schema"): The namespace for the XML Schema definition language as defined by [XMLSchema1](#Appendix-A-References) and [XMLSchema2](#Appendix-A-References): "`http://www.w3.org/2001/XMLSchema`".
- `ct` ("conformance targets"): The namespace defined by [CTAS](#Appendix-A-References) for the `ct:conformanceTargets` attribute: "`http://release.niem.gov/niem/conformanceTargets/3.0/`".
- `cli` ("code lists instance"): Defined by this specification, the code lists instance namespace defines attributes that connect XML element content to code lists at run time: "`http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/`". The XML schema document defining this namespace is provided in [Appendix B, _XML Schema document for the code lists instance namespace_, below](#appendix-b-xml-schema-document-for-the-code-lists-instance-namespace).
- `clsa` ("code list schema appinfo"): Defined by this specification, the code lists schema appinfo namespace defines an XML vocabulary for use in `xs:appinfo` on XML Schema component definitions, which connect XML element and attribute content to code lists: "`http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-schema-appinfo/`". The XML schema document defining this namespace is provided in [Appendix C, _XML Schema document for the code list schema appinfo namespace_, below](#appendix-c-xml-schema-document-for-the-code-list-schema-appinfo-namespace).
- `gc` ("Genericode"): The namespace for the XML vocabulary for Genericode, as defined by [Genericode](#Appendix-A-References): "`http://docs.oasis-open.org/codelist/ns/genericode/1.0/`".

## XML Information Set

This document refers to content of XML documents using terms from [XML Infoset](#Appendix-A-References). Terminology adapted from [XML Infoset](#Appendix-A-References) includes:

- The term element refers to an element information item as defined by [XML Infoset](#Appendix-A-References) [Section 2.2, _Element Information Items_](http://www.w3.org/TR/2004/REC-xml-infoset-20040204/#infoitem.element).
- The term attribute refers to an attribute information item as defined by [XML Infoset](#Appendix-A-References) [Section 2.3, _Attribute Information Items_](http://www.w3.org/TR/2004/REC-xml-infoset-20040204/#infoitem.attribute).
- The term text refers to the encapsulation of a series of character information items, as defined by defined by [XML Infoset](#Appendix-A-References) [Section 2.6, _Character Information Items_](http://www.w3.org/TR/2004/REC-xml-infoset-20040204/#infoitem.character). A text item aggregates all contiguous character information items that have the same parent node.
- Properties of information items used by this document include:

	- **[namespace name]** and **[local name]** of an element or attribute
	- **[parent]** of an element
	- **[attributes]** of an element

- An information item that is identified by a qualified name is referring to the **[namespace name]** corresponding to the qualified name’s prefix assigned value or namespace URI, and **[local name]** corresponding to the qualified name’s local name.

## XML Schema

This specification provides definitions and mechanisms that may be used within XML Schemas and individual XML Schema documents for validation of information exchanges. To define these mechanisms, terminology from the XML Schema specification must be clarified.

Terms adapted from [XMLSchema1](#Appendix-A-References) include:

- The term XML Schema definition language is defined by [XMLSchema1](#Appendix-A-References) [subsection _Abstract_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#abstract), which states:
<blockquote>_XML Schema: Structures_ specifies the XML Schema definition language, which offers facilities for describing the structure and constraining the contents of XML 1.0 documents, including those which exploit the XML Namespace facility. The schema language, which is itself represented in XML 1.0 and uses namespaces, substantially reconstructs and considerably extends the capabilities found in XML 1.0 document type definitions (DTDs).
</blockquote>
- The term XML Schema is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2, _XML Schema Abstract Data Model_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-schema), which states:
<blockquote>An **XML Schema** is a set of schema components.
</blockquote>
- The term schema component is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2, _XML Schema Abstract Data Model_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-component), which states:
<blockquote>**Schema component** is the generic term for the building blocks that comprise the abstract data model of the schema.
</blockquote>
- The term schema document is defined by [XMLSchema1](#Appendix-A-References) [Section 3.1.2, _XML Representations of Components_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-schemaDoc), which states:
<blockquote>A document in this form (i.e. a &lt;schema&gt; element information item) is a **schema document**.
</blockquote>
- The term normalized value is defined by [XMLSchema1](#Appendix-A-References) [Section 3.1.4, _White Space Normalization during Validation_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-nv).
- The term attribute declaration is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2.2.3, _Attribute Declaration_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#Attribute_Declaration).
- The term element declaration is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2.2.1, _Element Declaration_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#Element_Declaration).
- The substitution group of an element declaration is defined by [XMLSchema1](#Appendix-A-References) [Section 3.3.6, _Constraints on Element Declaration Schema Components_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-eq).
- The term type definition is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2.1, _Type Definition Components_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-typeDefn).
- The term simple type definition is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2.1.2, _Simple Type Definition_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#Simple_Type_Definition).
- The term complex type definition is defined by [XMLSchema1](#Appendix-A-References) [Section 2.2.1.3, _Complex Type Definition_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#Complex_Type_Definition).
- The term schema-valid refers to "valid" as defined by [XMLSchema1](#Appendix-A-References) [Section 2.1, _Overview of XML Schema_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-vn).
Note that a requirement for XML content to be schema-valid does not imply or require that validation against XML Schemas must actually occur at run time. Rather, it means that the XML content that is required to be schema-valid must be composed such that it would be assessed as valid were schema validity assessment to take place. Schema validity may be described in terms of a schema document, in which case validity should be considered as strictly assessed against the namespaces defined by that schema document.

- A type `$derived` is derived from a type `$base` if and only if type `$derived` is validly derived from type `$base` for _{extension, restriction}_ as defined by [XMLSchema1](#Appendix-A-References) [Section 3.4.6, _Constraints on Complex Type Definition Schema Components_, subsection _Schema Component Constraint: Type Derivation OK (Complex)_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#cos-ct-derived-ok) and [Section 3.14.6, _Constraints on Simple Type Definition Schema Components_, subsection _Schema Component Constraint: Type Derivation OK (Simple)_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#cos-st-derived-ok).
Note that this means that a type can be said to be derived from itself.

The XML Schema defines properties of schema components, including:

- {type definition} of an _attribute declaration_, as defined by [XMLSchema1](#Appendix-A-References) [Section 3.2.1, _The Attribute Declaration Schema Component_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#a-simple_type_definition)
- {type definition} of an _element declaration_, as defined by [XMLSchema1](#Appendix-A-References) [Section 3.3.1, _The Element Declaration Schema Component_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#type_definition)

The XML Schema specification defines additional properties of information set information items as part of the [post-schema-validation infoset (PSVI)](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#key-psvi). These properties include:

- **[attribute declaration]** of an _attribute_, as defined by [XMLSchema1](#Appendix-A-References) [Section 3.2.5, _Attribute Declaration Information Set Contributions_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#a-declaration)
- **[element declaration]** of an _element_, as defined by [XMLSchema1](#Appendix-A-References) [Section 3.3.5, _Element Declaration Information Set Contributions_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#e-declaration)
- **[type definition]** of an _element_, as defined by [XMLSchema1](#Appendix-A-References) [Section 3.3.5, _Element Declaration Information Set Contributions_](http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/#e-type_definition)

To facilitate code lists representing ranges of values as described in [Section 7.5, _Columns supporting ranges of values_, below](#columns-supporting-ranges-of-values), the following terms are adapted from [XMLSchema2](#Appendix-A-References), [Section 4.2, _Fundamental Facets_, Subsection 4.2.1, _bounded_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#rf-bounded):

- The term inclusive upper bound is as defined by [XMLSchema2](#Appendix-A-References) [Section 4.2.1, _bounded_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#dt-inclusive-upper-bound).
- The term exclusive upper bound is as defined by [XMLSchema2](#Appendix-A-References) [Section 4.2.1, _bounded_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#dt-exclusive-upper-bound).
- The term inclusive lower bound is as defined by [XMLSchema2](#Appendix-A-References) [Section 4.2.1, _bounded_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#dt-inclusive-lower-bound).
- The term exclusive lower bound is as defined by [XMLSchema2](#Appendix-A-References) [Section 4.2.1, _bounded_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#dt-exclusive-lower-bound).

See also [Section 2.8, _NIEM Naming and Design Rules_, below,](#niem-naming-and-design-rules) for the term _XML Schema document set_.

## Conformance Targets Attribute Specification

[CTAS](#Appendix-A-References) defines several terms used normatively within this specification.

The term conformance target is defined by [CTAS](#Appendix-A-References) [Section 3.1, _Conformance Target Defined_](http://reference.niem.gov/niem/specification/conformance-targets-attribute/3.0/NIEM-CTAS-3.0-2014-07-31.html#definition_conformance_target) which states:

> A _conformance target_ is a class of artifact, such as an interface, protocol, document, platform, process or service, that is the subject of conformance clauses and normative statements. There may be several conformance targets defined within a specification, and these targets may be diverse so as to reflect different aspects of a specification. For example, a protocol message and a protocol engine may be different conformance targets.

The term conformance target identifier is defined by [CTAS](#Appendix-A-References) [Section 3.1, _Conformance Target Defined_](http://reference.niem.gov/niem/specification/conformance-targets-attribute/3.0/NIEM-CTAS-3.0-2014-07-31.html#definition_conformance_target_identifier), which states:

> A _conformance target identifier_ is an internationalized resource identifier that uniquely identifies a conformance target.

The term effective conformance target identifier is defined by [CTAS](#Appendix-A-References) [Section 4, _Semantics and Use_](http://reference.niem.gov/niem/specification/conformance-targets-attribute/3.0/NIEM-CTAS-3.0-2014-07-31.html#definition_effective_conformance_target_identifier), which states:

> An _effective conformance target identifier_ of a conformant document is an internationalized resource identifier reference that occurs in the document’s effective conformance targets attribute.

## NIEM Naming and Design Rules

The term application information (of a _schema component_) is defined by [NIEM NDR](#Appendix-A-References) [Section 10.9, _Machine-readable annotations_](http://reference.niem.gov/niem/specification/naming-and-design-rules/5.0/niem-ndr-5.0.html#definition_application_information), describing the contents of `xs:appinfo` annotations on the element that defines a schema component.

The term XML Schema document set is defined by [NIEM NDR](#Appendix-A-References) [Section 3.4, _XML Schema terminology_](http://reference.niem.gov/niem/specification/naming-and-design-rules/5.0/niem-ndr-5.0.html#definition_XML_Schema_document_set), which states:

> An XML Schema document set is a set of schema documents that together define an XML Schema suitable for assessing the validity of an XML document.

## Code Lists

To facilitate the use of code lists, this document must define some terms related to code lists and their use. [Genericode](#Appendix-A-References) is the source of some of this terminology, although in this specification much of this terminology refers to code lists in the abstract, rather than only as concrete Genericode documents.

> **[Definition: code list]**
> A **code list** is a set of _distinct entries_ with a corresponding set of _columns_. A code list may be thought of as a table, with table rows as distinct entries, table columns as code list columns, and individual cells as _code values_.

> **[Definition: distinct entry]**
> A **distinct entry** is a single conceptual entity within a _code list_. It is composed of a set of _code values_, each corresponding to a _column_ of the code list. It may be thought of as a row of a table, where each individual cell of a row corresponds to a column of the table.

> **[Definition: code value]**
> A **code value** is a single data value within a _distinct entry_ in a _code list_. Each code value of a distinct entry corresponds to a _column_ of the code list.

[Genericode](#Appendix-A-References) uses the term "_code value_ when referring to a value of a _distinct entry_.

> **[Definition: column]**
> A **column** of a _code list_ is metadata that describes a _code value_ within each _distinct entry_ of the code list. Each code value within the code list corresponds to one column of the code list.

> **[Definition: code list identifier]**
> A **code list identifier** is an _absolute URI_ that identifies a _code list_.

This document defines two designators for a column of a code list, the _column identifier_ and the _column name_.

> **[Definition: column identifier]**
> A **column identifier** is an _absolute URI_ that identifies a _column_ of a _code list_.

A _column identifier_ identifies a column irrespective of the specific code list in which it occurs. [Genericode](#Appendix-A-References) defines `CanonicalUri` and `CanonicalVersionUri` that are column identifiers, which it provides for assigning universal semantics to code list columns.

> **[Definition: column name]**
> A **column name** is a character string value that identifies a _column_ within the scope of a _code list_.

A _column name_ is a text (character string) value that identifies a column, only within the scope of a specific code list. A column within a _Genericode code list document_ has an XML ID that uniquely identifies it within the document.

Note that all of the above definitions are abstract. They do not get into the details of Genericode, (e.g., canonical URIs, version URIs, location URIs, `ColumnRef`s, `ColumnSet`s, and `KeyRef`s). These terms and identifiers are generically defined here so that they may be applied to CSV and Genericode documents, or to other methods of expressing code lists, including other data file formats and registry-based services.

To summarize, a _code list_ is a set of distinct entries with a corresponding set of columns. Each _distinct entry_ contains a set of code values. Each _code value_ corresponds to a distinct column in the code list. Each _column_ identifies and describes the code values within the distinct entries of the code list. A _code list identifier_ is a name for the code list as a whole, and a _column name_ is a name of a single column within a code list.

Further, this document defines the terms _code list document_, _CSV code list document_, and _Genericode code list document_. These are _conformance targets_ of this specification. A _code list document_ is a file, document or other _resource_ that carries one or more code lists. A _CSV code list document_ is a _code list document_ that uses comma-separated values format defined by [RFC4180](#Appendix-A-References). A _Genericode code list document_ is a _code list document_ that uses syntax defined by [Genericode](#Appendix-A-References).

## RFC 4180: Comma-separated values (CSV) files

This document uses the definition of CSV files as defined by [RFC4180](#Appendix-A-References). The following terms take their definitions from the ABNF (Augmented Backus-Naur Form) grammar defined by [Section 2, _Definition of the CSV Format_](http://www.ietf.org/rfc/rfc4180.txt) of that specification.

- A CSV file is a _resource_ matching rule "file" of the ABNF grammar.
- A CSV header is the portion of a _CSV file_ matching rule "header" of the ABNF grammar, and which provides names of columns within the CSV file.
- A CSV column name is the portion of a _CSV file_ matching rule "name" of the ABNF grammar.
- A CSV record is the portion of a _CSV file_ matching rule "record" of the ABNF grammar.
- A CSV field is the portion of a _CSV file_ matching rule "field" of the ABNF grammar.

## XML Catalogs

This document relies on [XML Catalogs](#Appendix-A-References) for the mechanisms for identifying and finding a code list from its _code list identifier_.

The term entity catalog is defined by [XML Catalogs](#Appendix-A-References), which states in [XML Catalogs](#Appendix-A-References) [Section 3, _An Entity Catalog_](https://www.oasis-open.org/committees/download.php/14809/std-entity-xml-catalogs-1.1.html#s.entity.catalog):

> The catalog is effectively an ordered list of (one or more) catalog entry files. It is up to the application to determine the ordered list of catalog entry files to be used as the logical catalog.

The resources (i.e., files) that are within the same local cache, ZIP file, or other contained location as an entity catalog are the local context of the entity catalog.

The term catalog entry file is defined by [XML Catalogs](#Appendix-A-References) [Section 2, _Terminology_](https://www.oasis-open.org/committees/download.php/14809/std-entity-xml-catalogs-1.1.html#s.terminology), which states:

> A catalog may be physically contained in one or more catalog entry files. A catalog entry file is a document that contains a set of catalog entries.

The term resolve refers to the process of resolving URI references, as described by [XML Catalogs](#Appendix-A-References) [Section 7.2.2, _Resolution of URI references_](https://www.oasis-open.org/committees/download.php/14809/std-entity-xml-catalogs-1.1.html#s.uri.resx), which defines the process for resolving a URI reference to a URI for a corresponding resource, as identified by an entity catalog.

> **[Definition: locally-resolved resource]**
> A **locally-resolved resource** for a _URI_ relative to an entity catalog is the _resource_ yielded through the process of _resolving_ the URI into a resource URI using the entity catalog, and then producing the corresponding resource from the _local context_ of the entity catalog.

# Conformance targets

This document defines multiple _conformance targets_. Each conformance target is defined normatively by this specification. Each conformance target has an associated abbreviation, which is used to identify to which conformance targets a rule applies.

## Table 3-1: Codes representing conformance targets

| Code    | Conformance target                  |
| ------- | ----------------------------------- |
| CLD     | code list document                  |
| GC-CLD  | Genericode code list document       |
| CSV-CLD | CSV code list document              |
| XSD     | code list-enabled schema document   |
| INS     | code list-enabled instance document |
| VSET    | code list validation set            |

## Code list document

> **[Definition: code list document]**
> A **code list document** is a file or _resource_ that contains one or more _code lists_. It is a _conformance target_ of this specification. A code list document MUST conform to all rules of this specification that apply to this conformance target. An _XML document_ with an _effective conformance target identifier_ of `http://reference.niem.gov/niem/specification/code-lists/4.0/#CodeListDocument` MUST be a code list document.

The specification for an implementation of a code list document by a class of _resource_ (such as with Genericode or CSV) needs to specify the following characteristics:

1. Candidate _code list identifiers_. Some code list documents specify what URIs may be used to reference the code list. Some _resources_ may feature multiple code lists within a single resource, and the specification must describe how a specific code list is identified within the resource.
1. The mapping between features of the resource and _distinct entries_.
1. The mapping between features of the resource and _code values_.
1. The mapping between features of the resource and _column names_.
1. The method of identifying a column as being a well-known column (described in [Section 7, _Well-known columns and references_, below](#well-known-columns-and-references)).
1. The method of identifying well-known column reference "#code" (described in [Section 7, _Well-known columns and references_, below](#well-known-columns-and-references)).
1. The method of identifying the data type of a code value, which can be a data type defined by an XML Schema, or empty.

These characteristics are described for Genericode files in [Section 6, _Genericode code lists_, below](#genericode-code-lists). They are described for CSV files in [Section 5, _Comma-separated values (CSV) code lists_, below](#comma-separated-values-(csv)-code-lists).

## Genericode code list document

> **[Definition: Genericode code list document]**
> A **Genericode code list document** is a _code list document_. It is a _conformance target_ of this specification. A Genericode code list document MUST conform to all rules of this specification that apply to this conformance target. The _conformance target identifier_ for this conformance target is `http://reference.niem.gov/niem/specification/code-lists/4.0/#GenericodeCodeListDocument`.

[Section 6, _Genericode code lists_, below,](#genericode-code-lists) provides rules for Genericode code list documents.

## CSV code list document

> **[Definition: CSV code list document]**
> A **CSV code list document** is a _code list document_. It is a _conformance target_ of this specification. A CSV code list document MUST conform to all rules of this specification that apply to this conformance target. The _conformance target identifier_ for this conformance target is `http://reference.niem.gov/niem/specification/code-lists/4.0/#CSVCodeListDocument`.

## Code list-enabled schema document

> **[Definition: code list-enabled schema document]**
> A **code list-enabled schema document** is an XML Schema document that supports the use of _code list documents_ for validation and meaning. It is a _conformance target_ of this specification. A code list-enabled schema document MUST conform to all rules of this specification that apply to this conformance target. The conformance target identifier for this conformance target is `http://reference.niem.gov/niem/specification/code-lists/4.0/#SchemaDocument`.

### Rule 3-1. Code list-enabled schema document has conformance target

> **[Rule 3-1] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> A _code list-enabled schema document_ MUST have an _effective conformance target identifier_ of `http://reference.niem.gov/niem/specification/code-lists/4.0/#SchemaDocument` 

### Rule 3-2. Document with conformance target is a code list-enabled schema document

> **[Rule 3-2] (<a href="#conformance_target_VSET">VSET</a>) (Constraint)**
> A _resource_ with an _effective conformance target identifier_ of `http://reference.niem.gov/niem/specification/code-lists/4.0/#SchemaDocument` MUST be a _code list-enabled schema document_.

## Code list-enabled instance document

> **[Definition: code list-enabled instance document]**
> A **code list-enabled instance document** is an XML document that leverages this specification to connect data values with code lists. A code list-enabled instance document MUST conform to all rules of this specification that apply to this conformance target. An _XML document_ with an _effective conformance target identifier_ of `http://reference.niem.gov/niem/specification/code-lists/4.0/#InstanceDocument` MUST be a _code list-enabled instance document_.

Although this specification defines a conformance target identifier for a code list-enabled instance document, it does not require the conformance target identifier to appear within an instance document.

## Code list validation set

A code list validation set is an abstract concept that brings together the necessary components to define validity of XML documents with respect to code lists, and to identify correspondences between XML data and code list distinct entries. There may be multiple code list validation sets in use at any point of a validation or analysis process; it is a concept meant to facilitate working with code lists.

> **[Definition: code list validation set]**
> A **code list validation set** is an abstraction that contains one or more of:
> 
> - The instance, a _code list-enabled instance document_
> - The catalog, an _entity catalog_, with its _local context_
> - The schema, an _XML Schema_, and
> - A _code list document_

# Binding XML content to code lists

XML content in a message may be identified as corresponding to content of a code list. This correspondence is referred to as a _code list binding_, connecting the XML content to the code list. This specification provides methods for binding XML content to code lists in two ways:

- At run time: An XML document may use identifiers within a message to identify correspondence of content to code lists. This is introduced in [Section 1.5, _Identifying a code list at run time_, above](#identifying-a-code-list-at-run-time), and details are provided in [Section 4.4, _Run-time binding_, below](#run-time-binding).
- At schema time: An XML Schema document may use application information annotations that identify code lists corresponding to the content of schema components. This is introduced in [Section 1.6, _Identifying a code list at schema time_, above](#identifying-a-code-list-at-schema-time), and details are provided in [Section 4.4, _Run-time binding_, below](#run-time-binding).

## Multiple bindings

Code list bindings should be seen as additional semantics and validation for parts of a message. A particular piece of XML content may be bound to multiple code lists at the same time.

For example, a message may contain elements for "vehicle make" and "vehicle model". These values may have multiple bindings, including:

- The "vehicle make" element may be bound to a code list containing vehicle manufacturers.
- The "vehicle model" element may be bound to a code list containing vehicle models.
- The pair, together, of "vehicle make" and "vehicle model" may be bound to a code list identifying a complete list of all known valid vehicle make and model combinations.
- The pair, together, may be bound to a code list identifying only valid make and model combinations of vehicles with diesel engines, which were manufactured in the United States. This represents an intentional subset of all known combinations.

## Binding by URI

Content is bound to a code list using a URI as the identifier of the code list. This identifier may be any of the following:

- A canonical URI, as defined by [Genericode](#Appendix-A-References). This identifies the code list in general, and it may be satisfied by the latest version of the code list, or some other version, as determined by the information exchange developer.
- A canonical version URI, as defined by [Genericode](#Appendix-A-References). This identifies a specific version of the code list, as implemented by a particular Genericode document.
- A location URI for a Genericode document. This identifies a particular Genericode document by a resolvable URL.
- Some other URI, identifying some other source of code list semantics. Although this specification is focused on leveraging concrete local code list documents, the mechanisms this specification provides may be used to express a dependence on registry-maintained code lists, or on other network-based semantics. The URI is just an identifier, and may have a well-known semantic within a community. Such semantics should be identified within documentation in an information exchange.

## Definition of code list binding

A code list binding brings together a set of columns from a code list with a corresponding set of data from an XML document. The binding can provide meaning for data in an XML document, and can provide additional validity constraints on an XML document. The code list binding defined here is an abstract concept, bringing together a code list (via a _code list identifier_), _column names_, and data values (such as from an information exchange package or other XML document). This abstract definition is leveraged in [Section 4.4, _Run-time binding_, below,](#run-time-binding) and [Section 4.5, _Schema-time binding_, below](#schema-time-binding).

A code list binding may be applied to a single value or to multiple values. The abstract definition of _code list binding_ is applied to the concrete mechanisms for binding data values to code lists, through run-time binding or schema-time binding.

> **[Definition: code list binding]**
> A **code list binding** is an assigned correspondence between a set of data values, such as data within an XML document, and a set of columns within a code list, identified via a _code list identifier_ and a set of _column names_.
> 
> A code list binding has the following properties:
> 
> - a _code list identifier_
> - a set of column/value pairs, each having:
> 	- a column reference: either a _column name_ or a well-known column reference, and
> 	- a data value
> - A boolean value, `constraining`.

## Run-time binding

This document provides an XML Schema document for run-time binding of XML content to code lists. This schema is provided in [Appendix B, _XML Schema document for the code lists instance namespace_, below](#appendix-b-xml-schema-document-for-the-code-lists-instance-namespace).

### Syntax for run-time code list binding

#### Rule 4-1. Content in the <q>cli</q> namespace conforms to schema

> **[Rule 4-1] ([INS](#Applicability-of-rules-to-conformance-targets)) (Constraint)**
> Any XML content in the namespace `http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/` MUST be _schema-valid_ to the XML Schema definitions contained in the schema document in [Appendix B, _XML Schema document for the code lists instance namespace_, below](#appendix-b-xml-schema-document-for-the-code-lists-instance-namespace).

#### Rule 4-2. Code list URI is an absolute URI

> **[Rule 4-2] ([INS](#Applicability-of-rules-to-conformance-targets)) (Constraint)**
> The _normalized value_ of an _attribute_ `cli:codeListURI` MUST be an _absolute URI_.

#### Rule 4-3. Column identifier accompanied by code list identifier

> **[Rule 4-3] ([INS](#Applicability-of-rules-to-conformance-targets)) (Constraint)**
> An _element_ having an attribute `cli:codeListColumnName` MUST have an attribute `cli:codeListURI`.

#### Rule 4-4. Constraining indicator accompanied by code list identifier

> **[Rule 4-4] ([INS](#Applicability-of-rules-to-conformance-targets)) (Constraint)**
> An _element_ having an attribute `cli:codeListConstrainingIndicator` MUST have an attribute `cli:codeListURI`.

### Run-time effective code list binding

#### Rule 4-5. Effective run-time binding.

> **[Rule 4-5] ([INS](#Applicability-of-rules-to-conformance-targets)) (Interpretation)**
> An element `$element` with an attribute `$attribute` `cli:codeListURI` denotes a code list binding of:
> 
> - a _code list identifier_ of the _normalized value_ of the attribute `cli:codeListURI`
> - a single column/value pair, having:
> 	- a column reference of: if `$element` has attribute `cli:codeListColumnName`, then the _normalized value_ of that attribute, else "#code".
> 	- a data value that is the _normalized value_ of `$element`.
> - A value for `constraining` that is: if `$element` has attribute `cli:codeListConstrainingIndicator`, then its value, otherwise `true`.

## Schema-time binding

This document provides XML elements for annotating XML Schema document components, to indicate, at schema time, a code list binding between a code list and one or more data values of the code list.

### Syntax for schema-time code list binding

#### Rule 4-6. Content in the <q>clsa</q> namespace conforms to schema

> **[Rule 4-6] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> Any XML content in the namespace `http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-schema-appinfo/` MUST be _schema-valid_ to the XML Schema definitions contained in the schema document in [Appendix C, _XML Schema document for the code list schema appinfo namespace_, below](#appendix-c-xml-schema-document-for-the-code-list-schema-appinfo-namespace).

#### Rule 4-7. Elements are `xs:appinfo` annotations

> **[Rule 4-7] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> An element `clsa:SimpleCodeListBinding` or `clsa:ComplexCodeListBinding` MUST have **[parent]** element `xs:appinfo`.

#### Rule 4-8. Code list URI is absolute URI

> **[Rule 4-8] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> An attribute `codeListURI` that has **[owner element]** of `clsa:SimpleCodeListBinding` or `clsa:ComplexCodeListBinding` MUST have a _normalized value_ that is an _absolute URI_.

#### Rule 4-9. Simple code list binding to schema components

> **[Rule 4-9] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> Element `clsa:SimpleCodeListBinding` MUST be _application information_ on one of:
> 
> - element `xs:attribute` that defines a global _attribute declaration_
> - element `xs:element` that defines a global _element declaration_
> - element `xs:simpleType` that defines a global _simple type definition_
> - element `xs:complexType` that defines a global _complex type definition_

#### Rule 4-10. Complex code list binding to schema components

> **[Rule 4-10] (<a href="#conformance_target_XSD">XSD</a>) (Constraint)**
> Element `clsa:ComplexCodeListBinding` MUST be _application information_ on one of:
> 
> - element `xs:element` that defines a global _element declaration_
> - element `xs:complexType` that defines a global _complex type definition_

### Simple binding of schema components

#### Rule 4-11. Attribute declaration effective simple binding

> **[Rule 4-11] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> An element `xs:attribute` defining an _attribute declaration_ `$attribute-declaration` with _application information_ of an element `$binding-element` `clsa:SimpleCodeListBinding` entails:
> 
> - Each _attribute_ `$attribute` in the instance of the _code list validation set_ with **[attribute declaration]** equal to `$attribute-declaration` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A column/value pair with:
> 		- A column reference of: if `$binding-element` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 		- A data value that is the _normalized value_ of `$attribute`
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.

#### Rule 4-12. Element declaration effective simple binding

> **[Rule 4-12] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> An element `xs:element` defining an _element declaration_ `$element-declaration` with _application information_ of an element `$binding-element` `clsa:SimpleCodeListBinding` entails:
> 
> - Each _element_ `$element` in the instance of the _code list validation set_ with **[element declaration]** that is in the _substitution group_ of `$element-declaration` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A column/value pair with:
> 		- A column reference of: if `$binding-element` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 		- A data value that is the _normalized value_ of `$element`
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.

#### Rule 4-13. Type definition effective simple binding

> **[Rule 4-13] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> An element `xs:simpleType` or `xs:complexType` defining a _type definition_ `$type-definition` with _application information_ of an element `$binding-element` `clsa:SimpleCodeListBinding` entails:
> 
> - Each _attribute_ `$attribute` in the instance of the _code list validation set_ with **[attribute declaration]** with {type definition} _derived_ from `$type-definition` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A column/value pair with:
> 		- A column reference of: if `$binding-element` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 		- A data value that is the _normalized value_ of `$attribute`
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.
> - Each _element_ `$element` in the instance of the _code list validation set_ with **[type definition]** _derived_ from `$type-definition` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A column/value pair with:
> 		- A column reference of: if `$binding-element` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 		- A data value that is the _normalized value_ of `$element`
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.

### Complex binding of schema components

#### Rule 4-14. Element declaration effective complex binding

> **[Rule 4-14] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> An element `xs:element` defining an _element declaration_ `$element-declaration` with _application information_ of an element `$binding-element` `clsa:ComplexCodeListBinding` entails:
> 
> - Each _element_ `$element` in the instance of the _code list validation set_ with **[element declaration]** that is in the _substitution group_ of `$element-declaration` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A set of column/value pairs, containing: For each `clsa:ElementCodeListBinding` child `$element-binding` of `$binding-element`:
> 		- A column/value pair with:
> 			- A column reference of: if `$element-binding` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 			- A data value that is: if it exists, the first element child of `$element` that is in the _substitution group_ of an _element declaration_ with a name that is equal to the value of attribute `elementName` of `$element-binding`, otherwise empty.
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.

#### Rule 4-15. Complex type definition effective complex binding

> **[Rule 4-15] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> An element `xs:complexType` defining a _complex type definition_ `$type-definition` with _application information_ of an element `$binding-element` `clsa:ComplexCodeListBinding` entails:
> 
> - Each _element_ `$element` in the instance of the _code list validation set_ with **[type definition]** _derived_ from `$type-definition` entails a _code list binding_ with:
> 	- A _code list identifier_ that is the _normalized value_ of the attribute `codeListURI` of `$binding-element`.
> 	- A list of column/value pairs, containing: For each `clsa:ElementCodeListBinding` child `$element-binding` of `$binding-element`:
> 		- A column/value pair with:
> 			- A column reference of: if `$element-binding` has attribute `columnName`, then the _normalized value_ of that attribute, else "#code".
> 			- A data value that is: if it exists, the first element child of `$element` that is in the _substitution group_ of an _element declaration_ with a name that is equal to the value of attribute `elementName` of `$element-binding`, otherwise empty.
> 	- A value for `constraining` that is: if `$binding-element` has attribute `constrainingIndicator`, then its value, otherwise `true`.

## Matches for code list bindings

A _code list binding_ defined against a code list document may be matched to zero or more _distinct entries_ within the code list. The process of finding matches for a code list binding `$binding` against a _code list validation set_ is defined by the following rule.

### Rule 4-16. Matches and validity for a code list binding

> **[Rule 4-16] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> A _code list binding_ matching against against a _code list validation set_ yields a set of _distinct entries_ and a validity value (_valid_ or _invalid_).
> 
> The matches for a _code list binding_ `$binding` against a _code list validation set_ MUST be:
> 
> - The _code list identifier_ `$identifier` is provided by the `$binding`.
> - Using the _entity catalog_ defined for the _code list validation set_, _resolve_ _code list identifier_ `$identifier` to a _locally-resolved resource_ `$resource`.
> - If `$resource` is not a _code list document_, or if no resource is identified for `$identifier`, then this specification does not define any matches for `$binding`. The binding is evaluated to be _invalid_. In this case, the code list identified by `$identifier` SHOULD be handled by means other than this specification.
> - If `$resource` is a _code list document_, then the set of matches for `$binding` is the list of distinct entries in the code list for which every column referenced by `$binding` has the corresponding value.
> 	- A column/value pair in `$binding` with a column reference of "#code" matches as specified for the appropriate class of _code list document_ for that _column name_.
> 	- A column/value pair in `$binding` with a column reference of "#range" matches:
> 		- If `$resource` does not contain a column corresponding to the well-known columns "minimum-inclusive", "minimum-exclusive", "maximum-inclusive", or "maximum-exclusive", then the binding has no matches.
> 		- Otherwise, yield all distinct entries for which all of the following are true, given that the value of the column/value pair is `$value`:
> 			- Either there is no _code value_ for column "minimum-inclusive", or the _code value_ of that column is less than or equal to `$value`.
> 			- Either there is no _code value_ for column "minimum-exclusive", or the _code value_ of that column is less than `$value`.
> 			- Either there is no _code value_ for column "maximum-inclusive", or the _code value_ of that column is greater than or equal to `$value`.
> 			- Either there is no _code value_ for column "maximum-exclusive", or the _code value_ of that column is greater than `$value`.
> - If the binding has no matches, then:
> 	- If the binding is constraining, then it is invalid.
> 	- If the binding is not constraining, then it is valid.
> - If the binding has one or more matches, then it is valid.

The above rule specifies that code list identifiers are to be resolved to _locally-resolved resources_, which are in the _local context_ of the entity catalog. This specification **does not** specify that code list identifiers should be resolved by network fetches of code list resources. Code list identifiers are meant to be treated as identifiers, as names, and not as network locations of resources.

A code list binding that is used to connect a value to a service or other code list methodology that does not use _code list documents_ will result in invalid matches. This is as designed; matches for services or other methodologies should be determined by a method other than this rule.

### Rule 4-17. Value comparisons based on types
[Rule 4-16, _Matches and validity for a code list binding_ (VSET), above,](#rule-4-16-matches-and-validity-for-a-code-list-binding) requires values from an XML document to be compared to values from code lists. Whether values match, and how they compare, is dependent on what kind of data those values are. For example, text values and string values are compared using different methods. This rule establishes that typing of comparisons is based on the types of the values.

[XPathFunctions](#Appendix-A-References) [Section 17, _Casting_](https://www.w3.org/TR/xpath-functions/#casting) provides a set of rules for type casting among XML Schema primitive types.

> **[Rule 4-17] (<a href="#conformance_target_VSET">VSET</a>) (Interpretation)**
> Comparisons between a value `$instance-value` of a column/value pair and a code value `$code-value` MUST be conducted as follows:
> 
> 1.  `$instance-value` has a data type, `$instance-data-type`, provided by its XML Schema definition.
> 2.  `$code-value` has a data type, `$code-data-type`, as provided by its code list document as specified for its class of code list document. That data type is either a data type defined by the XML Schema definition language, or is empty.
> 3.  A data type, `$comparison-data-type`, is calculated as:
> 	-   If `$code-data-type` is empty, then `$instance-date-type`.
> 	-   If it exists, the lowest common ancestor of the two data types.
> 	-   Otherwise, `xs:string`.
> 4.  `$instance-value` and `$code-value` are cast to `$comparison-data-type`, in accordance with [[XPathFunctions]](https://reference.niem.gov/niem/specification/code-lists/4.0/niem-code-lists-4.0.html#XPathFunctions) [Section 17, _Casting_](https://www.w3.org/TR/xpath-functions/#casting).
> 5.  Equality comparisons are conducted as appropriate for `$comparison-data-type`.
> 6.  Inequality comparisons (e.g., less than, greater than) for ranges are conducted as appropriate for lowest atomic base type of `$comparison-data-type`.

### Rule 4-18. Code list identified by candidate code list identifiers
Each class of code list document specifies how its instances define code list identifiers that may refer to a code list. This rule ensures that code lists are referred to via the correct code list identifier, when it is defined.

> **[Rule 4-18] (<a href="#conformance_target_VSET">VSET</a>) (Constraint)**
> When a _code list document_ defines candidate _code list identifiers_, a _code list identifier_ against which a _code list document_ _resource_ is _resolved_ MUST be a candidate code list identifier for that code list document.

# Comma-separated values (CSV) code lists

This document provides for the use of a _CSV file_ as an implementation of a _code list document_. This section lays out the rules for using CSV files as code list documents. The definitions of CSV structural terms are provided by [RFC4180](#Appendix-A-References), as noted in [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_, above](#rfc-4180:-comma-separated-values-(csv)-files).

## Rule 5-1. CSV code list document is a CSV file

> **[Rule 5-1] (<a href="#conformance_target_CSV-CLD">CSV-CLD</a>) (Constraint)**
> A _CSV code list document_ MUST be a _CSV file_.

## Rule 5-2. CSV code list document has header

> **[Rule 5-2] (<a href="#conformance_target_CSV-CLD">CSV-CLD</a>) (Constraint)**
> A _CSV code list document_ MUST have a _CSV header_.

## Rule 5-3. CSV column name is not empty

> **[Rule 5-3] (<a href="#conformance_target_CSV-CLD">CSV-CLD</a>) (Constraint)**
> A _CSV column name_ of a _CSV code list document_ MUST not be empty.

## Rule 5-4. CSV file as a code list document

> **[Rule 5-4] (<a href="#conformance_target_CSV-CLD">CSV-CLD</a>) (Interpretation)**
> A _CSV file_ may act as a _CSV code list document_ in the following manner:
> 
> 1.   _Code list identifiers_: The CSV file does not specify its code list identifiers. Each CSV file contains a single _code list_. The CSV file MAY be resolved to any _code list identifier_.
> 2.  _Distinct entries_: Each _CSV record_ of the _CSV file_ constitutes a distinct entry.
> 3.  _Code values_: Each _CSV field_ corresponds to a code value.
> 4.  _Column names_: The column name of a _code value_ is the _CSV column name_ corresponding by position within the _CSV header_ to the position of the _CSV field_ within its _CSV record_
> 5.  A _column_ in a _CSV file_ is a well-known column when its _CSV column name_ is the same as the _column name_ of a well-known column.
> 6.  A reference to _column_ #code is matched, in order, to:
>     -   a column with _CSV column name_ of code, or
>     -   the first _column_ of the _CSV file_.
> 7.  A _code value_ in a _CSV file_ has no type; its data type is empty.

# Genericode code lists

This document incorporates a Genericode document as an implementation of a _code list document_. This section lays out rules for Genericode documents and their use as code list documents.

## Rule 6-1. Genericode code list document defined by Genericode

> **[Rule 6-1] (<a href="#conformance_target_GC-CLD">GC-CLD</a>) (Constraint)**
> A _Genericode code list document_ MUST be a Genericode code list document as defined by [Genericode](#Appendix-A-References) [Section 3.2, _Genericode Document Types_](http://docs.oasis-open.org/codelist/cs-genericode-1.0/doc/oasis-code-list-representation-genericode.html#_Toc190622791), which states:
> 
>> A Genericode code list document has the root element `<gc:CodeList>`. It contains metadata describing the code list as a whole, as well as explicit code list data — codes and associated values.

## Rule 6-2. Document with conformance target is Genericode code list document

> **[Rule 6-2] (<a href="#conformance_target_VSET">VSET</a>) (Constraint)**
> A _resource_ with an _effective conformance target identifier_ of `http://reference.niem.gov/niem/specification/code-lists/4.0/#GenericodeCodeListDocument` MUST be a _Genericode code list document_.

## Rule 6-3. Genericode code list document is schema-valid

> **[Rule 6-3] (<a href="#conformance_target_GC-CLD">GC-CLD</a>) (Constraint)**
> A _Genericode code list document_ MUST be _schema-valid_ against the schema document for the Genericode namespace as provided at <a class="url" target="_blank" href="http://docs.oasis-open.org/codelist/ns/genericode/1.0/">http://docs.oasis-open.org/codelist/ns/genericode/1.0/</a>.

## Rule 6-4. XML Schema alternate datatypes are treated the same as built in datatypes

[XMLSchema2](#Appendix-A-References) defines an alternate namespace name as an alias that may be used to refer to simple datatypes it defines. [XMLSchema2](#Appendix-A-References) [Section 3.1, _Namespace considerations_](http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/#namespaces) states:

> To facilitate usage in specifications other than the XML Schema definition language, such as those that do not want to know anything about aspects of the XML Schema definition language other than the datatypes, each ·built-in· datatype is also defined in the namespace whose URI is:
> 
> - http://www.w3.org/2001/XMLSchema-datatypes
> 
> This applies to both ·built-in· ·primitive· and ·built-in· ·derived· datatypes.

[Genericode](#Appendix-A-References) uses this alternate namespace name as a default for the datatype library in Genericode documents, referring to it as "the URI for W3C XML Schema datatypes". As this separate namespace is not expressing a semantic distinction, and in order to keep Genericode documents simple, this document specifies that the alternate namespace name is to be treated as if it was the namespace name for the XML Schema definition language.

> **[Rule 6-4] (<a href="#conformance_target_GC-CLD">GC-CLD</a>) (Interpretation)**
> A datatype with a namespace name of `http://www.w3.org/2001/XMLSchema-datatypes` MUST be evaluated as if it had a namespace name of `http://www.w3.org/2001/XMLSchema`.

## Rule 6-5. Genericode file as a code list document

> **[Rule 6-5] (<a href="#conformance_target_GC-CLD">GC-CLD</a>) (Interpretation)**
> A _Genericode code list document_ may act as a _code list document_ in the following manner:

1.  _Code list identifier_: Candidate code list identifiers for the document are the values for `CanonicalUri`, `CanonicalVersionUri`, and `LocationUri` defined by the Genericode document for the code list.
2.  _Distinct entries_: Each row of the Genericode code list document constitutes a distinct entry.
3.  _Code values_: Each `Value` element of the Genericode code list document corresponds to a code value.
4.  _Column names_: The columns are as defined by Genericode; the _column name_ of a column is the value of attribute `Id` of that column.
5.  A column in a _Genericode code list document_ is a well-known column when its value for `CanonicalUri` or `CanonicalVersionUri` corresponds to the _code list identifier_ specified for that well-known column.
6.  A reference to _column_ \#code is matched, in order, to:
    -   a column corresponding to well-known column code,
    -   a column with _column name_ code,
    -   the column in the first single-column key for the code list, or
    -   the first column in the code list.
7.  A _code value_ in a Genericode file has a type as specified by the data definition of its column. If the `Type` attribute references an element declaration, then the type is the type of that element. If a `Parameter`, which introduces `gc:DatatypeFacet`, is used, then the type is treated as an anonymous type derived from the type of the column. A value for which no data type is specified has an empty data type.

# Well-known columns and references

This specification defines _column identifiers_ and _column names_ for several columns that have well-understood semantics. These identifiers and names may be used to define columns in _code list documents_ that implement these semantics. These values may be used different ways in different contexts:

- The **column identifier** is an _absolute URI_ that a column in a code list document may use to identify a column as being a well-known column. A _Genericode code list document_ will use this URI as a `CanonicalUri` value to indicate that a column is a well-known column.
- The **column name** is a string that may be used by a column in a code list document to identify the column as a well-known column. A _CSV code list document_ will use this name as a _column name_ to indicate that a column is a well-known column.

In addition to well-known columns, this specification defines well-known column references. A well-known column reference is used in _code list bindings_. The well-known column references defined by this specification are:

- "**#code**": A binding will use the column name "#code" to refer to a default code value in a code list. Each class of _code list document_ defines how a reference to "#code" is resolved (q.v. [Rule 5-4, _CSV file as a code list document_ (CSV-CLD), above,](#rule-5-4-csv-file-as-a-code-list-document) and [Rule 6-5, _Genericode file as a code list document_ (GC-CLD), above](#rule-6-5-genericode-file-as-a-code-list-document)). A binding that doesn't specify a column name will default to column name "#code".
- "**#range**": A binding will use the column name "#range" to match into a range of values, as described by [Section 7.5, _Columns supporting ranges of values_, below](#columns-supporting-ranges-of-values).

## Column: "code"

_Column name_: code

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/code`

Description: A "code" column carries a value that stands for some other value or meaning, or acts as an enumeration. A code value may be a single-column key within its code list, to uniquely identify some distinct entry.

## Column: "definition"

_Column name_: definition

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/definition`

Description: A "definition" column carries a human-readable meaning of a _distinct entry_. This is analogous to the data definition of an enumerated code in a simple type in a NIEM schema.

## Column: "subclass-of"

_Column name_: subclass-of

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/subclass-of`

Description: A "subclass-of" column indicates that a given distinct entry is a subclass of some other distinct entry. It is a key reference within its code list, referring to a distinct entry having the indicated value for its default code column.

## Column: "uri"

_Column name_: uri

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/uri`

Description: A "uri" column provides a uniform resource identifier for a distinct entry.

## Columns supporting ranges of values

This specification establishes a set of columns that support code tables that describe ranges of values. This enables code lists to be used that map between sets of values. One use for this is to enable translation between continuous numeric values and discrete enumerated values. Another use is to support fixed-point integer values used to represent more meaningful numeric values. For example, fixed-length bit field values can be mapped to elevation in meters.

In _Table 7-1, _Example code list: directions_, below_, a direction value in degrees is mapped to enumerated values for the cardinal and ordinal directions. This code list establishes the ranges using the columns "minimum-inclusive" and "maximum-exclusive". Each distinct entry contains a "direction" column, identifying to what direction the range is mapped. A _Genericode code list document_ expressing this code list would define columns with `CanonicalUri` matching the _column identifiers_ for "minimum-inclusive" and "maximum-exclusive". A _CSV code list document_ would define columns named "minimum-inclusive" and "maximum-exclusive".

### Table 7-1: Example code list: directions

| minimum-inclusive | maximum-exclusive | direction |
| ----------------- | ----------------- | --------- |
| 0                 | 22.5              | north     |
| 22.5              | 67.5              | northeast |
| 67.5              | 112.5             | east      |
| 112.5             | 157.5             | southeast |
| 157.5             | 202.5             | south     |
| 202.5             | 247.5             | southwest |
| 247.5             | 292.5             | west      |
| 292.5             | 337.5             | northwest |
| 337.5             | 360               | north     |

A code list binding that refers to range columns uses the _column name_ "#range". For example, _Figure 7-1, _Instance referencing range columns_, below,_ uses a run-time binding. It identifies the code list with attribute `cli:codeListURI`. It refers to range columns with attribute `cli:codeListColumnName` set to "#range".

## Figure 7-1: Instance referencing range columns

```xml
<m:Position
  xmlns:cli="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
  xmlns:ext="http://example.org/code-lists/example/directions/extension"
  xmlns:m="http://release.niem.gov/niem/domains/maritime/4.0/"
  xmlns:nc="http://release.niem.gov/niem/niem-core/4.0/">
 <m:PositionHeadingMeasure>
   <ext:DegreeAngleValue
      cli:codeListURI="http://example.org/code-lists/example/directions/code-list/1"
      cli:codeListColumnName="#range">122.31</ext:DegreeAngleValue>
   <ext:AngleUnitText>deg</ext:AngleUnitText>
 </m:PositionHeadingMeasure>
</m:Position>

```

Matching into _Table 7-1, _Example code list: directions_, above,_ would yield the _distinct entry_ for "southeast", since it is the sole entry with a minimum-inclusive value (112.5) that is less than or equal to 122.31, and a maximum-exclusive value (157.5) that is greater than 122.31.

### Column: "minimum-inclusive"

_Column name_: minimum-inclusive

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/minimum-inclusive`

Description: A value that is an _inclusive lower bound_ of a range.

### Column: "minimum-exclusive"

_Column name_: minimum-exclusive

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/minimum-exclusive`

Description: A value that is an _exclusive lower bound_ of a range.

### Column: "maximum-inclusive"

_Column name_: maximum-inclusive

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/maximum-inclusive`

Description: A value that is an _inclusive upper bound_ of a range.

### Column: "maximum-exclusive"

_Column name_: maximum-exclusive

_Column identifier_: `http://reference.niem.gov/niem/specification/code-lists/4.0/column/maximum-exclusive`

Description: A value that is an _exclusive upper bound_ of a range.

## Code list example using well-known columns

The following examples show well-known columns being reused in a code list. A single code list is presented as an abstract table, corresponding CSV, and portions of corresponding Genericode. First, _Table 7-2, _Use of columns in a code list_, below,_ is a tabular representation.

### Table 7-2: Use of columns in a code list

| code               | definition | uri                                                             |
| ------------------ | ---------- | --------------------------------------------------------------- |
| application/json   | json       | https://www.iana.org/assignments/media-types/application/json   |
| application/msword | doc        | https://www.iana.org/assignments/media-types/application/msword |
| application/pdf    | pdf        | https://www.iana.org/assignments/media-types/application/pdf    |

In this table, we see the well-known columns "code", "definition", and "uri" being used. The next three rows represent the _distinct entries_ of the code list, with a _code value_ for each _column_.

_Figure 7-2, _Definition of columns in Genericode_, below,_ shows a CSV file corresponding to the abstract table. In this version, the columns are identifiable as well-known columns because each _CSV column name_ is a _column name_ of a well-known column defined above.

## Figure 7-2: Definition of columns in Genericode

```
code,definition,uri
application/json,json,https://www.iana.org/assignments/media-types/application/json
application/msword,doc,https://www.iana.org/assignments/media-types/application/msword
application/pdf,pdf,https://www.iana.org/assignments/media-types/application/pdf
```
For the above code list, Genericode in _Figure 7-3, _Definition of columns in Genericode_, below,_ defines columns that reuse the well-known columns. Each column is identifiable as a well-known column because its `CanonicalUri` value is a _column identifier_ of a well-known column.

## Figure 7-3: Definition of columns in Genericode

```xml
<Column Id="code" Use="required">
 <ShortName>code</ShortName>
 <CanonicalUri>http://reference.niem.gov/niem/specification/code-lists/4.0/column/code</CanonicalUri>
 <Data Type="normalizedString" Lang="en"/>
</Column>
<Column Id="definition" Use="optional">
 <ShortName>definition</ShortName>
 <CanonicalUri>http://reference.niem.gov/niem/specification/code-lists/4.0/column/definition</CanonicalUri>
 <Data Type="normalizedString" Lang="en"/>
</Column>
<Column Id="uri" Use="optional">
 <ShortName>uri</ShortName>
 <CanonicalUri>http://reference.niem.gov/niem/specification/code-lists/4.0/column/uri</CanonicalUri>
 <Data Type="anyURI" Lang="en"/>
</Column>
```
_Figure 7-4, _Distinct entries in Genericode_, below,_ contains distinct entries for the code lists, in the form of Genericode rows. These rows contain the same data as the other code list representations above.

## Figure 7-4: Distinct entries in Genericode

```xml
<Row>
 <Value ColumnRef="code">
   <SimpleValue>application/json</SimpleValue>
 </Value>
 <Value ColumnRef="definition">
   <SimpleValue>json</SimpleValue>
 </Value>
 <Value ColumnRef="uri">
   <SimpleValue>https://www.iana.org/assignments/media-types/application/json</SimpleValue>
 </Value>
</Row>
<Row>
 <Value ColumnRef="code">
   <SimpleValue>application/msword</SimpleValue>
 </Value>
 <Value ColumnRef="definition">
   <SimpleValue>doc</SimpleValue>
 </Value>
 <Value ColumnRef="uri">
   <SimpleValue>https://www.iana.org/assignments/media-types/application/msword</SimpleValue>
 </Value>
</Row>
<Row>
 <Value ColumnRef="code">
   <SimpleValue>application/pdf</SimpleValue>
 </Value>
 <Value ColumnRef="definition">
   <SimpleValue>pdf</SimpleValue>
 </Value>
 <Value ColumnRef="uri">
   <SimpleValue>https://www.iana.org/assignments/media-types/application/pdf</SimpleValue>
 </Value>
</Row>
```

# Appendix A. References

<p class="hang">[CTAS]: Roberts, Webb. "NIEM Conformance Targets Attribute Specification, Version 3.0." NIEM Technical Architecture Committee, July 31, 2014. <a class="url" target="_blank" href="http://reference.niem.gov/niem/specification/conformance-targets-attribute/3.0/NIEM-CTAS-3.0-2014-07-31.html">http://reference.niem.gov/niem/specification/conformance-targets-attribute/3.0/NIEM-CTAS-3.0-2014-07-31.html</a>.

<p class="hang">[Genericode]: Anthony B. Coates, ed. "Code List Representation (Genericode) Version 1.0, Committee Specification 02." OASIS, April 6, 2022. <a class="url" target="_blank" href="https://docs.oasis-open.org/codelist/genericode/v1.0/genericode-v1.0.html">https://docs.oasis-open.org/codelist/genericode/v1.0/genericode-v1.0.html</a>.

<p class="hang">[NIEM NDR]: Roberts, Webb. "National Information Exchange Model Naming and Design Rules, Version 5.0." NIEM Technical Architecture Committee, December 18, 2020. <a class="url" target="_blank" href="http://reference.niem.gov/niem/specification/naming-and-design-rules/5.0/niem-ndr-5.0.html">http://reference.niem.gov/niem/specification/naming-and-design-rules/5.0/niem-ndr-5.0.html</a>.

<p class="hang">[RFC2119]: Bradner, S. (1997, March). _Key words for use in RFCs to Indicate Requirement Levels_. Internet Engineering Task Force. Retrieved from <a class="url" target="_blank" href="http://www.ietf.org/rfc/rfc2119.txt">http://www.ietf.org/rfc/rfc2119.txt</a>

<p class="hang">[RFC3986]: Berners-Lee, T., Fielding, R., and L. Masinter, "Uniform Resource Identifier (URI): Generic Syntax", STD 66, RFC 3986, DOI 10.17487/RFC3986, January 2005, <a class="url" target="_blank" href="http://www.rfc-editor.org/info/rfc3986">http://www.rfc-editor.org/info/rfc3986</a>.

<p class="hang">[RFC4180]: Shafranovich, Y. "Common Format and MIME Type for Comma-Separated Values (CSV) Files, RFC 4180." IETF Network Working Group, October 2005. <a class="url" target="_blank" href="http://www.ietf.org/rfc/rfc4180.txt">http://www.ietf.org/rfc/rfc4180.txt</a>. 

<p class="hang">[XPathFunctions]: Malhotra, Ashok, Jim Melton, Norman Walsh, and Michael Kay. "XQuery 1.0 and XPath 2.0 Functions and Operators (Second Edition)." W3C, December 14, 2010. <a class="url" target="_blank" href="https://www.w3.org/TR/xpath-functions/">https://www.w3.org/TR/xpath-functions/</a>.

<p class="hang">[XML]: Bray, T., Paoli, J., Sperberg-McQueen, C. M., Maler, E., &amp; Yergeau, F. (2008, November 26). _Extensible Markup Language (XML) 1.0 (Fifth Edition)_. The World Wide Web Consortium (W3C). Retrieved from <a class="url" target="_blank" href="http://www.w3.org/TR/2008/REC-xml-20081126/">http://www.w3.org/TR/2008/REC-xml-20081126/</a>

<p class="hang">[XML Catalogs]: Walsh, Norman. "XML Catalogs—OASIS Standard V1.1, 7 October 2005." OASIS Open, Inc., October 7, 2005. <a class="url" target="_blank" href="https://www.oasis-open.org/committees/download.php/14809/std-entity-xml-catalogs-1.1.html">https://www.oasis-open.org/committees/download.php/14809/std-entity-xml-catalogs-1.1.html</a>.

<p class="hang">[XML Infoset]: Cowan, John, and Richard Tobin. "XML Information Set (Second Edition)", 4 February 2004. <a class="url" target="_blank" href="http://www.w3.org/TR/2004/REC-xml-infoset-20040204/">http://www.w3.org/TR/2004/REC-xml-infoset-20040204/</a>.

<p class="hang">[XMLNamespaces]: Bray, T., Hollander, D., Layman, A., Tobin, R., &amp; Thompson, H. S. (2009, December 8). _Namespaces in XML 1.0 (Third Edition)_. W3C. Retrieved from <a class="url" target="_blank" href="http://www.w3.org/TR/2009/REC-xml-names-20091208/">http://www.w3.org/TR/2009/REC-xml-names-20091208/</a>

<p class="hang">[XMLSchema1]: Thompson, H. S., Beech, D., Maloney, M., &amp; Mendelsohn, N. (2004, October 28). _XML Schema Part 1: Structures Second Edition_. Retrieved from <a class="url" target="_blank" href="http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/">http://www.w3.org/TR/2004/REC-xmlschema-1-20041028/</a>.

<p class="hang">[XMLSchema2]: Biron, Paul V., and Ashok Malhotra. "XML Schema Part 2: Datatypes Second Edition," October 28, 2004. <a class="url" target="_blank" href="http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/">http://www.w3.org/TR/2004/REC-xmlschema-2-20041028/</a>.

# Appendix B. XML Schema document for the code lists instance namespace

The following XML Schema document defines the _code lists instance namespace_, a namespace for binding the content of XML documents to code lists at run time. This vocabulary may be incorporated into exchange specifications, and is used in exchanged XML documents to express code list bindings at run time. This schema document conforms to NIEM 3 and NIEM 4, and may be integrated into either NIEM 3 or NIEM 4-conformant schema sets.

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<xs:schema
   ct:conformanceTargets="http://reference.niem.gov/niem/specification/naming-and-design-rules/4.0/#ReferenceSchemaDocument http://reference.niem.gov/niem/specification/naming-and-design-rules/3.0/#ReferenceSchemaDocument"
   targetNamespace="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
   version="4.0"
   xmlns:ct="http://release.niem.gov/niem/conformanceTargets/3.0/"
   xmlns:xs="http://www.w3.org/2001/XMLSchema">

 <xs:annotation>
   <xs:documentation>Definitions for the use of the NIEM Code Lists Specification, version 4.0, in XML message instances.</xs:documentation>
 </xs:annotation>

 <xs:attribute name="codeListURI" type="xs:anyURI">
   <xs:annotation>
     <xs:documentation>A universal identifier for a code list.</xs:documentation>
   </xs:annotation>
 </xs:attribute>

 <xs:attribute name="codeListColumnName" type="xs:string">
   <xs:annotation>
     <xs:documentation>A local name for a code list column within a code list.</xs:documentation>
   </xs:annotation>
 </xs:attribute>

 <xs:attribute name="codeListConstrainingIndicator" type="xs:boolean">
   <xs:annotation>
     <xs:documentation>True when a code list binding constrains the validity of a code list value, false otherwise.</xs:documentation>
   </xs:annotation>
 </xs:attribute>

</xs:schema>

```

# Appendix C. XML Schema document for the code list schema appinfo namespace

The following XML Schema document defines the _code lists schema appinfo namespace_, a namespace for annotating XML Schema component definitions. These annotations connect XML components to code lists at schema development time.

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<xs:schema 
  targetNamespace="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-schema-appinfo/"
  version="4.0"
  xmlns:clsa="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-schema-appinfo/"
  xmlns:xs="http://www.w3.org/2001/XMLSchema">

 <xs:annotation>
   <xs:documentation>This schema provides annotations for connecting content defined within an XML Schema document to the content of code lists.</xs:documentation>
 </xs:annotation>

 <xs:element name="SimpleCodeListBinding">
   <xs:annotation>
     <xs:documentation>An element for connecting simple content defined by an XML Schema component to a a column of a code list.</xs:documentation>
   </xs:annotation>
   <xs:complexType>
     <xs:attribute name="codeListURI" type="xs:anyURI" use="required">
       <xs:annotation>
         <xs:documentation>A universal identifier for a code list.</xs:documentation>
       </xs:annotation>
     </xs:attribute>
     <xs:attribute name="columnName" type="xs:string" use="optional">
       <xs:annotation>
         <xs:documentation>A local name for a code list column within a code list.</xs:documentation>
       </xs:annotation>
     </xs:attribute>
     <xs:attribute name="constrainingIndicator" type="xs:boolean" use="optional">
       <xs:annotation>
         <xs:documentation>True when a code list binding constrains the validity of a code list value, false otherwise.</xs:documentation>
       </xs:annotation>
     </xs:attribute>
   </xs:complexType>
 </xs:element>

 <xs:element name="ComplexCodeListBinding">
   <xs:annotation>
     <xs:documentation>An element for connecting complex content defined by an XML Schema component to a set of columns of a code list.</xs:documentation>
   </xs:annotation>
   <xs:complexType>
     <xs:sequence>
       <xs:element name="ElementCodeListBinding" form="qualified" maxOccurs="unbounded">
         <xs:complexType>
           <xs:attribute name="elementName" type="xs:QName" use="required">
             <xs:annotation>
               <xs:documentation>A qualified name of an XML element.</xs:documentation>
             </xs:annotation>
           </xs:attribute>
           <xs:attribute name="columnName" type="xs:string" use="optional">
             <xs:annotation>
               <xs:documentation>A local name for a code list column within a code list.</xs:documentation>
             </xs:annotation>
           </xs:attribute>
         </xs:complexType>
       </xs:element>
     </xs:sequence>
     <xs:attribute name="codeListURI" type="xs:anyURI" use="required">
       <xs:annotation>
         <xs:documentation>A universal identifier for a code list.</xs:documentation>
       </xs:annotation>
     </xs:attribute>
     <xs:attribute name="constrainingIndicator" type="xs:boolean" use="optional">
       <xs:annotation>
         <xs:documentation>True when a code list binding constrains the validity of a code list value, false otherwise.</xs:documentation>
       </xs:annotation>
     </xs:attribute>
   </xs:complexType>
 </xs:element>

</xs:schema>

```

# Appendix D. Example documents: Make–Model example

This section contains a single code list, with instances and supporting schemas for both run-time binding and schema-time binding:

A code list provides makes and models of vehicles.

- [Appendix D.1, _Vehicle make and model code list_, below,](#appendix-d1-vehicle-make-and-model-code-list) shows the code list as a table.
- [Appendix D.2, _Make–Model code list CSV file_, below,](#appendix-d2-make–model-code-list-csv-file) shows the code list as comma-separated values (CSV).
- [Appendix D.3, _Make–Model code list Genericode file_, below,](#appendix-d3-make–model-code-list-genericode-file) shows the code list rendered into Genericode.

The code list is used in XML exchanges. There are two methods provided by this specification for binding XML document content (messages) to code lists: schema-time binding through XML Schema appinfo annotations, and run-time binding through the `cli:codeListURI` attribute. The first example shows the code list bound to the message at schema time:

- [Appendix D.4, _XML instance with schema-time code list binding_, below,](#appendix-d4-xml-instance-with-schema-time-code-list-binding) shows the XML instance that relies on schema-time binding.
- [Appendix D.5, _Extension schema with schema-time code list binding_, below,](#appendix-d5-extension-schema-with-schema-time-code-list-binding) shows an extension schema that defines new components, and which binds the XML message to the code list via schema annotations.
- [Appendix D.6, _XML catalog for schema-time code list binding_, below,](#appendix-d6-xml-catalog-for-schema-time-code-list-binding) shows an XML catalog that directs assembly of the XML Schema, and which resolves the _code list identifier_ to the Genericode file for the code list.

The second example shows the code list bound to the XML data through run-time binding, using the `cli:codeListURI` attribute.

- [Appendix D.7, _XML instance with run-time code list binding_, below,](#appendix-d7-xml-instance-with-run-time-code-list-binding) shows the XML instance with run-time binding.
- [Appendix D.8, _Extension schema with run-time code list binding_, below,](#appendix-d8-extension-schema-with-run-time-code-list-binding) shows an extension schema that defines new components that provide for run-time reference to the code list.
- [Appendix D.9, _XML catalog for run-time code list binding_, below,](#appendix-d9-xml-catalog-for-run-time-code-list-binding) shows an XML catalog that directs assembly of the XML Schema and resolves the location of the Genericode file for the code list.

## Appendix D.1. Vehicle make and model code list

### Table D-1: Vehicle make and model code list

| Make code | Make description | Model code | Model description | Class  |
| --------- | ---------------- | ---------- | ----------------- | ------ |
| FORD      | Ford             | FUS        | Fusion            | Auto   |
| HOND      | Honda            | CIV        | Civic             | Auto   |
| HOND      | Honda            | CRV        | CRV               | SUV    |
| DODG      | Dodge            | R15        | Ram 1500          | Pickup |
| NISS      | Nissan           | ALT        | Altima            | Auto   |
| FORD      | Ford             | F15        | F-150             | Pickup |
| TOYT      | Toyota           | COA        | Corolla           | Auto   |
| FORD      | Ford             | 500        | Five Hundred      | Auto   |
| HOND      | Honda            | ACC        | Accord            | Auto   |
| TOYT      | Toyota           | CAM        | Camry             | Auto   |
| CHEV      | Chevrolet        | SLV        | Silverado         | Pickup |
| MERZ      | Mercedes-Benz    | 500        | 500 Series        | Auto   |

## Appendix D.2. Make–Model code list CSV file

```
Make code,Make description,Model code,Model description,Class
FORD,Ford,FUS,Fusion,Auto
HOND,Honda,CIV,Civic,Auto
HOND,Honda,CRV,CRV,SUV
DODG,Dodge,R15,Ram 1500,Pickup
NISS,Nissan,ALT,Altima,Auto
FORD,Ford,F15,F-150,Pickup
TOYT,Toyota,COA,Corolla,Auto
FORD,Ford,500,Five Hundred,Auto
HOND,Honda,ACC,Accord,Auto
TOYT,Toyota,CAM,Camry,Auto
CHEV,Chevrolet,SLV,Silverado,Pickup
MERZ,Mercedes-Benz,500,500 Series,Auto
```

## Appendix D.3. Make–Model code list Genericode file

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<gc:CodeList xmlns:ct="http://release.niem.gov/niem/conformanceTargets/3.0/"
            xmlns:gc="http://docs.oasis-open.org/codelist/ns/genericode/1.0/"
            xmlns:gca="http://example.org/namespace/genericode-appinfo">
  <Annotation>
     <AppInfo>
        <gca:ConformanceTargets ct:conformanceTargets="http://reference.niem.gov/niem/specification/code-lists/4.0/#GenericodeCodeListDocument"/>
     </AppInfo>
 </Annotation>
  <Identification>
     <ShortName>VMA</ShortName>
     <Version>1</Version>
     <CanonicalUri>http://example.org/code-list/vehicle-make-model</CanonicalUri>
     <CanonicalVersionUri>http://example.org/code-list/vehicle-make-model/2013-03-05</CanonicalVersionUri>
  </Identification>
  <ColumnSet>
     <Column Id="make" Use="required">
        <ShortName>Make-code</ShortName>
        <Data Type="token"/>
     </Column>
     <Column Id="make-descr" Use="required">
        <ShortName>Make-description</ShortName>
        <Data Type="string"/>
     </Column>
     <Column Id="model" Use="required">
        <ShortName>Model-code</ShortName>
        <Data Type="token"/>
     </Column>
     <Column Id="model-descr" Use="required">
        <ShortName>Model-description</ShortName>
        <Data Type="string"/>
     </Column>
     <Column Id="class" Use="required">
        <ShortName>Class</ShortName>
        <Data Type="token"/>
     </Column>
     <Key Id="key-make-model">
        <ShortName>Key</ShortName>
        <ColumnRef Ref="make"/>
        <ColumnRef Ref="model"/>
     </Key>
  </ColumnSet>
  <SimpleCodeList>
     <Row>
        <Value>
           <SimpleValue>FORD</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Ford</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>FUS</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Fusion</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>HOND</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Honda</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>CIV</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Civic</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>HOND</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Honda</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>CRV</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>CRV</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>SUV</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>DODG</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Dodge</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>R15</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Ram 1500</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Pickup</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>NISS</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Nissan</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>ALT</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Altima</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>FORD</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Ford</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>F15</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>F-150</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Pickup</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>TOYT</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Toyota</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>COA</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Corolla</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>FORD</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Ford</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>500</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Five Hundred</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>HOND</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Honda</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>ACC</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Accord</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>TOYT</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Toyota</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>CAM</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Camry</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>CHEV</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Chevrolet</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>SLV</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Silverado</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Pickup</SimpleValue>
        </Value>
     </Row>
     <Row>
        <Value>
           <SimpleValue>MERZ</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Mercedes-Benz</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>500</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>500 Series</SimpleValue>
        </Value>
        <Value>
           <SimpleValue>Auto</SimpleValue>
        </Value>
     </Row>
  </SimpleCodeList>
</gc:CodeList>

```

## Appendix D.4. XML instance with schema-time code list binding

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<ext:Vehicle xmlns:ext="http://example.org/namespace/extension-schema-time">
 <ext:VehicleMakeCode>DODG</ext:VehicleMakeCode>
 <ext:VehicleModelCode>R15</ext:VehicleModelCode>
</ext:Vehicle>

```

## Appendix D.5. Extension schema with schema-time code list binding

```xml
<?xml version="1.0" encoding="us-ascii"?>
<xs:schema
  ct:conformanceTargets="
    http://reference.niem.gov/niem/specification/naming-and-design-rules/4.0/#ReferenceSchemaDocument
    http://reference.niem.gov/niem/specification/code-lists/4.0/#SchemaDocument"
  targetNamespace="http://example.org/namespace/extension-schema-time"
  version="1"
  xmlns:clsa="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-schema-appinfo/"
  xmlns:ct="http://release.niem.gov/niem/conformanceTargets/3.0/"
  xmlns:ext="http://example.org/namespace/extension-schema-time"
  xmlns:nc="http://release.niem.gov/niem/niem-core/4.0/"
  xmlns:niem-xs="http://release.niem.gov/niem/proxy/xsd/4.0/"
  xmlns:xs="http://www.w3.org/2001/XMLSchema">

 <xs:annotation>
   <xs:documentation>An extension schema for vehicle make and model values, showing schema-time binding of XML content to a code list.</xs:documentation>
 </xs:annotation>

 <xs:import namespace="http://release.niem.gov/niem/niem-core/4.0/"/>
 <xs:import namespace="http://release.niem.gov/niem/proxy/xsd/4.0/"/>

 <xs:element name="Vehicle" type="nc:VehicleType"
             substitutionGroup="nc:Vehicle">
   <xs:annotation>
     <xs:appinfo>
       <clsa:ComplexCodeListBinding
           codeListURI="http://example.org/code-list/vehicle-make-model">
         <clsa:ElementCodeListBinding elementName="ext:VehicleMakeCode"
                                      columnName="make"/>
         <clsa:ElementCodeListBinding elementName="ext:VehicleModelCode"
                                      columnName="model"/>
       </clsa:ComplexCodeListBinding>
     </xs:appinfo>
   </xs:annotation>
 </xs:element>

 <xs:element name="VehicleMakeCode" type="niem-xs:token"
             substitutionGroup="nc:VehicleMakeAbstract">
   <xs:annotation>
     <xs:documentation>A code for a manufacturer of a vehicle.</xs:documentation>
     <xs:appinfo>
       <clsa:SimpleCodeListBinding
           codeListURI="http://example.org/code-list/vehicle-make-model"
           columnName="make"/>
     </xs:appinfo>
   </xs:annotation>
 </xs:element>

 <xs:element name="VehicleModelCode" type="niem-xs:token"
             substitutionGroup="nc:VehicleModelAbstract">
   <xs:annotation>
     <xs:documentation>A code for a model of a vehicle.</xs:documentation>
     <xs:appinfo>
       <clsa:SimpleCodeListBinding
           codeListURI="http://example.org/code-list/vehicle-make-model"
           columnName="model"/>
     </xs:appinfo>
   </xs:annotation>
 </xs:element>

</xs:schema>

```

## Appendix D.6. XML catalog for schema-time code list binding

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<!DOCTYPE catalog PUBLIC "-//OASIS//DTD Entity Resolution XML Catalog V1.0//EN" "http://www.oasis-open.org/committees/entity/release/1.0/catalog.dtd">
<catalog prefer="public" xmlns="urn:oasis:names:tc:entity:xmlns:xml:catalog">
 <uri name="http://example.org/namespace/extension-schema-time"
      uri="extension.xsd"/>
 <uri name="http://example.org/code-list/vehicle-make-model"
      uri="../make-model.gc"/>
 <nextCatalog catalog="../../niem/xml-catalog.xml"/>
</catalog>

```

## Appendix D.7. XML instance with run-time code list binding

```xml
<?xml version="1.0" encoding="US-ASCII" standalone="yes"?>
<nc:Vehicle
   xmlns:cli="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
   xmlns:ext="http://example.org/namespace/extension-run-time"
   xmlns:nc="http://release.niem.gov/niem/niem-core/4.0/">
 <ext:VehicleMakeCode
     cli:codeListURI="http://example.org/code-list/vehicle-make-model"
     cli:codeListColumnName="make"
   >DODG</ext:VehicleMakeCode>
 <ext:VehicleModelCode
     cli:codeListURI="http://example.org/code-list/vehicle-make-model"
     cli:codeListColumnName="model"
   >R15</ext:VehicleModelCode>
</nc:Vehicle>

```

## Appendix D.8. Extension schema with run-time code list binding

```xml
<?xml version="1.0" encoding="us-ascii"?>
<xs:schema
  ct:conformanceTargets="http://reference.niem.gov/niem/specification/naming-and-design-rules/4.0/#ExtensionSchemaDocument"
  targetNamespace="http://example.org/namespace/extension-run-time"
  version="1"
  xmlns:cli="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
  xmlns:ct="http://release.niem.gov/niem/conformanceTargets/3.0/"
  xmlns:ext="http://example.org/namespace/extension-run-time"
  xmlns:nc="http://release.niem.gov/niem/niem-core/4.0/"
  xmlns:structures="http://release.niem.gov/niem/structures/4.0/"
  xmlns:xs="http://www.w3.org/2001/XMLSchema">

 <xs:annotation>
   <xs:documentation>An extension schema for vehicle make and model values, providing for run-time binding of XML content to a code list.</xs:documentation>
 </xs:annotation>

 <xs:import namespace="http://release.niem.gov/niem/niem-core/4.0/"/>
 <xs:import namespace="http://release.niem.gov/niem/structures/4.0/"/>
 <xs:import namespace="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"/>

 <xs:complexType name="CodeType">
   <xs:annotation>
     <xs:documentation>A data type for a code with codes sourced from an external code list.</xs:documentation>
   </xs:annotation>
   <xs:simpleContent>
     <xs:extension base="xs:token">
       <xs:attributeGroup ref="structures:SimpleObjectAttributeGroup"/>
       <xs:attribute ref="cli:codeListColumnName" use="optional"/>
       <xs:attribute ref="cli:codeListConstrainingIndicator" use="optional"/>
       <xs:attribute ref="cli:codeListURI" use="required"/>
     </xs:extension>
   </xs:simpleContent>
 </xs:complexType>

 <xs:element name="VehicleMakeCode" type="nc:CodeType"
             substitutionGroup="nc:VehicleMakeAbstract">
   <xs:annotation>
     <xs:documentation>A code for a manufacturer of a vehicle.</xs:documentation>
   </xs:annotation>
 </xs:element>

 <xs:element name="VehicleModelCode" type="nc:CodeType"
             substitutionGroup="nc:VehicleModelAbstract">
   <xs:annotation>
     <xs:documentation>A code for a model of a vehicle.</xs:documentation>
   </xs:annotation>
 </xs:element>

</xs:schema>

```

## Appendix D.9. XML catalog for run-time code list binding

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<!DOCTYPE catalog PUBLIC "-//OASIS//DTD Entity Resolution XML Catalog V1.0//EN" "http://www.oasis-open.org/committees/entity/release/1.0/catalog.dtd">
<catalog prefer="public" xmlns="urn:oasis:names:tc:entity:xmlns:xml:catalog">
 <uri name="http://example.org/namespace/extension-run-time"
      uri="extension.xsd"/>
 <uri name="http://reference.niem.gov/niem/specification/code-lists/4.0/code-lists-instance/"
      uri="../../../code-lists-instance.xsd"/>
 <uri name="http://example.org/code-list/vehicle-make-model"
      uri="../make-model.gc"/>
 <nextCatalog catalog="../../niem/xml-catalog.xml"/>
</catalog>

```

# Appendix E. Index

- code list: _Section 1.1_, _Section 1.1_, _Section 1.1_, _Section 2.9 (definition)_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 3.1_, _Section 5_
- code list binding: _Section 4_, _Section 4.3 (definition)_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.3_, _Section 4.5.3_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 7_
- code list document: _Section 1.4_, _Section 2.9_, _Section 2.9_, _Section 3_, _Section 3.1 (definition)_, _Section 3.3_, _Section 3.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 5_, _Section 7_
- code list identifier: _Section 1.4_, _Section 1.5_, _Section 2.9 (definition)_, _Section 3.1_, _Section 4.3_, _Section 4.3_, _Section 4.4.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.3_, _Section 4.5.3_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 5_, _Section 5_, _Section 6_, _Section 6_, _Section Appendix D_
- code list validation set: _Section 3_, _Section 3.6 (definition)_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.2_, _Section 4.5.3_, _Section 4.5.3_, _Section 4.6_, _Section 4.6_
- code list-enabled instance document: _Section 3_, _Section 3.5 (definition)_, _Section 3.5_, _Section 3.6_
- code list-enabled schema document: _Section 3_, _Section 3.4 (definition)_, _Section 3.4_, _Section 3.4_
- code value: _Section 1.1_, _Section 2.9_, _Section 2.9_, _Section 2.9 (definition)_, _Section 2.9_, _Section 2.9_, _Section 3.1_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 4.6_, _Section 5_, _Section 5_, _Section 5_, _Section 6_, _Section 6_, _Section 7.6_
- column: _Section 1.1_, _Section 1.1_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 2.9 (definition)_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 5_, _Section 5_, _Section 5_, _Section 6_, _Section 7.6_
- column identifier: _Section 2.9 (definition)_, _Section 2.9_, _Section 7_, _Section 7.1_, _Section 7.2_, _Section 7.3_, _Section 7.4_, _Section 7.5.1_, _Section 7.5.2_, _Section 7.5.3_, _Section 7.5.4_, _Section 7.6_
- column name: _Section 1.1_, _Section 2.9_, _Section 2.9 (definition)_, _Section 2.9_, _Section 2.9_, _Section 3.1_, _Section 4.3_, _Section 4.3_, _Section 4.3_, _Section 5_, _Section 6_, _Section 6_, _Section 6_, _Section 7_, _Section 7_, _Section 7.1_, _Section 7.2_, _Section 7.3_, _Section 7.4_, _Section 7.5_, _Section 7.5.1_, _Section 7.5.2_, _Section 7.5.3_, _Section 7.5.4_, _Section 7.6_
- CSV code list document: _Section 2.9_, _Section 2.9_, _Section 3_, _Section 3.3 (definition)_, _Section 5_, _Section 5_, _Section 5_, _Section 5_, _Section 7.5_
- distinct entry: _Section 1.1_, _Section 2.9_, _Section 2.9 (definition)_, _Section 2.9_, _Section 2.9_, _Section 2.9_, _Section 3.1_, _Section 4.6_, _Section 4.6_, _Section 5_, _Section 6_, _Section 7.2_, _Section 7.6_
- Genericode code list document: _Section 2.9_, _Section 2.9_, _Section 3_, _Section 3.2 (definition)_, _Section 6_, _Section 6_, _Section 6_, _Section 6_, _Section 6_, _Section 7_, _Section 7.5_
- locally-resolved resource: _Section 2.11 (definition)_, _Section 4.6_

# Appendix F. Index of definitions

- _absolute URI_: [Section 2.2, _RFC 3986: Uniform Resource Identifier (URI): Generic Syntax_](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
- _application information_: [Section 2.8, _NIEM Naming and Design Rules_](#niem-naming-and-design-rules)
- _attribute_: [Section 2.5, _XML Information Set_](#xml-information-set)
- _attribute declaration_: [Section 2.6, _XML Schema_](#xml-schema)
- _catalog entry file_: [Section 2.11, _XML Catalogs_](#xml-catalogs)
- _code list_: [Section 2.9, _Code Lists_](#code-lists)
- _code list binding_: [Section 4.3, _Definition of code list binding_](#definition-of-code-list-binding)
- _code list document_: [Section 3.1, _Code list document_](#code-list-document)
- _code list identifier_: [Section 2.9, _Code Lists_](#code-lists)
- _code list validation set_: [Section 3.6, _Code list validation set_](#code-list-validation-set)
- _code list-enabled instance document_: [Section 3.5, _Code list-enabled instance document_](#code-list-enabled-instance-document)
- _code list-enabled schema document_: [Section 3.4, _Code list-enabled schema document_](#code-list-enabled-schema-document)
- _code lists instance namespace_: [Section 2.4, _XML Namespaces_](#xml-namespaces)
- _code lists schema appinfo namespace_: [Section 2.4, _XML Namespaces_](#xml-namespaces)
- _code value_: [Section 2.9, _Code Lists_](#code-lists)
- _column_: [Section 2.9, _Code Lists_](#code-lists)
- _column identifier_: [Section 2.9, _Code Lists_](#code-lists)
- _column name_: [Section 2.9, _Code Lists_](#code-lists)
- _complex type definition_: [Section 2.6, _XML Schema_](#xml-schema)
- _conformance target_: [Section 2.7, _Conformance Targets Attribute Specification_](#conformance-targets-attribute-specification)
- _conformance target identifier_: [Section 2.7, _Conformance Targets Attribute Specification_](#conformance-targets-attribute-specification)
- _CSV code list document_: [Section 3.3, _CSV code list document_](#csv-code-list-document)
- _CSV column name_: [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- _CSV field_: [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- _CSV file_: [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- _CSV header_: [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- _CSV record_: [Section 2.10, _RFC 4180: Comma-separated values (CSV) files_](#rfc-4180:-comma-separated-values-(csv)-files)
- _derived_: [Section 2.6, _XML Schema_](#xml-schema)
- _distinct entry_: [Section 2.9, _Code Lists_](#code-lists)
- _effective conformance target identifier_: [Section 2.7, _Conformance Targets Attribute Specification_](#conformance-targets-attribute-specification)
- _element_: [Section 2.5, _XML Information Set_](#xml-information-set)
- _element declaration_: [Section 2.6, _XML Schema_](#xml-schema)
- _entity catalog_: [Section 2.11, _XML Catalogs_](#xml-catalogs)
- _exclusive lower bound_: [Section 2.6, _XML Schema_](#xml-schema)
- _exclusive upper bound_: [Section 2.6, _XML Schema_](#xml-schema)
- _Genericode code list document_: [Section 3.2, _Genericode code list document_](#genericode-code-list-document)
- _inclusive lower bound_: [Section 2.6, _XML Schema_](#xml-schema)
- _inclusive upper bound_: [Section 2.6, _XML Schema_](#xml-schema)
- _local context_: [Section 2.11, _XML Catalogs_](#xml-catalogs)
- _locally-resolved resource_: [Section 2.11, _XML Catalogs_](#xml-catalogs)
- _normalized value_: [Section 2.6, _XML Schema_](#xml-schema)
- _resolve_: [Section 2.11, _XML Catalogs_](#xml-catalogs)
- _resource_: [Section 2.2, _RFC 3986: Uniform Resource Identifier (URI): Generic Syntax_](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
- _schema component_: [Section 2.6, _XML Schema_](#xml-schema)
- _schema document_: [Section 2.6, _XML Schema_](#xml-schema)
- _schema-valid_: [Section 2.6, _XML Schema_](#xml-schema)
- _simple type definition_: [Section 2.6, _XML Schema_](#xml-schema)
- _substitution group_: [Section 2.6, _XML Schema_](#xml-schema)
- _text_: [Section 2.5, _XML Information Set_](#xml-information-set)
- _type definition_: [Section 2.6, _XML Schema_](#xml-schema)
- _uniform resource identifier_: [Section 2.2, _RFC 3986: Uniform Resource Identifier (URI): Generic Syntax_](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
- _URI_: [Section 2.2, _RFC 3986: Uniform Resource Identifier (URI): Generic Syntax_](#rfc-3986:-uniform-resource-identifier-(uri):-generic-syntax)
- _XML document_: [Section 2.3, _XML_](#xml)
- _XML Schema_: [Section 2.6, _XML Schema_](#xml-schema)
- _XML Schema definition language_: [Section 2.6, _XML Schema_](#xml-schema)
- _XML Schema document set_: [Section 2.8, _NIEM Naming and Design Rules_](#niem-naming-and-design-rules)

# Appendix G. Index of rules

- [Rule 3-1, _Code list-enabled schema document has conformance target_ (XSD)](#rule-3-1-code-list-enabled-schema-document-has-conformance-target): [Section 3.4, _Code list-enabled schema document_](#code-list-enabled-schema-document)
- [Rule 3-2, _Document with conformance target is a code list-enabled schema document_ (VSET)](#rule-3-2-document-with-conformance-target-is-a-code-list-enabled-schema-document): [Section 3.4, _Code list-enabled schema document_](#code-list-enabled-schema-document)
- [Rule 4-1, _Content in the "cli" namespace conforms to schema_ (INS)](#rule-4-1-content-in-the-cli-namespace-conforms-to-schema): [Section 4.4.1, _Syntax for run-time code list binding_](#syntax-for-run-time-code-list-binding)
- [Rule 4-2, _Code list URI is an absolute URI_ (INS)](#rule-4-2-code-list-uri-is-an-absolute-uri): [Section 4.4.1, _Syntax for run-time code list binding_](#syntax-for-run-time-code-list-binding)
- [Rule 4-3, _Column identifier accompanied by code list identifier_ (INS)](#rule-4-3-column-identifier-accompanied-by-code-list-identifier): [Section 4.4.1, _Syntax for run-time code list binding_](#syntax-for-run-time-code-list-binding)
- [Rule 4-4, _Constraining indicator accompanied by code list identifier_ (INS)](#rule-4-4-constraining-indicator-accompanied-by-code-list-identifier): [Section 4.4.1, _Syntax for run-time code list binding_](#syntax-for-run-time-code-list-binding)
- [Rule 4-5, _Effective run-time binding._ (INS)](#rule-4-5-effective-run-time-binding): [Section 4.4.2, _Run-time effective code list binding_](#run-time-effective-code-list-binding)
- [Rule 4-6, _Content in the "clsa" namespace conforms to schema_ (XSD)](#rule-4-6-content-in-the-clsa-namespace-conforms-to-schema): [Section 4.5.1, _Syntax for schema-time code list binding_](#syntax-for-schema-time-code-list-binding)
- [Rule 4-7, _Elements are `xs:appinfo` annotations_ (XSD)](#rule-4-7-elements-are-xs:appinfo-annotations): [Section 4.5.1, _Syntax for schema-time code list binding_](#syntax-for-schema-time-code-list-binding)
- [Rule 4-8, _Code list URI is absolute URI_ (XSD)](#rule-4-8-code-list-uri-is-absolute-uri): [Section 4.5.1, _Syntax for schema-time code list binding_](#syntax-for-schema-time-code-list-binding)
- [Rule 4-9, _Simple code list binding to schema components_ (XSD)](#rule-4-9-simple-code-list-binding-to-schema-components): [Section 4.5.1, _Syntax for schema-time code list binding_](#syntax-for-schema-time-code-list-binding)
- [Rule 4-10, _Complex code list binding to schema components_ (XSD)](#rule-4-10-complex-code-list-binding-to-schema-components): [Section 4.5.1, _Syntax for schema-time code list binding_](#syntax-for-schema-time-code-list-binding)
- [Rule 4-11, _Attribute declaration effective simple binding_ (VSET)](#rule-4-11-attribute-declaration-effective-simple-binding): [Section 4.5.2, _Simple binding of schema components_](#simple-binding-of-schema-components)
- [Rule 4-12, _Element declaration effective simple binding_ (VSET)](#rule-4-12-element-declaration-effective-simple-binding): [Section 4.5.2, _Simple binding of schema components_](#simple-binding-of-schema-components)
- [Rule 4-13, _Type definition effective simple binding_ (VSET)](#rule-4-13-type-definition-effective-simple-binding): [Section 4.5.2, _Simple binding of schema components_](#simple-binding-of-schema-components)
- [Rule 4-14, _Element declaration effective complex binding_ (VSET)](#rule-4-14-element-declaration-effective-complex-binding): [Section 4.5.3, _Complex binding of schema components_](#complex-binding-of-schema-components)
- [Rule 4-15, _Complex type definition effective complex binding_ (VSET)](#rule-4-15-complex-type-definition-effective-complex-binding): [Section 4.5.3, _Complex binding of schema components_](#complex-binding-of-schema-components)
- [Rule 4-16, _Matches and validity for a code list binding_ (VSET)](#rule-4-16-matches-and-validity-for-a-code-list-binding): [Section 4.6, _Matches for code list bindings_](#matches-for-code-list-bindings)
- [Rule 4-17, _Value comparisons based on types_ (VSET)](#rule-4-17-value-comparisons-based-on-types): [Section 4.6, _Matches for code list bindings_](#matches-for-code-list-bindings)
- [Rule 4-18, _Code list identified by candidate code list identifiers_ (VSET)](#rule-4-18-code-list-identified-by-candidate-code-list-identifiers): [Section 4.6, _Matches for code list bindings_](#matches-for-code-list-bindings)
- [Rule 5-1, _CSV code list document is a CSV file_ (CSV-CLD)](#rule-5-1-csv-code-list-document-is-a-csv-file): [Section 5, _Comma-separated values (CSV) code lists_](#comma-separated-values-(csv)-code-lists)
- [Rule 5-2, _CSV code list document has header_ (CSV-CLD)](#rule-5-2-csv-code-list-document-has-header): [Section 5, _Comma-separated values (CSV) code lists_](#comma-separated-values-(csv)-code-lists)
- [Rule 5-3, _CSV column name is not empty_ (CSV-CLD)](#rule-5-3-csv-column-name-is-not-empty): [Section 5, _Comma-separated values (CSV) code lists_](#comma-separated-values-(csv)-code-lists)
- [Rule 5-4, _CSV file as a code list document_ (CSV-CLD)](#rule-5-4-csv-file-as-a-code-list-document): [Section 5, _Comma-separated values (CSV) code lists_](#comma-separated-values-(csv)-code-lists)
- [Rule 6-1, _Genericode code list document defined by Genericode_ (GC-CLD)](#rule-6-1-genericode-code-list-document-defined-by-genericode): [Section 6, _Genericode code lists_](#genericode-code-lists)
- [Rule 6-2, _Document with conformance target is Genericode code list document_ (VSET)](#rule-6-2-document-with-conformance-target-is-genericode-code-list-document): [Section 6, _Genericode code lists_](#genericode-code-lists)
- [Rule 6-3, _Genericode code list document is schema-valid_ (GC-CLD)](#rule-6-3-genericode-code-list-document-is-schema-valid): [Section 6, _Genericode code lists_](#genericode-code-lists)
- [Rule 6-4, _XML Schema alternate datatypes are treated the same as built in datatypes_ (GC-CLD)](#rule-6-4-xml-schema-alternate-datatypes-are-treated-the-same-as-built-in-datatypes): [Section 6, _Genericode code lists_](#genericode-code-lists)
- [Rule 6-5, _Genericode file as a code list document_ (GC-CLD)](#rule-6-5-genericode-file-as-a-code-list-document): [Section 6, _Genericode code lists_](#genericode-code-lists)

