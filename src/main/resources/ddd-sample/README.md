# DDD "Cargo" Sample Application

This example is illustrates the Context Mapper DSL capabilities on the basis the [DDD "Cargo" sample application](https://github.com/citerus/dddsample-core). 
Since CML is dealing with context maps, we divided the application into three bounded contexts. Evans already mentioned in his book, that the voyage scheduling part is a candidate for a possible bounded contexts. Thus, we made a separate bounded context for this part. Since they still share code, they are in shared kernel relationship. Further we proposed the idea of splitting the locations into a separate bounded context. This context could provide everything related to locations as an OPEN HOST SERVICE. Note that this is just an example in order to have another bounded context and must not be a good solution necessarily.

The following figure illustrates the example. You find the CML example in the file [DDD_Sample.cml](DDD_Sample.cml).

<img alt="DDD Sample Context Map" src="./images/DDD-Cargo-Tracking-ContextMap-Illustration.png" width="500px">
