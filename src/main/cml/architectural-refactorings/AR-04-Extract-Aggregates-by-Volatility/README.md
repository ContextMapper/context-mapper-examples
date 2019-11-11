# AR-4: Extract Aggregates by Volatility
Extracts all aggregates from a bounded context by a given volatility, or likelihood for change 
(RARELY, NORMAL or OFTEN), and moves them to a separate context.

## Context & Rationales
By decomposing a system into multiple bounded contexts we aim for loose coupling between the bounded context and a high cohesion 
within them. One approach of decomposing components is to isolate parts which are likely to change.

**See also:**
 * Coupling criterion [Structural Volatility](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-4-Structural-Volatility) of [ServiceCutter](https://servicecutter.github.io/)
 * [On the criteria to be used in decomposing systems into modules](https://dl.acm.org/citation.cfm?id=361623) by D. L. Parnas

In the Context Mapper DSL you can specify how often an aggregate changes with the _likelihoodForChange_ attribute.
See our page [aggregate documentation page](https://contextmapper.org/docs/aggregate/#likelihood-for-change) for more 
details.

## Goal
This Architectural Refactoring (AR) extracts all aggregates with a given volatility which is provided as input parameter
(RARELY, NORMAL or OFTEN) and moves those aggregates into a new bounded context. Thereby you are able to isolate aggregates with
a certain likelihood for change in one bounded context. This AR can be applied if your model exhibits a bounded context with 
aggregates which have different likelihoods for change.

**Inverse AR's:**
 * [AR-7: Merge Bounded Contexts](./../AR-7-Merge-Bounded-Contexts)

## Preconditions
 * The selected bounded context must contain **at least two aggregates**.
 * The aggregates of the selected bounded context must have **different likelihoods for change**.

## Input
 * One bounded context.
 
## Output
 * Another bounded context containing all the aggregates with the selected volatility.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context contains two aggregates with different likelihoods for change:
```
/* With a right-click on the 'CustomerSelfServiceContext' bounded context you can execute the 'Extract Aggregates by Volatility' 
 * refactoring. If you choose the volatility 'OFTEN', it will extract the volatile 'CustomerFrontend' aggregate and create a new bounded context for it.
 */
BoundedContext CustomerSelfServiceContext implements CustomerManagementDomain {
  type = APPLICATION
  domainVisionStatement = "This context represents a web application which allows the customer to login and change basic data records like the address."
  responsibilities = "AddressChange"
  implementationTechnology = "PHP Web Application"
  
  Aggregate CustomerFrontend {
    likelihoodForChange = OFTEN
    
    DomainEvent CustomerAddressChange {
      aggregateRoot
      
      - UserAccount issuer
      - Address changedAddress
    }
  }
  Aggregate Acounts {
    Entity UserAccount {
      aggregateRoot
      
      String username
      - Customer accountCustomer
    }
  }
}

```

### Output
Applying the AR **Extract Aggregates by Volatility** with the volatility parameter **OFTEN** produces another 
bounded context containing the _CustomerFrontend_ aggregate:
```
BoundedContext CustomerSelfServiceContext implements CustomerManagementDomain {
  domainVisionStatement = "This context represents a web application which allows the customer to login and change basic data records like the address."
  type = APPLICATION
  responsibilities = "AddressChange"
  implementationTechnology = "PHP Web Application"
  
  Aggregate Acounts {
    Entity UserAccount {
      aggregateRoot
      
      String username
      - Customer accountCustomer
    }
  }
}

/**
 * The extracted bounded context after applying 'Extract Aggregates by Volatility'
 * to 'example-input.cml'. The chosen volatility was 'OFTEN'.
 * 
 * You may want to change the name of newly created bounded contexts after applying refactorings.
 */
BoundedContext CustomerSelfServiceContext_Volatility_OFTEN {
  Aggregate CustomerFrontend {
    likelihoodForChange = OFTEN
    
    DomainEvent CustomerAddressChange {
      aggregateRoot
      
      - UserAccount issuer
      - Address changedAddress
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-4: Extract Aggregates by Volatility](https://contextmapper.org/docs/ar-extract-aggregates-by-volatility/)
