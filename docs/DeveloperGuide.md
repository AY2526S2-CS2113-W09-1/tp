# Developer Guide

## Acknowledgements

{list here sources of all reused/adapted ideas, code, documentation, and third-party libraries -- include links to the original source as well}

## Design


## Implementation

### Add / Delete SKU Feature

#### Implementation Details
### Add / Delete SKU Feature

#### Implementation Details
The Add and Delete SKU mechanism is facilitated by the `CommandRunner` component, which manages the application's core state through a single primary data structure: the `SKUList`. Following strict Object-Oriented encapsulation, there are no external maps; each `SKU` inherently manages its own `SKUTaskList`.

The operations are exposed and handled internally via the following methods:
* `CommandRunner#handleAddSku(ParsedCommand)` — Validates constraints and delegates to `SKUList` to instantiate a new `SKU` (which automatically initializes its own internal task list).
* `CommandRunner#handleDeleteSku(ParsedCommand)` — Removes the `SKU` from the inventory, which inherently purges all tasks associated with it.

Given below is an example usage scenario demonstrating how the Add SKU mechanism behaves at each step.

**Step 1.** The user executes `addsku n/PALLET-A l/A1`. The `Ui` reads the input, and the `Parser` extracts the command word and maps the arguments `n/` to `PALLET-A` and `l/` to `A1` into a `ParsedCommand` object.

**Step 2.** The `CommandRunner#run()` method receives this `ParsedCommand`. Recognizing the `addsku` command word, it routes execution to `CommandRunner#handleAddSku()`.

**Step 3.** `handleAddSku()` parses the location string into a `Location` enum. It then calls `findSku("PALLET-A")` to iterate through the `SKUList`. Finding no duplicates, it proceeds with the insertion.

![System Memory State Steps 1 to 3](plantUML/add-delete-sku/add-sku-step1-3.png)

**Step 4.** The `SKUList#addSKU()` method is invoked. This method calls the `SKU` constructor, instantiating a new `SKU` object. During instantiation, the `SKU` automatically generates an empty `SKUTaskList` for itself. The `SKU` is then appended to the internal `ArrayList`.

![System Memory State Step 4](plantUML/add-delete-sku/add-sku-step4.png)

**Step 5.** Back in `handleAddSku()`, execution completes successfully. Control returns to the `Ui` to print the success message. The system's memory state now contains the new `SKU`, fully equipped to accept tasks without requiring any external mapping.

![System Memory State Step 5](plantUML/add-delete-sku/add-sku-step5.png)

*Note: The `deletesku` command operates by simply calling `SKUList#deleteSKU()` to remove the object from the array. Due to encapsulation, dropping the `SKU` object automatically garbage-collects its associated `SKUTaskList`, preventing memory leaks.*

The following sequence diagram shows the flow of adding a SKU:
![Add SKU Sequence Diagram](plantUML/add-delete-sku/add-sku-sequence.png)


The following class diagram shows the architecture:
![Add SKU Class Diagram](plantUML/add-delete-sku/add-sku-architecture.png)

#### Design considerations:

**Aspect: How SKU tasks are stored and mapped to their parent SKU:**
* **Current Implementation:** Require all task operations to access the `SKUTaskList` directly through the `SKU` object residing in the `SKUList`.
  * *Pros:* High cohesion and strict encapsulation. A SKU is solely responsible for its own tasks. Memory overhead is reduced, and state mutations are safer as there is no need to synchronize deletions across multiple data structures.
  * *Cons:* Slightly slower lookup times, as finding a task requires iterating through the `SKUList` to locate the parent SKU first (O(n) complexity).
* **Alternative:** Maintain a `HashMap<String, SKUTaskList>` inside the `CommandRunner` to map SKU IDs to their tasks.
  * *Pros:* Fast, O(1) time complexity when looking up tasks for a specific SKU during filtering or task addition.
  * *Cons:* Severe data duplication and poor encapsulation. This requires the `CommandRunner` to juggle references and manually synchronize deletions across two separate data structures, leading to an architecture prone to orphaned tasks if not correctly synced.


## Appendix A: Product Scope

### Target user profile

{Describe the target user profile}

### Value proposition

{Describe the value proposition: what problem does it solve?}

## Appendix B: User Stories

|Version| As a ... | I want to ... | So that I can ...|
|--------|----------|---------------|------------------|
|v1.0|new user|see usage instructions|refer to them when I forget how to use the application|
|v2.0|user|find a to-do item by name|locate a to-do without having to go through the entire list|

## Appendix C: Non-Functional Requirements

{Give non-functional requirements}

## Appendix D: Glossary

* *glossary item* - Definition

## Appendix E: Instructions for Manual Testing

{Give instructions on how to do a manual product testing e.g., how to load sample data to be used for testing}
