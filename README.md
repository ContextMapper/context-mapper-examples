![Context Mapper](https://raw.githubusercontent.com/wiki/ContextMapper/context-mapper-dsl/logo/cm-logo-github-small.png)  
# DSL Examples [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
This project contains example DDD Context Maps written in the ContextMapper DSL. Find out more about the DSL project on our website [https://contextmapper.github.io/](https://contextmapper.github.io/) and the [project report](https://eprints.hsr.ch/722/) published by [HSR](https://www.hsr.ch).

## IDE Requirements
This is a gradle project and can easily be imported into Eclipse by using the "Existing Gradle Project" importer.

### ContextMapper Eclipse Plugin
In order to have language support for editing the CML files (Context Mapper Language), you need to install the ContextMapper Eclipse Plugin.
Use the following Eclipse Update Site to install it:

[https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/](https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/)

## The examples:
The following graphical illustrations of the Context Maps are inspired by [Vernon][2] and [Brandolini][3].

### Insurance Example
In the folder [src/main/resources/insurance-example](./src/main/resources/insurance-example) you find example context maps for a fictitious insurance company, inspired by [Lakeside Mutual](https://github.com/Microservice-API-Patterns/LakesideMutual).

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

## Contributing
Contribution is always welcome! Here are some ways how you can contribute:
 * Create Github issues if you find bugs or just want to give suggestions for improvements.
 * This is an open source project: if you want to code, [create pull requests](https://help.github.com/articles/creating-a-pull-request/) from [forks of this repository](https://help.github.com/articles/fork-a-repo/). Please refer to a Github issue if you contribute this way.
 * If you want to contribute to our documentation and user guides on our website [https://contextmapper.github.io/](https://contextmapper.github.io/), create pull requests from forks of the corresponding page repo [https://github.com/ContextMapper/contextmapper.github.io](https://github.com/ContextMapper/contextmapper.github.io) or create issues [there](https://github.com/ContextMapper/contextmapper.github.io/issues).

## Licence
ContextMapper is released under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

[1]: https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/
[2]: https://www.amazon.de/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577
[3]: https://www.infoq.com/articles/ddd-contextmapping
