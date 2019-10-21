# AR-6: Merge Aggregates
Merges two aggregates within a bounded context together to one aggregate.

## Context & Rationales
On the level of entities we typically try to group attributes or [nanoentities in the terminology of ServiceCutter](https://servicecutter.github.io/) 
together, which belong to the same identity and share a common lifecycle. Thereby we aim to reduce the coupling between the entities
and increase the cohesion within the entities.

 * **See also**: Coupling criterion [Identity and Lifecycle Commonality](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-1-Identity-and-Lifecycle-Commonality)
 of [ServiceCutter](https://servicecutter.github.io/).
 
The same approach can be applied on the aggregate level. The aggregates within one bounded context shall be structured in a way which
reduces coupling between the aggregates and increases the cohesion within them.

During the evolution of your bounded context you may find multiple aggregates containing entities which belong together (for
example because they share a common lifecycle) and merging the aggregates together improves coupling and cohesion.

## Goal
This Architectural Refactoring (AR) merges two aggregates in a bounded context together into one aggregate. It can be applied
in a situation where the entities in the two aggregates somehow belong together and a merge of the aggregates improves the 
coupling and cohesion. 

**Inverse AR's:**
 * [AR-1: Split Aggregate by Entities](./../AR-1-Split-Aggregate-by-Entities)

## Preconditions
 * Your bounded context must contain **at least two aggregates** which can be merged.

## Input
 * Two aggregates which belong to the same bounded context.
 
## Output
 * One aggregate containing all objects (entities, value objects, etc.) of the two input aggregates.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context contains two aggregates:
```
/* With a right-click on the 'Customers' aggregate (or on the 'Addresses' aggregate, as you wish) 
 * you can execute the 'Merge Aggregates' refactoring. A dialog will show up and ask you with 
 * which other aggregate you want to merge. Choose the other aggregate and the refactoring will merge them.
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
    ValueObject SocialInsuranceNumber {
      String sin key
    }
  }
  Aggregate Addresses {
    Entity Address {
      String street
      int postalCode
      String city
    }
  }
}
```

### Output
Applying the AR **Merge Aggregates** with the aggregate selection **[ Customers, Addresses ]** 
merges the objects of both aggregates into the _Customers_ aggregate:
```
/* 
 * The resulting bounded context after applying 'Merge Aggregates' to the file 'example-input.cml'.
 * The 'Addresses' aggregate has been merged into the 'Customers' aggregate.
 */
BoundedContext CustomerManagementContext implements CustomerManagementDomain {
  domainVisionStatement = "The customer management context is responsible for managing all the data of the insurance companies customers."
  responsibilities = "Customers, Addresses" 
  implementationTechnology = "Java, JEE Application"
  Aggregate Customers {
    Entity Customer {
      aggregateRoot
      - SocialInsuranceNumber sin
      String firstname
      String lastname
      - List<Address> addresses
    }
    ValueObject SocialInsuranceNumber {
      String sin key
    }
    Entity Address {
      String street
      int postalCode
      String city
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-6: Merge Aggregates](https://contextmapper.org/docs/ar-merge-aggregates/)
