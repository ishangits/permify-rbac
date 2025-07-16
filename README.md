# 🔐 permify-rbac – Modular Role-Based Access Control System

A real-world RBAC (Role-Based Access Control) implementation using **Permify**, designed to dynamically manage permissions at the module level and enforce access checks during chatbot interactions.

---

## 📌 Project Overview

This system allows fine-grained access control across dynamically created modules. It uses **Permify** for relationship-based authorization, and **ChromaDB** for storing permission metadata (feeds).

---

## 🧱 Tech Stack

| Layer       | Technology     |
|-------------|----------------|
| Backend     | Golang         |
| Auth Engine | Permify        |
| Storage     | ChromaDB       |
| Frontend    | (Internal tool/CLI/API layer) |
| AI Agents   | agent1, agent2 (API layer) |

---

## 🧠 Features & Flow

### ✅ 1. **Module Creation**
- New modules are created dynamically.
- For each module, permissions (endpoints) like `read`, `write`, `delete` are defined.

### ✅ 2. **Feeds Info Storage**
Each permission has:
- **Module selection**
- **Endpoint/permissions**
- **Prompt**
- **Filters**
- **Parameters**

All of this is stored in **ChromaDB** for fast vector-based querying (used by `agent1`).

### ✅ 3. **Schema Update in Permify**
When modules and permissions are created, the **Permify schema is updated automatically** to reflect the new relationships (e.g., roles → module → permission).

### ✅ 4. **Role Management**
- Roles are created and assigned to sets of permissions.
- Schema is again updated in Permify to bind roles with modules and actions.

### ✅ 5. **User Role Assignment**
- Users are assigned roles dynamically.
- The relationship is updated in Permify (`user -> role`).

### ✅ 6. **Chatbot Integration (agent2)**
- When a prompt is sent through the chatbot, the system:
  - First checks permission via **Permify's permission check API**.
  - If allowed, **agent2 API** is called to fetch or execute information.
  - If not allowed, it responds with a "No permission" message.

---

## 🧩 Example Use Case

1. Admin creates a new module: `customer-support`
2. Permissions: `read_ticket`, `close_ticket`, `assign_ticket`
3. Feeds are added and stored for agent1 to reference
4. A `SupportManager` role is created and assigned relevant permissions
5. A user (`user123`) is assigned the `SupportManager` role
6. When the chatbot receives a prompt from `user123`, it checks:
   - Does `user123` have permission to `close_ticket`?
   - If yes → agent2 executes it
   - If no → denies access

---

## 🚀 Highlights of What I Did

- ✅ Designed and implemented dynamic **module-based RBAC**
- ✅ Synced permission feeds with **Permify schema updates**
- ✅ Built flows to store agent-specific metadata in **ChromaDB**
- ✅ Integrated **chatbot permission checks** before calling downstream APIs
- ✅ Handled **role-to-permission** and **user-to-role** mappings with fine granularity

---

## 🛠️ How This Can Be Used

- SaaS multi-tenant access control
- Internal developer platforms
- Secure chatbot/AI agents with permission gating
- Enterprise dashboards where role and action mapping is highly dynamic

## 🧭 Permission Flow Diagram

User Action → Chatbot Prompt
     |
     v
Check User Role (via Permify)
     |
     v
 ┌───────────────────────────────┐
 | Does user have permission?   |
 └───────────────────────────────┘
     |                             \
     | Yes                          \ No
     v                               v
Call Agent2 API                Respond: No Access
     |
     v
Get/Modify Resource (via Feed Info)
     |
     v
Show Response to User

## 📎 References

- [Permify Docs](https://docs.permify.co)
- [ChromaDB](https://www.trychroma.com/)
- [RBAC vs ABAC – Explained](https://permify.co/blog/rbac-vs-abac)

---

> 📌 _This project highlights my ability to implement complex authorization flows across dynamic systems using Golang, Permify, and intelligent access design._

