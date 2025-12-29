# Production & Scaling Guide

Moving from development to production requires several architectural shifts to ensure stability and performance.

## 🗄️ 1. Database Migration (SQLite -> PostgreSQL)

**Why**: SQLite is excellent for development but struggles with high concurrency and large binary blobs.

**Steps**:
1.  Change `DATABASE_URL` in `.env` to a PostgreSQL connection string.
2.  Enable the `postgres` feature in `backend/Cargo.toml`:
    ```toml
    sqlx = { version = "0.7", features = ["runtime-tokio-native-tls", "postgres", "uuid", "chrono", "macros"] }
    ```
3.  Migrate queries: PostgreSQL uses `$1, $2` placeholders instead of SQLite's `?`. Update all queries in `database.rs`.

## 🖼️ 2. Blob Storage Strategy

**Current**: Profile pictures are stored as Base64 strings directly in the DB.
**Production Recommendation**: 
- Transition to using an **S3-compatible bucket** (Amazon S3, MinIO, Cloudflare R2).
- Update the backend to store only the *URL* or *Object Key* in the database.
- Use a dedicated directory like `/uploads` if storing locally, but ensure it is persistent and backed up.

## 🛡️ 3. Security Headers

Ensure your reverse proxy (Nginx, Caddy, or Cloudflare) is configured with these essential headers:

- `Strict-Transport-Security`: Forces HTTPS.
- `Content-Security-Policy`: Mitigates XSS and data injection.
- `X-Frame-Options`: Prevents Clickjacking attacks.
- `X-Content-Type-Options`: Disables MIME-type sniffing.

## 🚀 4. Performance Tuning

- **Connection Pooling**: Tune the SQLx pool size based on your CPU cores and expected load.
- **Backend Build**: Always build the backend using `--release` to enable Rust's full optimizations.
- **Frontend Build**: Use `npm run build` to generate optimized static files.
