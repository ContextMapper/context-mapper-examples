# AR-1: Split Aggregate by Entities
Splits an aggregate which contains multiple entities and produces one aggregate per entity.

## Context & Rationales
On the level of entities we typically try to group attributes or [nanoentities in the terminology of ServiceCutter](https://servicecutter.github.io/) 
together, which belong to the same identity and share a common lifecycle. Thereby we aim to reduce the coupling between the entities
and increase the cohesion within the entities.

 * **See also**: Coupling criterion [Identity and Lifecycle Commonality](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-1-Identity-and-Lifecycle-Commonality)
 of [ServiceCutter](https://servicecutter.github.io/).
 
The same approach can be applied on the aggregate level. The aggregates within one bounded context shall be structured in a way which
reduces coupling between the aggregates and increases the cohesion within them.

As your bounded context develops you may face the problem that an aggregate contains entities which exhibit an unsatisfying
cohesiveness. In such a case you may want to split your aggregate into multiple aggregates in order to improve coupling and cohesion.

## Goal
This Architectural Refactoring (AR) splits an aggregate and creates one aggregate for each entity. This AR can be applied when 
the entities within an aggregate exhibit unsatisfying cohesiveness and you decide to create multiple aggregates for the single 
entities.

**Inverse AR's:**
 * [AR-6: Merge Aggregates](./../AR-6-Merge-Aggregates)

## Preconditions
 * The input aggregate must contain **at least two entities**.

## Input
 * The aggregate which shall be split.
 
## Output
 * Multiple aggregates which contain one entity each.
 * All entities become **aggregate roots** within their own aggregates.
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The following bounded context contains one aggregate with two entities:
```
BoundedContext CustomerManagementContext {
  type = FEATURE
  domainVisionStatement = "The customer management context is responsible for managing all the data of the insurance companies customers."
  implementationTechnology = "Java, JEE Application"
  responsibilities = "Customers, Addresses"

  /* With a Right-Click on the 'Customers' aggregate you can call the 'Split Aggregate by Entities' refactoring in the 
   * 'Context Mapper: Refactor' context menu. The refactoring will create a new aggregate and move one of the two entities 
   * to the new aggregate (see the result in the 'split-aggregate-by-entities-output-example.cml' file).
   */  
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
  }
}
```

### Output
Applying the AR **Split Aggregate by Entities** produces two aggregates, one for each entity:
```
BoundedContext CustomerManagementContext {
  domainVisionStatement = "The customer management context is responsible for managing all the data of the insurance companies customers."
  responsibilities = "Customers, Addresses" implementationTechnology = "Java, JEE Application"
  Aggregate Customers {
    Entity Address {
      aggregateRoot
      
      String street
      int postalCode
      String city
    }
  }
  /* The newly created aggregate after applying 'Split Aggregate by Entities' on the aggregate in the input file 
   * 'example-input.cml'.
   * 
   * Note that the refactoring does not produce meaningful aggregate names. You can use the 'Rename Element' 
   * refactoring (SHIFT-ALT-R) to rename the new aggregate.
   */
  Aggregate NewAggregate1 {
    Entity Customer {
      aggregateRoot
      
      - SocialInsuranceNumber sin
      String firstname
      String lastname
      - List<Address> addresses
    }
  }
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-1: Split Aggregate by Entities](https://contextmapper.org/docs/ar-split-aggregate-by-entities/)
