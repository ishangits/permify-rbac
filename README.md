<h1 align="center">🔐 Permify RBAC — Modular Role-Based Access Control System</h1>
<p align="center">A production-grade RBAC system with dynamic modules, permissions, roles, and real-time authorization using <b>Permify</b> & <b>ChromaDB</b>.</p>

---

## 🚀 Overview

**Permify RBAC** is a fully dynamic and modular Role-Based Access Control system designed for real-world SaaS, enterprise dashboards, and AI/agent authorization.

It solves the modern access-control challenges:

- Permissions change frequently  
- Schema updates should NOT require code changes  
- Organizations need module-based permission structures  
- Chatbots/AI agents must obey user permissions  
- Systems need real-time authorization checks  

This project centralizes RBAC logic with **Permify’s policy engine** + **ChromaDB vector store**, making permission checks fast, scalable, and secure.

---

## ⭐ Key Features

### ✅ 1. **Dynamic Module Creation**
Create system modules like:
- User Management  
- Dashboard  
- Projects  
- Reports  
- Billing  

Each module auto-generates its permissions:
create, read, update, delete

yaml
Copy code

---

### ✅ 2. **Automatic Permify Schema Sync**
Whenever modules/permissions/roles update, your **Permify schema updates automatically**.

No more manually editing policy files.

---

### ✅ 3. **Role Management**
- Create roles (Admin, Editor, Viewer, Ops, Agent, etc.)
- Assign module-level permissions to each role
- Fully dynamic, no hardcoding

---

### ✅ 4. **User Role + Permission Mapping**
Each user can have multiple roles.

User → Role → Permissions → Modules → Allowed Actions

---

### ✅ 5. **ChromaDB Integration**
Stores:
- Module metadata  
- Permission descriptions  
- Feeds for AI/Agents  
- Fast permission lookup vectors  

Built for **AI copilots / AI agents** that need permission-awareness.

---

### ✅ 6. **Real-Time Permission Check API**
Before any API or Agent action, the RBAC system checks:

User → Roles → Permissions → Allowed?

yaml
Copy code

If permission is denied → the action is blocked instantly.

---

### ✅ 7. **Multi-Tenant Ready**
For SaaS products supporting multiple organizations.

Each org can have:
- Its own modules  
- Its own roles  
- Its own permissions  
- Its own schema & users  

---

## 🧱 Architecture

Modules → Permissions → Roles → Users
↓
Permify Schema Sync
↓
Real-Time Authorization Engine
↓
Allow/Deny API or Agent Action

yaml
Copy code

---

## 🛠️ Tech Stack

| Layer | Technology |
|------|------------|
| Authorization Engine | **Permify** |
| Vector DB | **ChromaDB** |
| Backend | **Go (Golang)** |
| Data Model | Dynamic JSON-based RBAC schema |
| Use Cases | SaaS, Enterprise Admin, AI Agent Gating |

---

## 📂 Project Structure

permify-rbac/
├── modules/ # Module & permission creation
├── roles/ # Role management
├── permissions/ # Permission mapping
├── feeds/ # ChromaDB stored metadata
├── utils/ # Helper functions
├── main.go
├── go.mod
└── README.md

yaml
Copy code

---

## ⚙️ Install & Run

### 1️⃣ Clone the repository
```bash
git clone https://github.com/ishangits/permify-rbac
cd permify-rbac
2️⃣ Install dependencies
bash
Copy code
go mod tidy
3️⃣ Add environment variables
Create .env:

ini
Copy code
PERMIFY_HOST=http://localhost:3476
CHROMA_PATH=./chromadb
PORT=8080
4️⃣ Run the server
bash
Copy code
go run main.go
Server runs at:
👉 http://localhost:8080

📌 API Examples
➤ Create Module
http
Copy code
POST /modules
{
  "moduleName": "User Management"
}
➤ Create Role
http
Copy code
POST /roles
{
  "roleName": "Editor"
}
➤ Assign Permissions to Role
http
Copy code
POST /roles/assign
{
  "roleName": "Editor",
  "permissions": ["dashboard:read", "user-management:update"]
}
➤ Assign Role to User
http
Copy code
POST /users/assign-role
{
  "userId": "user_123",
  "roleName": "Editor"
}
➤ Permission Check Before API Call
http
Copy code
POST /check
{
  "userId": "user_123",
  "module": "dashboard",
  "permission": "read"
}
Response:

json
Copy code
{ "allowed": true }
🧠 Ideal Use Cases
✔ SaaS Multi-Tenant Apps
✔ Enterprise Admin Dashboards
✔ Internal Platforms
✔ AI Agents (permission-aware bots)
✔ Access-Control Layers for Microservices

🤝 Contributing
Pull requests are welcome. Open an issue for suggestions or improvements.

⭐ Show Support
If this project helped you, consider starring ⭐ the repo.

<p align="center"><b>Made with ❤️ by Ishan</b></p> ```
