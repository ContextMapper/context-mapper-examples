[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# ContextMapper DSL Examples

This project contains example DDD Context Maps written in the ContextMapper DSL. Find out more about the DSL project [here](https://github.com/ContextMapper/context-mapper-dsl)

## IDE Requirements
This is a gradle project and can easily be imported into Eclipse by using the "Existing Gradle Project" importer.

### ContextMapper Eclipse Plugin
In order to have language support for editing the CML files (Context Mapper Language), you need to install the ContextMapper Eclipse Plugin.
Use the following Eclipse Update Site to install it:

[https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/](https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/)

## The examples:

### Insurance Example
In the folder [src/main/resources/insurance-example](./src/main/resources/insurance-example) you find example context maps for a fictive insurance company.

#### Context Map
The insurance example contains an example for a classic DDD context map written in the ContextMapper DSL (CML).

<img alt="Insurance Company Example Context Map" src="./src/main/resources/insurance-example/images/ContextMap-Illustration.png" width="500px">

#### Team Map
It further contains a team map, illustrating the teams and their relationships. Additionally, CML allows to define which bounded contexts are implemented by which teams.

<img alt="Insurance Company Example Context Map" src="./src/main/resources/insurance-example/images/TeamMap-Illustration.png" width="500px">

### DDD Sample
The folder [src/main/resources/ddd-sample](./src/main/resources/ddd-sample) contains a context map based on the [DDD sample](https://github.com/citerus/dddsample-core) from [Eric Evans DDD book][1]. 

To make the sample interesting for our context mapping language, we splitted the Cargo application into three bounded contexts.

<img alt="Insurance Company Example Context Map" src="./src/main/resources/ddd-sample/images/DDD-Cargo-Tracking-ContextMap-Illustration.png" width="300px">

[1]: https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/
