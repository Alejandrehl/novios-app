# Wedding Platform (Página de Novios)

A modern, full-stack wedding management platform built with Next.js 15, TypeScript, and PostgreSQL. Couples can create personalized wedding pages, manage guest lists with RSVP functionality, and receive monetary contributions via Mercado Pago.

## 🎯 Project Overview

**Status**: 🚧 Initial Setup - MVP in Development

**Reference**: Similar to [milistadenovios.cl](https://milistadenovios.cl/)

### Key Features

- ✅ User authentication (email/password)
- ✅ Wedding creation and management
- ✅ Guest list management with RSVP system
- ✅ Monetary contribution system (Mercado Pago)
- ✅ Public wedding pages (`/[lang]/boda/[slug]`)
- ✅ Private dashboard for couples
- ✅ Payment webhook handling
- ✅ Responsive design (mobile-first)
- ✅ Internationalization (English/Spanish)

## 🛠️ Tech Stack

### Frontend + Backend

- **Framework**: Next.js 15+ (App Router)
- **Language**: TypeScript (strict mode)
- **Styling**: Tailwind CSS
- **UI Components**: shadcn/ui
- **Forms**: React Hook Form + Zod

### Database & ORM

- **Database**: PostgreSQL 14+
- **ORM**: Prisma 5+
- **Hosting**: Neon / Railway / Supabase

### Authentication & Payments

- **Auth**: Auth.js (NextAuth.js v5)
- **Payments**: Mercado Pago

### Development Tools

- **Package Manager**: pnpm
- **Testing**: Vitest (unit/integration) + Playwright (E2E)
- **Linting**: ESLint + Prettier
- **Git Hooks**: Husky + lint-staged
- **Commits**: Commitlint (Conventional Commits)

### Internationalization

- **Approach**: Next.js dictionary-based i18n
- **Locales**: English (default), Spanish
- **Packages**: @formatjs/intl-localematcher, negotiator

## 📋 Prerequisites

- Node.js 20+
- pnpm 8+
- PostgreSQL 14+ (or Neon/Railway/Supabase account)
- Mercado Pago account (for payments)

## 🚀 Getting Started

### 1. Clone and Install

```bash
# Clone repository
git clone <repository-url>
cd novios-app

# Install dependencies
pnpm install
```

### 2. Environment Setup

Create `.env.local` file in the root directory:

```bash
# Database
DATABASE_URL="postgresql://user:pass@host:5432/db?pgbouncer=true"
DIRECT_URL="postgresql://user:pass@host:5432/db"

# Auth
NEXTAUTH_SECRET="generate-with-openssl-rand-base64-32"
NEXTAUTH_URL="http://localhost:3000"

# Mercado Pago
MERCADOPAGO_ACCESS_TOKEN="TEST-xxx-xxx"
MERCADOPAGO_PUBLIC_KEY="TEST-xxx-xxx"
MERCADOPAGO_WEBHOOK_SECRET="your-webhook-secret"

# App
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

**Generate NEXTAUTH_SECRET**:

```bash
openssl rand -base64 32
```

### 3. Database Setup

```bash
# Generate Prisma Client
pnpm prisma generate

# Run migrations
pnpm prisma migrate dev

# (Optional) Seed database
pnpm db:seed
```

### 4. Start Development Server

```bash
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📁 Project Structure

```text
novios-app/
├── app/
│   ├── [lang]/                    # Internationalized routes
│   │   ├── dictionaries/         # Translation files (en.json, es.json)
│   │   ├── dictionaries.ts       # Dictionary loader
│   │   ├── (auth)/               # Auth route group
│   │   │   ├── login/
│   │   │   └── register/
│   │   ├── (dashboard)/          # Protected dashboard
│   │   │   ├── layout.tsx       # Dashboard layout with auth
│   │   │   └── weddings/        # Wedding management
│   │   └── boda/                # Public wedding pages
│   │       └── [slug]/
│   ├── api/                      # API routes (Route Handlers)
│   │   ├── auth/                # Auth endpoints
│   │   └── payments/            # Payment endpoints
│   └── globals.css
│
├── components/
│   ├── ui/                       # shadcn/ui components
│   ├── forms/                    # Form components
│   ├── features/                 # Feature-specific components
│   └── layout/                   # Layout components
│
├── lib/
│   ├── services/                 # Business logic layer
│   ├── repositories/             # Data access layer (Prisma)
│   ├── schemas/                  # Zod validation schemas
│   ├── actions/                  # Server Actions
│   ├── auth/                     # Auth.js configuration
│   ├── utils/                    # Utility functions
│   ├── types/                    # TypeScript types
│   ├── prisma.ts                # Prisma client
│   └── env.ts                   # Environment validation
│
├── prisma/
│   ├── schema.prisma            # Database schema
│   ├── migrations/              # Database migrations
│   └── seed.ts                  # Seed data
│
├── public/                       # Static assets
├── .cursor/rules/               # Cursor AI rules
└── README.md
```

## 🧪 Testing

### Run Tests

```bash
# Unit/Integration tests
pnpm test

# Watch mode
pnpm test:watch

# Coverage report (must be >80%)
pnpm test:coverage

# UI for debugging
pnpm test:ui

# E2E tests
pnpm test:e2e

# E2E UI
pnpm test:e2e:ui
```

### Test-Driven Development (TDD)

**MANDATORY**: All features must follow TDD (Red-Green-Refactor).

1. **Red**: Write failing test
2. **Green**: Implement minimal code to pass
3. **Refactor**: Improve code while keeping tests green

**Coverage Requirements**:

- Services: >90%
- Repositories: >85%
- Utilities: >80%
- Complex business logic: 100%

## 🎨 Code Quality

### Linting & Formatting

```bash
# Run ESLint (must pass with zero warnings)
pnpm lint

# Fix ESLint errors
pnpm lint:fix

# Format with Prettier
pnpm format

# Type check
pnpm type-check
```

### Pre-commit Hooks

Husky enforces quality gates before every commit:

- ✅ ESLint (zero errors/warnings)
- ✅ Prettier formatting
- ✅ TypeScript type checking
- ✅ Tests for changed files
- ✅ Coverage >80%
- ✅ Conventional Commits format

**DO NOT skip hooks** with `--no-verify`.

### Commit Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Feature
feat(wedding): add public wedding page with RSVP form

# Bug fix
fix(dashboard): correct guest count calculation

# Refactor
refactor(services): extract payment logic to separate service

# Documentation
docs: update README with installation instructions

# Tests
test(wedding): add unit tests for WeddingService

# Chore
chore(deps): upgrade Next.js to 15.1.0
```

## 🌐 Internationalization (i18n)

**MANDATORY**: All user-facing text must use i18n dictionaries.

### Adding Translations

Add keys to both `app/[lang]/dictionaries/en.json` and `es.json`:

```json
{
  "common": {
    "save": "Save" // en.json
    "save": "Guardar" // es.json
  }
}
```

Use in Server Components:

```typescript
import { getDictionary } from "@/app/[lang]/dictionaries";

export default async function Page({ params }) {
  const { lang } = await params;
  const dict = await getDictionary(lang);
  
  return <button>{dict.common.save}</button>;
}
```

Pass to Client Components:

```typescript
"use client";

interface Props {
  dict: Dictionary["common"];
}

export function MyComponent({ dict }: Props) {
  return <button>{dict.save}</button>;
}
```

### Important Rule

❌ NEVER hardcode user-facing text in components

## 🗄️ Database

### Prisma Commands

```bash
# Generate Prisma Client
pnpm prisma generate

# Create migration
pnpm prisma migrate dev --name add_wedding_table

# Apply migrations
pnpm prisma migrate dev

# Deploy migrations (production)
pnpm prisma migrate deploy

# Open Prisma Studio
pnpm prisma studio

# Reset database (development only)
pnpm prisma migrate reset
```

### Data Models

- **User**: Wedding organizers (couples)
- **Wedding**: Wedding event with details and slug
- **Guest**: Invited people with RSVP status
- **Contribution**: Monetary contributions with payment status
- **PaymentConfig**: Payment provider configuration

## 🚢 Deployment

### Vercel (Recommended)

1. Connect repository to Vercel
2. Set environment variables in Vercel dashboard
3. Deploy automatically on push to `main`

### Environment Variables (Production)

```bash
DATABASE_URL="postgresql://..."
DIRECT_URL="postgresql://..."
NEXTAUTH_SECRET="strong-secret-for-production"
NEXTAUTH_URL="https://yourdomain.com"
MERCADOPAGO_ACCESS_TOKEN="APP-xxx-xxx"
MERCADOPAGO_PUBLIC_KEY="APP-xxx-xxx"
NEXT_PUBLIC_APP_URL="https://yourdomain.com"
```

### Pre-deployment Checklist

- [ ] All tests passing
- [ ] Coverage >80%
- [ ] Zero linting errors
- [ ] Environment variables set
- [ ] Database migrations applied
- [ ] NEXTAUTH_SECRET is strong and unique
- [ ] Mercado Pago uses production credentials

## 📖 Documentation

### Cursor AI Rules

This project uses Cursor AI rules for consistent development. See [`.cursor/rules/README.md`](.cursor/rules/README.md) for details.

**Rule Files**:

- `behavior.mdc` - Agent methodology and workflow
- `stack.mdc` - Technology stack and tools
- `architecture.mdc` - Code structure and patterns
- `project.mdc` - Business requirements and features
- `infrastructure.mdc` - Deployment and configuration
- `team.mdc` - Team composition and processes

### Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Auth.js Documentation](https://authjs.dev)
- [Mercado Pago API](https://www.mercadopago.com.ar/developers)

## 👥 Team

- **Alejandro Exequiel Hernández Lara** - Full-Stack Developer & Product Owner - [LinkedIn](https://www.linkedin.com/in/alejandrehl/)
- **Rodrigo Eduardo Guerrero Godoy** - Full-Stack Developer & Tech Lead - [LinkedIn](https://www.linkedin.com/in/rodrigoguerrerogodoy/)
- **Diego Emilio Fuentes Gómez** - Full-Stack Developer & UI/UX Specialist - [LinkedIn](https://www.linkedin.com/in/diegoemiliofuentesgomez/)

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

Copyright (c) 2025 Alejandro Hernández, Rodrigo Guerrero, Diego Fuentes

## 🤝 Contributing

1. Follow all rules in `.cursor/rules/`
2. Write tests first (TDD)
3. Ensure zero linting errors
4. Use Conventional Commits
5. Request review from relevant specialist

---

**Last Updated**: November 26, 2025
**Version**: 0.1.0 (Initial Setup)
**Status**: 🚧 MVP in Development
