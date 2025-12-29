# Backend Architecture

The backend is built with **Rust** using the **Axum** web framework. It follows an asynchronous, thread-safe design tailored for high performance.

## Core Stack

- **Web Framework**: [Axum](https://github.com/tokio-rs/axum)
- **Runtime**: [Tokio](https://tokio.rs/)
- **Database**: [SQLx](https://github.com/launchbadge/sqlx) (SQLite/PostgreSQL)
- **Serialization**: [Serde](https://serde.rs/)
- **Logging**: [Tracing](https://github.com/tokio-rs/tracing)

## Project Structure

```text
backend/src/
├── auth.rs           # Security logic (Hashing, JWT, Password rules)
├── database.rs       # Raw SQLx queries and DB init
├── handlers_*.rs     # Request handlers grouped by domain:
│   ├── handlers_auth.rs    # Login, Register, 2FA
│   ├── handlers_tickets.rs # CRUD for tickets
│   ├── handlers_tasks.rs   # Team task management
│   └── handlers_members.rs # Team profile management
├── main.rs           # Router setup, CORS, App State
├── middleware.rs     # Auth checks interceptor
├── models.rs         # Structs mirroring DB tables & JSON
└── totp.rs           # Two-Factor (Google Authenticator) logic
```

## Internal Flow

1.  **Initialization**: `main.rs` loads environment variables, initializes the database pool, and wraps them in an `Arc<AppState>`.
2.  **Routing**: Routes are defined with nested scopes (e.g., `/api/auth`, `/api/tickets`).
3.  **Middleware**: The `auth_middleware` interceptor runs before protected routes to validate JWT claims.
4.  **Handlers**: Extract state and request body, perform logic, and return JSON responses.
5.  **Database**: All queries are handled asynchronously via `sqlx`.

## Concurrency & State

The `AppState` is shared across all threads:
```rust
pub struct AppState {
    pub db: SqlitePool, // or PgPool
    pub jwt_secret: String,
    pub registration_secret: String,
}
```
This ensures that the application can handle multiple concurrent requests without data races or performance bottlenecks.
