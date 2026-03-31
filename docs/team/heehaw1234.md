# heehaw1234 - Project Portfolio Page

## Project: ItemTasker

ItemTasker is a desktop application used for managing stock-keeping units (SKUs) and their associated tasks efficiently. The user interacts with it using a CLI (Command Line Interface). It is written in Java and helps users streamline their inventory and task management workflows.

Given below are my contributions to the project.

### Summary of Contributions

* **New Feature**: Added the core `SKUTask` and `SKUTaskList` models.
  * **What it does**: Establishes the foundational data structures for the application, representing individual stock keeping unit tasks and managing the central collection of all tasks. 
  * **Justification**: This feature forms the backbone of the application's data layer, enabling the creation, retrieval, and tracking of tasks and their associated priority states.
  * **Highlights**: This required careful consideration of the fields, priority states, and overall class responsibility to ensure other components (like storage and UI) could seamlessly interact with the task data.

* **New Feature**: Implemented the `find` command data-matching logic in `ViewCommandHandler`.
  * **What it does**: Provides a robust search mechanism that allows users to filter tasks by SKU IDs, descriptions, and specific task indices. It parses multi-parameter search conditions and safely iterates over the inventory.
  * **Justification**: Finding specific tasks is crucial for inventory scaling. The function was specifically designed with the Single Level of Abstraction Principle (SLAP) in mind, breaking down complex filtering validations across `handleFind`, `searchTasks`, and nested SKU traversal methods.
  * **Highlights**: Navigating edge cases—like preventing out-of-bounds exceptions when searching arbitrary indices across differently sized SKU inventories—required careful loop tracking and error handling. It elegantly isolates reading/filtering logic cleanly within the `ViewCommandHandler`.

* **New Feature**: Co-Implemented `ViewCommandHandler`.
  * **What it does**: Handles commands related to reading, sorting, and displaying tasks to the user. It isolates view-specific logic away from execution logic.
  * **Justification**: Increases the cohesiveness of the system. By splitting the logic from a monolithic runner into specialized handlers, the code obeys the Single Responsibility Principle, making view modifications isolated and sustainable.

* **Code contributed**: [RepoSense link](https://nus-cs2113-ay2526-s2.github.io/tp-dashboard/?search=heehaw1234&breakdown=true&sort=groupTitle%20dsc&sortWithin=title&since=2026-02-20T00%3A00%3A00&timeframe=commit&mergegroup=&groupSelect=groupByRepos&checkedFileTypes=docs~functional-code~test-code~other&filteredFileName=)

* **Enhancements to existing features**:
  * Set up logging infrastructure via `ItemTaskerLogger` to debug file handler states and capture runtime output.
  * Wrote comprehensive JUnit tests for `SKUTaskTest`, `SKUTaskListTest`, and `FindCommandTest` to verify core operations and edge cases in parsing and data storage.

* **Documentation**:
  * **User Guide**:
    * Added FAQ entries addressing application logging locations for bug reporting (`itemtasker.log`) and explaining the software's scalability constraints regarding SKU/task capacity limits.
    * Assisted in aligning documentation to accurately reflect actual Command Line commands for `ItemTasker` following the project's refactoring from boilerplate AddressBook commands.
  * **Developer Guide**:
    * Authored the implementation details and specifications for the `SKUTask` component, ensuring it cleanly documented the system's class structures and logic flows using AddressBook-Level 3 formatting.
    * Authored **Appendix B (Target User Profile)** and **Appendix C (Non-Functional Requirements)**, establishing the intended user constraints, system performance expectations, environment boundaries, and data management scoping.
    * Created and integrated multiple PlantUML diagrams (`skutask-architecture.puml`, `addTaskSequence.puml`, `deleteTaskSequence.puml`, `settersSequence.puml`, `gettersSequence.puml`) to visually represent the interaction between the `Ui`, `TaskCommandHandler`, and `CommandHelper`.
    * Kept architectural diagrams up to date by tracking the transition of logic from `CommandRunner` to `TaskCommandHandler` & `ViewCommandHandler`.

* **Community**:
  * Diligently managed GitHub pull request alignments and merged documentation refactors to ensure the repository remains functional.
