# AR-10 Change Shared Kernel to Partnership
This simple relationship refactoring changes a Shared Kernel relationship on a Context Map to a Partnership relationship.

## Summary
Our relationship refactorings allow the user/modeller to change the type of a relationship on a Context Map easily without manual work.
The symmetric relationships according to our [semantic model](/docs/language-model/), Shared Kernel and Partnership, are interchangeable without impacts
to the structure of the decomposition. This refactoring changes a Shared Kernel relationship to a Partnership relationship.
 
**Inverse AR:**
 * [AR-11: Change Partnership to Shared Kernel](./../AR-11-Change-Partnership-To-Shared-Kernel)
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The input Context Map:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  contains PolicyManagementContext
  contains DebtCollection

  /* With a right-click on the Shared Kernel relationship ([SK]<->[SK]) you can execute the 'Change to Partnership' 
   * refactoring. It will replace the Shared Kernel relationship below with a corresponding Partnership relationship
   * between the two Bounded Contexts.
   */
  PolicyManagementContext [SK]<->[SK] DebtCollection

}

BoundedContext PolicyManagementContext

BoundedContext DebtCollection
```

### Output
Applying the AR **Change Shared Kernel to Partnership** replaces the existing Shared Kernel relationship with a
Partnership relationship:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  contains PolicyManagementContext
  contains DebtCollection

  /* The new Partnership relationship after applying the 'Change Shared Kernel to Partnership' refactoring to the 
   * Shared Kernel within the 'example-input.cml' file:
   */
  PolicyManagementContext [P] <-> [P] DebtCollection

}

BoundedContext PolicyManagementContext

BoundedContext DebtCollection 
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-10 Change Shared Kernel to Partnership](https://contextmapper.org/docs/ar-change-shared-kernel-to-partnership/)
