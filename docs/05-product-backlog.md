# 5. Product Backlog

## 5.1 Estimation scale
Story points: 1, 2, 3, 5, 8, 13. Reference story: "Archive a project" = 2.
Items above 8 are split. Estimates are revised after each sprint.

## 5.2 Definition of Done
- All acceptance criteria pass
- Merged to `main` through a reviewed pull request
- Automated tests written and passing
- No lint or build errors
- Documentation updated
- Works in the deployed dev environment (once available)

## 5.3 Backlog (ordered by priority)

| Rank | ID | Item | Points | Milestone |
|-----:|----|------|-------:|-----------|
| 1 | TECH-01 | Set up development environment and repo structure | 2 | M1 |
| 2 | TECH-02 | Design database schema and Row Level Security foundation | 5 | M1 |
| 3 | US-AUTH-03 | Register an account | 3 | M1 |
| 4 | US-AUTH-02 | Log in | 3 | M1 |
| 5 | US-AUTH-01 | Assign roles to users | 5 | M1 |
| 6 | US-PRJ-01 | Create a project | 3 | M2 |
| 7 | US-TSK-01 | Create a task | 3 | M2 |
| 8 | US-TSK-02 | Assign a task | 3 | M2 |
| 9 | US-TSK-03 | Update the status of my task | 2 | M2 |
| 10 | US-PRJ-02 | Archive a project | 2 | M2 |
| 11 | TECH-03 | Set up CI pipeline (GitHub Actions) | 3 | M2 |
| 12 | US-KAN-01 | Move cards on the Kanban board | 5 | M3 |
| 13 | US-NTF-01 | Be notified of changes to my work | 5 | M3 |
| 14 | US-CMT-01 | Comment on a task *(story to be written)* | 3 | M3 |
| 15 | US-DSH-01 | View my dashboard *(story to be written)* | 5 | M3 |
| 16 | US-AI-01 | Generate tasks from text | 8 | M4 |
| 17 | US-AI-02 | Review and approve suggested tasks | 5 | M4 |

Total: 65 points. Should-have items (M5) and later milestones are added when
M1–M4 are underway.
