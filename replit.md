# Chebyshev Filter Calculator

## Overview

A professional web application for calculating Chebyshev filter g-values (coefficients) for engineering applications. The application provides precision calculations for filter orders 1-30 with customizable passband ripple specifications. Built as a full-stack TypeScript application with a React frontend and Express backend, it offers both single-order and batch calculation modes with real-time computation and export capabilities.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18 with TypeScript, bundled using Vite

**UI Component System**: shadcn/ui (Radix UI primitives) with Tailwind CSS
- **Design Philosophy**: Material Design-inspired approach focused on clarity, data-dense presentations, and functional efficiency for engineering tools
- **Typography**: Inter font family for UI, JetBrains Mono for numerical data to ensure proper alignment
- **Theme System**: Light/dark mode support with CSS custom properties for theming
- **Component Strategy**: Modular, accessible components built on Radix UI primitives

**State Management**:
- React Hook Form with Zod validation for form state
- TanStack Query (React Query) for server state management and API data caching
- Local React state for UI interactions (theme toggle, mode selection)

**Routing**: Wouter for lightweight client-side routing

**Key Architectural Decisions**:
- **Component Library Choice**: Selected shadcn/ui over pre-built libraries to maintain design flexibility while ensuring accessibility through Radix UI primitives
- **Form Validation**: Zod schemas provide type-safe validation shared between client and server
- **No Database on Frontend**: All persistent data comes from API, frontend focuses on presentation and interaction

### Backend Architecture

**Runtime**: Node.js with Express framework

**Language**: TypeScript with ES modules

**API Design**: RESTful API with single calculation endpoint (`/api/calculate`)
- Accepts mode (single/batch), filter order, and passband ripple parameters
- Returns computed g-values for requested configuration

**Calculation Engine**: 
- Pure TypeScript implementation of Chebyshev filter mathematics
- Follows reference formulas (4.7.6 to 4.7.13) for precision
- Uses standard JavaScript Math library for calculations
- Handles edge cases for odd/even filter orders

**Development vs Production**:
- **Development**: Vite dev server integrated as Express middleware with HMR support
- **Production**: Pre-built static assets served by Express
- Separate entry points (`index-dev.ts`, `index-prod.ts`) for environment-specific configuration

**Key Architectural Decisions**:
- **Stateless API**: Calculations are performed on-demand without storing results, prioritizing computation accuracy over caching
- **Server-side Computation**: Complex mathematical operations handled on backend to ensure consistency and precision
- **Shared Validation**: Zod schemas in `/shared` directory used by both frontend and backend

### Data Storage Solutions

**Database**: PostgreSQL (via Neon serverless driver)
- **ORM**: Drizzle ORM with type-safe query builder
- **Schema Location**: `shared/schema.ts` (shared type definitions)
- **Migration Strategy**: Drizzle Kit for schema migrations stored in `/migrations`

**Current Usage**: Database infrastructure is configured but not actively used for the calculator functionality. The storage layer (`server/storage.ts`) provides an abstraction with `MemStorage` implementation, suggesting future data persistence features may be planned.

**Key Architectural Decisions**:
- **Database Ready**: Infrastructure in place for future features (saved calculations, user profiles, etc.)
- **Session Management**: connect-pg-simple configured for PostgreSQL-backed sessions
- **Current State**: Application operates statelessly; database not required for core functionality

### External Dependencies

**Frontend Libraries**:
- `@tanstack/react-query`: Server state management
- `react-hook-form`: Form state management
- `@hookform/resolvers`: Form validation integration
- `zod`: Runtime type validation
- `wouter`: Lightweight routing
- `lucide-react`: Icon system
- `date-fns`: Date formatting utilities
- `class-variance-authority` & `clsx`: Conditional styling utilities
- `tailwind-merge`: Tailwind class merging
- `cmdk`: Command palette component
- `embla-carousel-react`: Carousel functionality
- Multiple `@radix-ui/*` packages: Accessible UI primitives

**Backend Libraries**:
- `express`: Web server framework
- `drizzle-orm`: Database ORM
- `@neondatabase/serverless`: PostgreSQL driver for Neon
- `connect-pg-simple`: PostgreSQL session store
- `nanoid`: Unique ID generation

**Build Tools**:
- `vite`: Frontend build tool and dev server
- `esbuild`: Backend bundling
- `tsx`: TypeScript execution for development
- `tailwindcss`: Utility-first CSS framework
- `postcss`: CSS processing
- `autoprefixer`: CSS vendor prefixing
- `drizzle-kit`: Database migration toolkit

**Development Tools**:
- `@replit/vite-plugin-runtime-error-modal`: Error overlay for Replit
- `@replit/vite-plugin-cartographer`: Replit integration
- `@replit/vite-plugin-dev-banner`: Development banner

**Key Architectural Decisions**:
- **Neon Serverless PostgreSQL**: Chosen for Replit compatibility and serverless architecture
- **Vite over Webpack**: Faster development experience with native ES modules
- **Minimal Backend Dependencies**: Express-only approach keeps server lightweight and focused
- **shadcn/ui Pattern**: Copy-paste components rather than package dependency reduces bundle size and increases customization flexibility