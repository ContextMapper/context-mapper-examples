# AR-7 Merge Bounded Contexts
Merges two bounded contexts together. The result is one bounded context containing all the aggregates of the two input bounded
contexts.

## Context & Rationales
By decomposing a system into multiple bounded contexts we aim for loose coupling between the bounded context and a high cohesion 
within them. However, sometimes a decomposition may be too fine-granular and merging bounded contexts with a high
coupling together improves the cohesion within the corresponding resulting bounded context.

## Goal
This Architectural Refactoring (AR) merges two bounded contexts together. The resulting bounded context contains all aggregates
of the two input bounded contexts. It can be applied if two bounded context are tightly coupled and the aggregates somehow
belong together. This may improve the cohesion within the resulting bounded context.

**Notes:**
 * By applying this AR multiple times you may end with one single Bounded Context and an empty Context Map (no relationships).
 
**Inverse AR's:**
 * [AR-4: Extract Aggregates by Volatility](./../AR-4-Extract-Aggregates-by-Volatility)
 * [AR-5: Extract Aggregates by Cohesion](./../AR-5-Extract-Aggregates-by-Cohesion)
 * [AR-2: Split Bounded Context by Use Cases](./../AR-2-Split-Bounded-Context-by-Use-Cases) (may need multiple merges to completely revert)
 * [AR-3: Split Bounded Context by Owner](./../AR-3-Split-Bounded-Context-by-Owner) (may need multiple merges to completely revert)

## Preconditions
 * Your model needs **at least two bounded contexts** to merge.

## Input
 * Two bounded contexts.
 
## Output
 * One bounded context containing all aggregates of the two input bounded contexts.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
Two input bounded contexts:
```
/* With a right-click on the 'CustomerManagementContext' (or one of the other contexts, as you wish) 
 * bounded context you can execute the 'Merge Bounded Contexts' refactoring. A dialog will show up and ask you with 
 * which other bounded context you want to merge. Choose a second bounded context and the refactoring will merge them.
 */
BoundedContext CustomerManagementContext implements CustomerManagementDomain {
  type = FEATURE
  domainVisionStatement = "The customer management context is responsible for managing all the data of the insurance companies customers."
  implementationTechnology = "Java, JEE Application"
  responsibilities = "Customers, Addresses"
  
  Aggregate Customers {
    Entity Customer {
      aggregateRoot
      
      - SocialInsuranceNumber sin
      String firstname
      String lastname
      - List<Address> addresses
    }
    Entity Address {
      String street
      int postalCode
      String city
    }
    ValueObject SocialInsuranceNumber {
      String sin key
    }
  }
}

BoundedContext CustomerSelfServiceContext implements CustomerManagementDomain {
  type = APPLICATION
  domainVisionStatement = "This context represents a web application which allows the customer to login and change basic data records like the address."
  responsibilities = "AddressChange"
  implementationTechnology = "PHP Web Application"
  
  Aggregate CustomerFrontend {
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
Applying the AR **Merge Bounded Contexts** merges all aggregates of the _CustomerSelfServiceContext_ bounded context
into the _CustomerManagementContext_ bounded context:
```
/**
 * The merged bounded context after applying 'Merge Bounded Contexts' to 'example-input.cml'.
 * We selected the 'CustomerSelfServiceContext' context as second bounded context.
 */
BoundedContext CustomerManagementContext implements CustomerManagementDomain {
  domainVisionStatement = "The customer management context is responsible for managing all the data of the insurance companies customers."
  responsibilities = "Customers, Addresses" , "AddressChange" 
  implementationTechnology = "Java, JEE Application"
  Aggregate Customers {
    Entity Customer {
      aggregateRoot
      
      - SocialInsuranceNumber sin
      String firstname
      String lastname
      - List<Address> addresses
    }
    Entity Address {
      String street
      int postalCode
      String city
    }
    ValueObject SocialInsuranceNumber {
      String sin key
    }
  }
  Aggregate CustomerFrontend {
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

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-7 Merge Bounded Contexts](https://contextmapper.org/docs/ar-merge-bounded-contexts/)
