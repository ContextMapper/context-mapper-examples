# DDD "Cargo" Sample Application

This example is illustrates the Context Mapper DSL capabilities on the basis the [DDD "Cargo" sample application](https://github.com/citerus/dddsample-core). 

Since CML is dealing with context maps, we divided the application into three bounded contexts. [Evans][1] already mentioned in his book, that the voyage scheduling part is a candidate for a possible bounded contexts. Thus, we made a separate bounded context for this part. Since they still share code, they are in shared kernel relationship. Further we proposed the idea of splitting the locations into a separate bounded context, inspired by the example of [Rademacher][2]. This context could provide everything related to locations as an OPEN HOST SERVICE. Note that this is just an example in order to have another bounded context and must not be a good solution necessarily.

The following figure illustrates the example. 

<img alt="DDD Sample Context Map" src="./images/DDD-Cargo-Tracking-ContextMap-Illustration.png" width="400px">

Here you can find the corresponding context map in CML (Context Mapper Language) in different versions and levels of detail:

 * [DDD-Sample-Simple](./DDD-Sample-Simple.cml): A simple (business analysis) version without technical details (data type attributes etc.)
 * [DDD-Sample-Detailed](./DDD-Sample-Detailed.cml): The detailed context map on the architect and engineering level
 * [DDD-Sample_Alternative-Relationship-Syntax](./DDD-Sample_Alternative-Relationship-Syntax.cml): The simple context map example illustrating the alternative relationship syntax.
 * [DDD-Sample_User-Representations](./DDD-Sample_User-Representations.scl): Service Cutter user representations file (for Service Cutter integration) to generate new service cuts

[1]: https://www.oreilly.com/library/view/domain-driven-design-tackling/0321125215/
[2]: https://link.springer.com/chapter/10.1007/978-3-319-74781-1_17
