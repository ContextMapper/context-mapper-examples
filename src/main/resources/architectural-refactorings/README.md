# Architectural Refactoring (AR) Examples

This folder contains input and ouput examples written in CML to illustrate the idea behind the [architectural refactorings][1] implemented by the Context Mapper tool. The refactorings can be executed with a right-click on the corresponding element in the editor (aggregate or bounded context) and choosing the AR in the _Context Mapper: Refactor_ context menu entry. The context menu shows only refactorings for which the selected model element fulfills the preconditions.

**Note (Formatting):** The execution of a refactoring in a CML file always formats the model according to our predefined formatting. You can format your models manually by using the Eclipse formatting shortcut (SHIFT-CTRL-F by default). If your file is not formatted or contains user-specific formattings, the execution of a refactoring will change the formatting accordingly.  

**Note (Root Element Order):** The execution of a refactoring in a CML file always _unparses_ the complete model by using the following order of elements on the root level:
 1. Context Map
 2. Bounded Contexts
 3. Domains
 4. Use Cases

If the elements in your CML file are not ordered correspondingly, the execution of a refactoring will **reorder** them. 

## AR-1: Split Aggregate by Entities
Splits an aggregate which contains multiple entities. Produces one aggregate per entity.

Example input: [split-aggregate-by-entities-input-example.cml](AR-1-Split-Aggregate-by-Entities/example-input.cml)

Example output: [split-aggregate-by-entities-output-example.cml](AR-1-Split-Aggregate-by-Entities/example-output.cml)

**Preconditions:** Aggregate must contain at least two entities.

## AR-2: Split Bounded Context by Use Cases
Splits a bounded context by grouping those aggregates together in one bounded context which are used by the same use case.

Example input: [split-bc-by-use-cases-input-example.cml](./split-bc-by-use-cases-input-example.cml)

Example output: [split-bc-by-use-cases-output-example.cml](./split-bc-by-use-cases-output-example.cml)

**Preconditions:** At least to aggregates within the selected bounded context which have different use cases.

## AR-3: Split Bounded Context by Owner
Splits a bounded context by grouping those aggregates together in one bounded context which maintained by the same owner.

Example input: [split-bc-by-owners-input-example.cml](./split-bc-by-owners-input-example.cml)

Example output: [split-bc-by-owners-output-example.cml](./split-bc-by-owners-output-example.cml)

**Preconditions:** At least to aggregates within the selected bounded context which belong to different owners.

## AR-4: Extract Aggregates by Volatility
Extracts all aggregates from a bounded context by a given volatility, or _likelihood for change_ (RARELY, NORMAL or OFTEN), and moves them to a separate context.
See [Structural Volatility](https://github.com/ServiceCutter/ServiceCutter/wiki/CC-4-Structural-Volatility) in the [ServiceCutter](https://github.com/ServiceCutter/ServiceCutter/wiki/Coupling-Criteria) coupling criteria catalog for more information and the idea behind this refactoring.

Example input: [extract-aggregates-by-volatility-input-example.cml](./extract-aggregates-by-volatility-input-example.cml)

Example output: [extract-aggregates-by-volatility-output-example.cml](./extract-aggregates-by-volatility-output-example.cml)

**Preconditions:** At least two aggregates with different values in the attribute _likelihoodForChange_ (RARELY, NORMAL, OFTEN). The bounded context must also contain some other aggregates, otherwise an extraction makes no sense.

## AR-5: Extract Aggregates by Cohesion
The user/architect may want to extract certain aggregates of a bounded context based on specific and individual non-functional requirement (NFR) criteria concerning the cohesion between bounded contexts. This refactoring allows manually select these aggregates and extract them to a new bounded context.

Example input: [extract-aggregates-by-cohesion-input-example.cml](./extract-aggregates-by-cohesion-input-example.cml)

Example output: [extract-aggregates-by-cohesion-output-example.cml](./extract-aggregates-by-cohesion-output-example.cml)

**Preconditions:** Bounded context must contain at least two aggregates.

## AR-6: Merge Aggregates
Allows you to merge two aggregates within a bounded context. Start the refactoring on one aggregate and a dialog will pop up, asking you for the second aggregate with which you want to merge.

Example input: [merge-aggregates-input-example.cml](./merge-aggregates-input-example.cml)

Example output: [merge-aggregates-output-example.cml](./merge-aggregates-output-example.cml)

**Preconditions:** You need at least two bounded contexts in your model to merge.

## AR-7: Merge Bounded Contexts
Allows you to merge two bounded contexts. Start the refactoring on one bounded context and a dialog will pop up, asking you for the second bounded context with which you want to merge.

Example input: [merge-bounded-contexts-input-example.cml](./merge-bounded-contexts-input-example.cml)

Example output: [merge-bounded-contexts-output-example.cml](./merge-bounded-contexts-output-example.cml)

**Preconditions:** You need at least two bounded contexts in your model to merge.

[1]: https://link.springer.com/article/10.1007%2Fs00607-016-0520-y
