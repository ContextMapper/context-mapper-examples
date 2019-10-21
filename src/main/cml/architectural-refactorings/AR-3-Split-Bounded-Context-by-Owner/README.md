# AR-3: Split Bounded Context by Owner
Splits a bounded context by grouping those aggregates together into one bounded context which belong to the same team.

**Hint:** An aggregate in CML can belong to one owner/team (therefore the singular _owner_ in the AR name).

## Context & Rationales
By decomposing a system into multiple bounded contexts we aim for loose coupling between the bounded context and a high cohesion 
within them. One approach to achieve this and to decompose a system into components or (micro-) services is to split by owner (team).

**See also:**
 * Coupling criterion [Shared Owner](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-3-Shared-Owner) of [ServiceCutter](https://servicecutter.github.io/)
 * [Conway's Law](https://en.wikipedia.org/wiki/Conway's_law)
 * ["Bounded contexts decouple PARTS. Parts are code **and teams**."](http://ntcoding.co.uk/speaking/talks/domain-driven-design-hidden-lessons-from-the-big-blue-book/craft-conf-budapest-may-2019) 
 by [Nick Tune](http://www.ntcoding.co.uk/)

In Context Mapper you can assign an aggregate the owning team. Consult our 
[aggregate documentation page](https://contextmapper.org/docs/aggregate/#aggregate-owner) to see
how this can be modeled in CML.

## Goal
This Architectural Refactoring (AR) splits a bounded context by the owners of the aggregates. This means, it creates bounded contexts
containing aggregates which all belong to the same team. It can be applied if your model exhibits a bounded contexts with 
aggregates which are owned by different teams.

**Inverse AR's:**
 * [AR-7: Merge Bounded Contexts](./../AR-7-Merge-Bounded-Contexts)

## Preconditions
  * The bounded context must contain **at least two aggregates**.
  * The aggregates must be **assigned to different teams**.

## Input
 * One bounded context.
 
## Output
 * The AR creates multiple bounded contexts. Each bounded context contains one or more aggregates which are owned by the same
 team.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context contains two aggregates which are owend by two different teams:
```
/* With a right-click on the 'CustomerSelfServiceContext' bounded context you can execute the 'Split Bounded Context by Owners' refactoring.
 * It will split the existing bounded context according to the two owning teams 'CustomerBackendTeam' and 'CustomerFrontendTeam'.
 */
BoundedContext CustomerSelfServiceContext implements CustomerManagementDomain {
  type = APPLICATION
  domainVisionStatement = "This context represents a web application which allows the customer to login and change basic data records like the address."
  responsibilities = "AddressChange"
  implementationTechnology = "PHP Web Application"
  
  Aggregate CustomerFrontend {
    owner = CustomerFrontendTeam
    
    DomainEvent CustomerAddressChange {
      aggregateRoot
      
      - UserAccount issuer
      - Address changedAddress
    }
  }
  Aggregate Acounts {
    owner = CustomerBackendTeam
    
    Entity UserAccount {
      aggregateRoot
      
      String username
      - Customer accountCustomer
    }
  }
}
```

### Output
Applying the AR **Split Bounded Context by Owner** produces two bounded contexts, one for each team:
```
BoundedContext CustomerSelfServiceContext implements CustomerManagementDomain {
  domainVisionStatement = "This context represents a web application which allows the customer to login and change basic data records like the address."
  type = APPLICATION
  responsibilities = "AddressChange"
  implementationTechnology = "PHP Web Application"
  
  Aggregate CustomerFrontend {
    owner = CustomerFrontendTeam
    
    DomainEvent CustomerAddressChange {
      aggregateRoot
      
      - UserAccount issuer
      - Address changedAddress
    }
  }
}

/**
 * The new bounded context created by the 'Split Bounded Context by Owners' refactoring applied to 'example-input.cml'.
 * 
 * Note that the refactoring does not produce meaningful bounded context names. You can use the 'Rename Element' refactoring (SHIFT-ALT-R) 
 * to rename the new aggregate.
 * 
 * The automated refactorings add newly created bounded contexts at the end of the 'bounded context' block, which might not always be the
 * desired order. You may change the order after the refactoring manually.
 */
BoundedContext NewBoundedContext1 {
  Aggregate Acounts {
    owner = CustomerBackendTeam
    
    Entity UserAccount {
      aggregateRoot
      
      String username
      - Customer accountCustomer
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-3: Split Bounded Context by Owner](https://contextmapper.org/docs/ar-split-bounded-context-by-owners/)
