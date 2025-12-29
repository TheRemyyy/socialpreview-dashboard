# Routing & Access Guards

The frontend uses **React Router DOM v6** to manage navigation and protect sensitive views.

## 🚦 Navigation Logic

Routing is defined in `App.tsx`. We distinguish between public and private routes.

### Public Routes
- `/login`: The entry point for all users.

### Protected Routes
Protected routes are wrapped in a `<ProtectedRoute>` component. This component:
1.  Verifies the existence of a token.
2.  Fetches the user profile if not already in state.
3.  Redirects to `/login` if unauthorized.

## 👥 Role-Based Rendering

Inside the dashboard, we use a dispatcher to render the appropriate view based on the user's role:

```tsx
// Simplified logic
{user.role === 'management' || user.role === 'team' ? (
    <TeamDashboard />
) : (
    <UserDashboard />
)}
```

## 🔐 XSS Protection

All dynamic user input is sanitized using `dompurify` before rendering to prevent malicious script execution from ticket comments or blog posts.
