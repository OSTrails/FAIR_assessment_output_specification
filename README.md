# FAIR_assessment_output_specification
[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip) (work in progress)

Repository to track the requirements and specifications of FAIR assessment reports.

**Authors**:  Daniel Garijo, Mark Wilkinson, Rober Huber, Lukas Arnhold, Allyson Lister, Elli Papadopoulou, Leonidas Pispiringas, Neil Chue Hong, Clement Jonquet, Wim Hugo

**Source document**: [https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing](https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing)

## Core test result representation
We distinguish three main concepts:
- **TestResult**: Assessment score resultant of running a test over a resource to analyze. A test result also should contain provenance metadata about the process followed to create it. `TestResult`is represented as an extension of `dqv:QualityMeasurement` and `prov:Entity`. A test result points to the corresponding test specification through the `dpv:isQualityMeasurementOf` property, following the W3C DQV specification.
- **TestResultSet**: A set of FAIR test results, together with their respective metadata. Common metadata may describe the set. For example, if all results where run by a request to the same API.
- **TestExecutionActivity**: The action carried out by an agent of calling an API in which a test (or set of tests) were run. The result of this activity is either a `TestResult` or a `TestResultSet`.

![diagram](./development/img/FAIRTestResult_diagram.drawio.png "test result overview")

### Example: A single test execution
[Ongoing]

A tool called an API to generate a test result. In this case the result set is not used. 

RDF (ttl representation below. Example from F-UJI).
```
TO DO
```

You can do two test results:
RDF (ttl representation below. Example from F-UJI).
```
TO DO
```

### Example: Grouping test results in a test set
Many assessment tools run a set of tests (e.g., organized under a test collection), and they may share common metadata. In those cases, we propose a flexible approach by 

RDF (ttl representation below. Example from FOOPS!)
```
TO DO
```

## Scope
So far, the next release aims to represent test **results**. Future releases will address:
- Test specification metadata (i.e., the test from which a test 
result is derived from)
- What a quality metric is, and its prpovenance. For example, how two tests results may be used to generate a quality metric.
- How a FAIR assessment score is calculated (e.g., how different quality metrics are aggregated together) 
- How tests are supposed incorporate suggestions, and which metadata should they include.




## Requirements
The proposed vocabulary is derived from a set of competency questions, available at the `cqs` folder. CQs come from:
* Requirements based on the experience of the authors (as FAIR assessment tool developers)
* The [open document](https://docs.google.com/document/d/1HusredfHgymRg2ub4L0GnVSRV8IWZvFJyMkE6POejpc/edit?usp=sharing) where experts from various projects regarding FAIR assessment have gathered.