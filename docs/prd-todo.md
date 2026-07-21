# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

The basic TODO app currently supports task titles and completion status. This upgrade adds lightweight deadline and priority management so users can identify and filter urgent work without introducing backend complexity. The MVP is intentionally simple, teachable, and limited to local storage.

The scope in this document follows the September 17 Slack confirmation when it further classified the requirements discussed in the September 16 meeting.

---

## 2. MVP Scope

- Preserve the existing task title and completed status.
- Add an optional `dueDate` field to each task.
  - Store valid dates in ISO `YYYY-MM-DD` format.
  - Treat invalid date values as absent rather than preventing the task from being used.
- Add a `priority` field with the enum values `P1`, `P2`, and `P3`.
  - Default the priority to `P3` when it is not provided.
- Require a task `title`.
- Provide task filters for:
  - **All**: show completed and incomplete tasks.
  - **Today**: show only incomplete tasks due today.
  - **Overdue**: show only incomplete tasks with a due date before today.
- Persist task data locally.
- Do not require backend changes or external storage.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks so they stand out, such as with a red treatment.
- Add task sorting in this order:
  1. Overdue tasks first.
  2. Priority from `P1` to `P3`.
  3. Due date ascending.
  4. Tasks without a due date last.

---

## 4. Out of Scope

- Notifications or reminders.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation or other special accessibility features for this iteration.
- Backend persistence or other external storage.