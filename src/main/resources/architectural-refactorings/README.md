# Architectural Refactoring (AR) Examples

This folder contains input and ouput examples written in CML to illustrate the idea behind the [Architectural Refactorings (ARs)][1] 
implemented by the Context Mapper tool. The refactorings can be executed with a right-click on the corresponding element in 
the editor (aggregate or bounded context) and choosing the AR in the _Context Mapper: Refactor_ context menu entry. 
The context menu shows only refactorings for which the selected model element fulfills the preconditions.

You find an overview table with all ARs below. Within the sub-folders of this directory you find detailed descriptions and the
code samples for each AR:

 * [AR-1: Split Aggregate by Entities](./AR-1-Split-Aggregate-by-Entities)
 * [AR-2: Split Bounded Context by Use Cases](./AR-2-Split-Bounded-Context-by-Use-Cases)
 * [AR-3: Split Bounded Context by Owner](./AR-3-Split-Bounded-Context-by-Owner)
 * [AR-4: Extract Aggregates by Volatility](./AR-4-Extract-Aggregates-by-Volatility)
 * [AR-5: Extract Aggregates by Cohesion](./AR-5-Extract-Aggregates-by-Cohesion)
 * [AR-6: Merge Aggregates](./AR-6-Merge-Aggregates)
 * [AR-7: Merge Bounded Contexts](./AR-7-Merge-Bounded-Contexts)

You can also find the ARs in our [documentation page](https://contextmapper.github.io/docs/architectural-refactorings/).

## AR Overview
| Name                                                                                              | Subject         | Description                                                                                                                                                     | Input              | Output             |
|---------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|--------------------|
| [AR-1: Split Aggregate by Entities](./AR-1-Split-Aggregate-by-Entities)                           | Aggregate       | Splits an aggregate which contains multiple entities and produces one aggregate per entity.                                                                     | 1 Aggregate        | n Aggregates       |
| [AR-2: Split Bounded Context by Use Cases<sup>1</sup>](./AR-2-Split-Bounded-Context-by-Use-Cases) | Bounded Context | Splits a bounded context by grouping those aggregates together into one bounded context which are used by the same use case(s).                                 | 1 Bounded Context  | n Bounded Contexts |
| [AR-3: Split Bounded Context by Owner<sup>1</sup>](./AR-3-Split-Bounded-Context-by-Owner)         | Bounded Context | Splits a bounded context by grouping those aggregates together into one bounded context which belong to the same team.                                          | 1 Bounded Context  | n Bounded Contexts |
| [AR-4: Extract Aggregates by Volatility](./AR-4-Extract-Aggregates-by-Volatility)                 | Bounded Context | Extracts all aggregates from a bounded context by a given volatility, or likelihood for change (RARELY, NORMAL or OFTEN), and moves them to a separate context. | 1 Bounded Context  | 2 Bounded Contexts |
| [AR-5: Extract Aggregates by Cohesion](./AR-5-Extract-Aggregates-by-Cohesion)                     | Bounded Context | Extracts a set of aggregates which are chosen by certain cohesion criteria and moves them to a separate bounded context.                                        | 1 Bounded Context  | 2 Bounded Contexts |
| [AR-6: Merge Aggregates](./AR-6-Merge-Aggregates)                                                 | Aggregate       | Merges two aggregates within a bounded context together to one aggregate.                                                                                       | 2 Aggregates       | 1 Aggregate        |
| [AR-7: Merge Bounded Contexts](./AR-7-Merge-Bounded-Contexts)                                     | Bounded Context | Merges two bounded contexts together. The result is one bounded context containing all the aggregates of the two input boundedcontexts.                         | 2 Bounded Contexts | 1 Bounded Context  |

<sup>1</sup>: An aggregate in CML can be used by **multiple** use cases and is owned by **one** owner (team).

## Hints
* **Split** vs. **Extract**:
  * The ARs which **split** the subject create n new elements of the type of the subject, one for each child element by which 
    the AR splits. For example: _Split Bounded Context by Owner_ creates n new bounded contexts, one for each aggregate owner (team).
  * The ARs which **extract** in comparison, create only one new element of the subjects type. An extraction moves a set of child
    elements to the newly created element of the subjects type. For example: _Extract Aggregates by Volatility_ creates one new
    bounded context and moves a specific set of aggregates to this new bounded context.
* **Note (Formatting):** The execution of a refactoring in a CML file always formats the model according to our predefined formatting. You can format your models manually by using the Eclipse formatting shortcut (SHIFT-CTRL-F by default). If your file is not formatted or contains user-specific formattings, the execution of a refactoring will change the formatting accordingly.  
* **Note (Root Element Order):** The execution of a refactoring in a CML file always _unparses_ the complete model by using the following order of elements on the root level:
  1. Context Map
  2. Bounded Contexts
  3. Domains
  4. Use Cases

  If the elements in your CML file are not ordered correspondingly, the execution of a refactoring will **reorder** them. 

[1]: https://link.springer.com/article/10.1007%2Fs00607-016-0520-y
