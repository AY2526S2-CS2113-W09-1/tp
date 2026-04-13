# SeanTLY23 - Project Portfolio Page

## Project: ItemTasker

ItemTasker is a desktop application used for managing stock-keeping units (SKUs) and their associated tasks efficiently. The user interacts with it using a CLI (Command Line Interface). It is written in Java and helps users streamline their inventory and task management workflows.

### Overview
I was primarily responsible for the **User Interface (Ui)** component, the physical warehouse visualization logic (**`viewmap`**), and the SKU health-tracking features (**`status`**). I also played a key role in refactoring the command handling architecture and maintaining the project's documentation standards.

Given below are my contributions to the project.

### Summary of Contributions

* **New Feature**: Implemented the **`viewmap`** command.
  * **What it does**: Generates a visual 3x3 grid in the terminal representing the physical warehouse layout. It maps SKU IDs to their specific grid coordinates (e.g., A1 to C3).
  * **Justification**: Warehouse managers need a spatial mental model of their inventory. This feature allows users to quickly identify occupied versus vacant storage slots without scrolling through text lists.
  * **Highlights**: Required implementing a mapping logic between the `Location` enum and a coordinate-based grid display, ensuring the CLI output remained aligned regardless of SKU ID length.

* **New Feature: Task Filtering & Sorting (`listtasks`)**
  * **What it does**: Allows users to filter tasks by SKU ID (**n/**) or Priority (**p/**), and sort tasks by physical distance from a chosen location (**l/**).
  * **Justification**: Helps users find specific tasks quickly or see what tasks are physically closest to them to save travel time.
  * **Highlights**: Implemented a Manhattan distance formula to calculate the distance between warehouse sectors for sorting.
* **New Feature: SKU Health Status (`status`)**
  * **What it does**: Shows a summary for SKUs, including completion percentage, pending high-priority tasks, and overdue counts.
  * **Justification**: Provides a high-level progress report so users don't have to manually count tasks.
  * **Highlights**: Created the **SKUStatusAnalyzer** to process task data and identify overdue items based on the current date.
* **Code contributed**: [RepoSense link](https://nus-cs2113-ay2526-s2.github.io/tp-dashboard/?search=seant&breakdown=true&sort=groupTitle%20dsc&sortWithin=title&since=2026-02-20T00%3A00%3A00&timeframe=commit&mergegroup=&groupSelect=groupByRepos&checkedFileTypes=docs~functional-code~test-code~other&filteredFileName=)

* **Enhancements implemented**:
  * Refactored the monolithic `CommandRunner` into specialized handlers (specifically co-implementing `ViewCommandHandler`), improving adherence to the **Single Responsibility Principle**.
  * Standardized all command output formats across the team to ensure a cohesive user experience.
  * Fixed UI rendering bugs where special characters or long SKU names caused the `viewmap` grid to misalign.

* **Contributions to the UG**:
  * Added documentation and examples for the `viewmap` and `status` commands.
  * Authored a new **FAQ entry** explaining how to use `viewmap` to identify available warehouse space before adding new SKUs.


* **Contributions to the DG**:
  * Authored the **UI Component Design** section, documenting the boundary pattern used to separate internal logic from terminal output.
  * Wrote the implementation details for the **View SKU Task** and **Status Analysis** features.
  * Created sequence diagrams for the distance-sorting and filtering logic.
* **Contributions to team-based tasks**:
  * Assisted in refactoring `ViewCommandHandler` to separate read-only logic from data-mutation logic.
  * * **Testing**: Wrote JUnit tests for **SKUStatusAnalyzer**, **ViewSKUTask**, and **ViewMap** to ensure the stats and sorting worked correctly for all cases.