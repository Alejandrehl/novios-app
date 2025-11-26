# Cursor Rules - Wedding Platform (Página de Novios)

This directory contains Cursor rules that define the standards, patterns, and guidelines for the Wedding Platform project.

## Rules Overview

Each rule file has a specific, non-overlapping responsibility to maximize context engineering efficiency.

### Rule File Format

All rule files follow this YAML frontmatter structure:

```yaml
---
alwaysApply: true/false          # Whether rule loads in every interaction
description: "Brief description"  # One-line summary of the rule
keywords: ["key", "words"]       # Keywords for search/discovery
relevantWhen: ["when", "to use"] # When this rule should be applied
---
```

### 1. `behavior.mdc` ⚡ (Always Applied)

WHO executes and HOW they work

- Agent identity and autonomy level
- Code language policy (English only)
- **i18n implementation** (MANDATORY - no hardcoded text)
- Communication style
- **TDD methodology** (Red-Green-Refactor)
- **Test coverage requirements** (>80%)
- **Zero linting tolerance** policy
- **Husky pre-commit hooks** enforcement
- Conventional Commits workflow
- Refactoring practices
- Quality standards and gates

**Relevant when**: Generating code, making architectural decisions, communicating changes, planning features, debugging, committing code, writing documentation, handling errors, validating input.

### 2. `stack.mdc` ⚡ (Always Applied)

WHAT technologies to use

- Next.js 16 (App Router), TypeScript, Tailwind CSS
- shadcn/ui, React Hook Form, Zod
- PostgreSQL, Prisma ORM
- Auth.js (NextAuth), Mercado Pago
- pnpm, Vitest, Playwright
- Husky, ESLint, Prettier, Commitlint
- i18n packages (@formatjs/intl-localematcher, negotiator)
- Version specifications and installation commands
- Prohibited technologies

**Relevant when**: Creating files, installing packages, making technology choices, implementing features, setting up configuration, structuring project, choosing auth methods, selecting database, implementing forms and validation.

### 3. `architecture.mdc` ⚡ (Always Applied)

HOW the code should be structured

- Layered architecture (Presentation, API, Service, Repository, Database)
- Folder structure and organization
- Server Components vs Client Components patterns
- Server Actions usage
- API Route Handlers patterns
- Service layer patterns (business logic)
- Repository layer patterns (data access)
- Zod schema organization
- Error handling patterns
- Type safety patterns
- File naming conventions
- Import order

**Relevant when**: Structuring features, creating files, organizing code, implementing business logic, accessing database, handling errors, creating Server/Client Components, writing Server Actions, creating API routes, validating data, managing types.

### 4. `project.mdc` ⚡ (Always Applied)

WHAT the platform does (business requirements)

- Product overview and MVP scope
- Data models (Prisma schema)
- Feature specifications (Auth, Dashboard, Public Pages, Payments, Guest Management)
- User flows
- Business rules
- UI/UX requirements
- Performance targets
- Security requirements

**Relevant when**: Implementing features, designing database schema, creating API endpoints, building UI components, validating user input, handling payments, writing business logic, making architectural decisions, understanding requirements.

### 5. `infrastructure.mdc` (Contextual)

WHERE and HOW the app runs

- Hosting (Vercel)
- Database hosting (Neon/Railway/Supabase)
- Environment variables
- Build configuration (Next.js, TypeScript, Tailwind, ESLint, Prettier)
- Database migrations
- CI/CD pipeline (GitHub Actions)
- Monitoring and logging
- Backups
- Performance optimization
- Scaling considerations
- Security checklist

**Relevant when**: Setting up environments, deploying to production, configuring database, setting environment variables, implementing CI/CD, monitoring application, scaling application, creating backups, optimizing performance, troubleshooting issues.

### 6. `team.mdc` (Contextual)

WHO is working on the project

- Team members (Alejandro, Rodrigo, Diego)
- Roles and responsibilities
- Decision-making authority
- Code review process
- Communication guidelines
- Expertise areas
- Development workflow
- Conflict resolution

**Relevant when**: Making product decisions, making technical decisions, making design decisions, requesting code reviews, resolving conflicts, assigning tasks, communicating with team, understanding expertise areas, escalating issues, planning features.

## Rules Priority

### Always Applied Rules (⚡)

These rules are loaded for EVERY interaction:

1. **behavior.mdc** - Agent methodology
2. **stack.mdc** - Technology choices
3. **architecture.mdc** - Code structure
4. **project.mdc** - Business requirements

### Contextual Rules

These rules are loaded when needed:

1. **infrastructure.mdc** - When deploying or configuring infrastructure
2. **team.mdc** - When considering team processes or decisions

## Key Principles

### 🚫 No Duplication

Each rule file contains ONLY its specific domain:

- **behavior.mdc**: Methodology and how agent works
- **stack.mdc**: Technology list and versions
- **architecture.mdc**: Code patterns and structure
- **project.mdc**: Business requirements and features
- **infrastructure.mdc**: Deployment and configuration
- **team.mdc**: Team composition and processes

### ✅ No Overlapping

Rules do NOT duplicate information:

- i18n **implementation** → behavior.mdc (how agent works)
- i18n **packages** → stack.mdc (what to install)
- TypeScript **usage patterns** → architecture.mdc (how to structure)
- TypeScript **version** → stack.mdc (what version)
- TypeScript **config** → infrastructure.mdc (build setup)

### 📊 Context Engineering Optimized

- Concise descriptions
- Clear separation of concerns
- No redundant examples
- Only real, verified information
- Optimized for AI context windows
- `relevantWhen` in frontmatter for precise rule loading

## Frontmatter Reference

### `alwaysApply`

- **Type**: `boolean`
- **Values**: `true` | `false`
- **Purpose**: Determines if rule loads in every AI interaction
- **Usage**:
  - `true`: Core rules that should always be active (behavior, stack, architecture, project)
  - `false`: Contextual rules loaded only when needed (infrastructure, team)

### `description`

- **Type**: `string`
- **Purpose**: Brief one-line summary of the rule's content
- **Format**: Plain text, no markdown
- **Length**: Keep under 200 characters
- **Example**: `"Agent behavior and work methodology. HOW the AI should work..."`

### `keywords`

- **Type**: `array of strings`
- **Purpose**: Keywords for search and discovery
- **Format**: Lowercase, specific terms
- **Example**: `["behavior", "TDD", "i18n", "testing"]`

### `relevantWhen`

- **Type**: `array of strings`
- **Purpose**: Defines when this rule should be applied
- **Format**: Action-oriented phrases
- **Example**: `["generating code", "committing changes", "testing features"]`
- **Best Practices**:
  - Use present participle (verb + -ing)
  - Be specific about the context
  - Cover all use cases for the rule

## Version History

### v2.1.0 (2024-11-26) - Frontmatter Optimization

**Changes**:

- **Added `relevantWhen` to frontmatter** - Moved from section at end of files
- **Removed redundant sections** - Eliminated "Always Apply" and "Relevant When" headings
- **Documented frontmatter structure** - Added reference guide for all fields
- **Updated README** - Comprehensive documentation of rule format

**Benefits**:

- More efficient context loading
- Clearer rule triggering conditions
- Better AI understanding of when to apply rules
- Consistent structure across all rule files

### v2.0.0 (2024-11-26) - Context Engineering Optimization

**Major Changes**:

- **Eliminated all redundancies** across files
- **Clear separation** of concerns (WHO/WHAT/HOW/WHERE)
- **Optimized for context engineering** (no duplications)
- **Removed outdated** "only Spanish for MVP" (now bilingual en/es)
- **Consolidated i18n**: Implementation in behavior, packages in stack
- **Simplified stack.mdc**: Only technology list, no code examples
- **Cleaned project.mdc**: Removed duplicated error handling, testing strategy
- **Streamlined infrastructure.mdc**: Added missing configs, removed Husky details (in behavior)

**Consistency Improvements**:

- All user-facing text must use i18n (no hardcoded text)
- All routes prefixed with `[lang]` for internationalization
- All code and comments in English (user text in dictionaries)
- All files pass linting with zero errors/warnings

### v1.1.0 (2024-11-25) - TDD and Quality Gates

- Added mandatory TDD (Red-Green-Refactor)
- Added >80% test coverage requirement
- Added zero linting tolerance policy
- Added Husky pre-commit hooks enforcement
- Updated behavior.mdc and stack.mdc with testing details

### v1.0.0 (2024-11-24) - Initial Rules

- Created initial rule set
- Defined behavior, stack, architecture, project, infrastructure, team
- Established Conventional Commits workflow
- Defined MVP scope and features

## How to Use

### For AI Agents

1. **Always** load behavior, stack, architecture, and project rules
2. **Conditionally** load infrastructure when deploying
3. **Conditionally** load team when making decisions
4. **Follow** all mandatory requirements (i18n, TDD, zero linting)
5. **Enforce** quality gates before commits
6. **Check `relevantWhen`** to determine rule applicability

### For Developers

1. **Read** relevant rule files before starting work
2. **Follow** patterns defined in architecture.mdc
3. **Use** technologies specified in stack.mdc
4. **Implement** features according to project.mdc
5. **Test** following TDD methodology in behavior.mdc
6. **Ensure** zero linting errors before committing

### For Team Leads

1. **Enforce** mandatory rules (TDD, coverage, linting)
2. **Review** code against architecture patterns
3. **Ensure** business rules from project.mdc are met
4. **Verify** team processes in team.mdc are followed
5. **Update** rules when requirements evolve

## Updating Rules

### When to Update

- Stack changes (new technology, version upgrade)
- New patterns established
- Project requirements evolve
- Team composition changes
- Infrastructure changes
- Process improvements

### How to Update

1. Identify the correct file for your change
2. Ensure no overlap with other files
3. Keep examples concise and real
4. Update frontmatter if needed (especially `relevantWhen`)
5. Update version history in this README
6. Ensure all linting passes
7. Get team approval for major changes

### Frontmatter Update Guidelines

When updating frontmatter:

- **`alwaysApply`**: Only change if rule's loading strategy changes
- **`description`**: Update if rule's scope or purpose changes
- **`keywords`**: Add new keywords when adding new concepts
- **`relevantWhen`**: Update when adding new use cases or features

### Rule Ownership

- **behavior.mdc**: Tech Lead (Rodrigo)
- **stack.mdc**: Tech Lead (Rodrigo)
- **architecture.mdc**: Tech Lead (Rodrigo)
- **project.mdc**: Product Owner (Alejandro)
- **infrastructure.mdc**: Tech Lead (Rodrigo)
- **team.mdc**: All team members

## Contact

For questions or suggestions about these rules:

- **Product**: Alejandro Exequiel Hernández Lara - [LinkedIn](https://www.linkedin.com/in/alejandrehl/)
- **Technical**: Rodrigo Eduardo Guerrero Godoy - [LinkedIn](https://www.linkedin.com/in/rodrigoguerrerogodoy/)
- **Design**: Diego Emilio Fuentes Gómez - [LinkedIn](https://www.linkedin.com/in/diegoemiliofuentesgomez/)

## Repository

**GitHub**: [github.com/Alejandrehl/novios-app](https://github.com/Alejandrehl/novios-app)

---

**Last Updated**: November 26, 2025
**Version**: 2.1.0
**Status**: ✅ Optimized for Context Engineering with Frontmatter
