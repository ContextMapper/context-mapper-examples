# Architectural Refactoring (AR) Examples

This folder contains input and ouput examples written in CML to illustrate the idea behind the [architectural refactorings][1] implemented by the Context Mapper tool. The refactorings can be executed with a right-click on the corresponding element in the editor (aggregate or bounded context) and choosing the AR in the _Context Mapper: Refactor_ context menu entry. The context menu shows only refactorings for which the selected model element fulfills the preconditions.

**Note (Formatting):** The execution of a refactoring in a CML file always formats the model according to our predefined formatting. You can format your models manually by using the Eclipse formatting shortcut (SHIFT-CTRL-F by default). If your file is not formatted or contains user-specific formattings, the execution of a refactoring will change the formatting accordingly.  

**Note (Root Element Order):** The execution of a refactoring in a CML file always _unparses_ the complete model by using the following order of elements on the root level:
 1. Context Map
 2. Bounded Contexts
 3. Domains
 4. Use Cases

If the elements in your CML file are not ordered correspondingly, the execution of a refactoring will **reorder** them. 

## AR: Split Aggregate by Entities
Splits an aggregate which contains multiple entities. Produces one aggregate per entity.

Example input: [split-aggregate-by-entities-input-example.cml](./split-aggregate-by-entities-input-example.cml)

Example output: [split-aggregate-by-entities-output-example.cml](./split-aggregate-by-entities-output-example.cml)

**Preconditions:** Aggregate must contain at least two entities.

## AR: Split Bounded Context by Use Cases
Splits a bounded context by grouping those aggregates together in one bounded context which are used by the same use case.

Example input: [split-bc-by-use-cases-input-example.cml](./split-bc-by-use-cases-input-example.cml)

Example output: [split-bc-by-use-cases-output-example.cml](./split-bc-by-use-cases-output-example.cml)

**Preconditions:** At least to aggregates within the selected bounded context which have different use cases.

## AR: Split Bounded Context by Owner
Splits a bounded context by grouping those aggregates together in one bounded context which maintained by the same owner.

Example input: [split-bc-by-owners-input-example.cml](./split-bc-by-owners-input-example.cml)

Example output: [split-bc-by-owners-output-example.cml](./split-bc-by-owners-output-example.cml)

**Preconditions:** At least to aggregates within the selected bounded context which belong to different owners.

## AR: Extract Aggregates which are Likely to Change
Extracts all aggregates from a bounded context which are likely to change (likelihoodForChange = OFTEN) and moves them to a separate context.

Example input: [extract-aggregates-likely-to-change-input-example.cml](./extract-aggregates-likely-to-change-input-example.cml)

Example output: [extract-aggregates-likely-to-change-output-example.cml](./extract-aggregates-likely-to-change-output-example.cml)

**Preconditions:** At least one aggregate with the attribute _likelihoodForChange_ set to _OFTEN_. The bounded context must also contain some other aggregates, otherwise an extraction makes no sense.

## AR: Extract Aggregates by NFR (Manual Selection)
The user/architect may want to extract certain aggregates of a bounded context based on specific and individual non-functional requirement (NFR) criteria. This refactoring allows manually select these aggregates and extract them to a new bounded context.

Example input: [extract-aggregates-by-nfr-input-example.cml](./extract-aggregates-by-nfr-input-example.cml)

Example output: [extract-aggregates-by-nfr-output-example.cml](./extract-aggregates-by-nfr-output-example.cml)

**Preconditions:** Bounded context must contain at least two aggregates.

## AR: Split Bounded Context by Duplicate Entity Name
As your bounded contexts develop you may find yourself in the situation that you have _two terms with different meanings_ within the ubiquitous language of your bounded context. This refactoring splits a bounded context if you have to aggregates which contains two such entities with the same name

Example input: [split-bc-by-duplicate-entity-input-example.cml](./split-bc-by-duplicate-entity-input-example.cml)

Example output: [split-bc-by-duplicate-entity-output-example.cml](./split-bc-by-duplicate-entity-output-example.cml)

**Preconditions:** The bounded context must contain two aggregates which contain two entities with the same name

## AR: Merge Bounded Contexts
Allows you to merge two bounded contexts. Start the refactoring on one bounded context and a dialog will pop up, asking you for the second bounded context with which you want to merge.

Example input: [merge-bounded-contexts-input-example.cml](./merge-bounded-contexts-input-example.cml)

Example output: [merge-bounded-contexts-output-example.cml](./merge-bounded-contexts-output-example.cml)

**Preconditions:** You need at least two bounded contexts in your model to merge.

[1]: https://link.springer.com/article/10.1007%2Fs00607-016-0520-y
