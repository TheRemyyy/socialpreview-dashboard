<div align="center">

# SocialPreview Dashboard

**Enterprise-Grade Team Management & Client Portal**

[![Rust](https://img.shields.io/badge/Backend-Axum-orange?style=flat-square&logo=rust)](https://github.com/tokio-rs/axum)
[![React](https://img.shields.io/badge/Frontend-React_18-blue?style=flat-square&logo=react)](https://reactjs.org/)
[![Database](https://img.shields.io/badge/DB-SQLite%2fPostgreSQL-lightgrey?style=flat-square&logo=postgresql)](https://www.postgresql.org/)

*A comprehensive dashboard for managing teams, tickets, tasks, and client services.*

[Features](#features) • [Installation](#installation) • [Architecture](#architecture) • [Documentation](#documentation)

</div>

---

## Overview

SocialPreview Dashboard is a monolithic full-stack application designed to streamline internal operations and client interactions. It combines a high-performance Rust backend with a modern React frontend to deliver a seamless experience for task management, support ticketing, and service tracking.

### Key Features

* **👥 Team Management** — Role-based access control (Management, Team, User) with detailed member profiles.
* **🎫 Support Tickets** — Full-featured ticketing system with priorities, status tracking, and comments.
* **✅ Task Management** — Assign tasks, track deadlines, set priorities, and collaborate in real-time.
* **🔒 Secure Authentication** — JWT-based auth with 2FA (TOTP) support and secure password hashing (Argon2).
* **📅 Planning & Features** — Integrated calendar, absence tracking, future plans, and internal blog.
* **💰 Service Tracking** — Manage client services, track progress, pricing, and active status.
* **📊 Statistics** — Real-time insights into team productivity and service performance.

---

## <a id="architecture"></a>🏗️ Architecture

The project follows a standard client-server architecture:

### Backend (`/backend`)
* **Framework:** Rust (Axum)
* **Database:** SQLx (SQLite for dev / PostgreSQL recommended for prod)
* **Auth:** Secure HttpOnly Cookies + JWT + Argon2 + TOTP

### Frontend (`/frontend`)
* **Framework:** React 18 + TypeScript + Vite
* **Styling:** Tailwind CSS
* **State:** Context API

---

## <a id="installation"></a>🚀 Installation

### 1. Backend Setup
```bash
cd backend
sqlx database create
sqlx migrate run
cargo run
```

### 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

---

## <a id="documentation"></a>📄 Documentation

Detailed technical information can be found in the `docs/` directory:

### Core Guides
- 📖 **[Overview](docs/overview.md)** — Start here for a complete project guide.
- 🏗️ **[Backend Architecture](docs/backend/architecture.md)** — Axum, Tokio, and internal Rust logic.
- 🔐 **[Authentication](docs/backend/auth.md)** — Deep dive into JWT, Argon2, and 2FA.
- ⚡ **[Frontend Stack](docs/frontend/stack.md)** — React, Vite, and Tailwind implementation.

### Technical & Production
- 🚀 **[Production Guide](docs/technical/production.md)** — Essential steps for deploying to production.
- 🚦 **[Routing & Guards](docs/frontend/routing.md)** — How we protect routes and handle roles.
- 👥 **[RBAC & Permissions](docs/technical/rbac.md)** — Understanding user access levels.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
<sub>Made with ❤️ by TheRemyyy</sub>
</div>