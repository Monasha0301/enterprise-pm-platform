# 3. Requirements Specification

## 3.1 Introduction

This document lists the functional requirements (FR) and non-functional
requirements (NFR) for the AI-Powered Enterprise Project Management & Team
Collaboration Platform (MVP scope). Each requirement has a unique ID, one
actor, one behaviour, and a way to verify it.

## 3.2 Roles and Permission Matrix

The system has three roles: **Admin**, **Manager** and **Member**.

| Action | Admin | Manager | Member |
|--------|:-----:|:-------:|:------:|
| Create project | ✅ | ✅ | ❌ |
| Archive project | ✅ (any) | ✅ (own projects) | ❌ |
| Add / remove project members | ✅ | ✅ | ❌ |
| Create task in a project | ✅ | ✅ | ✅ (project members only) |
| Edit any task's details | ✅ | ✅ | ❌ |
| Assign / reassign task | ✅ | ✅ | ❌ |
| Change status of an **assigned** task | ✅ | ✅ | ✅ (own assigned tasks) |
| Archive task | ✅ | ✅ | ❌ |
| Use AI Task Generator | ✅ | ✅ | ❌ |
| Manage users and roles | ✅ | ❌ | ❌ |

## 3.3 Functional Requirements

### 3.3.1 Authentication and Roles (AUTH)

| ID | Requirement |
|----|-------------|
| FR-AUTH-01 | A visitor can register with an email address and password. |
| FR-AUTH-02 | A registered user can log in with email and password. |
| FR-AUTH-03 | A logged-in user can log out. |
| FR-AUTH-04 | A user can reset a forgotten password using an emailed link. |
| FR-AUTH-05 | An **Admin** can assign a role (Admin, Manager, Member) to a user in the same organisation. |
| FR-AUTH-06 | The system shall deny any action not permitted by the user's role, according to the permission matrix. |

### 3.3.2 Organisations (ORG)

| ID | Requirement |
|----|-------------|
| FR-ORG-01 | A new user can create an organisation and becomes its **Admin**. |
| FR-ORG-02 | An **Admin** can invite a user to the organisation by email and assign a role. |
| FR-ORG-03 | An **Admin** can deactivate a user. A deactivated user cannot log in. |
| FR-ORG-04 | The system shall prevent users from viewing or changing data that belongs to another organisation. |

### 3.3.3 Projects (PRJ)

| ID | Requirement |
|----|-------------|
| FR-PRJ-01 | A **Manager** or **Admin** can create a project with a name (required), description, start date and end date. |
| FR-PRJ-02 | A **Manager** or **Admin** can edit a project's name, description and dates. |
| FR-PRJ-03 | A **Manager** (own projects) or **Admin** (any project) can archive a project. Archived projects are read-only and keep their history. |
| FR-PRJ-04 | A user can view the projects they are a member of. An **Admin** can view all projects in the organisation. |
| FR-PRJ-05 | A **Manager** or **Admin** can add or remove Members on a project. |
| FR-PRJ-06 | The project page shall show the number of tasks in each status. |
| FR-PRJ-07 | An **Admin** can view and archive any project in the organisation. |
| FR-PRJ-08 | The system shall deny access to projects of another organisation, and to projects the user is not a member of (except Admins within their own organisation). |
| FR-PRJ-09 | Project completion percentage = tasks with status Completed ÷ total non-archived tasks in the project. |

### 3.3.4 Tasks (TSK)

| ID | Requirement |
|----|-------------|
| FR-TSK-01 | A **Manager**, **Admin** or project **Member** can create a task in a project with a title (required) and optional description, priority and due date. |
| FR-TSK-02 | A **Manager** or **Admin** can edit a task's title, description, priority, assignee and due date. |
| FR-TSK-03 | A **Manager** or **Admin** can assign or reassign a task to a member of the same project. |
| FR-TSK-04 | The assignee, a **Manager** or an **Admin** can change a task's status to one of: To Do, In Progress, Review, Completed. |
| FR-TSK-05 | A **Manager** or **Admin** can set a task's priority to Low, Medium, High or Critical. |
| FR-TSK-06 | A user can filter and search the tasks of a project they can access by status, priority, assignee and due date. |
| FR-TSK-07 | A **Manager** or **Admin** can archive a completed task. Archived tasks keep their history. |
| FR-TSK-08 | The system shall enforce the permission matrix (section 3.2) on every task action. |

### 3.3.5 Kanban Board (KAN)

| ID | Requirement |
|----|-------------|
| FR-KAN-01 | A project member can view the project's tasks on a board with one column per status. |
| FR-KAN-02 | A user can move a task card between columns to change its status, subject to FR-TSK-04. |
| FR-KAN-03 | Each card shall display the task title, priority and assignee. |

### 3.3.6 Comments (CMT)

| ID | Requirement |
|----|-------------|
| FR-CMT-01 | A project member can add a comment to a task in that project. |
| FR-CMT-02 | Comments shall display the author and timestamp, in chronological order. |
| FR-CMT-03 | A comment's author can delete their own comment. A **Manager** or **Admin** can delete any comment in the project. |

### 3.3.7 Dashboard (DSH)

| ID | Requirement |
|----|-------------|
| FR-DSH-01 | After login, the dashboard shall show the user's assigned tasks grouped by status. |
| FR-DSH-02 | The dashboard shall highlight overdue tasks (due date passed and status not Completed). |
| FR-DSH-03 | For a **Manager** or **Admin**, the dashboard shall list their accessible projects with completion percentage (FR-PRJ-09). |

### 3.3.8 Notifications (NTF)

| ID | Requirement |
|----|-------------|
| FR-NTF-01 | A user shall receive an in-app notification when a task is assigned to them. |
| FR-NTF-02 | A user shall receive an in-app notification when a comment is added to a task assigned to them. |
| FR-NTF-03 | A user can see their unread notification count and mark notifications as read. |

### 3.3.9 AI Task Generator (AI)

| ID | Requirement |
|----|-------------|
| FR-AI-01 | A **Manager** or **Admin** can enter a project description, feature description or requirement text as input for AI task generation. |
| FR-AI-02 | The system shall return a list of suggested tasks, each with a title, description and priority. |
| FR-AI-03 | The system shall display generated tasks for review before saving them to the project. |
| FR-AI-04 | The user can edit, remove, select or approve generated tasks before they are created. |
| FR-AI-05 | If the AI service fails or times out, the system shall show an error message and keep the user's input text. |
| FR-AI-06 | Input text is limited to 5,000 characters. Longer input is rejected with a message. |
| FR-AI-07 | Each user is limited to 10 AI generations per hour. |

#### AI Design Decision
The AI Task Generator **does not automatically save tasks**. Generated tasks
appear as suggestions and must be reviewed and approved by the user.

**Reasons:**
- AI-generated tasks may not match business requirements.
- Human approval prevents incorrect tasks entering the project.
- It improves trust and quality control, and avoids unwanted data creation.

## 3.4 Non-Functional Requirements

| ID | Category | Requirement |
|----|----------|-------------|
| NFR-01 | Performance | The project dashboard shall load within 3 seconds for 95% of requests under normal usage. |
| NFR-02 | Security | After 5 failed login attempts within 15 minutes, further login attempts for that account shall be blocked for 15 minutes. |
| NFR-03 | Availability | Target: 99% monthly uptime on the production environment, excluding planned maintenance. To be reviewed against the hosting tier in the deployment phase. |
| NFR-04 | Scalability | The system shall be designed to support 500 concurrent users, and verified by a load test at 100 concurrent users on a test environment. |
| NFR-05 | Usability | A new user shall be able to create a project and assign a task within 5 minutes of first login without help, tested with at least 3 first-time users. |
| NFR-06 | Data Integrity | The database shall be backed up at least once every 24 hours, with restoration possible within 4 hours. The backup method is decided in the deployment phase. |
| NFR-07 | Security | All traffic shall use HTTPS. Passwords shall be stored only as salted hashes. Row Level Security shall be enabled on every table holding organisation data. |
| NFR-08 | Compatibility | The interface shall be usable at screen widths from 360 px to desktop, in the latest two versions of Chrome, Firefox, Edge and Safari. |
| NFR-09 | Maintainability | Automated tests shall cover at least 70% of backend business logic, and shall run on every pull request. |
| NFR-10 | AI Performance | 95% of AI task generation requests shall return a result within 15 seconds. |

## 3.5 Testability Examples (Given / When / Then)

**FR-TSK-01 (task needs a title)**
> **Given** a Member who belongs to Project A
> **When** they create a task with an empty title
> **Then** the system rejects the request and no task is created.

**FR-TSK-04 and the permission matrix (Member cannot change another's task)**
> **Given** a task assigned to Member X
> **When** Member Y (same project, not the assignee) tries to change its status
> **Then** the system denies the action.

**FR-AI-03 (review before saving)**
> **Given** a Manager submits a valid project description
> **When** the AI returns suggested tasks
> **Then** the tasks are shown as suggestions and none exist in the project
> until the Manager approves them.

## 3.6 Traceability: Must-Have Features to Requirements

| Must-Have feature | Requirement IDs |
|-------------------|-----------------|
| Authentication & RBAC | FR-AUTH-01 to 06, FR-ORG-02, 03 |
| Organisations & Projects | FR-ORG-01, 04, FR-PRJ-01 to 09 |
| Task Management | FR-TSK-01 to 08 |
| Kanban Board | FR-KAN-01 to 03 |
| Comments | FR-CMT-01 to 03 |
| Basic Dashboard | FR-DSH-01 to 03 |
| In-app Notifications | FR-NTF-01 to 03 |
| AI Task Generator | FR-AI-01 to 07, NFR-10 |
