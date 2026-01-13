# Strategic Foresight Game Platform

## Overview

This is a Strategic Foresight Game platform for Dubai Police - an enterprise-grade web application for scenario planning, future retreats, and collaborative foresight gaming. The platform supports multiple user roles (Super Admin, Admin, Game Master, Player) with role-based interfaces and navigation. Built as a modern React SPA with an Express backend, it follows Dubai Police Design System v5.0 with a futuristic, glassmorphism-inspired UI.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight alternative to React Router)
- **State Management**: React Context API for auth, language, game state, and design mode
- **Data Fetching**: TanStack React Query for server state management
- **Styling**: Tailwind CSS v4 with custom design tokens following Dubai Police branding
- **UI Components**: Shadcn/ui (New York style) with Radix UI primitives
- **Build Tool**: Vite with custom plugins for Replit integration

### Backend Architecture
- **Runtime**: Node.js with Express
- **API Pattern**: RESTful endpoints prefixed with `/api`
- **Session Management**: Express sessions with connect-pg-simple for PostgreSQL storage
- **Development**: Hot module replacement via Vite middleware in development mode

### Data Storage
- **Database**: PostgreSQL with Drizzle ORM
- **Schema Location**: `shared/schema.ts` - shared between client and server
- **Migrations**: Drizzle Kit with `db:push` command for schema sync
- **In-Memory Fallback**: MemStorage class in `server/storage.ts` for development

### Application Structure
```
client/src/
├── components/     # Reusable UI components
├── contexts/       # React Context providers (Auth, Language, Game, Tour)
├── pages/          # Route-level components organized by role
│   ├── admin/      # Admin (SFD) interface
│   ├── gm/         # Game Master interface
│   ├── player/     # Player interface
│   └── super/      # Super Admin dashboard widgets
├── hooks/          # Custom React hooks
└── lib/            # Utilities and query client

server/
├── index.ts        # Express app entry point
├── routes.ts       # API route definitions
├── storage.ts      # Data access layer interface
├── static.ts       # Static file serving for production
└── vite.ts         # Vite dev server integration

shared/
└── schema.ts       # Drizzle schema + Zod validation
```

### Role-Based Navigation
The platform renders different interfaces based on user role after login:
- **Super Admin**: Full system access, user management, all scenarios/retreats
- **Admin (SFD)**: Game requests approval, scenario oversight, reports
- **Game Master**: Game creation, facilitation, session management
- **Player**: Active games, scenario participation, leaderboards

### Design System
- Custom CSS variables for Dubai Police color palette (brand-green, brand-navy, brand-red)
- Glassmorphism effects with backdrop-blur and semi-transparent cards
- Inter font for body text, Rajdhani for display headings
- Design mode toggle supporting normal, wireframe, and low-fidelity views

## External Dependencies

### Database
- **PostgreSQL**: Primary database via `DATABASE_URL` environment variable
- **Drizzle ORM**: Type-safe database queries and schema management
- **connect-pg-simple**: PostgreSQL session store

### UI Libraries
- **Radix UI**: Accessible component primitives (dialogs, dropdowns, tabs, etc.)
- **Recharts**: Data visualization for dashboards
- **Embla Carousel**: Carousel component
- **Lucide React**: Icon library
- **date-fns**: Date formatting utilities

### Build & Development
- **Vite**: Frontend build tool with React plugin
- **esbuild**: Server bundling for production
- **Tailwind CSS v4**: Utility-first styling with `@tailwindcss/vite` plugin

### Replit-Specific
- **@replit/vite-plugin-runtime-error-modal**: Error overlay in development
- **@replit/vite-plugin-cartographer**: Code navigation assistance
- **@replit/vite-plugin-dev-banner**: Development environment indicator

### Form & Validation
- **React Hook Form**: Form state management
- **Zod**: Schema validation
- **drizzle-zod**: Auto-generate Zod schemas from Drizzle tables