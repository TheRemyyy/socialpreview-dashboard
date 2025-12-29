# Database & Models

SocialPreview Dashboard uses **SQLx** for type-safe database interactions. It supports **SQLite** for local development and is ready for **PostgreSQL** in production.

## 🗄️ Database Schema

The system relies on several core tables to manage users, tickets, tasks, and services.

### `users` table
The heart of the system's identity management.
- `id`: UUID (Primary Key)
- `name`: Full name
- `nickname`: Display name
- `email`: Unique login email
- `password_hash`: Argon2 hashed password
- `role`: user / team / management
- `totp_secret`: Encrypted 2FA secret
- `totp_enabled`: Boolean flag for 2FA

### `tickets` table
- `id`: UUID
- `user_id`: ID of the client who created the ticket
- `assigned_to`: ID of the team member handling the ticket
- `status`: open / in_progress / resolved / closed
- `priority`: low / medium / high / urgent

### `tasks` table
- `id`: UUID
- `created_by`: ID of the staff member
- `priority`: task priority levels
- `status`: pending / in_progress / completed / cancelled

## 🧬 Rust Models (`models.rs`)

The application uses Serde for seamless serialization between DB rows and JSON responses.

### User Role Enum
```rust
pub enum UserRole {
    Management,
    Team,
    User,
}
```

### Claims Struct
Used for JWT token encoding/decoding:
```rust
pub struct Claims {
    pub sub: String, // User UUID
    pub email: String,
    pub role: UserRole,
    pub exp: usize,
}
```

## 🛠️ Migrations

Migrations are managed via the `sqlx-cli`. They are located in `backend/migrations/`.
To run migrations manually:
```bash
sqlx migrate run
```
The backend also automatically runs migrations on startup via the `init_db` function.
