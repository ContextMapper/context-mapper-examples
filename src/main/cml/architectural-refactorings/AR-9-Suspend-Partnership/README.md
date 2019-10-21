# AR-9 Suspend Partnership
Provides different approaches to suspend a Partnership relationship.

## Context & Rationales
The Partnership pattern describes a close relationship where two development teams are interdependent. For some reason they can
only succeed or fail together. New developments and releases must be coordinated between the teams. However, this requires a lot
of coordination and communication between the teams and in some situations it might be beneficial to suspend such a partnership 
in order to increase team autonomy.

## Goal
This AR provides three strategies to suspend a Partnership relationship. Each strategy fulfills the goal to remove the partnership
relationship and replace it with another strategy how the two Bounded Contexts depend on each other. The strategies are:

 * **a) Merge the two Bounded Contexts:**
   
   Since the two teams have to work very closely together, a solution might be to merge the teams and see them as one single Bounded Context.
   This strategy basically calls the [AR-7 Merge Bounded Contexts](./../AR-7-Merge-Bounded-Contexts) refactoring to merge the two contexts.
   
 * **b) Extract a new Bounded Context for commonalities and establish upstream-downstream relationships:**
 
   The interdependence may come from common parts within the domain model or APIs which are maintained by both teams. In such a case it might 
   be a solution to extract common parts to a new Bounded Context. A new team may maintain these parts an offer corresponding APIs which
   can be used by the existing Bounded Contexts. This strategy extracts a new Bounded Context and creates two upstream-downstream
   relationships between the new and the two existing Bounded Contexts.
   
 * **c) Simply replace the Partnership with an upstream-downstream relationship:**
 
   Another solution might be that one of the two teams takes the lead regarding common parts or APIs. Decisions regarding changes on these
   common parts are only done by this leading team. All parts which both contexts depend on are moved to the leading context. Thus, the
   dependency becomes unidirectional. This strategy replaces the Partnership relationship with an upstream-downstream relationship. If you
   select this strategy you have to define which Bounded Context becomes the upstream context.
 
## Preconditions
 * Your model needs **at least two bounded contexts** which are in a **Partnership** relationship.

## Input
 * The Partnership relationship.
 
## Output
The output of this AR depends on the selected mode:
 * a) One (merged) bounded context containing all aggregates of the two input bounded contexts.
 * b) A new Bounded Context for commonalities and two new upstream-downstream relationships between the new and the two existing Bounded Context.
 * c) The same model but the Partnership relationship will be replaced with an upstream-downstream relationship.
 
## Example
The following CML snippets show an example _input_ and the corresponding _outputs_ for all three modes, illustrating how this AR works.

### Input
The input Context Map:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  
  contains PolicyManagementContext
  contains RiskManagementContext

  /* With a right-click on the Partnership relationship ([P]<->[P]) you can execute the 'Suspend Partnership' 
   * refactoring. On a dialog you can then choose between three modes how to suspend the partnership:
   * a) Merge the two Bounded Contexts (executes 'AR-7 Merge Bounded Contexts').
   * b) Extract a new Bounded Context for commonalities and establish upstream-downstream relationships between
   *    the new and the existing two Bounded Contexts.
   * c) Simply replace the Partnership relationship with an upstream-downstream relationship (in this case
   *    you have to choose which Bounded Context becomes upstream context).
   */
  RiskManagementContext [P]<->[P] PolicyManagementContext {
    implementationTechnology = "RabbitMQ"
  }

}

BoundedContext PolicyManagementContext {
  /* ... */
}

BoundedContext RiskManagementContext {
  /* ... */
}
```

### Output for "a) Merge the two Bounded Contexts":
Applying the AR **Suspend Partnership** with the mode "a) Merge the two Bounded Contexts" merges the two
Bounded Contexts and therefore removes the relationship between them:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  
  contains RiskManagementContext
  
  /* Since the AR merged the two Bounded Context, the relationship has been removed. */
}

/* The merged Bounded Context contains all Aggregates of both contexts now.  */
BoundedContext RiskManagementContext {
  /* ... */
}
```

### Output for "b) Extract a new Bounded Context for commonalities and establish upstream-downstream relationships":
Applying the AR **Suspend Partnership** with the mode "b) Extract a new Bounded Context for commonalities and establish 
upstream-downstream relationships" creates a new Bounded Context and two new upstream-downstream relationships between
the new and the existing Bounded Contexts:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  
  contains PolicyManagementContext
  contains RiskManagementContext
  contains RiskManagementContext_PolicyManagementContext_Partnership

  /* New upstream-downstream relationships between the new and the existing two Bounded Contexts: */

  RiskManagementContext_PolicyManagementContext_Partnership [ U ] -> [ D ] RiskManagementContext

  RiskManagementContext_PolicyManagementContext_Partnership [ U ] -> [ D ] PolicyManagementContext

}

BoundedContext PolicyManagementContext {
  /* ... */
}

BoundedContext RiskManagementContext {
  /* ... */
}

/* The new Bounded Context created by the 'Suspend Partnership' refactoring:
 * (can be renamed with the 'Rename Element' refactoring)
 */
BoundedContext RiskManagementContext_PolicyManagementContext_Partnership
```

### Output for "c) Simply replace the Partnership with an upstream-downstream relationship":
Applying the AR **Suspend Partnership** with the mode "c) Simply replace the Partnership with an upstream-downstream 
relationship" replaces the Partnership relationship with a new upstream-downstream relationship:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  
  contains PolicyManagementContext
  contains RiskManagementContext

  /* The new upstream-downstream relationship replacing the original Partnership relationship: */
  
  PolicyManagementContext [ U ] -> [ D ] RiskManagementContext

}

BoundedContext PolicyManagementContext {
  /* ... */
}

BoundedContext RiskManagementContext {
  /* ... */
}
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source for mode a): [example-output-a.cml](./example-output-a.cml)
 * Example output source for mode b): [example-output-b.cml](./example-output-b.cml)
 * Example output source for mode c): [example-output-c.cml](./example-output-c.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-9 Suspend Partnership](https://contextmapper.org/docs/ar-suspend-partnership/)
