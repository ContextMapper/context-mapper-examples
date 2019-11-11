# AR-11 Change Partnership to Shared Kernel
This simple relationship refactoring changes a Partnership relationship on a Context Map to a Shared Kernel relationship.

## Summary
Our relationship refactorings allow the user/modeller to change the type of a relationship on a Context Map easily without manual work.
The symmetric relationships according to our [semantic model](/docs/language-model/), Shared Kernel and Partnership, are interchangeable without impacts
to the structure of the decomposition. This refactoring changes a Partnership relationship to a Shared Kernel relationship.
 
**Inverse AR:**
 * [AR-10: Change Shared Kernel to Partnership](./../AR-10-Change-Shared-Kernel-To-Partnership)
 
## Example
The following two CML snippets show an example _input_ and _output_ illustrating how this AR works.

### Input
The input Context Map:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  contains PolicyManagementContext
  contains RiskManagementContext

  /* With a right-click on the Partnership relationship ([P]<->[P]) you can execute the 'Change to Shared Kernel' 
   * refactoring. It will replace the Partnership relationship below with a corresponding Shared Kernel relationship
   * between the two Bounded Contexts.
   */
  RiskManagementContext [P]<->[P] PolicyManagementContext

}

BoundedContext PolicyManagementContext

BoundedContext RiskManagementContext
```

### Output
Applying the AR **Change Partnership to Shared Kernel** replaces the existing Partnership relationship with a
Shared Kernel relationship:
```
ContextMap InsuranceContextMap {
  type = SYSTEM_LANDSCAPE
  state = TO_BE
  contains PolicyManagementContext
  contains RiskManagementContext

  /* The new Shared Kernel relationship after applying the 'Change Partnership to Shared Kernel' refactoring to the 
   * Partnership within the 'example-input.cml' file:
   */
  RiskManagementContext [SK] <-> [SK] PolicyManagementContext

}

BoundedContext PolicyManagementContext

BoundedContext RiskManagementContext
```

### Example Sources
 * Example input source: [example-input.cml](./example-input.cml)
 * Example output source: [example-output.cml](./example-output.cml)
 
## Further documentation
 * Context Mapper [Architectural Refactorings (ARs)](https://contextmapper.org/docs/architectural-refactorings/)
 * [AR-11 Change Partnership to Shared Kernel](https://contextmapper.org/docs/ar-change-partnership-to-shared-kernel/)
