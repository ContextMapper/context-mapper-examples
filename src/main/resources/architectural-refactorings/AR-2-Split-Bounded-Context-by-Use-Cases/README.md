# AR-2: Split Bounded Context by Use Cases
Splits a bounded context by grouping those aggregates together into one bounded context which are used by the same use case(s).

**Hint:** An aggregate in CML can belong to multiple use cases (therefore the plural _use cases_ in the AR name). 

## Context & Rationales
By decomposing a system into multiple bounded contexts we aim for loose coupling between the bounded context and a high cohesion 
within them. One approach to achieve this and to decompose a system into components or (micro-) services is to split by use cases.

**See also:**
 * Coupling criterion [Semantic Proximity](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-2-Semantic-Proximity) of [ServiceCutter](https://servicecutter.github.io/)
 * [How to decompose the application into services?](https://microservices.io/patterns/microservices.html#how-to-decompose-the-application-into-services) by [Chris Richardson](https://microservices.io/book)
 * [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)

In Context Mapper you can assign multiple use cases to an aggregate, which allows you to model by which use cases an aggregate
is used. Consult our [aggregate documentation page](https://contextmapper.github.io/docs/aggregate/#aggregate-use-cases) to see
how this can be modeled in CML.

## Goal
This Architectural Refactoring (AR) splits a bounded context by use cases. This means, it creates bounded contexts containing
aggregates which are used by the same use cases. It can be applied if your model exhibits a bounded contexts with aggregates which
are used by multiple different use cases.

**Inverse AR's:**
 * [AR-7: Merge Bounded Contexts](./../AR-7-Merge-Bounded-Contexts)

## Preconditions
 * The bounded context must contain **at least two aggregates**.
 * The aggregates must be **assigned to different use cases**.

## Input
 * One bounded context.
 
## Output
 * The AR creates multiple bounded contexts. Each bounded context contains one or more aggregates which are used by the same 
 use cases.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context three aggregates which are used by two different use cases:
```
/* With a right-click on the 'PolicyManagementContext' bounded context you can execute the 'Split Bounded Context by Use Cases' refactoring.
 * It will split the existing bounded context and group the two aggregates of the 'CreateOffer4Customer' use case together. The 'Contract'
 * aggregate used by the 'UpdateContract' use case will be separated.
 */
BoundedContext PolicyManagementContext implements PolicyManagementDomain {
  type = FEATURE
  domainVisionStatement = "This bounded context manages the contracts and policies of the customers."
  responsibilities = "Offers, Contracts, Policies"
  implementationTechnology = "Java, Spring App"
  
  Aggregate Offers {
    useCases = CreateOffer4Customer
    
    Entity Offer {
      aggregateRoot
      
      int offerId
      - Customer client
      - List<Product> products
      BigDecimal price
    }
  }
  Aggregate Products {
    useCases = CreateOffer4Customer
    
    Entity Product {
      aggregateRoot
      
      - ProductId identifier
      String productName
    }
    ValueObject ProductId {
      int productId key
    }
  }
  Aggregate Contract {
    useCases = UpdateContract
    
    Entity Contract {
      aggregateRoot
      
      - ContractId identifier
      - Customer client
      - List<Product> products
    }
    ValueObject ContractId {
      int contractId key
    }
    
    Entity Policy {
      int policyNr
      - Contract contract
      BigDecimal price
    }
  }
}
```

### Output
Applying the AR **Split Bounded Context by Use Cases** produces two bounded context, one for each use case:
```
BoundedContext PolicyManagementContext implements PolicyManagementDomain {
  domainVisionStatement = "This bounded context manages the contracts and policies of the customers."
  responsibilities = "Offers, Contracts, Policies"
  implementationTechnology = "Java, Spring App"
  
  Aggregate Contract {
    useCases = UpdateContract
    
    Entity Contract {
      aggregateRoot
      
      - ContractId identifier
      - Customer client
      - List<Product> products
    }
    ValueObject ContractId {
      int contractId key
    }
    
    Entity Policy {
      int policyNr
      - Contract contract
      BigDecimal price
    }
  }
}

/**
 * A new bounded context created by the 'Split Bounded Context by Use Cases' refactoring applied to 'example-input.cml'.
 * 
 * Note that the refactoring does not produce meaningful bounded context names. You can use the 'Rename Element' refactoring (SHIFT-ALT-R) 
 * to rename the new aggregate.
 */
BoundedContext NewBoundedContext1 {
  Aggregate Offers {
    useCases = CreateOffer4Customer
    
    Entity Offer {
      aggregateRoot
      
      int offerId
      - Customer client
      - List<Product> products
      BigDecimal price
    }
  }
  Aggregate Products {
    useCases = CreateOffer4Customer
    
    Entity Product {
      aggregateRoot
      
      - ProductId identifier
      String productName
    }
    ValueObject ProductId {
      int productId key
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.github.io/docs/architectural-refactorings/)
 * [AR-2: Split Bounded Context by Use Cases](https://contextmapper.github.io/docs/ar-split-bounded-context-by-use-cases/)
