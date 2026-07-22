# Epics and Stories

## MVP

- Epic: Task Data Management
  - Story: Preserve task titles and completion status
    - Acceptance Criteria: Existing task titles and completed status remain available and unchanged.
    - Technical Requirements: Preserve the existing task title and completion-status fields in the frontend task model and API contract.
    - Technical Requirements: Add regression tests covering title and completion-status preservation.
  - Story: Add optional due dates to tasks
    - Acceptance Criteria: A task can be created and used without a due date.
    - Acceptance Criteria: A valid due date is stored in `YYYY-MM-DD` format.
    - Acceptance Criteria: An invalid due date is treated as absent and does not prevent the task from being used.
    - Technical Requirements: Represent `dueDate` as an optional task field and normalize valid values to `YYYY-MM-DD`.
    - Technical Requirements: Validate due dates at the task data boundary and convert invalid values to absent values.
    - Technical Requirements: Add unit tests for omitted, valid, and invalid due dates.
  - Story: Add task priorities
    - Acceptance Criteria: A task priority can be `P1`, `P2`, or `P3`.
    - Acceptance Criteria: A task defaults to `P3` when no priority is provided.
    - Technical Requirements: Define the allowed priority values as `P1`, `P2`, and `P3`.
    - Technical Requirements: Apply `P3` as the default when constructing or reading a task without a priority.
    - Technical Requirements: Add tests for valid priorities and the default priority.
  - Story: Require task titles
    - Acceptance Criteria: A task cannot be created without a title.
    - Technical Requirements: Validate that a task title is present before creating a task.
    - Technical Requirements: Add tests for rejected missing-title input and accepted titled tasks.

- Epic: Task Filtering
  - Story: Filter tasks to show all tasks
    - Acceptance Criteria: The All filter shows both completed and incomplete tasks.
    - Technical Requirements: Implement the All filter without excluding tasks based on completion status or due date.
    - Technical Requirements: Add a component or integration test covering completed and incomplete results.
  - Story: Filter tasks to show incomplete tasks due today
    - Acceptance Criteria: The Today filter shows only incomplete tasks due today.
    - Technical Requirements: Compare normalized `YYYY-MM-DD` due dates with the current date.
    - Technical Requirements: Exclude completed tasks and tasks without a due date from the Today filter.
    - Technical Requirements: Add tests for matching, completed, undated, and non-matching tasks.
  - Story: Filter tasks to show overdue incomplete tasks
    - Acceptance Criteria: The Overdue filter shows only incomplete tasks with a due date before today.
    - Technical Requirements: Define overdue as a valid due date earlier than the current date.
    - Technical Requirements: Exclude completed tasks, today’s tasks, future tasks, and tasks without a due date.
    - Technical Requirements: Add tests covering each excluded task category and an overdue match.

- Epic: Local Task Persistence
  - Story: Persist task data locally
    - Acceptance Criteria: Task data persists in local storage.
    - Acceptance Criteria: The feature does not require backend changes or external storage.
    - Technical Requirements: Serialize and restore task data using browser local storage in the frontend.
    - Technical Requirements: Handle missing or invalid stored data without preventing the app from loading.
    - Technical Requirements: Add tests that mock local storage and verify save and restore behavior.

## Post-MVP

- Epic: Overdue Task Visibility
  - Story: Highlight overdue tasks
    - Acceptance Criteria: Overdue tasks receive a visual treatment that makes them stand out.
    - Technical Requirements: Apply an overdue visual state only to incomplete tasks with a due date before today.
    - Technical Requirements: Implement the state using the project’s CSS styling conventions with sufficient color contrast.
    - Technical Requirements: Add a component test that verifies the overdue state is rendered.

- Epic: Task Sorting
  - Story: Sort overdue tasks first
    - Acceptance Criteria: Overdue tasks appear before non-overdue tasks.
    - Technical Requirements: Use a deterministic comparator that evaluates overdue status before later sort keys.
    - Technical Requirements: Add unit tests with overdue and non-overdue task groups.
  - Story: Sort tasks by priority
    - Acceptance Criteria: Tasks with the same overdue status are ordered from `P1` to `P3`.
    - Technical Requirements: Apply an explicit priority ranking of `P1`, `P2`, then `P3` after overdue status.
    - Technical Requirements: Add unit tests covering all priority ordering combinations.
  - Story: Sort tasks by due date
    - Acceptance Criteria: Tasks with the same overdue status and priority are ordered by ascending due date.
    - Technical Requirements: Compare valid normalized due-date values chronologically after overdue status and priority.
    - Technical Requirements: Add unit tests for ascending due-date ordering within equal preceding sort keys.
  - Story: Place tasks without due dates last
    - Acceptance Criteria: Tasks without a due date appear after tasks with a due date when the preceding sort criteria are equal.
    - Technical Requirements: Treat an absent or invalid due date as undated in the comparator.
    - Technical Requirements: Place undated tasks after dated tasks when overdue status and priority are equal.
    - Technical Requirements: Add unit tests for mixed dated and undated tasks.
