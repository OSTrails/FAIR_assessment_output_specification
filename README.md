# FAIR_assessment_output_specification
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip) (work in progress)

Repository to track the requirements and specifications of FAIR assessment reports.

**Permanent identifier:** [https://w3id.org/ftr#](https://w3id.org/ftr#) (click to see documentation and examples beyond the README file)

**Authors**:  Daniel Garijo, Mark Wilkinson, Pablo Alarcón, Rober Huber, Lukas Arnhold, Allyson Lister, Elli Papadopoulou, Leonidas Pispiringas, Neil Chue Hong, Clement Jonquet, Wim Hugo

**Source document**: [https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing](https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing), with contributions from an initial modeling by Robert Huber and a [diagram](https://owncloud.tuwien.ac.at/index.php/s/VaGxqnf5MxfDtzz#/files_mediaviewer/dmp-dqv.png) authored by Lukas Arnhold.

**Ongoing document**: [Assessment components glossary and description](https://docs.google.com/document/d/1_dFj5bi6JKlcGZt40BEzVWUg6NjG1CBzGnCWAaad6NU/edit?usp=sharing) and [Metadata elements for FAIR assessment](https://docs.google.com/spreadsheets/d/1QKOoy-YJLNgnQywe6wOTTCBqCg0YuRWmIT-xFoB3ZCo/edit?usp=sharing)


## Core test result representation
We distinguish the following main concepts:
- **TestResult**: Output of running a test over a resource. A test result also should contain provenance metadata about the process followed to create it. `TestResult`is represented as an extension of `prov:Entity`. A test result points to the corresponding test through the `ftr:outputFromTest` property.
- **Test**: Service, formed by an API and associated piece of code that implements a Metric, and is executed (by a FAIR assessment tool), retrieving a particular and standardised result.
- **TestResultSet**: A set of FAIR test results, together with their respective metadata. Common metadata may describe the set. For example, if all results where run by a request to the same API.
- **TestExecutionActivity**: The action carried out by an agent of calling an API in which a test (or set of tests) were run. The result of this activity is either a `TestResult` or a `TestResultSet`.
- **Metric**: Narrative domain-agnostic description that a Test must wholly implement.
- **Benchmark**: Benchmarks are community-specific groupings of a set of Metrics that provides a narrative of those particular ways in which that community defines FAIR for assessment purposes.
- **Algorithm**: Piece of code that contextualises the sum of all test results for a given benchmark, into a final quantitative assessment result. 

![diagram](./development/img/FAIRTestResult_diagram_v10.drawio.png "Test result overview")

## Exemplar metadata

### Test and Test Result 

Test results have basic metadata to understand which test did they run, an explanation and whether they passes or not (or whether they were completed to a certain extend, if applicable).

The following snippet shows a test result over the entity `https://go-fair.org`:

```turtle
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix dcterms: <http://purl.org/dc/terms/>
@prefix ftr: <https://w3id.org/ftr#>
@prefix dcat: <http://www.w3.org/ns/dcat#>
@prefix sio: <http://semanticscience.org/resource/>
@prefix xsd: <http://www.w3.org/2001/XMLSchema#>
@prefix prov: <http://www.w3.org/ns/prov#>
@prefix schema: <http://schema.org/>


<urn:fairtestoutput:873a8370-77e0-40ad-a6e5-0d8349fdaea4>
    a ftr:TestResult ;
    dcterms:description "OUTPUT OF Tests metadata GUID for the ability to implement authentication and authorization in its resolution protocol.  Currently passes InChI Keys, DOIs, Handles, and URLs.  Recognition of other identifiers will be added upon request by the community."^^xsd:string ;
    dcterms:identifier <urn:fairtestoutput:873a8370-77e0-40ad-a6e5-0d8349fdaea4> ;
    dcterms:license <https://creativecommons.org/publicdomain/zero/1.0/> ;
    dcterms:title "FAIR Champion: Metadata Authorization OUTPUT"^^xsd:string ;
    prov:generatedAtTime "2025-01-14T10:12:13+01:00"^^xsd:date ;
    prov:wasDerivedFrom <https://go-fair.org> ;
    ftr:completion "100"^^xsd:int ;
    ftr:log """INFO: TEST VERSION 'Hvst-1.4.2:Tst-2.0.0'
PASS:  The GUID of the metadata is a uri, which is known to be allow authentication/authorization."""^^xsd:string ;
    ftr:outputFromTest <urn:ostrails:fairtestsoftware:e5e67c2a-769a-4efd-aa1c-c9cc96148e22> ;
    prov:value "pass"^^xsd:string ;
    ftr:summary ""^^xsd:string .

<https://go-fair.org>
    dcterms:identifier "https://go-fair.org"^^xsd:string ;
    a prov:Entity .

<urn:ostrails:fairtestsoftware:e5e67c2a-769a-4efd-aa1c-c9cc96148e22>
    a schema:SoftwareApplication, <https://w3id.org/ftr#Test> ;
    dcterms:description "Tests metadata GUID for the ability to implement authentication and authorization in its resolution protocol.  Currently passes InChI Keys, DOIs, Handles, and URLs.  Recognition of other identifiers will be added upon request by the community."^^xsd:string ;
    dcterms:identifier "https://tests.ostrails.eu/tests/fc_metadata_authorization" ;
    dcterms:license <https://github.com/wilkinsonlab/FAIR-Core-Tests/blob/main/LICENSE> ;
    dcterms:title "FAIR Champion: Metadata Authorization"^^xsd:string ;
    sio:SIO_000233 <https://tests.ostrails.eu/tests/fc_metadata_authorization/about> ;
    dcat:endpointDescription <https://tests.ostrails.eu/tests/fc_metadata_authorization/API> ;
    dcat:endpointURL <https://tests.ostrails.eu/tests/fc_metadata_authorization> ;
    dcat:version "Hvst-1.4.2:Tst-2.0.0"^^xsd:string .

<urn:ostrails:testexecutionactivity:9c0a5639-4aaf-480e-8bd4-066c7626c725>
    a ftr:TestExecutionActivity ;
   prov:generated <urn:fairtestoutput:873a8370-77e0-40ad-a6e5-0d8349fdaea4> ;
   prov:used <https://go-fair.org> ;
   prov:wasAssociatedWith <urn:ostrails:fairtestsoftware:e5e67c2a-769a-4efd-aa1c-c9cc96148e22> .
```


### Metric 

FAIR Metric contains basic metadata to undertand the test must wholly implement. This is exemplar representation of a Metric:

```turtle

@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix vcard: <http://www.w3.org/2006/vcard/ns#> .
@prefix ftr: <https://w3id.org/ftr#> .
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix doap: <http://usefulinc.com/ns/doap#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix dqv: <http://www.w3.org/ns/dqv#> .
@prefix vivo: <http://vivoweb.org/ontology/core#> . 

<https://w3id.org/foops/metric/CN1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/CN1> ;
	dcterms:title "Content negotiation for RDF"@en ;
	dcterms:description """ 

This metric ensures that the vocabulary is accessible in recognized RDF serialization formats.

**What is being measured?**

The accessibility of the vocabulary in any of the following RDF serializations:

* RDF/XML
* Turtle (TTL)
* N-Triples
* JSON-LD

**Why should we measure it?**

RDF serializations are fundamental for semantic web technologies. Ensuring accessibility in at least one of these formats allows tools and systems to process the vocabulary effectively, enabling interoperability and usability across platforms.

**What must be provided for the measurement?**

An ontology URI.

**What are considered valid results?**

Valid results occur if the ontology is accessible in at least one specified RDF serialization. The test fails if no recognized serialization is returned or the serialization does not match the required formats.
	"""@en ;
	rdfs:label "Metric CN1"^^xsd:string ;
	vivo:abbreviation "Metric CN1"^^xsd:string ;	
	dcat:contactPoint <https://orcid.org/0000-0003-0454-7145> ;
	dcterms:creator <https://orcid.org/0000-0003-0454-7145> ;
	dcterms:creator <https://orcid.org/0000-0003-3587-0367> ;
	dqv:inDimension  <https://w3id.org/fair/principles/terms/A1> ;
	dcterms:publisher <https://oeg.fi.upm.es> ;
	dcat:version "0.0.1"^^xsd:string ;
	dcterms:license <http://creativecommons.org/licenses/by/2.0/> ;
	dcat:keyword "Content negotiation"@en , "Metric"@en ;
	<http://semanticscience.org/resource/SIO_000233> <https://w3id.org/foops/test/CN1> ;
	dcat:landingPage <https://w3id.org/foops/metric/CN1> ; 
	ftr:hasBenchmark <https://w3id.org/foops/benchmark/ALL> ; 
	ftr:status "Active"@en .
<https://orcid.org/0000-0003-0454-7145> a vcard:Individual;
	vcard:fn "Daniel Garijo"^^xsd:string ;
	vcard:hasEmail <mailto:dgarijo@upm.es> .
<https://orcid.org/0000-0003-3587-0367> a vcard:Individual;
	vcard:fn "Maria Poveda"^^xsd:string ;
	vcard:hasEmail <mailto:m.poveda@upm.es> .
<https://w3id.org/fair/principles/terms/A1> a <https://w3id.org/fair/principles/terms/FAIR-SubPrinciple> ;
	rdfs:label "A1"^^xsd:string ;
	vivo:abbreviation "A1"^^xsd:string ;
	dcterms:description "(meta)data are retrievable by their identifier using a standardized communications protocol"@en .
<https://oeg.fi.upm.es> a vcard:Organization .
<https://w3id.org/foops/test/CN1> a ftr:Test .
<https://w3id.org/foops/benchmark/ALL> a ftr:Benchmark;
    dcterms:title "General Benchmark ALL for FAIR Principles"@en ;
    dcterms:description "This benchmark specifies the criteria for evaluating aspects of data quality according to the FAIR principle. Apply to all metrics."@en .

```


### Test results set
Many assessment tools run a set of tests (e.g., organized under a test collection), and they may share common provenance metadata. In those cases, we propose a flexible approach by using a test set to record their provenance information. For example, let us have two tests from an assessment service run over a single resource:

```turtle
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix ftr: <https://w3id.org/fair_test_result#> .
@prefix schema: <https://schema.org/> .
@prefix ex: <http://example.org/fair/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

ex:result1 a ftr:TestResult;
    schema:identifier "long_random_id";
    schema:name "Result of test for checking if HTML representation of the resource is reachable";
    ftr:isDefinedBy <http://example.org/foops/test/12>; #assuming this URL will have a specification of the test
    schema:description "A HTML representation of this resource was found";
    ftr:log """
        LOG indicating the operations undertaken goes here
        """;
    ftr:status "pass".

ex:result2 a ftr:TestResult;
    schema:identifier "long_random_id";
    schema:name "Result of test for checking if an RDF representation of the resource is reachable";
    ftr:isDefinedBy <http://example.org/foops/test/15>; #assuming this URL will have a specification of the test
    schema:description "An RDF representation of this resource was found";
    ftr:log """
        LOG indicating the operations undertaken goes here
        """; 
    ftr:status "fail".

ex:testResultSet1 a ex:TestResultSet;
    prov:wasGeneratedBy ex:foopsExecution123;
    prov:used ex:assessedResource;
    prov:wasDerivedFrom ex:assessedResource;
    prov:hadMember ex:result1, result2 .

ex:assessedResource a prov:Entity;
    schema:url "https://w3id.org/example".

ex:foopsExecution123 a ftr:TestExecutionActivity;
    prov:used ex:assessedResource;
    ftr:usedAPI "https://foops.linkeddata.es/assessOntology/"^^xsd:anyURI;
    prov:wasStartedBy [
        a prov:Agent;
        schema:identifier <ORCID_ID>;
        schema:name "Daniel".
    ];
    prov:startedAtTime "DATE"^^xsd:dateTime;
    prov:endedAtTime "DATE"^^xsd:dateTime.

ex:foops a schema:SoftwareApplication;
    schema:url "https://w3id.org/foops"^^xsd:anyURI;
    schema:softwareVersion "0.1.0".
```


### Benchmark

This exemplar metadata describes are community-specific groupings of a set of Metrics that provides a narrative of those particular ways in which that community defines FAIR for assessment purposes.

```turtle
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .
@prefix vcard: <http://www.w3.org/2006/vcard/ns#> .
@prefix ftr: <https://w3id.org/ftr#> .
@prefix dcat: <http://www.w3.org/ns/dcat#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix doap: <http://usefulinc.com/ns/doap#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix dqv: <http://www.w3.org/ns/dqv#> .
@prefix vivo: <http://vivoweb.org/ontology/core#> .

<https://w3id.org/foops/benchmark/ALL> a ftr:Benchmark ;
	dcterms:identifier <https://w3id.org/foops/benchmark/ALL> ;
	dcterms:title "General Benchmark for FAIR Principles"@en ;
    rdfs:label "Benchmark ALL"^^xsd:string ;
    vivo:abbreviation "Benchmark ALL"^^xsd:string ;
	dcterms:description """ This benchmark specifies the criteria for evaluating aspects of data quality according to the FAIR principle. """@en ; 
	dcat:contactPoint <https://orcid.org/0000-0003-0454-7145> ;
	dcterms:creator <https://orcid.org/0000-0003-0454-7145> ;
	dcterms:creator <https://orcid.org/0000-0003-3587-0367> ;
    dcat:keyword "General Benchmark"@en , "Benchmark"@en , "All"@en ;
	dcat:landingPage <https://w3id.org/foops/benchmark/ALL> ; 
    dcat:version "0.0.1"^^xsd:string ;
	dcterms:license <http://creativecommons.org/licenses/by/2.0/> ;
	ftr:status "Active"@en ;
    ftr:associatedMetric 
        <https://w3id.org/foops/metric/CN1> ,
        <https://w3id.org/foops/metric/DOC1> ,
        <https://w3id.org/foops/metric/FIND1> ,
        <https://w3id.org/foops/metric/FIND2> ,
        <https://w3id.org/foops/metric/FIND3> ,
        <https://w3id.org/foops/metric/FIND_3_BIS> ,
        <https://w3id.org/foops/metric/HTTP1> ,
        <https://w3id.org/foops/metric/OM1> ,
        <https://w3id.org/foops/metric/OM2> ,
        <https://w3id.org/foops/metric/OM3> ,
        <https://w3id.org/foops/metric/OM4.1> , 
        <https://w3id.org/foops/metric/OM4.2> ,
        <https://w3id.org/foops/metric/OM5.1> ,
        <https://w3id.org/foops/metric/OM5.2> ,
        <https://w3id.org/foops/metric/PURL1> ,
        <https://w3id.org/foops/metric/URI1> ,
        <https://w3id.org/foops/metric/URI2> ,
        <https://w3id.org/foops/metric/VER1> ,
        <https://w3id.org/foops/metric/VER2> ,
        <https://w3id.org/foops/metric/VOC1> ,
        <https://w3id.org/foops/metric/VOC2> ,
        <https://w3id.org/foops/metric/VOC3> ,
        <https://w3id.org/foops/metric/VOC4> 
         .
<https://orcid.org/0000-0003-0454-7145> a vcard:Individual;
	vcard:fn "Daniel Garijo"^^xsd:string ;
	vcard:hasEmail <mailto:dgarijo@upm.es> .
<https://orcid.org/0000-0003-3587-0367> a vcard:Individual;
	vcard:fn "Maria Poveda"^^xsd:string ;
	vcard:hasEmail <mailto:m.poveda@upm.es> .
<https://w3id.org/foops/metric/CN1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/CN1> ;
	rdfs:label "Metric CN1"^^xsd:string ;
    vivo:abbreviation "Metric CN1"^^xsd:string .
<https://w3id.org/foops/metric/DOC1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/DOC1> ;
	rdfs:label "Metric DOC1"^^xsd:string ;
    vivo:abbreviation "Metric DOC1"^^xsd:string .
<https://w3id.org/foops/metric/FIND1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/FIND1> ;
	rdfs:label "Metric FIND1"^^xsd:string ;
    vivo:abbreviation "Metric FIND1"^^xsd:string .
<https://w3id.org/foops/metric/FIND2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/FIND2> ;
	rdfs:label "Metric FIND2"^^xsd:string ;
    vivo:abbreviation "Metric FIND2"^^xsd:string .
<https://w3id.org/foops/metric/FIND3> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/FIND3> ;
	rdfs:label "Metric FIND3"^^xsd:string ;
    vivo:abbreviation "Metric FIND3"^^xsd:string .
<https://w3id.org/foops/metric/FIND_3_BIS> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/FIND_3_BIS> ;
	rdfs:label "Metric FIND_3_BIS"^^xsd:string ;
    vivo:abbreviation "Metric FIND_3_BIS"^^xsd:string .
<https://w3id.org/foops/metric/HTTP1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/HTTP1> ;
	rdfs:label "Metric HTTP1"^^xsd:string ;
    vivo:abbreviation "Metric HTTP1"^^xsd:string .
<https://w3id.org/foops/metric/OM1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM1> ;
	rdfs:label "Metric OM1"^^xsd:string ;
    vivo:abbreviation "Metric OM1"^^xsd:string .
<https://w3id.org/foops/metric/OM2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM2> ;
	rdfs:label "Metric OM2"^^xsd:string ;
    vivo:abbreviation "Metric OM2"^^xsd:string .
<https://w3id.org/foops/metric/OM3> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM3> ;
	rdfs:label "Metric OM3"^^xsd:string ;
    vivo:abbreviation "Metric OM3"^^xsd:string .
<https://w3id.org/foops/metric/OM4.1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM4.1> ;
	rdfs:label "Metric OM4.1"^^xsd:string ;
    vivo:abbreviation "Metric OM4.1"^^xsd:string .
<https://w3id.org/foops/metric/OM4.2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM4.2> ;
	rdfs:label "Metric OM4.2"^^xsd:string ;
    vivo:abbreviation "Metric OM4.2"^^xsd:string .
<https://w3id.org/foops/metric/OM5.1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM5_1> ;
	rdfs:label "Metric OM5_1"^^xsd:string ;
    vivo:abbreviation "Metric OM5_1"^^xsd:string .
<https://w3id.org/foops/metric/OM5.2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/OM5_2.1> ;
	rdfs:label "Metric OM5_2.1"^^xsd:string ;
    vivo:abbreviation "Metric OM5.2"^^xsd:string .
<https://w3id.org/foops/metric/PURL1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/PURL1> ;
	rdfs:label "Metric PURL1"^^xsd:string ;
    vivo:abbreviation "Metric PURL1"^^xsd:string .
<https://w3id.org/foops/metric/URI1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/URI1> ;
	rdfs:label "Metric URI1"^^xsd:string ;
    vivo:abbreviation "Metric URI1"^^xsd:string .
<https://w3id.org/foops/metric/URI2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/URI2> ;
	rdfs:label "Metric URI2"^^xsd:string ;
    vivo:abbreviation "Metric URI2"^^xsd:string .
<https://w3id.org/foops/metric/VER1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VER1> ;
	rdfs:label "Metric VER1"^^xsd:string ;
    vivo:abbreviation "Metric VER1"^^xsd:string .
<https://w3id.org/foops/metric/VER2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VER2> ;
	rdfs:label "Metric VER2"^^xsd:string ;
    vivo:abbreviation "Metric VER2"^^xsd:string .
<https://w3id.org/foops/metric/VOC1> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VOC1> ;
	rdfs:label "Metric VOC1"^^xsd:string ;
    vivo:abbreviation "Metric VOC1"^^xsd:string .
<https://w3id.org/foops/metric/VOC2> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VOC2> ;
	rdfs:label "Metric VOC2"^^xsd:string ;
    vivo:abbreviation "Metric VOC2"^^xsd:string .
<https://w3id.org/foops/metric/VOC3> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VOC3> ;
	rdfs:label "Metric VOC3"^^xsd:string ;
    vivo:abbreviation "Metric VOC3"^^xsd:string .
<https://w3id.org/foops/metric/VOC4> a dqv:Metric ;
	dcterms:identifier <https://w3id.org/foops/metric/VOC4> ;
	rdfs:label "Metric VOC4"^^xsd:string ;
    vivo:abbreviation "Metric VOC4"^^xsd:string .

```

## Scope
Future releases will address:
- How a FAIR assessment score is calculated by an algorithm and its metadata


## Requirements
The proposed vocabulary is derived from a set of competency questions, available at the `cqs` folder. CQs come from:
* Requirements based on the experience of the authors (as FAIR assessment tool developers)
* The [open document](https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing) where experts from various projects regarding FAIR assessment have gathered.