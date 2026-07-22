# Cloud Architecture Overview

This monorepo contains a React frontend and an Express API backed by an in-memory SQLite store. The store is initialized when the backend starts and is not persisted outside the running process.

```mermaid
flowchart LR
    user[User]
    frontend[React Frontend]
    api[Express API]
    store[(In-memory SQLite Store)]

    user -->|Uses TODO app| frontend
    frontend -->|HTTP requests to /api/tasks| api
    api -->|Reads and writes task data| store
```

## System Context

- **User** interacts with the TODO application through the React frontend.
- **React Frontend** renders task forms and lists and sends task operations to the API.
- **Express API** validates requests and provides task endpoints for creating, reading, updating, completing, and deleting tasks.
- **In-memory SQLite Store** holds task data for the lifetime of the backend process. Restarting the backend clears the data.

## Creating a TODO

```mermaid
sequenceDiagram
    actor User
    participant Frontend as React Frontend
    participant API as Express API
    participant Store as In-memory SQLite Store

    User->>Frontend: Enter task title and submit
    Frontend->>API: POST /api/tasks with task data
    API->>API: Validate task title
    API->>Store: Insert task
    Store-->>API: Return created task
    API-->>Frontend: 201 Created with task data
    Frontend-->>User: Display the new TODO
```
