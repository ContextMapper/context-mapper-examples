![Context Mapper](https://raw.githubusercontent.com/wiki/ContextMapper/context-mapper-dsl/logo/cm-logo-github-small.png)  
# DSL Examples [![Build Status](https://travis-ci.com/ContextMapper/context-mapper-examples.svg?branch=master)](https://travis-ci.com/ContextMapper/context-mapper-examples) [![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/ContextMapper/context-mapper-examples) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
This project contains example DDD Context Maps written in the ContextMapper DSL. The examples are provided for two different types of users. The simpler business analysis examples should be easy to understand for business analysts without technical background, while the detailed examples are meant for software architects and/or engineers.  

Find out more about our DSL and tools on our website [https://contextmapper.org/](https://contextmapper.org/) and [papers](https://contextmapper.org/background-and-publications/) published by [OST (former HSR)](https://www.ost.ch).

Start exploring the examples in the Context Mapper online IDE right now:

<a href="https://gitpod.io/from-referrer/" style="padding: 10px;">
    <img src="https://gitpod.io/button/open-in-gitpod.svg" width="150" alt="Push" align="center">
</a>

## IDE Requirements
This is a Gradle project and can easily be imported into any IDE (ideally VS Code or Eclipse with Context Mapper installed) that supports Gradle.

### Context Mapper
In order to have language support for editing the CML files (Context Mapper Language), you need to install ContextMapper in Eclipse, Visual Studio Code, or use the online IDE Gitpod:

 * [Context Mapper for VS Code](https://marketplace.visualstudio.com/items?itemName=contextmapper.context-mapper-vscode-extension) (Marketplace)
 * [Context Mapper for Eclipse](https://marketplace.eclipse.org/content/context-mapper) (Marketplace)
   * Alternatively use this Eclipse update site URL for manual installation: 
     <br>[https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/](https://dl.bintray.com/contextmapper/context-mapping-dsl/updates/)
 * [VS Code Extension in Open VSX](https://open-vsx.org/extension/contextmapper/context-mapper-vscode-extension)
   * Can be found easily in your Gitpod's.
   * Or: [Start right now by using our demo repository](https://contextmapper.org/demo/).

## The examples:
The following graphical illustrations of the context maps are inspired by [Vernon][2] and [Brandolini][3]. Once you modelled your context map in CML you can [generate such graphical representations](https://contextmapper.org/docs/context-map-generator/).

 * [Insurance Example](#insurance-example)
 * [Lakeside Mutual](#lakeside-mutual)
 * [Context Mapper Example](#context-mapper-example)
 * [DDD Cargo Sample](#ddd-cargo-sample)
 * [Architectural Refactoring (AR) Examples](#architectural-refactoring-ar-examples)

### [Insurance Example](./src/main/cml/insurance-example)
In the folder [src/main/cml/insurance-example](./src/main/cml/insurance-example) you find example context maps for a fictitious insurance company, inspired by [Lakeside Mutual](https://github.com/Microservice-API-Patterns/LakesideMutual).

#### Context Map
The insurance example contains an example for a classic DDD context map written in the ContextMapper DSL (CML).

<img alt="Insurance Company Example Context Map" src="./src/main/cml/insurance-example/images/ContextMap-Illustration.png" width="600px">

#### Team Map
It further contains a team map, illustrating the teams and their relationships. Additionally, CML allows to define which bounded contexts are implemented by which teams.

<img alt="Insurance Company Example Context Map" src="./src/main/cml/insurance-example/images/TeamMap-Illustration-1.png">

### [Lakeside Mutual](./src/main/cml/lakeside-mutual)
The [Lakeside Mutual](https://github.com/Microservice-API-Patterns/LakesideMutual) microservice project is another fictitious insurance application that demonstrates microservices and the application of 
[Microservice API Patterns (MAP)](https://microservice-api-patterns.org/). 

We reverse engineered the initial CML model of the project by using our [discovery library](https://github.com/ContextMapper/context-map-discovery). In addition we conducted an Event Storming (tutorial coming soon) for a future 
_claim processing feature_ and modeled the results in the CML model. The model and the Event Storming result can be found in the following folder: [src/main/cml/lakeside-mutual](./src/main/cml/lakeside-mutual)

The following graphical Context Map of the model has been generated with our [Context Map generator](https://contextmapper.org/docs/context-map-generator/):

<img alt="Lakeside Mutual Context Map" src="./src/main/cml/lakeside-mutual/images/ContextMap-Illustration.png" width="600px">

### [Context Mapper Example](./src/main/cml/context-mapper-example)
In the folder [src/main/cml/context-mapper-example](./src/main/cml/context-mapper-example) we modelled our own tool and framework with CML. The following context map illustration of our bounded contexts and framework components is generated out of the CML model with the [Context Map generator](https://contextmapper.org/docs/context-map-generator/):

<img alt="Context Mapper Example Context Map" src="./src/main/cml/context-mapper-example/images/ContextMapper-Example-Simple_ContextMap.png" width="600px">

### [DDD Cargo Sample](./src/main/cml/ddd-sample)
The folder [src/main/cml/ddd-sample](./src/main/cml/ddd-sample) contains a context map based on the [DDD sample](https://github.com/citerus/dddsample-core) from [Eric Evans DDD book][1]. 

To make the sample interesting for our context mapping language, we splitted the Cargo application into three bounded contexts.

<img alt="Insurance Company Example Context Map" src="./src/main/cml/ddd-sample/images/DDD-Cargo-Tracking-ContextMap-Illustration.png" width="300px">

### [Architectural Refactoring (AR) Examples](./src/main/cml/architectural-refactorings)
The Context Mapper tool provides several [Architectural Refactorings][4] which can be applied to your models. A documentation of all available refactorings can be found under [https://contextmapper.org/docs/architectural-refactorings](https://contextmapper.org/docs/architectural-refactorings). The folder [src/main/cml/architectural-refactorings](./src/main/cml/architectural-refactorings) contains example CML models (input and ouput) to illustrate the architectural refactorings purposes.

## Contributing
Contribution is always welcome! Here are some ways how you can contribute:
 * Create Github issues if you find bugs or just want to give suggestions for improvements.
 * This is an open source project: if you want to code, [create pull requests](https://help.github.com/articles/creating-a-pull-request/) from [forks of this repository](https://help.github.com/articles/fork-a-repo/). Please refer to a Github issue if you contribute this way.
 * If you want to contribute to our documentation and user guides on our website [https://contextmapper.org/](https://contextmapper.org/), create pull requests from forks of the corresponding page repo [https://github.com/ContextMapper/contextmapper.github.io](https://github.com/ContextMapper/contextmapper.github.io) or create issues [there](https://github.com/ContextMapper/contextmapper.github.io/issues).

## Licence
ContextMapper is released under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

[1]: https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/
[2]: https://www.amazon.de/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577
[3]: https://www.infoq.com/articles/ddd-contextmapping
[4]: https://link.springer.com/article/10.1007%2Fs00607-016-0520-y
