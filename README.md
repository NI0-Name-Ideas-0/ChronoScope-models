# Models

This repository contains architecture and design diagrams for the ChronoScope project.

---

## Activity Diagrams

### Account Management
| File | Description |
|------|-------------|
| [activity_account_linkage.pu](activity_account_linkage.pu) | Flow for linking two accounts: the user enters a target e-mail, a confirmation link is sent, and upon acceptance the two identities are merged. |

### Algorithms
| File | Description |
|------|-------------|
| [activity_algo.pu](activity_algo.pu) | End-to-end algorithm pipeline combining all three steps: topological sort → critical path method → task planning. |
| [activity_algo_topsort_dfs.pu](activity_algo_topsort_dfs.pu) | Topological sorting of tasks using depth-first search; detects cycles and produces a dependency-ordered task list. |
| [activity_algo_critical_path.pu](activity_algo_critical_path.pu) | Critical Path Method with a forward pass (earliest start/finish) and a backward pass (latest start/finish) over the sorted task graph. |
| [activity_algo_planning.pu](activity_algo_planning.pu) | Heuristic-guided recursive task planning that selects tasks by lowest heuristic score and backtracks on failure. |

### Task Management
| File | Description |
|------|-------------|
| [activity_create_task.pu](activity_create_task.pu) | Server-side create-task flow across Controller, Service, and Repository layers including validation and error handling. |
| [activity_create_task_userviewpoint.drawio](activity_create_task_userviewpoint.drawio) | User-facing create-task flow (Draw.io): from clicking "Add Task" through filling out the task modal. |

### Spring / Backend
| File | Description |
|------|-------------|
| [activity_spring_security_chain.pu](activity_spring_security_chain.pu) | Spring Security filter chain: JWT validation, on-demand account creation, organization linkage, and security context population. |
| [activity_typical_spring_flow.pu](activity_typical_spring_flow.pu) | Reference diagram of the standard Spring MVC request flow: Controller → Service → Repository → Service → Controller. |

---

## Component Diagrams

| File | Description |
|------|-------------|
| [component_system.pu](component_system.pu) | High-level system overview showing Frontend, Backend, Keycloak, and Mail Server and their interface dependencies. |
| [component_backend.pu](component_backend.pu) | Internal backend structure with Controller, Service, and Repository packages and their relationships to MariaDB. |

---

## Data Models

| File | Description |
|------|-------------|
| [er_backend.pu](er_backend.pu) | Chen-notation ER diagram of the backend domain: Identity, Account, Organization, Task, DynamicTask, StaticTask, WorkSlot, Scope, Tag, and TaskDependency. |
| [relational_schema_database.pu](relational_schema_database.pu) | Relational schema (UML class notation) showing table structures and foreign-key relationships for the database. |
| [frontend_task_class_model.pu](frontend_task_class_model.pu) | TypeScript class model used in the frontend: abstract `Task` with `AlgoTask` and `StaticTask` subtypes plus `Scope` and `Label`. |

---

## Sequence Diagrams

| File | Description |
|------|-------------|
| [sequence_create_task.pu](sequence_create_task.pu) | End-to-end task creation sequence: frontend submits the form, backend persists the task, reruns the scheduling algorithm, and returns the updated task list. |
| [sequence_login_org_idp.pu](sequence_login_org_idp.pu) | Login flow when the user's organization provides its own Identity Provider (IdP): Frontend → Keycloak → Org-IdP → Keycloak → Backend token verification. |
| [sequence_login_without_org_idp.pu](sequence_login_without_org_idp.pu) | Login flow using Keycloak directly (no external IdP): Frontend → Keycloak → Backend token verification. |
