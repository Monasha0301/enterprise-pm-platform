# 4. User Stories and Acceptance Criteria

## 4.1 Conventions

- **Story format:** As a [role], I want [capability], so that [benefit].
- **Acceptance criteria:** Given / When / Then, with at least one unhappy path.
- **Traceability:** each story lists the requirement IDs it covers
  (see `03-requirements.md`).
- **Actors** are drawn from the personas in `02-scope-and-personas.md`.

---

## Epic: Authentication and Administration

### US-AUTH-01: Assign roles to users
**As a** System Administrator (Kamal),
**I want** to assign a role to each user in my organisation,
**so that** people only have the permissions their job requires.

**Acceptance criteria**
- **Given** an Admin viewing a user in their organisation, **When** they change
  the user's role to Manager, **Then** the user receives Manager permissions.
- **Given** a Manager or Member, **When** they try to change anyone's role,
  **Then** the system denies the action.
- **Given** a user belonging to another organisation, **When** an Admin tries to
  change their role, **Then** the system denies the action and reveals no data.

**Covers:** FR-AUTH-05, FR-AUTH-06, FR-ORG-04
**Priority:** Must

---

## Epic: Project Management

### US-PRJ-01: Create a project
**As a** Project Manager (Sarah),
**I want** to create a project with a name, description and dates,
**so that** my team has one place to plan and track the work.

**Acceptance criteria**
- **Given** a Manager, **When** they submit a project with a valid name,
  **Then** the project is created and appears in their project list.
- **Given** a Manager, **When** they submit a project with an empty name,
  **Then** the system rejects it and shows a validation message.
- **Given** a Member, **When** they try to create a project,
  **Then** the system denies the action.

**Covers:** FR-PRJ-01, FR-PRJ-04, FR-AUTH-06
**Priority:** Must

### US-PRJ-02: Archive a project
**As a** Project Manager (Sarah),
**I want** to archive a finished project,
**so that** my active list stays clean while the history is kept.

**Acceptance criteria**
- **Given** a Manager who owns a project, **When** they archive it,
  **Then** it becomes read-only and its tasks and history remain viewable.
- **Given** an archived project, **When** anyone tries to add a task to it,
  **Then** the system rejects the request.
- **Given** a Manager who does not own a project, **When** they try to archive it,
  **Then** the system denies the action (an Admin can archive any project).

**Covers:** FR-PRJ-03, FR-PRJ-07
**Priority:** Must

---

## Epic: Task Management

### US-TSK-01: Create a task
**As a** Software Developer (Nimal),
**I want** to create a task in a project I belong to,
**so that** work I discover is recorded and not forgotten.

**Acceptance criteria**
- **Given** a project member, **When** they create a task with a title,
  **Then** the task is saved with status "To Do".
- **Given** a project member, **When** they submit a task with an empty title,
  **Then** the system rejects it and no task is created.
- **Given** a user who is not a member of the project, **When** they try to
  create a task in it, **Then** the system denies the action.

**Covers:** FR-TSK-01, FR-PRJ-08
**Priority:** Must

### US-TSK-02: Assign a task
**As a** Project Manager (Sarah),
**I want** to assign a task to a member of my project,
**so that** everyone knows who is responsible for it.

**Acceptance criteria**
- **Given** a Manager and a project member, **When** the Manager assigns a task
  to that member, **Then** the task shows the assignee and the member receives
  a notification.
- **Given** a Manager, **When** they try to assign a task to someone who is not
  in the project, **Then** the system rejects it.
- **Given** a Member, **When** they try to assign or reassign a task,
  **Then** the system denies the action.

**Covers:** FR-TSK-03, FR-NTF-01, FR-AUTH-06
**Priority:** Must

### US-TSK-03: Update the status of my task
**As a** Software Developer (Nimal),
**I want** to change the status of tasks assigned to me,
**so that** my team can see my progress without asking me.

**Acceptance criteria**
- **Given** a task assigned to a Member, **When** that Member changes the status
  to "In Progress", **Then** the new status is saved and visible to the team.
- **Given** a task assigned to someone else, **When** a Member (not a Manager or
  Admin) tries to change its status, **Then** the system denies the action.
- **Given** a Manager, **When** they change the status of any task in their
  project, **Then** the change is saved.

**Covers:** FR-TSK-04, FR-TSK-08
**Priority:** Must

---

## Epic: Kanban Board

### US-KAN-01: Move cards on the Kanban board
**As a** Software Developer (Nimal),
**I want** to drag my task cards between columns,
**so that** updating progress takes seconds.

**Acceptance criteria**
- **Given** a project board, **When** a member opens it, **Then** each task
  appears as a card in the column matching its status, showing title, priority
  and assignee.
- **Given** a task assigned to the user, **When** they drag its card to another
  column, **Then** the status changes and persists after a page refresh.
- **Given** a task the user is not allowed to change, **When** they drag its
  card, **Then** the card returns to its original column and an error is shown.

**Covers:** FR-KAN-01, FR-KAN-02, FR-KAN-03, FR-TSK-04
**Priority:** Must

---

## Epic: AI Task Generator

### US-AI-01: Generate tasks from text
**As a** university team leader (Monasha),
**I want** to paste a project brief and get suggested tasks,
**so that** I can plan the project quickly instead of writing every task by hand.

**Acceptance criteria**
- **Given** a Manager, **When** they submit a valid project description,
  **Then** the system shows a list of suggested tasks, each with a title,
  description and priority, and none are saved yet.
- **Given** a Manager, **When** they submit text over 5,000 characters,
  **Then** the system rejects it with a message.
- **Given** the AI service is unavailable, **When** a Manager submits text,
  **Then** an error message is shown and their text is kept.
- **Given** a user who has made 10 generations in the past hour, **When** they
  submit another, **Then** the system blocks it and says when they can retry.

**Covers:** FR-AI-01, FR-AI-02, FR-AI-05, FR-AI-06, FR-AI-07, NFR-10
**Priority:** Must

### US-AI-02: Review and approve suggested tasks
**As a** university team leader (Monasha),
**I want** to edit and approve the suggested tasks before they are saved,
**so that** only tasks I trust enter my project.

**Acceptance criteria**
- **Given** a list of suggested tasks, **When** the user edits a title and
  approves it, **Then** the task is created with the edited title.
- **Given** a list of suggested tasks, **When** the user removes one suggestion
  and approves the rest, **Then** only the remaining tasks are created.
- **Given** a list of suggested tasks, **When** the user leaves the page without
  approving, **Then** no tasks are created.

**Covers:** FR-AI-03, FR-AI-04
**Priority:** Must

---

## Epic: Notifications

### US-NTF-01: Be notified of changes to my work
**As a** Software Developer (Nimal),
**I want** to be notified when a task is assigned to me or someone comments on it,
**so that** I don't miss important updates.

**Acceptance criteria**
- **Given** a task assigned to me, **When** a Manager assigns it, **Then** my
  unread notification count increases by one.
- **Given** an unread notification, **When** I open it and mark it as read,
  **Then** my unread count decreases.
- **Given** a comment added to a task not assigned to me, **When** it is posted,
  **Then** I receive no notification for it.

**Covers:** FR-NTF-01, FR-NTF-02, FR-NTF-03
**Priority:** Must
