# Authentication & Security

Security is handled using a combination of modern cryptographic standards and best practices.

## 🔐 Core Mechanisms

### Password Hashing
- **Algorithm**: Argon2id
- **Library**: `argon2` crate
- **Why**: Resistant to GPU-based brute-force and side-channel attacks.

### JSON Web Tokens (JWT)
- **Library**: `jsonwebtoken`
- **Payload**: Contains `sub` (User UUID), `role`, and `email`.
- **Transmission**: Tokens are sent via the `Authorization: Bearer <token>` header.

### Two-Factor Authentication (2FA)
- **Method**: Time-based One-Time Password (TOTP).
- **Compliance**: Google Authenticator, Authy, etc.
- **Library**: `totp-rs`
- **Flow**: User enables 2FA -> Secret stored in DB (encrypted) -> Codes required on every login.

## 🚦 Authorization (RBAC)

The application implements Role-Based Access Control:

| Role | Internal Name | Context |
| :--- | :--- | :--- |
| **Management** | `management` | Full system access. |
| **Team** | `team` | Privileged access to all tickets/tasks. |
| **User** | `user` | Self-service access (own tickets/services only). |

## 🛡️ Secure Cookies (Production)

In production, we recommend using **Secure HttpOnly Cookies** for JWT storage to mitigate XSS (Cross-Site Scripting) risks. This can be configured in the backend settings.
