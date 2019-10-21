# AR-5: Extract Aggregates by Cohesion
Extracts a set of aggregates which are chosen by certain cohesion criteria and moves them to a separate bounded context.

## Context & Rationales
By decomposing a system into multiple bounded contexts we aim for loose coupling between the bounded context and a high cohesion 
within them. There are many different approaches and different coupling criteria by which the software architect may want
to decompose a system into components.

**See also:**
 * [Coupling criteria catalog](https://github.com/ServiceCutter/ServiceCutter/wiki/Coupling-Criteria) of [ServiceCutter](https://servicecutter.github.io/)

## Goal
This Architectural Refactoring (AR) allows to manually select the aggregates which should be extracted by any coupling criteria
or Non-functional Requirements (NFR). The goal of this AR is to isolate a set of aggregates within a new bounded context by
an individual criterion.

**Inverse AR's:**
 * [AR-7: Merge Bounded Contexts](./../AR-7-Merge-Bounded-Contexts)

## Preconditions
 * The selected bounded context must contain **at least two aggregates**.

## Input
 * One bounded context.
 * A selection of aggregates which shall be extracted to a new bounded context.
 
## Output
 * A new bounded context containing the selected aggregates.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context contains three aggregates:
```
/* With a right-click on the 'PolicyManagementContext' bounded context you can execute the 'Extract Aggregates by Cohesion' 
 * refactoring. A dialog will pop up which allows you to select the aggregates to be extracted. You can further specify
 * the name of the new bounded context. For example: As architect you may want to extract the 'Offers' aggregate due
 * to other differing availability requirements.
 */
BoundedContext PolicyManagementContext implements PolicyManagementDomain {
  type = FEATURE
  domainVisionStatement = "This bounded context manages the contracts and policies of the customers."
  responsibilities = "Offers, Contracts, Policies"
  implementationTechnology = "Java, Spring App"
  
  Aggregate Offers {
    Entity Offer {
      aggregateRoot
      
      int offerId
      - Customer client
      - List<Product> products
      BigDecimal price
    }
  }
  Aggregate Products {
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
Applying the AR **Extract Aggregates by Cohesion** with the aggregate selection **[ Offers ]** produces 
a new bounded context with the _Offers_ aggregate:
```
BoundedContext PolicyManagementContext implements PolicyManagementDomain {
  domainVisionStatement = "This bounded context manages the contracts and policies of the customers."
  responsibilities = "Offers, Contracts, Policies"
  implementationTechnology = "Java, Spring App"
  
  Aggregate Products {
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
 * New bounded context after applying 'Extract Aggregates by Cohesion' to 'example-input.cml'
 * with the following parameters:
 *  - New bounded context name: 'SalesBoundedContext'
 *  - Selected aggregates: 'Offers'
 */
BoundedContext SalesBoundedContext {
  Aggregate Offers {
    Entity Offer {
      aggregateRoot
      
      int offerId
      - Customer client
      - List<Product> products
      BigDecimal price
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-5: Extract Aggregates by Cohesion](https://contextmapper.org/docs/ar-extract-aggregates-by-cohesion/)
