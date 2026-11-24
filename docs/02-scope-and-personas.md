# 2. Scope and Personas

## 2.1 Scope Approach

Features are prioritised with the **MoSCoW** method. The MVP (Minimum Viable
Product) is the smallest complete product that solves the core problem: teams
managing projects and tasks in one place, with AI assistance.

## 2.2 MoSCoW Prioritisation

### Must Have (MVP)

| Feature | Justification |
|---------|---------------|
| Authentication & Authorization | Secures the system and identifies users. |
| Role-Based Access Control (Admin, Manager, Member) | Different users need different permissions. |
| Organisations & Projects | Core functionality of the platform. |
| Task Management | Creating, assigning and tracking work. |
| Kanban Board | Visual overview of task progress. |
| Comments | Communication within tasks. |
| Basic Dashboard | Overview of a user's projects and tasks. |
| In-app Notifications | Keeps users informed of assignments and updates. |
| AI Task Generator | Delivers the "AI-powered" promise at low build cost: text in, tasks out. |

### Should Have

| Feature | Justification |
|---------|---------------|
| Sprints & Product Backlog | Enables Agile planning; prerequisite for sprint summaries. |
| File Upload & Document Sharing | Important, but needs storage and permission design. |
| Real-Time Board Updates | Board refreshes live when a teammate moves a card. |
| Calendar & Milestone Tracking | Helpful for project planning. |
| AI Sprint Summary | Saves reporting time; depends on sprints existing. |
| AI Meeting Notes | Summarises meetings into action items. |
| Reports & Analytics | Useful for managers monitoring performance. |
| Angular Admin Panel | User management and system oversight for administrators. |

### Could Have

| Feature | Justification |
|---------|---------------|
| AI Risk Analyzer | Needs substantial project data to be useful. |
| AI Chat Assistant | Answers questions from project data. |
| Smart Assignment (workload + skills) | Recommends the best assignee. |
| Duplicate Task Detection | Prevents redundant work. |
| Knowledge Base & Smart Search | Semantic search over documentation. |
| Project Health Dashboard | Advanced KPIs for managers. |
| AI Documentation Generator | Reduces documentation effort. |
| Email Notifications | Extends in-app notifications. |
| Focus Mode | Reduces distractions. |

### Won't Have (Version 1.0)

| Feature | Justification |
|---------|---------------|
| Video Conferencing | Teams and Zoom already do this well. |
| Time Tracking / Payroll Integration | Outside project scope. |
| Multi-Tenant SaaS Billing | Not needed for the first release. |
| Mobile Apps (Android/iOS) | v1 is a responsive web application. |
| Offline Mode | Possible future version. |
| Real-Time Chat | Task comments cover basic communication. Chat needs WebSockets, message storage and read receipts. |

## 2.3 Build Order (First Three Features)

1. **Authentication & RBAC.** Every other feature depends on knowing who the
   user is and what they may do.
2. **Projects & Tasks.** The primary purpose of the platform.
3. **Kanban Board.** A visual view over tasks that delivers immediate value.

## 2.4 Design Decisions

### Decision 1: Three roles, not five
Roles represent **permissions**, not job titles. The system uses three roles:
**Admin, Manager, Member**. "Student", "Employee" and "Supervisor" are
context labels, not separate permission sets. A supervisor is given the
Manager role, and students and employees are Members. This keeps the
permission model small and testable.

### Decision 2: Multi-organisation data model
The system is **multi-tenant ready**: every core table includes an
`organization_id`, and access is enforced with database-level Row Level
Security. Users belong to one organisation in v1. Billing and tenant
self-service are out of scope (see Won't Have)..

## 2.5 User Personas

### Persona: Sarah Fernando — Project Manager
- **Age / context:** 35. Manages several development teams across departments
  in a large software company.
- **Goals:**
  - Plan and monitor projects efficiently.
  - Track deadlines and team progress.
  - Generate reports for senior management.
- **Frustrations:**
  - Information spread across multiple tools.
  - Difficulty identifying delayed tasks.
  - Spending excessive time preparing reports.
- **Tech skill:** High
- **Typical day in our system:**
  - Reviews the project dashboard.
  - Creates projects and assigns tasks.
  - Monitors sprint progress.
  - Reviews AI-generated summaries and risk alerts.

### Persona: Nimal Perera — Software Developer
- **Age / context:** 26. Full-stack developer working on several projects.
- **Goals:**
  - View assigned tasks clearly.
  - Collaborate with teammates.
  - Receive timely notifications about changes.
- **Frustrations:**
  - Unclear task priorities.
  - Switching between communication and project tools.
  - Missing important updates.
- **Tech skill:** High
- **Typical day in our system:**
  - Signs in to view assigned tasks.
  - Updates task status on the Kanban board.
  - Discusses work through task comments.
  - Checks notifications and deadlines.

### Persona: Monasha Silva — University Student (Team Leader)
- **Age / context:** 21. Leads a software engineering group project with
  classmates under a lecturer's supervision.
- **Goals:**
  - Organise project tasks.
  - Assign responsibilities fairly.
  - Track each member's progress.
  - Submit the project before the deadline.
- **Frustrations:**
  - Team members forgetting deadlines.
  - Poor communication.
  - Difficulty monitoring individual contributions.
- **Tech skill:** Medium
- **Typical day in our system:**
  - Creates a project for the semester.
  - Assigns tasks to group members.
  - Tracks completion on the Kanban board.
  - Uses AI to generate tasks from the project brief.

### Persona: Kamal Jayasuriya — System Administrator *(DRAFT, edit me)*
- **Age / context:** 40. IT administrator responsible for the platform across
  all departments of a large organisation.
- **Goals:**
  - Create and deactivate user accounts quickly.
  - Assign the correct roles and keep access secure.
  - See who did what, for audits and troubleshooting.
- **Frustrations:**
  - Manually managing accounts across several tools.
  - No clear record of permission changes.
- **Tech skill:** High
- **Typical day in our system:**
  - Uses the admin panel to create users and assign roles.
  - Reviews audit logs for unusual activity.
  - Deactivates accounts for people who have left.
