# OOAD Transformations Applied
On our [Rapid Object-oriented Analysis and Design](https://contextmapper.org/docs/rapid-ooad/) we explain how you can prototype an application with our OOAD
transformations rapidly. This folder contains another example on which we applied this concept.

## Use Case: Get Paid for Car Accident
The [example model](./claims-use-case.cml) contains a Use Case of Alistair Cockburn's book on [Writing Effective Use Cases](https://www.amazon.com/Writing-Effective-Cases-Alistair-Cockburn/dp/0201702258). 

## Application Generation
From the given Use Case we automatically derived the subdomain and the Bounded Context. Then, we generated the [JDL file](./claims-use-case-entities.jdl) from which we are able to generate
a microservice application.
