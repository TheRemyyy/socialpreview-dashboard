# Deployment & Operations

SocialPreview Dashboard is container-ready and can be deployed using Docker for both backend and frontend components.

## 🐳 Dockerization

The project uses a multi-stage build process to keep the final images as small as possible.

### Backend Deployment
- **Base**: `messense/rust-musl-cross` for static binary compilation.
- **Runtime**: `scratch` (the smallest possible image).
- **Network**: Exposes port 3000 by default.

### Frontend Deployment
- **Base**: `node:20-alpine` for building the optimized SPA.
- **Runtime**: `nginx:alpine` for serving static assets.
- **Config**: Includes a custom `nginx.conf` to handle React Router navigation (SPA fallback).

## ⚙️ Environment Variables

### Backend (`.env`)
| Variable | Description |
| :--- | :--- |
| `DATABASE_URL` | SQLite path or PostgreSQL connection string. |
| `JWT_SECRET` | Strong random key for signing tokens. |
| `REGISTRATION_SECRET`| Secret required for the initial admin registration. |
| `FRONTEND_URL` | URL of the frontend (for CORS). |

### Frontend (`.env`)
| Variable | Description |
| :--- | :--- |
| `VITE_API_BASE_URL`| Full URL of the backend API. |

## 🚀 Deployment Workflow

1.  **Build Images**:
    ```bash
    docker build -t socialpreview-backend ./backend
    docker build -t socialpreview-frontend ./frontend
    ```
2.  **Run with Compose**:
    Recommended for orchestration with a database.
    ```yaml
    services:
      db: { image: postgres }
      backend: { image: socialpreview-backend }
      frontend: { image: socialpreview-frontend }
    ```
3.  **Reverse Proxy**: Always use a reverse proxy (Nginx/Caddy) to handle SSL termination and security headers.
