# SocialPreview Dashboard Documentation

Welcome to the comprehensive documentation for the **SocialPreview Dashboard** — an enterprise-grade full-stack platform for team management, support ticketing, and client portals.

## Introduction

SocialPreview Dashboard is designed to provide a unified workspace for both internal teams and external clients. Built with a high-performance **Rust (Axum)** backend and a modern **React (TypeScript)** frontend, it ensures security, scalability, and an exceptional user experience.

## Documentation Structure

### ⚙️ Backend Reference
- 🏗️ **[Architecture](backend/architecture.md)**: Deep dive into the Axum framework and Rust logic.
- 🔐 **[Authentication](backend/auth.md)**: JWT, Argon2, and TOTP (2FA) implementation.
- 🗄️ **[Database & Models](backend/database.md)**: SQLx schema and data structures.

### 🎨 Frontend Reference
- ⚡ **[Frontend Stack](frontend/stack.md)**: React 18, Vite, and Tailwind CSS.
- 🚦 **[Routing & Guards](frontend/routing.md)**: Role-based route protection.
- 🌍 **[Internationalization](frontend/i18n.md)**: Multi-language support logic.

### 🛠️ Technical & DevOps
- 🚀 **[Production Guide](technical/production.md)**: PostgreSQL migration and security headers.
- 📦 **[Deployment](technical/deployment.md)**: Docker and environment configuration.
- 👥 **[Role-Based Access Control (RBAC)](technical/rbac.md)**: Permission levels and capabilities.

## Core Features

1.  **Unified Management**: Manage team members, blog posts, and internal news from a single interface.
2.  **Interactive Ticketing**: A robust support system with real-time status updates and comments.
3.  **Client Portal**: Secure area for clients to track their active services and open tickets.
4.  **Security First**: Enterprise-grade security with HttpOnly cookies, Argon2 hashing, and full 2FA support.
5.  **Analytics**: Built-in statistics for tracking team productivity and service growth.
