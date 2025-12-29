# Role-Based Access Control (RBAC)

The application implements a strict security model based on user roles. Permissions are enforced both in the backend (middleware) and the frontend (component rendering).

## 👥 User Roles

### 1. Management (`management`)
The highest privilege level.
- **Access**: Full system access.
- **Capabilities**:
    - Manage all users (create, edit, delete).
    - Manage all tickets, tasks, and services.
    - View global statistics.
    - System-wide configuration.

### 2. Team (`team`)
Staff members responsible for day-to-day operations.
- **Access**: Full access to operational modules.
- **Capabilities**:
    - Manage all tickets and tasks.
    - View and update client services.
    - Post news and blog articles.
    - **Restriction**: Cannot delete other members or modify system settings.

### 3. User (`user`)
External clients or customers.
- **Access**: Scoped to own data only.
- **Capabilities**:
    - Create and reply to own support tickets.
    - View own active services.
    - Manage personal profile and security (2FA).
    - **Restriction**: No access to internal team features (tasks, news, statistics).

## 🔒 Enforcement

### Backend (Rust)
Middleware checks the `role` claim in the JWT token.
```rust
if claims.role != UserRole::Management {
    return Err(StatusCode::FORBIDDEN);
}
```

### Frontend (React)
The `<ProtectedRoute>` and `DashboardRouter` ensure that users only see the interface relevant to their role.
