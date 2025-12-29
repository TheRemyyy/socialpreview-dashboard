# Frontend Stack & Design

The frontend is a modern Single Page Application (SPA) built for speed and responsiveness.

## ⚡ Core Technologies

- **Library**: React 18
- **Language**: TypeScript (Strict mode)
- **Build Tool**: Vite
- **Styling**: Tailwind CSS
- **Icons**: Lucide React

## 📂 Component Architecture

Components are organized by atomic design principles:

- `src/components/ui/`: Reusable primitive components (Button, Modal, Card).
- `src/components/dashboard/`: Large layout components for different dashboard views.
- `src/routes/`: Top-level page components managed by React Router.

## 🧠 State Management

We use the **React Context API** for global state:

1.  **AuthContext**: Manages the logged-in user, token persistence, and login/logout logic.
2.  **LanguageContext**: Handles i18n switching and persists the user's preferred language.

## 🎨 Theme & UI

Tailwind CSS provides a utility-first styling approach.
- **Dark Mode**: Supported via class-based toggling.
- **Responsive**: Mobile-first design with a collapsible sidebar for desktops.
