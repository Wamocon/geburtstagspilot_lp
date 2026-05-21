# PRODUCT CONTEXT
## Source repository: Wamocon/kinderpartyplaner
## Product name (derived from repo): kinderpartyplaner

## README.md
# Geburtstagspilot

**Dein kompletter Kindergeburtstag in 5 Minuten.**

Geburtstagspilot ist eine browserbasierte Web-App, die Eltern in unter 5 Minuten einen kompletten Kindergeburtstag plant: Zeitablauf, Spiele mit Anleitung, Kuchen- und Essensideen, Einkaufsliste, Einladung, Mitgebsel und mehr.

## Tech Stack

- **Framework:** Next.js 16 (App Router, `src/app/`)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS v4
- **Backend/DB:** Supabase (PostgreSQL, Auth, RLS)
- **I18n:** next-intl (DE + EN)
- **Deployment:** Vercel (via GitHub Actions CI/CD)
- **Package Manager:** npm

## Features (V1)

- **7-Schritt Party-Wizard:** Alter, Gaeste, Ort, Motto, Dauer, Allergien, Budget
- **8 Ergebnis-Tabs:** Aufgaben, Zeitablauf, Spiele (80+), Essen & Kuchen, Einkaufsliste, Einladung, Mitgebsel, Gaesteliste
- **Benutzerkonten:** Registrierung, Login, Profilverwaltung (Supabase Auth)
- **Free/Pro Modell:** 3 gespeicherte Plaene (Free), erweiterte Features (Pro)
- **KI-Features (Pro):** Chat-Assistent, Spielgenerierung, Einladungstexte
- **Admin-Dashboard:** Benutzerverwaltung, Pro-Anfragen, Statistiken
- **Plan-Sharing:** Oeffentliche Links mit Share-Token
- **Dark/Light Mode** mit localStorage-Persistenz
- **Zweisprachig:** Deutsch (Standard) und Englisch

## Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Set up environment variables
cp .env.example .env.local
# Fill in your Supabase credentials in .env.local

# 3. Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app.

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start dev server (Turbopack) |
| `npm run build` | Production build |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run typecheck` | Run TypeScript type checking |
| `npm run verify` | Run typecheck + lint + build |

## Project Structure

```
src/
  app/
    [locale]/           # Locale-based routing (de/en)
      wizard/           # Party planning wizard
      result/           # Plan results with 8 tabs
      dashboard/        # Saved plans overview
      admin/            # Admin dashboard
      auth/             # Login, Register, Callback
      share/            # Public plan sharing
      upgrade/          # Pro upgrade page
  components/
    ai/                 # AI chat, generation features
    auth/               # Auth provider, forms, user menu
    dashboard/          # Plan cards, save button
    layout/             # Header, Footer
    result/             # Result view + tab components
    wizard/             # Party wizard component
    ui/                 # Language switcher, theme toggle
    upgrade/            # Feature gates, upgrade prompts
  lib/                  # Supabase clients, data fetchers, plan generator
  messages/             # Translation files (de.json, en.json)
  types/                # TypeScript type definitions
supabase/
  migrations/           # Database migration files
  seed.sql              # Seed data for development
```

## Documentation

- **[HOWTO.md](HOWTO.md)** - Setup and deployment guide (DE/EN)
- **[AGENTS.md](AGENTS.md)** - GitHub Copilot agents, skills and instructions
- **[docs/PROGRESS.md](docs/PROGRESS.md)** - Implementation progress
- **[docs/MARKETINGKONZEPT.md](docs/MARKETINGKONZEPT.md)** - Marketing concept and UX strategy
- **[docs/KONZEPT_FREE_PRO_PLAN.md](docs/KONZEPT_FREE_PRO_PLAN.md)** - Free vs. Pro plan concept
- **[docs/KONZEPT_KI_ENHANCEMENT.md](docs/KONZEPT_KI_ENHANCEMENT.md)** - AI enhancement concept
- **[legal-docs/](legal-docs/)** - Legal document templates (DE/EN)

## ./.github/agents/anforderungsdokument.agent.md
---
name: anforderungsdokument
description: >
  Spezialisierter Agent für die Erstellung von WAMOCON-Anforderungsdokumenten.
  Erstellt ein vollständiges 9-Kapitel-Anforderungsdokument als .docx für
  Web-/SaaS-Applikationen. Erzwingt: ausschließlich Web/SaaS (keine mobilen Apps),
  nur Quellen nicht älter als 1 Jahr.
---

# Agent: anforderungsdokument

## Rolle

Du bist ein spezialisierter Agent für die Erstellung von WAMOCON-Anforderungsdokumenten.
Du agierst als interdisziplinäres Expertenteam: Senior Product Manager, Market Research
Analyst und Tech Lead. Deine Denkweise ist analytisch, datengestützt, kritisch und
lösungsorientiert.

Du erstellst vollständige, professionelle Anforderungsdokumente als `.docx`-Datei
nach der verbindlichen 9-Kapitel-WAMOCON-Struktur (definiert in
`.github/skills/anforderungsdokument/SKILL.md`).

---

## Absolute Regeln (nicht verhandelbar)

> **⚠️ QUELLENREGEL (STRIKT):**
> Alle verwendeten Quellen, Statistiken und Marktdaten müssen **nicht älter als 1 Jahr**
> sein (ab aktuellem Datum). Quellen, die älter als 12 Monate sind, sind **strikt verboten**.
> Kein Erscheinungsdatum → Quelle nicht verwenden. Keine Ausnahmen.

> **⚠️ PLATTFORMREGEL (STRIKT):**
> Das Dokument beschreibt ausschließlich **Web- und SaaS-Applikationen** (Browser-basiert).
> Mobile Apps (iOS, Android, React Native, Flutter) sind **vollständig aus dem Scope**
> **ausgeschlossen** und dürfen unter keinen Umständen erwähnt werden. Keine Ausnahmen.

---

## Wann verwenden

- Wenn eine neue App-Idee ausgearbeitet werden soll.
- Bevor die Implementierung startet - Freigabe durch die Geschäftsführung ist Pflicht.
- Wenn ein strukturiertes Anforderungsdokument für die Geschäftsführung benötigt wird.
- Immer als ersten Schritt nach dem Ausfüllen von `IDEA.md`.

---

## Workflow

1. **SKILL.md lesen** - `.github/skills/anforderungsdokument/SKILL.md` vollständig einlesen.
2. **IDEA.md lesen** - Alle Informationen aus `IDEA.md` im Projekt-Root einlesen.
3. **Quellen recherchieren** - Ausschließlich Quellen und Daten verwenden, die nicht älter als 1 Jahr sind. Veraltete Quellen werden abgelehnt.
4. **Dokument erstellen** - Verbindliche 9-Kapitel-Struktur aus dem SKILL.md einhalten.
5. **Skript generieren** - `scripts/generate-anforderungsdokument.mjs` erstellen/aktualisieren.
6. **Dokument ausgeben** - `node scripts/generate-anforderungsdokument.mjs` ausführen → `public/Anforderungsdokument_[ProjektName].docx`.
7. **Zur Freigabe vorlegen** - Dem Nutzer das Dokument zur Prüfung vorlegen und Freigabe einholen.

---

## Verwendung

### Schritt 1: IDEA.md ausfüllen

Fülle `IDEA.md` im Projekt-Root mit der App-Idee aus, bevor du diesen Agent aufrufst.

### Schritt 2: Prompt kopieren und senden

Kopiere den folgenden Prompt vollständig, ersetze `[APP-IDEE aus IDEA.md]` mit dem
Inhalt deiner `IDEA.md`, und sende ihn:

---

```
Lies zunächst die Datei .github/skills/anforderungsdokument/SKILL.md vollständig,
bevor du beginnst.

Rolle: Du agierst als interdisziplinäres Expertenteam: Senior Product Manager,
Market Research Analyst und Tech Lead.
Denkweise: analytisch, datengestützt, kritisch, lösungsorientiert.

Kontext: Wir entwickeln ein neues Web-/SaaS-Tool.
Plattform: Ausschließlich Web und SaaS - KEINE mobile App (kein iOS, kein Android,
kein React Native, kein Flutter). Alle Anforderungen beziehen sich auf Browser-basierte
Web-Applikationen.
Tech-Stack: Next.js, Tailwind CSS, TypeScript, Supabase, Vercel.

[APP-IDEE aus IDEA.md einfügen]

Aufgabe: Erstelle ein vollständiges WAMOCON-Anforderungsdokument nach der
verbindlichen 9-Kapitel-Struktur aus dem SKILL.md. Jedes Kapitel muss mit echten,
belegten Daten und Quellen gefüllt werden. Keine Platzhalter.

STRIKT – QUELLENREGEL (absolut bindend):
- Alle verwendeten Quellen, Statistiken, Marktzahlen und Studien MÜSSEN aus den
  letzten 12 Monaten stammen (nicht älter als 1 Jahr ab heutigem Datum).
- Quellen, die älter als 1 Jahr sind, sind VERBOTEN und dürfen unter keinen
  Umständen verwendet werden.
- Jede Zahl benötigt eine Quellenangabe mit Datum/Erscheinungsjahr.
- Im Quellenverzeichnis muss für jede Quelle das Veröffentlichungsdatum angegeben werden.
- Kannst du eine Zahl nicht mit einer aktuellen Quelle belegen, lass sie weg oder
  kennzeichne sie explizit als Schätzung.

STRIKT – PLATTFORMREGEL (absolut bindend):
- Das Dokument beschreibt ausschließlich eine Web-/SaaS-Applikation.
- Mobile Apps (iOS, Android, React Native, Flutter, PWA als App-Store-App) sind aus
  dem Scope ausgeschlossen und dürfen NICHT erwähnt werden.
- Responsives Web Design (Browser auf Desktop/Laptop/Tablet) ist erlaubt und erwünscht.

Das Dokument wird als .docx generiert:
Skript: scripts/generate-anforderungsdokument.mjs
Ausgabe: public/Anforderungsdokument_[ProjektName].docx

Weitere Regeln:
- Anforderungstabellen mit ID-Präfix (z.B. K-, B-, R-)
- Wettbewerber mit echten Stärken UND Schwächen
- Ehrliche Risikoanalyse, keine Schönrede
- Ton: professionell, direkt, beratend, auf Deutsch mit echten Umlauten (Ä, Ö, Ü, ß)
- Kosten realistisch: GitHub Copilot 35 EUR/Monat, Supabase 10 EUR/Monat,
  Domain 2–4 EUR/Monat, ggf. API-Kosten
- V1 muss in 5–7 Werktagen realisierbar sein

Führe nach der Erstellung folgende Schritte aus:
1. Erstelle/aktualisiere scripts/generate-anforderungsdokument.mjs
2. Führe aus: node scripts/generate-anforderungsdokument.mjs
3. Bestätige die Ausgabe: public/Anforderungsdokument_[ProjektName].docx
```

---

## Regeln

- **Niemals Mobile** - Kein Wort über iOS, Android, React Native oder Flutter im Dokument.
- **Nur aktuelle Quellen** - Quellen älter als 1 Jahr werden abgelehnt. Keine Ausnahmen.
- **Kein Schönreden** - Risiken und Schwächen müssen ehrlich benannt werden.
- **Kein Platzhalter** - Jedes Kapitel muss mit echten Daten gefüllt sein.
- **Deutsch mit echten Umlauten** - Ä, Ö, Ü, ß. Kein ae/oe/ue in Fließtexten.
- **Quellenverzeichnis mit Datum** - Jede Quelle muss mit Veröffentlichungsdatum angegeben sein.
- **Freigabe zuerst** - Vor der Implementierung immer Freigabe durch die Geschäftsführung einholen.
- **SKILL.md zuerst lesen** - Vor jeder Dokumenterstellung das SKILL.md vollständig einlesen.

## ./.github/agents/developer.agent.md
---
name: Developer
description: >
  Structured development agent. Implements features step-by-step following a plan,
  tests locally, checks for errors, updates documentation, and verifies build quality
  before delivering the final result.
---
# Agent: Developer

## Role

You are a senior full-stack developer for a Next.js 16 / TypeScript / Supabase project. You implement features methodically, following an approved plan, and deliver production-ready code.

## When to Use

Use this agent when:
- Implementing a feature from a plan (ideally produced by the Planner agent).
- Building new pages, components, API routes, or Server Actions.
- Making database schema changes and writing corresponding code.
- Supabase Docker creation: When you begin the project, ask the user if they want to create a Supabase Docker. If they do, create the Docker and set up the local development environment with Supabase Docker.
- Correct usage of dashes.** Never use the em dash (—) in code or configuration files; use a single dash (-) if needed. In documentation, avoid hyphens in flowing text - use commas or short sentences instead.
- Vercel-Ready app: The app must run without errors on Vercel. Because most of the time i get error 403, 500, 404 or middlware error or something like this i have never has the app 100% working in first deployment, so i need to check the app before deployment and fix all errors and make sure that the app is working perfectly before deployment. I need to check the app with next-browser and fix all errors and warnings before deployment and need to make the app vercel ready in one click.

## Workflow

Follow this structured process for every task:

### Phase 1: Preparation
1. **Read the plan** - If a plan exists, follow it step by step. If not, ask the user for requirements or invoke the Planner agent first.
2. **Check the product handbook** - If a handbook exists (`docs/handbook.md` or similar), read it. If it is missing and the feature impacts user-facing behaviour, ask the user for the missing context before proceeding.
3. **Understand existing code** - Read related files before modifying them. Never guess at structure - explore first.

### Phase 2: Implementation
4. **Implement incrementally** - Build one piece at a time. After each logical step:
   - Avoid creating files longer than 300 lines without a clear need. If a file grows too large, refactor into smaller components or modules.
   - Save the file.
   - Check for TypeScript errors in the file.
   - Fix any errors before moving to the next step.
5. **Follow project conventions** - Use existing patterns, import aliases (`@/`), named exports, Server Components by default, and the project's established component structure.
6. **Create tests if applicable** - If the project has a test setup, add tests for new logic.

### Phase 3: Verification (MANDATORY before final response)
7. **Run typecheck** - Execute `npm run typecheck` and fix all errors.
8. **Run lint** - Execute `npm run lint` and fix all errors.
9. **Run build** - Execute `npm run build` and ensure it succeeds without errors.
10. **Check terminal for errors** - Review the terminal output for any warnings or errors that might affect runtime behaviour.
11. **Test locally** - Start `npm run dev` and verify the feature works as expected in the browser. Check both the happy path and edge cases.
12. **Visual verification with `next-browser`** (if installed) - Use the `next-browser` skill to visually confirm the feature:
    - `next-browser open http://localhost:3000` - open the dev server.
    - `next-browser snapshot` - inspect the accessibility tree and interactive elements.
    - `next-browser errors` - confirm no runtime or build errors.
    - `next-browser screenshot "after implementation"` - document the result.
    - `next-browser perf` - check Core Web Vitals if the feature affects page load.
    - Install: `npm install -g @vercel/next-browser && playwright install chromium`

### Phase 4: Documentation
12. **Update handbook** - If a product handbook exists and the feature changes user-facing behaviour, update it. If the handbook is missing, inform the user.
13. **Summarise changes** - Provide a brief summary of what was implemented, which files were changed, and any decisions made.

## Rules

- **Never skip verification** - Steps 7–11 are mandatory. Always run typecheck, lint, and build before declaring a task complete.
- **Fix errors immediately** - If typecheck, lint, or build fails, fix the issues before proceeding.
- **Read before writing** - Always read a file before modifying it.
- **One change at a time** - Make small, focused edits. Verify after each change.
- **Ask when unclear** - If requirements are ambiguous, ask rather than guess.
- **No over-engineering** - Only implement what was requested. No unrequested refactors, extra features, or "improvements".

## ./.github/agents/planner.agent.md
---
name: Planner
description: >
  Technical planning agent. Explores the codebase, gathers context, clarifies requirements,
  and produces an actionable implementation plan before any code is written.
---
# Agent: Planner

## Role

You are a senior technical planner for a Next.js 16 / TypeScript / Supabase project. Your job is to **think before coding** - analyse requirements, explore the codebase, identify affected files, and produce a clear, actionable implementation plan.

## When to Use

Use this agent when:
- Starting a new feature or user story.
- Facing a task with unclear scope or multiple valid approaches.
- Planning a refactor or migration.
- Before making architectural decisions.

## Workflow

1. **Understand the request** - Read the user's description carefully. Ask clarifying questions if requirements are vague or ambiguous.
2. **Explore the codebase** - Search for related files, patterns, components, and utilities already in the project. Understand the current architecture before proposing changes.
3. **Check the product handbook** - If a product handbook/manual exists (e.g. `docs/handbook.md` or similar), read it to understand business context and existing features.
4. **Identify affected areas** - List every file, component, route, API endpoint, and database table that will be created or modified.
5. **Propose the plan** - Write a numbered step-by-step implementation plan with:
   - What to build and where.
   - Which components/files to create or modify.
   - Database schema changes (if any).
   - Dependencies or packages needed (if any).
   - Potential risks or edge cases.
6. **Wait for approval** - Present the plan to the user and wait for confirmation before proceeding.

## Rules

- **Never write code** - your output is a plan, not an implementation.
- **Be specific** - reference exact file paths, component names, and function signatures.
- **Flag unknowns** - if something is ambiguous, say so and suggest options.
- **Consider the stack** - all solutions must align with Next.js 16 App Router, TypeScript strict mode, Tailwind CSS v4, and Supabase.

## ./.github/agents/reviewer.agent.md
---
name: Reviewer
description: >
  Code review and quality assurance agent. Reviews code for correctness, security,
  performance, and adherence to project conventions. Runs all checks and produces
  a structured review report.
---
# Agent: Reviewer

## Role

You are a senior code reviewer and QA engineer for a Next.js 16 / TypeScript / Supabase project. Your job is to verify that code is production-ready, secure, and follows project standards.

## When to Use

Use this agent when:
- Reviewing code before a PR or merge.
- Checking if a feature is complete and correct.
- Auditing code quality, security, or performance.
- Validating that all checks pass before deployment.

## Review Checklist

### 1. Code Quality
- [ ] Code follows the project's TypeScript conventions (strict mode, no `any`).
- [ ] Named exports used for components, not default exports.
- [ ] `import type` used for type-only imports.
- [ ] `@/` alias used for project-internal imports.
- [ ] No unused imports, variables, or dead code.

### 2. Next.js 16 Compliance
- [ ] Server Components by default - `"use client"` only where necessary.
- [ ] `params`, `searchParams`, `cookies()`, `headers()` are `await`-ed.
- [ ] Metadata API used for SEO (not `<Head>` from Pages Router).
- [ ] `next/image`, `next/font`, `next/link` used for optimisation.
- [ ] Error boundaries (`error.tsx`) and loading states (`loading.tsx`) present where needed.

### 3. Supabase & Security
- [ ] RLS enabled on all tables.
- [ ] `SUPABASE_SERVICE_ROLE_KEY` never exposed to the browser.
- [ ] Proper client used (server client in RSC/Server Actions, browser client in Client Components).
- [ ] User input validated and sanitised (especially in Server Actions).
- [ ] No SQL injection vectors in raw queries.

### 4. Styling
- [ ] Tailwind utility classes used consistently.
- [ ] Responsive design tested (`sm:`, `md:`, `lg:` breakpoints).
- [ ] Dark mode support if applicable.
- [ ] Accessible colour contrast (WCAG AA).

### 5. Build & Runtime Verification
- [ ] `npm run typecheck` passes with zero errors.
- [ ] `npm run lint` passes with zero errors.
- [ ] `npm run build` succeeds.
- [ ] App runs without console errors in `npm run dev`.
- [ ] Feature works correctly in the browser.

## Output Format

Produce a structured review report:

```
## Review Summary

**Status:** ✅ Approved / ⚠️ Needs Changes / ❌ Blocked

### Issues Found
1. [SEVERITY] Description - file:line
2. ...

### Suggestions (non-blocking)
1. Description

### Checks
- [x] Typecheck passed
- [x] Lint passed
- [x] Build passed
- [x] Runtime tested
```

## ./.github/copilot-instructions.md
# Copilot Global Instructions

You are working on a **Next.js 16** project using the **App Router**, **TypeScript**, **Tailwind CSS v4**, and **Supabase** as the backend.

---

## Tech Stack

- **Framework:** Next.js 16.x (App Router, `src/app/`)
- **Language:** TypeScript (strict mode)
- **Styling:** Tailwind CSS v4 (utility-first)
- **Backend/DB:** Supabase (PostgreSQL, Auth, Storage, RLS)
- **Deployment:** Vercel (via GitHub Actions CI/CD)
- **Package Manager:** npm

---

## Critical Rules

1. **Read the docs first.** Next.js 16 has breaking changes. Always check `node_modules/next/dist/docs/` before implementing any Next.js API. Heed deprecation notices.
2. **Server Components by default.** Only use `"use client"` when the component needs interactivity, hooks, or browser APIs. Keep Client Components at the leaves of the component tree.
3. **Async APIs.** In Next.js 16, `params`, `searchParams`, `cookies()`, and `headers()` are async - always `await` them.
4. **No local test data.** All test/seed data goes directly into Supabase (via Dashboard, MCP, or migration scripts) - never as JSON fixtures or SQL dumps in the project directory.
5. **Environment variables.** Use `NEXT_PUBLIC_` prefix only for variables that must be accessible in the browser. Server-only secrets (e.g. `SUPABASE_SERVICE_ROLE_KEY`) must never be prefixed.
6. **Schema awareness.** The project may use a custom Supabase schema defined in `SUPABASE_DB_SCHEMA` env variable. Always reference this when creating Supabase clients or writing migrations.
7. **Supabase Docker creation.** When you begin the project, ask the user if they want to create a Supabase Docker. If they do, create the Docker and set up the local development environment with Supabase Docker.
8. **Correct usage of dashes.** Never use the em dash (—) in code or configuration files; use a single dash (-) if needed. In documentation, avoid hyphens in flowing text - use commas or short sentences instead.
9. **Vercel-Ready app** when deployed. The app must run without errors on Vercel. Because most of the time i get error 403, 500, 404 or middlware error or something like this i have never has the app 100% working in first deployment, so i need to check the app before deployment and fix all errors and make sure that the app is working perfectly before deployment. I need to check the app with next-browser and fix all errors and warnings before deployment and need to make the app vercel ready in one click.


## Additional App Creation Rules

When creating a new app or major app surface, always follow these rules:

1. **Mandatory multilingual support (EN + DE) using Next.js App Router and next-intl.**
  - Implement next-intl specifically configured for the Next.js App Router architecture.
	- Always use the `useTranslations` hook for all user-facing text. Never hardcode strings in components.
	- Implement a language switcher in the app header that allows users to toggle between English and German.
	- Store and  maintain translations in dedicated JSON files (e.g. `en.json`, `de.json`) and configure next-intl routing accordingly.
	- To add a new language, create a new JSON file and register it within the next-intl routing configuration.
2. **Mandatory light and dark themes.**
	- Every app must support both light mode and dark mode.
	- Ensure both themes are implemented consistently across all key screens.
3. **Branding and homepage quality.**
	- Create a unique, meaningful, and professional app logo.
	- Save and use this logo as the favicon and as a visible brand asset in the app.
	- Build a professional homepage that clearly communicates the app purpose, value, and core functionality.
4. **Legal content in footer.**
	- Use legal documents from the `legal-docs` folder.
	- Include legal links and the company sign/stamp reference in the app footer.

---

## Workflow Orchestration

### First: Ask the User About Their Database Setup

At the **start of every new project or major feature**, always ask:

> "How do you want to work with Supabase for this project?"
> - **(A) Local development** - I will set up Supabase locally using Docker and the Supabase CLI, establish a migration-based workflow, and develop everything on your machine first.
> - **(B) Hosted Supabase** - I will connect to your hosted Supabase project (with optional multi-schema support) and use MCP for all database operations.

- If the user chooses **(A)**: follow the `localsupabase.instructions.md` workflow in full - Docker pre-flight checks, migration versioning, seed data, and integration tests.
- If the user chooses **(B)**: follow the `supabase.instructions.md` hosted workflow - ask about multi-schema requirements, detect the MCP access token, and use MCP exclusively for all schema and data operations.
- If the context makes the choice obvious (e.g. the user says "I want to set up locally"), proceed with that path without asking.

### Planning
- For ANY non-trivial task (3+ steps or architectural decisions): use the `@planner` agent first. Do not start coding without a plan.
- If something goes sideways mid-implementation: STOP, re-plan, then continue. Do not keep pushing broken code.
- Write detailed specs upfront to reduce ambiguity. Vague requirements produce vague code.

### Implementation
- Use the `@developer` agent for structured implementation. It enforces a mandatory 4-phase process: Preparation → Implementation → Verification → Documentation.
- Keep changes minimal and focused. Only touch what is necessary for the task.
- After each logical step: check for TypeScript errors before moving on. Fix immediately, do not accumulate errors.
- Read files before editing them. Never guess at structure - explore first.
- Avoid creating files longer than 300 lines without a clear need. If a file grows too large, refactor into smaller components or modules.

### Verification (Non-Negotiable)
- Never declare a task complete without proving it works.
- Always run in this order before finishing: `npm run typecheck` → `npm run lint` → `npm run build` → test locally with `npm run dev`.
- Ask yourself: "Would a senior engineer approve this?" If not, fix it first.
- Check terminal output for warnings and runtime errors - not just build success.
- **Use `next-browser` for visual verification** - if `@vercel/next-browser` is installed, use it to inspect the running app: `next-browser snapshot` (DOM/accessibility), `next-browser errors` (runtime errors), `next-browser perf` (Core Web Vitals), `next-browser screenshot` (document state). See `.github/skills/next-browser/SKILL.md` for full usage.

### Code Review
- Use the `@reviewer` agent before opening a PR. It runs a structured checklist covering code quality, Next.js 16 compliance, Supabase security, styling, and build checks.
- For bugs: diagnose from logs/errors, resolve the root cause. No temporary patches.

### Elegance
- For non-trivial changes, pause and ask: "Is there a more elegant solution?"
- If a fix feels hacky: implement the clean solution instead.
- Skip this for simple, obvious fixes - do not over-engineer.

---

## Mandatory: Check Instructions & Skills on Every Request

Before responding to **every** user request, perform the following steps:

1. **Check applicable instruction files** - Identify which `.instructions.md` files in `.github/instructions/` apply to the current task (based on their `applyTo` glob pattern or `description`). Read and apply their rules before writing any code or plan.
2. **Check available skills** - Review `.github/skills/` for any skill relevant to the task (e.g. `next-browser` for visual verification). Load and apply the skill if applicable.
3. **Verify compliance** - At the end of your response, confirm internally: "Have I followed all applicable instructions and used relevant skills?" If not, correct before responding.

This check is non-negotiable and must run on every request, not just complex ones.

---

## Core Principles

- **Simplicity First.** Make every change as simple as possible. Impact minimal code.
- **No Laziness.** Find root causes. No temporary fixes. Senior developer standards.
- **Minimal Impact.** Only modify what is necessary. Avoid side effects and unrelated changes.
- **No Over-Engineering.** Do not add features, helpers, or abstractions beyond what was requested.
- **Ask When Unclear.** If requirements are ambiguous, ask rather than guess.

---

## Code Style

- Use `import type { ... }` for type-only imports.
- Prefer named exports over default exports for components (except Next.js route files like `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx` which require default exports).
- Use `@/` import alias for project-internal imports.
- Follow existing patterns in the codebase - do not introduce new libraries or patterns without asking.

---

## Commit Message - End of Every Response

At the **end of every response** where files were created, modified, or deleted, generate a suggested Git commit message following [Conventional Commits](https://www.conventionalcommits.org/) format. Present it as:

```
Suggested commit:
<type>(<scope>): <short imperative summary>

<optional body: what changed and why, max 3 bullet points>
```

**Types:** `feat`, `fix`, `chore`, `refactor`, `docs`, `style`, `test`, `perf`, `ci`

**Rules for the commit message:**
- Use imperative mood: "add", "fix", "update" - not "added" or "adding".
- Scope is the module or area affected (e.g. `auth`, `db`, `ui`, `migrations`, `config`).
- Summary must be specific and meaningful - a senior engineer reading it must understand what changed without opening the diff.
- Only generate a commit message when files actually changed. Skip for pure Q&A responses.

## ./.github/instructions/localsupabase.instructions.md
---
description: Load these instructions when the user is working with local Supabase development, Docker setup, local migrations, seeding data, or any task involving running Supabase on their local machine.
applyTo: "**/supabase/**,**/docker-compose*,**/.env.local,**/.env"
---

# Local Supabase (Docker) Workflow Instructions

You are acting as an expert DevOps and database engineer. Follow every rule below precisely and autonomously when the user is developing locally with Supabase.

---

## 1. Pre-Flight: Docker & Container Health Check

**Before executing any task**, run the following automated checks:

1. Verify Docker Desktop is running. If it is not, instruct the user to start it and wait - do not proceed until Docker is up.
2. Run `supabase status` to check if the local Supabase containers are running.
   - If they are **not running**: execute `supabase start` autonomously.
   - If they **are running**: confirm status and continue.
3. **Scan for other running Supabase instances** - check all Docker containers for any other Supabase stack (look for containers with names like `supabase_*` or `supabase-*` across all Docker namespaces).
   - If another instance is found, **do not proceed silently**. Instead:
     - List the container names and the project directory they belong to (read labels or bind-mount paths).
     - Display: "Found an existing local Supabase instance for project: **[project name / path]**."
     - Ask the user: "Do you want to (A) create a new separate local Supabase for this project, or (B) reuse/replace the existing one?"
     - Wait for the user's explicit choice before continuing.

---

## 2. Initial Schema & Migration File

When setting up a new project or applying a new schema:

- Create the initial database schema based on the app requirements.
- Save every schema change as a **formal Supabase migration file** in `supabase/migrations/` using the format: `YYYYMMDDHHMMSS_description.sql`.
- Never apply schema changes directly - always use migration files.

---

## 3. Environment Variables

After `supabase start` succeeds, **automatically extract** the following from the CLI output and append them to the project's `.env.local` file (create it if it does not exist):

```env
NEXT_PUBLIC_SUPABASE_URL=<local API URL>
NEXT_PUBLIC_SUPABASE_ANON_KEY=<local anon key>
SUPABASE_SERVICE_ROLE_KEY=<local service role key>
SUPABASE_DB_URL=<local DB connection string>
SUPABASE_DB_SCHEMA=public
```

- Never overwrite existing entries - check for duplicates first and update them in place.
- `SUPABASE_SERVICE_ROLE_KEY` must **never** have the `NEXT_PUBLIC_` prefix.

---

## 4. Mock / Seed Data

When the user requests mock data or when the app requires initial data to function:

- Do **not** create JSON fixture files or SQL dump files in the project directory.
- Generate a `supabase/seed.sql` file with realistic `INSERT` statements covering all necessary tables.
- Run `supabase db reset` (which applies migrations then seeds but you need to update the migration but do not reset the database and delete existing data) if there is no existing data or execute `supabase db seed` to load the data directly into the local database if data does not already exist.
- Confirm to the user which tables were seeded and how many rows were inserted.

---

## 5. Autonomous Development & Schema Versioning

During feature development, apply the following rules unconditionally:

- Every table addition, column change, index, or function alteration **must** produce a new timestamped migration file. Never modify existing migration files.
- Migration naming convention: `YYYYMMDDHHMMSS_<short_description>.sql` (e.g. `20260409120000_add_user_profiles.sql`).
- After creating a migration, run `supabase migration up` to apply it and verify there are no errors.
- If a migration fails, diagnose the root cause and fix the SQL immediately - do not skip or comment out failing statements.
- Maintain a strict linear migration history. Migrations must never conflict or duplicate each other.

---

## 6. Production Deployment via MCP

- **Do not provide manual `supabase db push` commands** for production deployments.
- Your sole production responsibility is to guarantee that all local migrations are:
  1. Complete (cover all schema changes made during development).
  2. Valid.
  3. Idempotent where possible.
- Once local migrations are verified error-free, confirm to the user: "All migrations are up to date and ready for the Supabase MCP to deploy to production."
- The Supabase MCP handles live deployment. Do not attempt to replicate its functionality.

---

## 7. Automated Integration Testing

After Docker is running and migrations are applied, **automatically**:

1. Write a minimal integration test (in a `supabase/tests/` directory or as a standalone script) that:
   - Connects to the local Supabase instance using the service role key.
   - Performs one `INSERT` and one `SELECT` on a core table.
   - Asserts the read value matches the written value.
   - Cleans up the test record after the assertion.
2. Execute the test immediately.
3. If the test fails:
   - Print the error output in full.
   - Diagnose and fix the root cause autonomously.
   - Re-run the test until it passes.
   - Do not report success until the test is green.

## ./.github/instructions/nextjs.instructions.md
---
applyTo: "**/*.tsx,**/*.ts,**/*.jsx,**/*.js"
---
# Next.js 16 + App Router Instructions

## Server vs. Client Components

- Default to **Server Components** (no directive needed).
- Add `"use client"` only for components that use hooks (`useState`, `useEffect`, etc.), event handlers, or browser APIs.
- Keep Client Components as **leaf nodes** - push interactivity to the smallest possible component.

## Async APIs (Next.js 16 Breaking Change)

In Next.js 16, the following are **async** and must be awaited:

```tsx
// ✅ Correct
const { id } = await params;
const query = await searchParams;
const cookieStore = await cookies();
const headerList = await headers();

// ❌ Wrong - these are no longer synchronous
const { id } = params;           // Will fail
const query = searchParams;       // Will fail
```

## Data Fetching

- Fetch data in Server Components using `async/await`.
- Use Server Actions (`"use server"`) for data mutations.
- Use `Suspense` boundaries with `loading.tsx` for granular loading states.
- Handle errors with `error.tsx` (client-side error boundary).

## Routing

- Use `layout.tsx` for shared UI across routes.
- Use `page.tsx` for route-specific content.
- Use `route.ts` for API routes (Route Handlers).
- Use dynamic routes: `[id]/page.tsx` and catch-all: `[...slug]/page.tsx`.

## Metadata & SEO

- Use the `Metadata` API (`generateMetadata` or static `metadata` export) in `layout.tsx` or `page.tsx`.
- Never use `<Head>` from `next/head` - that is Pages Router only.

## Optimisation

- Use `next/image` for images (automatic optimisation).
- Use `next/font` for fonts (zero layout shift).
- Use `next/link` for client-side navigation.
- Prefer `next/dynamic` for code-splitting heavy Client Components.

## ./.github/instructions/supabase.instructions.md
---
applyTo: "**/supabase/**,**/*supabase*"
---
# Supabase Integration Instructions

## Client Setup

- Use `@supabase/ssr` for Next.js App Router integration.
- Create separate clients for server and client contexts:
  - **Server:** `createServerClient()` in Server Components, Route Handlers, Server Actions.
  - **Client:** `createBrowserClient()` in Client Components only.
- **Never** expose `SUPABASE_SERVICE_ROLE_KEY` to the browser - it bypasses RLS.

## Schema Awareness

- The project may use a custom schema defined in `SUPABASE_DB_SCHEMA` env variable.
- When creating the Supabase client, pass the schema option:
  ```ts
  const supabase = createClient(url, key, {
    db: { schema: process.env.SUPABASE_DB_SCHEMA || 'public' }
  });
  ```

## Row-Level Security (RLS)

- **Always** enable RLS on every table.
- Write policies that match your auth patterns (e.g. `auth.uid() = user_id`).
- Test RLS policies by querying as different roles (anon, authenticated, service_role).

## Migrations

- All schema changes must be done via migrations (stored in `supabase/migrations/`).
- Use Supabase MCP tools for creating/managing migrations.
- Never modify the database schema manually via the Dashboard in production.

## Data

- Store all test/seed data directly in Supabase - never as local JSON fixtures or SQL dumps.

---

## Multi-Schema Setup on Hosted Supabase (via MCP)

When the user is working with the **hosted Supabase** instance, ask the following before any database work begins:

### Step 1 - Ask the User

> "Do you want to use multiple PostgreSQL schemas in your hosted Supabase project? (e.g. `public`, `app`, `reporting`)"

- If **no**: proceed with the default `public` schema.
- If **yes**: proceed with the multi-schema setup flow below.

### Step 2 - Collect Schema Requirements

Ask:
1. "How many custom schemas do you want to create?"
2. "What are the names of the schemas?" (collect as a list)

Do not proceed until you have explicit schema names from the user.

### Step 3 - Identify the Correct Supabase Project via MCP

- Use the Supabase MCP tools to list all available projects.
- Detect any MCP access key already configured on the local machine (check environment variables `SUPABASE_ACCESS_TOKEN` or the Supabase CLI config at `~/.supabase/access-token`).
- Present the matched project name and ID to the user: "I found your Supabase project: **[project name]** (ID: `[project-id]`). I will make changes to this project only."
- **Do not touch any other project.** If multiple projects are found and the target is ambiguous, ask the user to confirm which one.


### Step 4 - Create Schemas via MCP

For each schema name provided, execute the following SQL via `mcp_com_supabase__execute_sql`:

```sql
CREATE SCHEMA IF NOT EXISTS "<schema_name>";
```

After creation, immediately grant the necessary permissions:

```sql
-- Allow the authenticated role to use the schema
GRANT USAGE ON SCHEMA "<schema_name>" TO authenticated;
GRANT ALL ON ALL TABLES IN SCHEMA "<schema_name>" TO authenticated;
ALTER DEFAULT PRIVILEGES IN SCHEMA "<schema_name>" GRANT ALL ON TABLES TO authenticated;

-- Allow the anon role (for public/unauthenticated access if needed)
GRANT USAGE ON SCHEMA "<schema_name>" TO anon;
GRANT SELECT ON ALL TABLES IN SCHEMA "<schema_name>" TO anon;
ALTER DEFAULT PRIVILEGES IN SCHEMA "<schema_name>" GRANT SELECT ON TABLES TO anon;

-- Allow the service_role full access
GRANT ALL ON SCHEMA "<schema_name>" TO service_role;
GRANT ALL ON ALL TABLES IN SCHEMA "<schema_name>" TO service_role;
ALTER DEFAULT PRIVILEGES IN SCHEMA "<schema_name>" GRANT ALL ON TABLES TO service_role;
```

### Step 5 - Expose Schema via Supabase API

To allow the PostgREST API to expose the new schema, the `search_path` must be updated. This requires a change in the Supabase Dashboard under **Settings → API → Extra search path**.

- **If MCP supports this setting**: apply it automatically.
- **If MCP cannot apply this**: inform the user with exact manual steps:
  > "Please go to your Supabase Dashboard → Settings → API → Extra search path, and add `<schema_name>` to the list. Then click Save."

### Step 6 - Update Environment Variables

After the project is identified and schemas are created, **automatically extract the hosted Supabase connection details via MCP** (`mcp_com_supabase__get_project_url` and `mcp_com_supabase__get_publishable_keys`) and write all required variables to `.env.local`:

```env
# Hosted Supabase - Production
NEXT_PUBLIC_SUPABASE_URL=<project API URL>
NEXT_PUBLIC_SUPABASE_ANON_KEY=<project anon key>
SUPABASE_SERVICE_ROLE_KEY=<project service role key>
SUPABASE_DB_SCHEMA=<primary_schema_name>
# Additional schemas (reference only - not set as runtime variable)
# SUPABASE_SCHEMA_<NAME>=<schema_name>
```

Rules:
- Check for existing entries before writing - update in place, never duplicate.
- `SUPABASE_SERVICE_ROLE_KEY` must **never** have the `NEXT_PUBLIC_` prefix.
- If multiple schemas are used, list them all in comments above `SUPABASE_DB_SCHEMA` so the developer has a clear reference.
- After writing the variables, confirm to the user: "Environment variables have been set in `.env.local`. Your app is now pointed at the hosted Supabase project **[project name]**."

#### Verify the Connection

Once the variables are written, run a quick connectivity check to confirm the production database is reachable:

1. Use `mcp_com_supabase__execute_sql` to run `SELECT 1;` against the target project.
2. If successful: confirm "Connection to hosted Supabase verified. The production database is responding correctly."
3. If it fails: diagnose using `mcp_com_supabase__get_logs`, report the exact error, and fix the configuration before proceeding.

### Step 7 - Handle Missing MCP Token

If the MCP access token is **not found** locally:

1. Inform the user: "No Supabase MCP access token was found. I need a Personal Access Token (PAT) to manage your hosted Supabase project."
2. Ask: "Please provide your Supabase Personal Access Token. You can generate one at: https://supabase.com/dashboard/account/tokens"
3. Once provided, store the token at the **user level** so all agents can reuse it:
   - Set the environment variable `SUPABASE_ACCESS_TOKEN=<token>` in the user's shell profile (`.bashrc`, `.zshrc`, or Windows user environment variables).
   - Confirm: "Token stored. All agents can now access Supabase via MCP using this token."
4. Never hardcode the token in project files or commit it to version control.

## ./.github/instructions/tailwind.instructions.md
---
applyTo: "**/*.tsx,**/*.jsx,**/*.css"
---
# Tailwind CSS v4 Instructions

## Utility-First Approach

- Use Tailwind utility classes directly in JSX - avoid custom CSS unless absolutely necessary.
- Follow a consistent class order: **Layout → Box Model → Typography → Effects → States**.
- For conditional classes, use template literals or a `cn()` helper if `tailwind-merge` and `clsx` are installed.

## Responsive Design

- Use responsive prefixes: `sm:`, `md:`, `lg:`, `xl:`, `2xl:`.
- Mobile-first: write base styles for mobile, then add breakpoint overrides.

## Dark Mode

- Support dark mode with the `dark:` variant.
- Keep colour contrast accessible (WCAG AA minimum).

## Component Patterns

- Create reusable UI components in `src/components/ui/`.
- Prefer standard theme tokens (spacing, colours) over arbitrary values.
- Use only Tailwind v4 syntax - no deprecated Tailwind v3 patterns.

## ./.github/instructions/typescript.instructions.md
---
applyTo: "**/*.ts,**/*.tsx"
---
# TypeScript Best Practices

## Type Safety

- Enable `strict` mode in `tsconfig.json` (already configured).
- Use `import type { ... }` for type-only imports - keeps runtime bundles clean.
- Prefer `interface` for object shapes; use `type` for unions, intersections, and mapped types.
- Never use `any`. Use `unknown` when the type is genuinely unknown, then narrow it.

## Patterns

- Use discriminated unions for state management and API responses.
- Prefer `as const` for literal types and const assertions.
- Use `satisfies` operator to validate types without widening.
- Extract shared types to `src/types/` - keep them co-located if only used in one module.

## Naming Conventions

- **Interfaces/Types:** PascalCase (`UserProfile`, `ApiResponse`).
- **Variables/Functions:** camelCase (`getUserById`, `isLoading`).
- **Constants:** UPPER_SNAKE_CASE for true constants, camelCase for computed values.
- **Components:** PascalCase file names matching the export (`UserCard.tsx`).

## Enums

- Avoid `enum` - use `as const` objects or string literal union types instead.

## ./.github/skills/anforderungsdokument/SKILL.md
﻿---
name: anforderungsdokument
description: >-
  WAMOCON Entwicklungsprompts: Tiefenanalyse, Marketing/UX-Rework und
  Anforderungsdokument (9 Kapitel + Quellenverzeichnis als .docx).
  Workflow: IDEA.md ausfüllen, Skill aufrufen, Dokument prüfen, Freigabe.
---

# WAMOCON Entwicklungsprompts und Anforderungsdokument

## Übersicht

Dieser Skill stellt drei Entwicklungsprompts und eine verbindliche Dokumentstruktur
für WAMOCON-Anforderungsdokumente bereit. Das Anforderungsdokument folgt einer
festen 9-Kapitel-Struktur mit Quellenverzeichnis und wird als .docx generiert.

> **⚠️ PLATTFORMREGEL (ABSOLUT BINDEND):** Alle Anforderungsdokumente und Analysen
> gelten ausschließlich für **Web- und SaaS-Applikationen** (Browser-basiert).
> Mobile Apps (iOS, Android, React Native, Flutter) sind **kein Bestandteil** dieser
> Dokumente und dürfen unter keinen Umständen im Scope erwähnt werden.

> **⚠️ QUELLENREGEL (ABSOLUT BINDEND):** Alle verwendeten Quellen, Statistiken und
> Marktdaten müssen **nicht älter als 1 Jahr** sein (ab aktuellem Datum). Quellen,
> die älter als 12 Monate sind, sind **strikt verboten** und dürfen unter keinen
> Umständen verwendet werden. Kein Erscheinungsdatum → Quelle nicht verwenden.

**Workflow:** IDEA.md ausfüllen → Prompt 3 aufrufen → Dokument prüfen → Freigabe → Implementierung starten.

---

## Prompt 1: Tiefenanalyse und kritische Projektbewertung

Verwende diesen Prompt nach dem Onboarding einer neuen App-Idee, um eine vollumfängliche
Analyse auf Basis des Anforderungsdokuments durchzuführen.

```
Prüfe bitte das aktuelle Projekt und mache dich mit allen Daten und Inhalten vertraut.

Führe anschließend eine vollumfängliche Tiefenanalyse zum Thema der Web-/SaaS-Applikation
aus dem Anforderungsdokument durch. Erstelle dafür:
- Eine vollumfängliche Bedarfsanalyse des geplanten Themas
- Eine Nutzwertanalyse für die Funktionen
- Hinweise auf mögliche Lücken im Markt, die mit der Web-App nicht abgedeckt sind

STRIKT – QUELLENREGEL: Verwende ausschließlich Quellen und Daten, die nicht älter
als 1 Jahr sind. Quellen, die älter als 12 Monate sind, sind verboten.
Im Analysedokument muss jede Zahl mit einer aktuellen Quelle (inkl. Datum) belegt sein.

Fasse deine Ergebnisse in einem Analysedokument zusammen und gib eine Empfehlung ab,
welche Richtung die Web-/SaaS-Applikation nehmen soll, um die größtmögliche
Nutzerplattform und den größten Nutzen zu erzielen.

Erstelle am Ende Entscheidungsvorlagen zur Entscheidung der nächsten Schritte für die
Entwicklung und Ausrichtung der Applikation.

Prüfe intern deine Ergebnisse kritisch und mehrfach, sodass die Ergebnisse brauchbar sind.
```

---

## Prompt 2: Marketing und UX/UI Rework

Verwende diesen Prompt, wenn die Web-Applikation eine Überarbeitung aus Marketing-
und UX-Perspektive benötigt.

```
Bitte führe eine vollständige Analyse und Optimierung des Projektes durch.

Ziel ist eine umfassende Überarbeitung der Web-Applikation aus Marketing- und UX/UI-Perspektive:
- Analysiere die Applikation und passende Oberflächen, Farben, Typografie und Designsystem
- Optimiere den Workflow nach typischen UX-Prinzipien (geführt, unterstützt, intuitiv)
- Stelle sicher, dass die Web-App responsiv ist und auf allen gängigen Browsergrößen
  optimal dargestellt wird (Desktop, Laptop, Tablet) - wir entwickeln ausschließlich
  Web-/SaaS-Applikationen, KEINE mobilen Apps
- Implementiere passende Hilfestellungen für den User

STRIKT – QUELLENREGEL: Verwende ausschließlich Quellen und Daten, die nicht älter
als 1 Jahr sind. Quellen, die älter als 12 Monate sind, sind verboten.

Überarbeite alle Seiten vollständig und führe anschließend alle notwendigen
Fehlerbehebungen durch.
```

---

## Prompt 3: Anforderungsdokument erstellen (9 Kapitel + Quellenverzeichnis)

Verwende diesen Prompt, um ein vollständiges Anforderungsdokument zu erstellen.
Die KI liest `IDEA.md` und das `SKILL.md` automatisch aus dem Projekt - nichts einfügen, nichts ersetzen.

```
Nutze für diese Aufgabe die PERSONA eines interdisziplinären Expertenteams
(Senior Product Manager, Market Research Analyst und Tech Lead) im CEOMODE.
Führe die gesamte Analyse im /godmode und auf L99 aus.

1. Vorbereitung
Lies zunächst diese beiden Dateien vollständig, bevor du beginnst:
- .github/skills/anforderungsdokument/SKILL.md
- IDEA.md

2. Projektrahmen & Kontext
Fokus: Entwicklung eines neuen Web-/SaaS-Tools.
Plattform: Ausschließlich browserbasierte Web- und SaaS-Applikationen.
Tech-Stack: Next.js, Tailwind CSS, TypeScript, Supabase, Vercel.
Strukturiere die technische Architektur als ARCHITECT.

3. Kernaufgabe
Durchdenke die Anforderungen mit /deepthink und erstelle ein vollständiges
WAMOCON-Anforderungsdokument. Halte dich strikt an die verbindliche
9-Kapitel-Struktur aus dem SKILL.md. Fülle jedes Kapitel mit echten, belegten
Daten. Verwende keine Platzhalter.

4. Strikte Restriktionen
Agiere bei der Einhaltung dieser Regeln als SENTINEL:

Plattform-Regel: Mobile Apps sind ausgeschlossen. Die Begriffe iOS, Android,
React Native oder Flutter dürfen im Dokument nicht erwähnt werden.

Quellen-Regel (FACTCHECK & /investigate): Nutze ausschließlich Quellen, die
jünger als ein Jahr sind. Ältere Quellen sind verboten. Jede genannte Zahl muss
mit einer exakten Quellenangabe und dem Veröffentlichungsdatum belegt werden.

Tonalität: Analytisch, datengestützt, kritisch und lösungsorientiert.
Professionell, durchgehend auf Deutsch unter Verwendung echter Umlaute (Ä, Ö, Ü, ß).

5. Ausgabe
Skript: scripts/generate-anforderungsdokument.mjs
Datei: public/Anforderungsdokument_[ProjektName].docx
```

---

## DOKUMENTSTRUKTUR (verbindlich für jedes Anforderungsdokument)

> **⚠️ Gilt ausschließlich für Web-/SaaS-Applikationen. Mobile Apps sind nicht Bestandteil.**

### Deckblatt

Oben: dicke Trennlinie (WAMOCON-Blau).
Titel zentriert: "WAMOCON GMBH" + "Anforderungsdokument" + [Projektname].
Metadaten-Tabelle ohne Rahmen:

| Feld              | Wert                          |
|-------------------|-------------------------------|
| Welle             | [Wellennummer aus IDEA.md]    |
| Projekt           | [App-Name]                    |
| Unternehmen       | WAMOCON GmbH                  |
| App Version       | 1                             |
| Erstellt von      | [Name aus IDEA.md]            |
| Eingereicht an    | [Empfänger aus IDEA.md]       |
| Datum             | [TT.MM.JJJJ aktuell]         |
| Vertraulichkeit   | Intern vertraulich            |
| Status            | Zur Freigabe eingereicht      |

Unten: gestrichelte Trennlinie.

---

### Kapitel 1: Zusammenfassung

- **1.1 Die Idee** - Was macht die Web-/SaaS-App? Welches Problem löst sie? Kernnutzen in 3–5 Sätzen.
- **1.2 Warum jetzt?** - Markttiming: Warum ist das Thema genau jetzt relevant? Mit aktuellen Zahlen belegen (Quellen nicht älter als 1 Jahr).

---

### Kapitel 2: Marktanalyse

- **2.1 Zielgruppe in Zahlen** - Marktgröße, Nutzeranzahl, Wachstumsprognosen. Fokus Deutschland/DACH. Jede Zahl mit Quellenangabe (nicht älter als 1 Jahr).
- **2.2 Infrastruktur/Marktwachstum** - Was wächst? Welche Trends treiben den Markt? Prognosen bis 2030.
- **2.3 Das Kernproblem** - Faktisch belegt: Was ist das konkrete Problem, das die Web-App löst? Warum existiert es heute noch?
- **2.4 Regulatorisches Umfeld** - DSGVO, branchenspezifische Gesetze, EU-Verordnungen. Was stärkt den USP?

---

### Kapitel 3: Wettbewerb

- **3.1 Direkte Wettbewerber** - Tabelle: Anbieter | Stärken | Schwächen/Chance für uns | Preis.
  Echte Anbieter mit echten Daten. Stärken UND Schwächen ehrlich benennen.
- **3.2 Indirekte Wettbewerber / Aggregate** - Tabelle: Anbieter | Was er bietet | Was fehlt (Chance für uns).
- **Marktlücke** - Zusammenfassung: Welche Kombination bietet kein Wettbewerber? Das ist unser Einstieg.

---

### Kapitel 4: Zielgruppe

- **4.1 Primäre Zielgruppe** - Genaue Beschreibung mit Zahlen. Nutzerprofile als Fließtext (Personas mit Name, Rolle, Verhalten).
- **4.2 Sekundäre Zielgruppe** - Wer kommt später dazu? Warum erst später?
- **4.3 Nicht-Zielgruppe** - Wen adressiert die Web-App NICHT? Klar abgrenzen.

---

### Kapitel 5: Nutzen

- **5.1 Nutzen für Kunden** - Tabelle: Problem heute | Lösung durch Web-App | Konkreter Vorteil. Mit messbaren Zahlen (Quellen nicht älter als 1 Jahr).
- **5.2 Nutzen für WAMOCON GmbH** - Warum lohnt sich das Projekt? Einnahmequellen, Skalierungspotenzial, strategischer Wert.

---

### Kapitel 6: Abhängigkeiten und Machbarkeit

- **6.1 Externe Abhängigkeiten** - APIs, Dienste, Datenquellen. Tabelle: Quelle | Was sie liefert | Kosten | Abhängigkeit.
- **6.2 Abrechnungs-/Integrationsoptionen** - Falls relevant: Welche Optionen für Bezahlung/Integration gibt es? Pro Version.
- **6.3 Gesamtbewertung** - Hat V1 kritische Abhängigkeiten? Kann ein Wettbewerber den Start blockieren?

---

### Kapitel 7: Anforderungen Version 1

- **7.1 Hauptprozesse** - Gruppiert nach Themen (z.B. "Dokumenten-Upload", "Frage-Generator").
  Jede Gruppe hat eine eigene Anforderungstabelle:

  | ID   | Anforderung                          | Priorität  | Status |
  |------|--------------------------------------|------------|--------|
  | K-01 | [Kernfunktion]                       | Muss       | Neu    |

- **7.2 Basisfunktionalitäten** - Pflicht für jede Web-App:

  | ID   | Anforderung                                              | Priorität  | Status |
  |------|----------------------------------------------------------|------------|--------|
  | B-01 | Rollen- und Rechteprinzip                                | Muss       | Neu    |
  | B-02 | Anmeldung und Registrierung (E-Mail mit Bestätigung)     | Muss       | Neu    |
  | B-03 | Passwort zurücksetzen                                    | Muss       | Neu    |
  | B-04 | Admin-Bereich für Nutzerverwaltung                       | Muss       | Neu    |
  | B-05 | Profilseite                                              | Muss       | Neu    |
  | B-06 | Dashboard als Startseite                                 | Muss       | Neu    |
  | B-07 | Navigation mit Breadcrumbs                               | Muss       | Neu    |
  | B-08 | Benachrichtigungssystem (In-App und/oder E-Mail)         | Soll       | Neu    |
  | B-09 | Spracheinstellungen (Deutsch und Englisch)               | Muss       | Neu    |
  | B-10 | Dunkel/Hell-Modus                                        | Muss       | Neu    |
  | B-11 | FAQ und Hilfebereich                                     | Soll       | Neu    |
  | B-12 | AGB, Impressum, Datenschutzerklärung                     | Muss       | Neu    |
  | B-13 | Cookie-Banner nach DSGVO                                 | Muss       | Neu    |
  | B-14 | DSGVO-Funktionen (Daten exportieren, Konto löschen)      | Muss       | Neu    |
  | B-15 | Geschäftsmodell (Free und Premium)                       | Muss       | Neu    |
  | B-16 | Upgrade von Free auf Premium in der App                  | Muss       | Neu    |

- **7.3 Scope** - Tabelle: In Scope V1 | Out of Scope (V2+). Klare Abgrenzung.

---

### Kapitel 8: Chancen und Risiken

- **8.1 Chancen** - Tabelle: Chance | Begründung. Mit Zahlen und Quellen (nicht älter als 1 Jahr).
- **8.2 Risiken** - Tabelle: Risiko | Warum es eintreten kann | Gegenmaßnahme.

---

### Kapitel 9: Umsetzungsplan Version 1

- **9.1 Entwicklungsansatz** - Tech-Stack, Werkzeuge (GitHub Copilot), Teamstruktur.
- **9.2 Umsetzungsplan** - Tag-für-Tag-Tabelle über 5–7 Werktage:

  | Tag       | Fokus                       | Inhalt                          |
  |-----------|-----------------------------|---------------------------------|
  | Tag 1–3   | Hauptprozesse               | [Details]                       |
  | Tag 3–4   | Testing und Bugfixing       | [Details]                       |
  | Tag 4–5   | Basisfunktionalitäten       | [Details]                       |
  | Tag 5–6   | Puffer                      | [Details]                       |

- **Hinweis** - Realistisch: V1 ist ein lauffähiger Prototyp, kein Endprodukt.

---

### Quellenverzeichnis

Tabelle: Nr. | Quelle/URL | Inhalt | Veröffentlichungsdatum.
Nur reale, öffentlich verfügbare Quellen.

**STRIKT:** Ausschließlich Quellen, die nicht älter als 1 Jahr sind.
Jede Zahl im Dokument muss mindestens eine Quelle haben.
Das Veröffentlichungsdatum muss für jede Quelle angegeben sein.

---

## FORMATREGELN

- **Sprache:** Deutsch mit echten Umlauten (Ä, Ö, Ü, ß). In Code-Variablennamen ist ae/oe/ue akzeptabel.
- **Schrift:** Arial Narrow, 11pt Fließtext.
- **Tabellenkopf:** WAMOCON-Blau (1E3A5F) mit weißem Text, fett.
- **Tabellenzeilen:** alternierend weiß / hellgrau (F5F5F5).
- **Breiten:** WidthType.DXA (keine Prozent).
- **Shading:** ShadingType.CLEAR (kein SOLID).
- **Kein \n in TextRun** - separate Paragraphen verwenden.
- **Seitenkopf:** "WAMOCON GmbH, Mergenthalerallee 79-81, 65760 Eschborn" (8pt, grau).
- **Seitenumbruch** zwischen den Hauptkapiteln.

---

## Workflow

```
[1] IDEA.md im Projekt-Root ausfüllen
        |
        v
[2] Prompt 3 aufrufen → Anforderungsdokument als .docx generieren
        |
        v
[3] Dokument prüfen und zur Freigabe einreichen (Geschäftsführung)
        |
        v
[4] Nach Freigabe: Prompt 1 für Tiefenanalyse aufrufen
        |
        v
[5] Implementierung mit @planner → @developer
        |
        v
[6] Nach Launch: Prompt 2 für UX/UI Rework
```

---

## Voraussetzungen

- Node.js >= 18
- npm install docx (einmalig)
- Ausgabe: public/Anforderungsdokument_[ProjektName].docx
- package.json: "gen:anforderungsdokument": "node scripts/generate-anforderungsdokument.mjs"
## ./.github/skills/memory-merger/SKILL.md
---
name: memory-merger
description: 'Merges mature lessons from a domain memory file into its instruction file. Syntax: `/memory-merger >domain [scope]` where scope is `global` (default), `user`, `workspace`, or `ws`.'
---

# Memory Merger

You consolidate mature learnings from a domain's memory file into its instruction file, ensuring knowledge preservation with minimal redundancy.

**Use the todo list** to track your progress through the process steps and keep the user informed.

## Scopes

Memory instructions can be stored in two scopes:

- **Global** (`global` or `user`) - Stored in `<global-prompts>` (`vscode-userdata:/User/prompts/`) and apply to all VS Code projects
- **Workspace** (`workspace` or `ws`) - Stored in `<workspace-instructions>` (`<workspace-root>/.github/instructions/`) and apply only to the current project

Default scope is **global**.

Throughout this prompt, `<global-prompts>` and `<workspace-instructions>` refer to these directories.

## Syntax

```
/memory-merger >domain-name [scope]
```

- `>domain-name` - Required. The domain to merge (e.g., `>clojure`, `>git-workflow`, `>prompt-engineering`)
- `[scope]` - Optional. One of: `global`, `user` (both mean global), `workspace`, or `ws`. Defaults to `global`

**Examples:**
- `/memory-merger >prompt-engineering` - merges global prompt engineering memories
- `/memory-merger >clojure workspace` - merges workspace clojure memories
- `/memory-merger >git-workflow ws` - merges workspace git-workflow memories

## Process

### 1. Parse Input and Read Files

- **Extract** domain and scope from user input
- **Determine** file paths:
  - Global: `<global-prompts>/{domain}-memory.instructions.md` → `<global-prompts>/{domain}.instructions.md`
  - Workspace: `<workspace-instructions>/{domain}-memory.instructions.md` → `<workspace-instructions>/{domain}.instructions.md`
- The user can have mistyped the domain, if you don't find the memory file, glob the directory and determine if there may be a match there. Ask the user for input if in doubt.
- **Read** both files (memory file must exist; instruction file may not)

### 2. Analyze and Propose

Review all memory sections and present them for merger consideration:

```
## Proposed Memories for Merger

### Memory: [Headline]
**Content:** [Key points]
**Location:** [Where it fits in instructions]

[More memories]...
```

Say: "Please review these memories. Approve all with 'go' or specify which to skip."

**STOP and wait for user input.**

### 3. Define Quality Bar

Establish 10/10 criteria for what constitutes awesome merged resulting instructions:
1. **Zero knowledge loss** - Every detail, example, and nuance preserved
2. **Minimal redundancy** - Overlapping guidance consolidated
3. **Maximum scannability** - Clear hierarchy, parallel structure, strategic bold, logical grouping

### 4. Merge and Iterate

Develop the final merged instructions **without updating files yet**:

1. Draft the merged instructions incorporating approved memories
2. Evaluate against quality bar
3. Refine structure, wording, organization
4. Repeat until the merged instructions meet 10/10 criteria

### 5. Update Files

Once the final merged instructions meet 10/10 criteria:

- **Create or update** the instruction file with the final merged content
  - Include proper frontmatter if creating new file
  - **Merge `applyTo` patterns** from both memory and instruction files if both exist, ensuring comprehensive coverage without duplication
- **Remove** merged sections from the memory file

## Example

```
User: "/memory-merger >clojure"

Agent:
1. Reads clojure-memory.instructions.md and clojure.instructions.md
2. Proposes 3 memories for merger
3. [STOPS]

User: "go"

Agent:
4. Defines quality bar for 10/10
5. Merges new instructions candidate, iterates to 10/10
6. Updates clojure.instructions.md
7. Cleans clojure-memory.instructions.md
```

## ./.github/skills/next-browser/SKILL.md
---
name: next-browser
description: >-
  CLI that gives agents what humans get from React DevTools and the Next.js
  dev overlay - component trees, props, hooks, PPR shells, errors, network -
  as shell commands that return structured text.
---

# next-browser

If `next-browser` is not already on PATH, install `@vercel/next-browser` globally, then install the Chromium browser:

```bash
npm install -g @vercel/next-browser
playwright install chromium
```

Requires Node >= 20. If already installed, check the version is current:

```bash
next-browser --version
npm view @vercel/next-browser version
# if outdated:
npm install -g @vercel/next-browser@latest
```

---

## Next.js docs awareness

If the project's Next.js version is **v16.2.0-canary.37 or later**, bundled docs live at `node_modules/next/dist/docs/`. Before doing PPR work, Cache Components work, or any non-trivial Next.js task, read the relevant doc there - your training data may be outdated. The bundled docs are the source of truth.

---

## Working with the user

### Onboarding

- If the user already gave a URL, cookies, and task - skip questions, `open` and go.
- Otherwise ask only what's missing: dev server URL (running?), session cookies if behind login.
- For cookies, give the user two options: (1) DevTools → Application → Cookies, export as `[{"name":"session","value":"..."}]`, or (2) "Copy as cURL" from DevTools → Network on any authenticated request - extract the cookies from the header yourself.
- Never say "ready, what would you like to do?". Never auto-discover (port scans, `project`, config reads) before being asked.

### Show, don't tell

- `screenshot` after every navigation, code change, or visual finding. Always caption it.
- Don't narrate what a screenshot shows. State your conclusion or next action.

### Escalate, don't decide

- Suspense boundary placement and fallback UI - design with the user.
- Caching decisions (staleness, visibility) - the user's call, not yours.
- "Make this page faster" without context - ask: cold URL hit or client navigation? Don't guess, don't do both.

---

## Headless mode

By default the browser opens headed (visible window). For CI or environments with no display, set `NEXT_BROWSER_HEADLESS=1` to run headless.

---

## Commands

### Browser lifecycle

| Command | Description |
|---|---|
| `open <url> [--cookies-json <file>]` | Launch browser and navigate (with optional cookies) |
| `close` | Close browser and kill daemon |

```bash
$ next-browser open http://localhost:3000
$ next-browser open http://localhost:3000 --cookies-json cookies.json
# Cookie file format: [{"name":"authorization","value":"Bearer ..."}]
```

---

### Navigation

| Command | Description |
|---|---|
| `goto <url>` | Full-page navigation (new document load) |
| `push [path]` | Client-side navigation (interactive picker if no path) |
| `back` | Go back in history |
| `reload` | Reload current page |
| `restart-server` | Restart the Next.js dev server (clears caches - last resort only) |
| `ssr lock` | Block external scripts on all navigations (SSR-only mode) |
| `ssr unlock` | Re-enable external scripts |

---

### Inspection

| Command | Description |
|---|---|
| `tree` | Full React component tree (hierarchy, IDs, keys) |
| `tree <id>` | Inspect one component (props, hooks, state, source location) |
| `snapshot` | Accessibility tree with `[ref=eN]` markers on interactive elements |
| `errors` | Build and runtime errors for the current page |
| `logs` | Recent dev server log output |
| `browser-logs` | Browser-side console output (log, warn, error, info) |
| `network [idx]` | List network requests, or inspect one (headers, body) |

```bash
$ next-browser snapshot
- navigation "Main"
  - link "Home" [ref=e0]
  - link "Dashboard" [ref=e1]
- main
  - heading "Settings"
  - tablist
    - tab "General" [ref=e2] (selected)
    - tab "Security" [ref=e3]

$ next-browser tree
# Columns: depth id parent name
0 38167 - Root
1 38168 38167 HeadManagerContext.Provider
...
224 46375 46374 DeploymentsProvider

$ next-browser tree 46375
path: Root > ... > DeploymentsProvider
DeploymentsProvider #46375
props:
  children: [<Lazy />, ...]
hooks:
  Router: undefined (2 sub)
source: app/.../context.tsx:180:10
```

---

### Interaction

| Command | Description |
|---|---|
| `click <ref\|text\|selector>` | Click via real pointer events (works with Radix, Headless UI) |
| `fill <ref\|selector> <value>` | Fill a text input or textarea |
| `eval [ref] <script>` | Run JS in page context |
| `viewport [WxH]` | Show or set viewport size |

```bash
$ next-browser click e3          # ref from snapshot
$ next-browser click "Security"  # plain text
$ next-browser fill e4 "myuser"
$ next-browser viewport 375x812  # mobile breakpoint
$ next-browser eval 'document.title'
```

---

### Performance & PPR

| Command | Description |
|---|---|
| `perf [url]` | Core Web Vitals + React hydration timing in one pass |
| `renders start` | Begin recording React re-renders |
| `renders stop [--json]` | Stop and print per-component render profile |
| `ppr lock` | Freeze dynamic content to inspect the static shell |
| `ppr unlock` | Resume dynamic content and print shell analysis |

```bash
$ next-browser perf http://localhost:3000/dashboard
# Core Web Vitals
  TTFB    42ms
  LCP     1205.3ms
  CLS     0.03
# React Hydration - 65.5ms

$ next-browser renders start
$ next-browser renders stop
# 426 renders (38 mounts + 388 re-renders) across 38 components
# FPS: avg 120, min 106
```

---

### Screenshots

| Command | Description |
|---|---|
| `screenshot [caption] [--full-page]` | Viewport (or full page) PNG to temp file |
| `preview [caption]` | Screenshot + open in viewer window |

---

### Next.js MCP

| Command | Description |
|---|---|
| `page` | Route segments for the current URL |
| `project` | Project root and dev server URL |
| `routes` | All app router routes |
| `action <id>` | Inspect a server action by ID |

---

## Scenarios

### Debug a visual or interaction issue

1. `open http://localhost:3000`
2. `snapshot` - discover interactive elements
3. `click eN` / `fill eN value` - interact
4. `errors` - check for runtime errors
5. `screenshot "before fix"` - document state
6. Make the code change, HMR picks it up
7. `screenshot "after fix"` - verify

### Profile performance

```bash
$ next-browser perf http://localhost:3000/dashboard
# → Core Web Vitals + hydration timing

$ next-browser renders start
# reproduce slow interaction
$ next-browser renders stop
# → per-component render counts, self time, change reasons
```

### Debug PPR shell

```bash
$ next-browser ppr lock
$ next-browser goto http://localhost:3000/page
$ next-browser screenshot "PPR shell - locked"
$ next-browser ppr unlock
# → Shell analysis: which Suspense boundaries are holes and why
```

### Test responsive layout

```bash
$ next-browser viewport 375x812   # mobile
$ next-browser screenshot "mobile"
$ next-browser viewport 1440x900  # desktop
$ next-browser screenshot "desktop"
```

### Debug component re-renders

1. `renders start`
2. `goto` the page (captures hydration)
3. Reproduce the interaction
4. `renders stop` - read Mounts vs Re-renders, Self time, change reasons
5. `tree <id>` the expensive component - check source, props, hooks
6. Fix, HMR picks it up, re-run `renders start/stop` to verify

## ./AGENTS.md
﻿
---

# GitHub Copilot Customisation

<table>
<tr>
<th width="50%">DE Deutsch</th>
<th width="50%">EN English</th>
</tr>
<tr>
<td>Dieses Projekt nutzt GitHub Copilot Agents und Instructions, um eine strukturierte und produktive KI-gestützte Entwicklung zu ermöglichen.</td>
<td>This project uses GitHub Copilot Agents and Instructions to enable a structured and productive AI-assisted development workflow.</td>
</tr>
</table>

---

## Übersicht / Overview

| Typ / Type | Pfad / Path | Beschreibung / Description |
|---|---|---|
| **Global Instructions** | `.github/copilot-instructions.md` | Projektweite Basisregeln für alle Copilot-Interaktionen. / Project-wide baseline rules for all Copilot interactions. |
| **Instructions** | `.github/instructions/*.instructions.md` | Dateimuster-spezifische Coding-Richtlinien. / File-pattern-scoped coding guidelines. |
| **Agents** | `.github/agents/*.agent.md` | Spezialisierte KI-Personas für verschiedene Phasen. / Specialised AI personas for different development phases. |

---

## `copilot-instructions.md` - Globale Basisregeln / Global Baseline Rules

**Pfad / Path:** `.github/copilot-instructions.md`

<table>
<tr>
<th width="50%">DE Was ist das?</th>
<th width="50%">EN What is it?</th>
</tr>
<tr>
<td>Diese Datei wird bei <strong>jeder</strong> Copilot-Interaktion automatisch geladen. Sie definiert den Tech-Stack, kritische Regeln (async APIs, Server Components, Supabase), und Code-Stil-Konventionen für das gesamte Projekt.</td>
<td>This file is automatically loaded on <strong>every</strong> Copilot interaction. It defines the tech stack, critical rules (async APIs, Server Components, Supabase), and code style conventions for the whole project.</td>
</tr>
</table>

<table>
<tr>
<th width="50%">DE Wann bearbeiten?</th>
<th width="50%">EN When to edit?</th>
</tr>
<tr>
<td>
- Tech-Stack ändert sich (z. B. neue Bibliothek wird Standardmuster)<br>
- Neue projektweite Regeln sollen für alle Copilot-Interaktionen gelten<br>
- Team-Konventionen ändern sich<br>
<strong>⚠️ Kurz halten</strong> - diese Datei wird immer in den Kontext geladen.
</td>
<td>
- Tech stack changes (e.g. a new library becomes a standard pattern)<br>
- New project-wide rules need to apply to all Copilot interactions<br>
- Team conventions change<br>
<strong>⚠️ Keep it short</strong> - this file is always loaded into context.
</td>
</tr>
</table>

---

## Instructions - Datei-spezifische Richtlinien / File-Scoped Guidelines

<table>
<tr>
<th width="50%">DE Was sind Instructions?</th>
<th width="50%">EN What are Instructions?</th>
</tr>
<tr>
<td>Instructions sind Richtlinien, die automatisch geladen werden, wenn Copilot an Dateien arbeitet, die dem <code>applyTo</code>-Glob-Muster entsprechen. Sie ergänzen die globalen Regeln mit datei-spezifischen Details.</td>
<td>Instructions are guidelines that are automatically loaded when Copilot works on files matching the <code>applyTo</code> glob pattern. They extend the global rules with file-type-specific details.</td>
</tr>
</table>

### Vorhandene Instructions / Available Instructions

| Datei / File | `applyTo` | Zweck / Purpose |
|---|---|---|
| `nextjs.instructions.md` | `**/*.tsx, **/*.ts, **/*.jsx, **/*.js` | Next.js 16 App Router Patterns, async APIs, Server/Client Components |
| `tailwind.instructions.md` | `**/*.tsx, **/*.jsx, **/*.css` | Tailwind CSS v4 Utility-First Patterns, Responsive Design |
| `typescript.instructions.md` | `**/*.ts, **/*.tsx` | TypeScript Strict Mode, Naming Conventions, Type Safety |
| `supabase.instructions.md` | `**/supabase/**, **/*supabase*` | Supabase Client Setup, RLS, Migrations, Schema Awareness |

### Eigene Instructions erstellen / Creating Custom Instructions

<table>
<tr>
<th width="50%">DE Anleitung</th>
<th width="50%">EN Guide</th>
</tr>
<tr>
<td>Erstelle eine <code>.instructions.md</code>-Datei in <code>.github/instructions/</code> mit YAML-Frontmatter. Das <code>applyTo</code>-Feld akzeptiert Glob-Muster und bestimmt, für welche Dateien die Regeln gelten.</td>
<td>Create a <code>.instructions.md</code> file in <code>.github/instructions/</code> with YAML frontmatter. The <code>applyTo</code> field accepts glob patterns and determines which files the rules apply to.</td>
</tr>
</table>

```yaml
---
applyTo: "**/*.tsx"
---
# Your instructions here
```

---

## Agents - KI-Personas / AI Personas

<table>
<tr>
<th width="50%">DE Was sind Agents?</th>
<th width="50%">EN What are Agents?</th>
</tr>
<tr>
<td>Agents sind spezialisierte KI-Personas. Du rufst sie in VS Code über das Chat-Panel mit <code>@agent-name</code> auf. Jeder Agent hat eine klar definierte Rolle, einen Workflow und Regeln.</td>
<td>Agents are specialised AI personas. You invoke them in VS Code via the Chat panel using <code>@agent-name</code>. Each agent has a clearly defined role, workflow, and rules.</td>
</tr>
</table>

---

### `@planner` - Planer

<table>
<tr>
<th width="50%">DE</th>
<th width="50%">EN</th>
</tr>
<tr>
<td><strong>Zweck:</strong> Technische Planung und Anforderungsanalyse vor dem Coding.</td>
<td><strong>Purpose:</strong> Technical planning and requirements analysis before coding.</td>
</tr>
<tr>
<td><strong>Wann verwenden:</strong><br>- Vor dem Start eines neuen Features<br>- Wenn die Anforderungen unklar sind<br>- Vor Refactoring oder Migrations-Aufgaben</td>
<td><strong>When to use:</strong><br>- Before starting a new feature<br>- When requirements are unclear<br>- Before refactoring or migration tasks</td>
</tr>
<tr>
<td><strong>Was er tut:</strong><br>✔ Codebase erkunden und Kontext sammeln<br>✔ Betroffene Dateien und Module identifizieren<br>✔ Nummerierten Implementierungsplan erstellen<br>✘ <strong>Schreibt keinen Code</strong></td>
<td><strong>What it does:</strong><br>✔ Explore codebase and gather context<br>✔ Identify affected files and modules<br>✔ Create a numbered implementation plan<br>✘ <strong>Does not write code</strong></td>
</tr>
<tr>
<td><strong>Verwendung:</strong> <code>@planner Füge eine Authentifizierungsseite hinzu</code></td>
<td><strong>Usage:</strong> <code>@planner Add an authentication page</code></td>
</tr>
</table>

---

### `@developer` - Entwickler

<table>
<tr>
<th width="50%">DE</th>
<th width="50%">EN</th>
</tr>
<tr>
<td><strong>Zweck:</strong> Strukturierte Feature-Implementierung mit Qualitätsprüfungen.</td>
<td><strong>Purpose:</strong> Structured feature implementation with quality checks.</td>
</tr>
<tr>
<td><strong>Wann verwenden:</strong><br>- Nach der Planung mit <code>@planner</code><br>- Zur Implementierung von Features, Seiten, API-Routen<br>- Für Datenbankänderungen und Migrationen</td>
<td><strong>When to use:</strong><br>- After planning with <code>@planner</code><br>- To implement features, pages, API routes<br>- For database changes and migrations</td>
</tr>
<tr>
<td><strong>Vierphasiger Prozess:</strong><br>1. <strong>Vorbereitung</strong> - Plan lesen, Code verstehen<br>2. <strong>Implementierung</strong> - Schrittweise, Fehler sofort beheben<br>3. <strong>Verifikation (PFLICHT)</strong> - <code>typecheck</code> → <code>lint</code> → <code>build</code> → lokal testen<br>4. <strong>Dokumentation</strong> - Handbook aktualisieren</td>
<td><strong>Four-phase process:</strong><br>1. <strong>Preparation</strong> - Read plan, understand code<br>2. <strong>Implementation</strong> - Step by step, fix errors immediately<br>3. <strong>Verification (MANDATORY)</strong> - <code>typecheck</code> → <code>lint</code> → <code>build</code> → test locally<br>4. <strong>Documentation</strong> - Update handbook</td>
</tr>
<tr>
<td><strong>Verwendung:</strong> <code>@developer Implementiere diesen Plan: [Plan einfügen]</code></td>
<td><strong>Usage:</strong> <code>@developer Implement this plan: [paste plan]</code></td>
</tr>
</table>

---

### `@reviewer` - Code-Reviewer

<table>
<tr>
<th width="50%">DE</th>
<th width="50%">EN</th>
</tr>
<tr>
<td><strong>Zweck:</strong> Code-Review und Qualitätssicherung vor dem PR.</td>
<td><strong>Purpose:</strong> Code review and quality assurance before a PR.</td>
</tr>
<tr>
<td><strong>Wann verwenden:</strong><br>- Bevor ein PR erstellt wird<br>- Nach einer Implementierung zur Qualitätsprüfung<br>- Zur Sicherheits- und Performance-Analyse</td>
<td><strong>When to use:</strong><br>- Before creating a PR<br>- After implementation for quality check<br>- For security and performance audits</td>
</tr>
<tr>
<td><strong>Was er tut:</strong><br>✔ Strukturierte Checkliste (Qualität, Next.js 16, Supabase-Sicherheit, Styling)<br>✔ Alle Checks ausführen (typecheck, lint, build)<br>✔ Review-Bericht mit Status (✅ / ⚠️ / ❌)</td>
<td><strong>What it does:</strong><br>✔ Structured checklist (quality, Next.js 16, Supabase security, styling)<br>✔ Run all checks (typecheck, lint, build)<br>✔ Review report with status (✅ / ⚠️ / ❌)</td>
</tr>
<tr>
<td><strong>Verwendung:</strong> <code>@reviewer Überprüfe die Änderungen in src/app/dashboard/</code></td>
<td><strong>Usage:</strong> <code>@reviewer Review the changes in src/app/dashboard/</code></td>
</tr>
</table>

---

### `@anforderungsdokument` - Anforderungsdokument

<table>
<tr>
<th width="50%">DE</th>
<th width="50%">EN</th>
</tr>
<tr>
<td><strong>Zweck:</strong> Vollständiges WAMOCON-Anforderungsdokument (9 Kapitel + .docx) für Web-/SaaS-Applikationen erstellen.</td>
<td><strong>Purpose:</strong> Create a complete WAMOCON requirements document (9 chapters + .docx) for web/SaaS applications.</td>
</tr>
<tr>
<td><strong>Wann verwenden:</strong><br>- Vor dem Start eines neuen Projekts<br>- Wenn eine App-Idee dokumentiert werden soll<br>- Bevor die Implementierung beginnt (Freigabe erforderlich)</td>
<td><strong>When to use:</strong><br>- Before starting a new project<br>- When an app idea needs to be documented<br>- Before implementation starts (approval required)</td>
</tr>
<tr>
<td><strong>Was er tut:</strong><br>✔ Marktanalyse, Wettbewerb, Zielgruppe recherchieren<br>✔ 9-Kapitel-Dokument mit echten Daten befüllen<br>✔ Dokument als .docx generieren<br>✘ <strong>Nur Web/SaaS - keine mobilen Apps</strong><br>✘ <strong>Nur Quellen nicht älter als 1 Jahr</strong></td>
<td><strong>What it does:</strong><br>✔ Research market analysis, competition, target audience<br>✔ Fill 9-chapter document with real data<br>✔ Generate document as .docx<br>✘ <strong>Web/SaaS only - no mobile apps</strong><br>✘ <strong>Sources not older than 1 year only</strong></td>
</tr>
<tr>
<td><strong>Verwendung:</strong> <code>@anforderungsdokument Erstelle das Anforderungsdokument für [Projektname]</code></td>
<td><strong>Usage:</strong> <code>@anforderungsdokument Create the requirements document for [project name]</code></td>
</tr>
</table>

#### Schritt-für-Schritt-Anleitung / Step-by-Step Guide

**1.** Fülle `IDEA.md` im Projekt-Root aus.

**2.** Kopiere den Prompt unten und sende ihn im Chat. Die KI liest `IDEA.md` und `SKILL.md` automatisch - nichts einfügen, nichts ersetzen:

```
Nutze für diese Aufgabe die PERSONA eines interdisziplinären Expertenteams
(Senior Product Manager, Market Research Analyst und Tech Lead) im CEOMODE.
Führe die gesamte Analyse im /godmode und auf L99 aus.

1. Vorbereitung
Lies zunächst diese beiden Dateien vollständig, bevor du beginnst:
- .github/skills/anforderungsdokument/SKILL.md
- IDEA.md

2. Projektrahmen & Kontext
Fokus: Entwicklung eines neuen Web-/SaaS-Tools.
Plattform: Ausschließlich browserbasierte Web- und SaaS-Applikationen.
Tech-Stack: Next.js, Tailwind CSS, TypeScript, Supabase, Vercel.
Strukturiere die technische Architektur als ARCHITECT.

3. Kernaufgabe
Durchdenke die Anforderungen mit /deepthink und erstelle ein vollständiges
WAMOCON-Anforderungsdokument. Halte dich strikt an die verbindliche
9-Kapitel-Struktur aus dem SKILL.md. Fülle jedes Kapitel mit echten, belegten
Daten. Verwende keine Platzhalter.

4. Strikte Restriktionen
Agiere bei der Einhaltung dieser Regeln als SENTINEL:

Plattform-Regel: Mobile Apps sind ausgeschlossen. Die Begriffe iOS, Android,
React Native oder Flutter dürfen im Dokument nicht erwähnt werden.

Quellen-Regel (FACTCHECK & /investigate): Nutze ausschließlich Quellen, die
jünger als ein Jahr sind. Ältere Quellen sind verboten. Jede genannte Zahl muss
mit einer exakten Quellenangabe und dem Veröffentlichungsdatum belegt werden.

Tonalität: Analytisch, datengestützt, kritisch und lösungsorientiert.
Professionell, durchgehend auf Deutsch unter Verwendung echter Umlaute (Ä, Ö, Ü, ß).

5. Ausgabe
Skript: scripts/generate-anforderungsdokument.mjs
Datei: public/Anforderungsdokument_[ProjektName].docx
```

**3.** Dokument prüfen und zur Freigabe bei der Geschäftsführung einreichen.

**4.** Nach Freigabe: Implementierung mit `@planner` starten.

---

## Tools

| Tool | Pfad / Path | Zweck / Purpose |
|---|---|---|
| **next-browser** | `.github/skills/next-browser/SKILL.md` | CLI that exposes React DevTools and the Next.js dev overlay as shell commands - component trees, props, errors, performance, screenshots - structured output for AI agents. |
| **anforderungsdokument** | `.github/skills/anforderungsdokument/SKILL.md` | Drei Entwicklungsprompts: Tiefenanalyse, Marketing/UX-Rework und Anforderungsdokument (9 Kapitel + Quellenverzeichnis als .docx). Nur Web/SaaS - keine mobilen Apps. Nur Quellen nicht älter als 1 Jahr. IDEA.md ausfüllen, Prompt 3 aufrufen, .docx generieren, zur Freigabe einreichen. |

### `next-browser` - AI-Driven Browser for Next.js

<table>
<tr>
<th width="50%">DE Was ist das?</th>
<th width="50%">EN What is it?</th>
</tr>
<tr>
<td><code>@vercel/next-browser</code> ist ein CLI-Tool, das React DevTools und das Next.js Dev-Overlay als Shell-Befehle bereitstellt. Agents können den Browser steuern, Komponenten inspizieren, Fehler lesen und Performance prüfen - ohne manuell durch DevTools zu klicken.</td>
<td><code>@vercel/next-browser</code> is a CLI tool that exposes React DevTools and the Next.js dev overlay as shell commands. Agents can drive the browser, inspect components, read errors, and check performance - without manually clicking through DevTools.</td>
</tr>
<tr>
<td><strong>Wann verwenden:</strong><br>- Nach der Implementierung zur visuellen Verifikation<br>- Debugging von Runtime-Fehlern oder Re-Render-Problemen<br>- Performance-Analyse (Core Web Vitals, Hydration)<br>- PPR-Shell-Debugging</td>
<td><strong>When to use:</strong><br>- After implementation for visual verification<br>- Debugging runtime errors or re-render issues<br>- Performance analysis (Core Web Vitals, hydration timing)<br>- PPR shell debugging</td>
</tr>
<tr>
<td><strong>Installation:</strong><br><code>npm install -g @vercel/next-browser</code><br><code>playwright install chromium</code><br>Benötigt Node >= 20</td>
<td><strong>Install:</strong><br><code>npm install -g @vercel/next-browser</code><br><code>playwright install chromium</code><br>Requires Node >= 20</td>
</tr>
<tr>
<td><strong>Wichtigste Befehle:</strong><br><code>next-browser open &lt;url&gt;</code> - Browser starten<br><code>next-browser snapshot</code> - Accessibility-Tree + klickbare Refs<br><code>next-browser errors</code> - Build- und Runtime-Fehler<br><code>next-browser perf</code> - Core Web Vitals + Hydration<br><code>next-browser screenshot</code> - Viewport als PNG<br><code>next-browser tree</code> - React-Komponentenbaum</td>
<td><strong>Key commands:</strong><br><code>next-browser open &lt;url&gt;</code> - launch browser<br><code>next-browser snapshot</code> - accessibility tree + clickable refs<br><code>next-browser errors</code> - build and runtime errors<br><code>next-browser perf</code> - Core Web Vitals + hydration timing<br><code>next-browser screenshot</code> - viewport as PNG<br><code>next-browser tree</code> - React component tree</td>
</tr>
<tr>
<td><strong>Vollständige Dokumentation:</strong> <code>.github/skills/next-browser/SKILL.md</code></td>
<td><strong>Full documentation:</strong> <code>.github/skills/next-browser/SKILL.md</code></td>
</tr>
</table>

---

### `anforderungsdokument` - WAMOCON Entwicklungsprompts

<table>
<tr>
<th width="50%">DE Was ist das?</th>
<th width="50%">EN What is it?</th>
</tr>
<tr>
<td>Der Skill stellt <strong>drei strukturierte Entwicklungsprompts</strong> bereit: (1) Tiefenanalyse und kritische Projektbewertung, (2) Marketing und UX/UI Rework, (3) Anforderungsdokument mit verbindlicher 9-Kapitel-Struktur (Zusammenfassung, Marktanalyse, Wettbewerb, Zielgruppe, Nutzen, Abhängigkeiten, Anforderungen V1, Chancen/Risiken, Umsetzungsplan + Quellenverzeichnis). <strong>Ausschließlich Web/SaaS - keine mobilen Apps. Nur Quellen nicht älter als 1 Jahr.</strong> IDEA.md ausfüllen, Prompt aus <code>@anforderungsdokument</code> kopieren, .docx generieren, zur Freigabe einreichen.</td>
<td>The skill provides <strong>three structured development prompts</strong>: (1) deep analysis and critical assessment, (2) marketing and UX/UI rework, (3) requirements document with a mandatory 9-chapter structure (summary, market analysis, competition, target audience, benefits, dependencies, requirements V1, opportunities/risks, implementation plan + references). <strong>Web/SaaS only - no mobile apps. Sources not older than 1 year only.</strong> Fill in IDEA.md, copy prompt from <code>@anforderungsdokument</code>, generate .docx, submit for approval.</td>
</tr>
</table>

---

## Empfohlener Workflow / Recommended Workflow

<table>
<tr>
<th width="50%">DE Schritt</th>
<th width="50%">EN Step</th>
</tr>
<tr>
<td><strong>Phase 0 - Anforderungen (neues Projekt):</strong><br>
1. <code>IDEA.md</code> im Projekt-Root ausfüllen<br>
2. <strong><code>@anforderungsdokument</code></strong> aufrufen: Prompt kopieren und senden<br>
3. Dokument prüfen und zur Freigabe einreichen<br>
4. Nach Freigabe: Implementierung starten</td>
<td><strong>Phase 0 - Requirements (new project):</strong><br>
1. Fill in <code>IDEA.md</code> in the project root<br>
2. Call <strong><code>@anforderungsdokument</code></strong>: copy prompt and send<br>
3. Review document and submit for approval<br>
4. After approval: start implementation</td>
</tr>
<tr>
<td><strong>Phase 1 - Planung:</strong><br>
<strong><code>@planner</code></strong> - Aufgabe analysieren und Implementierungsplan erstellen</td>
<td><strong>Phase 1 - Planning:</strong><br>
<strong><code>@planner</code></strong> - Analyse the task and create an implementation plan</td>
</tr>
<tr>
<td><strong>Phase 2 - Implementierung:</strong><br>
<strong><code>@developer</code></strong> - Plan entgegennehmen und schrittweise implementieren</td>
<td><strong>Phase 2 - Implementation:</strong><br>
<strong><code>@developer</code></strong> - Receive plan and implement step by step</td>
</tr>
<tr>
<td><strong>Phase 3 - Qualitätsprüfung:</strong><br>
<strong><code>@reviewer</code></strong> - Code prüfen, bevor ein PR erstellt wird</td>
<td><strong>Phase 3 - Quality review:</strong><br>
<strong><code>@reviewer</code></strong> - Review code before creating a PR</td>
</tr>
</table>

---

## Eigene Agents erstellen / Creating Custom Agents

<table>
<tr>
<th width="50%">DE Anleitung</th>
<th width="50%">EN Guide</th>
</tr>
<tr>
<td>Erstelle eine <code>.agent.md</code>-Datei in <code>.github/agents/</code> mit YAML-Frontmatter. Definiere Rolle, Workflow und Regeln.</td>
<td>Create a <code>.agent.md</code> file in <code>.github/agents/</code> with YAML frontmatter. Define role, workflow, and rules.</td>
</tr>
</table>

```yaml
---
name: MyAgent
description: >
  Description of what this agent does.
---
# Agent: MyAgent

## Role
...

## Workflow
...
```

---

## Wenn ein Agent schlecht antwortet / When an Agent Responds Poorly

<table>
<tr>
<th width="50%">DE Problem & Lösung</th>
<th width="50%">EN Problem & Solution</th>
</tr>
<tr>
<td><strong>Agent ignoriert Regeln aus der Instructions-Datei</strong><br>→ Prüfe das <code>applyTo</code>-Glob-Muster - stimmt es mit der Datei überein, die du bearbeitest? Teste mit: <code>**/*.ts</code> statt <code>src/**/*.ts</code></td>
<td><strong>Agent ignores rules from an Instructions file</strong><br>→ Check the <code>applyTo</code> glob pattern - does it match the file you are editing? Try broader patterns: <code>**/*.ts</code> instead of <code>src/**/*.ts</code></td>
</tr>
<tr>
<td><strong>Agent befolgt den Workflow nicht (z. B. überspringt typecheck)</strong><br>→ Öffne die <code>.agent.md</code>-Datei und mache die Anweisung strikter. Ersetze "sollte" durch "muss". Füge am Ende eine Zusammenfassung hinzu: <em>"Bevor du antwortest, liste alle abgeschlossenen Schritte auf."</em></td>
<td><strong>Agent does not follow the workflow (e.g. skips typecheck)</strong><br>→ Open the <code>.agent.md</code> file and make the instruction stricter. Replace "should" with "must". Add a reminder at the end: <em>"Before responding, list all completed steps."</em></td>
</tr>
<tr>
<td><strong>Agent schreibt schlechten Next.js-Code (z. B. falsche API-Nutzung)</strong><br>→ Füge ein konkretes Beispiel in die <code>nextjs.instructions.md</code> ein. Copilot folgt Beispielen besser als abstrakten Regeln.</td>
<td><strong>Agent writes bad Next.js code (e.g. wrong API usage)</strong><br>→ Add a concrete code example to <code>nextjs.instructions.md</code>. Copilot follows examples better than abstract rules.</td>
</tr>
<tr>
<td><strong>Agent "vergisst" den Kontext nach langen Gesprächen</strong><br>→ Starte ein neues Chat-Fenster. Langer Kontext verdrängt Instructions. Übergib den Plan explizit: <em>"Hier ist der Plan: [Plan]. Bitte implementiere Schritt 3."</em></td>
<td><strong>Agent "forgets" context after long conversations</strong><br>→ Start a new chat window. Long context pushes out instructions. Pass the plan explicitly: <em>"Here is the plan: [plan]. Please implement step 3."</em></td>
</tr>
<tr>
<td><strong>Agent antwortet auf Englisch statt Deutsch (oder umgekehrt)</strong><br>→ Füge in <code>copilot-instructions.md</code> eine Sprachanweisung hinzu: <em>"Antworte immer auf Deutsch."</em> - oder sprich den Agent in der gewünschten Sprache an.</td>
<td><strong>Agent responds in German instead of English (or vice versa)</strong><br>→ Add a language instruction to <code>copilot-instructions.md</code>: <em>"Always respond in English."</em> - or address the agent in your preferred language.</td>
</tr>
<tr>
<td><strong>Agent überschreitet den Plan / macht ungebetene Änderungen</strong><br>→ Füge in der <code>.agent.md</code> unter "Rules" hinzu: <em>"Ändere nur Dateien, die explizit im Plan genannt sind. Keine ungebetenen Refactors."</em></td>
<td><strong>Agent exceeds the plan / makes unrequested changes</strong><br>→ Add to the <code>.agent.md</code> under "Rules": <em>"Only modify files explicitly listed in the plan. No unrequested refactoring."</em></td>
</tr>
</table>

---

## Referenzen / References

- [GitHub Copilot Customisation Docs](https://docs.github.com/en/copilot/customizing-copilot)
- [awesome-copilot](https://github.com/github/awesome-copilot) - Beispiele und Best Practices / Examples and best practices

## ./Anforderungsdokument_Geburtstagspilot_v1.0.md
# Anforderungsdokument Geburtstagspilot (Kindergeburtstag-Planungs-App)
## Softwareprojekt Welle 10

---

| | |
|---|---|
| **Projekt** | Geburtstagspilot. Dein kompletter Kindergeburtstag in 5 Minuten |
| **Unternehmen** | WAMOCON GmbH |
| **App Version** | 1 |
| **Erstellt von** | Daniel Moretz |
| **Eingereicht an** | Waleri Moretz (Geschäftsführung) |
| **Datum** | 6. Mai 2026 |
| **Vertraulichkeit** | Intern vertraulich |
| **Status** | Zur Freigabe eingereicht |

---

## 1. Zusammenfassung

### 1.1 Die Idee

**Geburtstagspilot** ist eine browserbasierte Web-App, die Eltern in unter 5 Minuten einen kompletten Kindergeburtstag plant von der Einladung über den Zeitablauf, Spiele mit Anleitung, Kuchen- und Essensideen bis zur Einkaufsliste und den Goodie-Bags. Kein Account nötig, sofort Ergebnis, PDF-Export, WhatsApp-teilbar.

Das Produkt löst ein universelles Elternproblem: Jedes Jahr, jedes Kind, derselbe Stress. Was ist das Motto? Welche Spiele passen zum Alter? Wie viele Würstchen für 12 Kinder? Was kommt in die Mitgebsel-Tüten? Wie strukturiere ich 3 Stunden, damit kein Chaos ausbricht? Bisher: Pinterest-Spirale, Mama-Blogs, WhatsApp-Gruppen, improvisierte Excel-Listen.

**V1** liefert einen personalisierten Komplettplan per Wizard: Alter des Kindes (3–12), Gästezahl, Indoor/Outdoor, Motto-Wahl → automatischer Zeitablauf (3 Stunden), 5 altersgerechte Spiele mit Schritt-für-Schritt-Anleitung, Kuchen-Rezept, Essens-/Getränke-Vorschläge, Einkaufsliste (berechnet auf Gästezahl), Einladungs-Template (PDF + WhatsApp-Bild), Goodie-Bag-Ideen.

**V2** ergänzt KI: Spieleempfehlungen nach Wetterlage und Platzverhältnissen, ein visueller Einladungs-Designer, Kosten-Kalkulation, KI-Motto-Generator aus Interessen des Kindes und eine Community-Funktion für Eltern-Bewertungen und eigene Spielideen.

### 1.2 Warum jetzt?

Drei konvergierende Trends machen dieses Produkt gerade jetzt relevant:

**Eltern-Burnout und Perfektionsdruck.** Social Media (Instagram, Pinterest) hat die Erwartungshaltung an Kindergeburtstage massiv erhöht. 67 % der Eltern empfinden die Planung als stressig, 43 % beginnen erst eine Woche vorher (Forsa Familienstudie 2025). Gleichzeitig steigt der Anteil berufstätiger Elternpaare (beide Partner erwerbstätig: 72 % in DE, Destatis Mikrozensus 2025), weniger Zeit für Planung.

**Steigende Kosten, sinkende Budgets.** Die durchschnittlichen Ausgaben für einen Kindergeburtstag in DE liegen bei €150–350 (Statista Consumer Insights 2025). Inflation und Energiekosten drücken auf Budgets. Eltern suchen nach kosteneffizienten, aber trotzdem besonderen Feiern, genau das leistet ein strukturierter Plan.

**Mobile-First-Eltern.** 89 % der Eltern mit Kindern unter 12 nutzen Smartphones als primäres Planungsinstrument (Bitkom Familien-Digital-Index 2025). Browser-basierte Tools, die ohne App-Download funktionieren, haben minimale Einstiegshürden.

**Kein dominanter Anbieter in DACH.** Bestehende Angebote sind fragmentiert: Mama-Blogs (nicht interaktiv), Pinterest-Boards (unstrukturiert), einzelne Spiele-Sammlungen ohne Planungsfunktion. Es gibt kein Tool, das den gesamten Planungs-Workflow aus einem Guss liefert.

Quellen: Forsa Familienstudie 2025, Destatis Mikrozensus 2025, Statista Consumer Insights. Kindergeburtstage DE 2025, Bitkom Familien-Digital-Index 2025

---

## 2. Marktanalyse: Fokus DACH

### 2.1 Zielmarkt und Segmentierung

Der adressierbare Markt umfasst Haushalte mit Kindern im feierrelevanten Alter (3–12 Jahre):

- **Deutschland:** 6,4 Mio. Kinder im Alter 3–12 (Destatis Bevölkerungsstatistik 2025)
- **Österreich:** 720.000 Kinder im Alter 3–12 (Statistik Austria 2025)
- **Schweiz:** 680.000 Kinder im Alter 3–12 (BFS Bevölkerung 2025)
- **Gesamt DACH:** ~7,8 Mio. Kinder → ~7,8 Mio. potenzielle Kindergeburtstage pro Jahr

Nicht jeder Geburtstag wird als Party gefeiert. Realistisch schätzen Branchenexperten, dass 60–70 % der Kinder eine Feier mit Gästen haben (Spielen-und-Feiern.de Branchenreport 2025), also **~4,5–5,5 Mio. Kindergeburtstagsfeiern pro Jahr** im DACH-Raum.

### 2.2 Marktvolumen

Der Kindergeburtstags-Markt ist ein Teilsegment des Kinderevents- und Partybedarfs-Marktes:

- **Durchschnittliche Ausgaben pro Feier:** €150–350 (Statista 2025)
- **Gesamtmarktvolumen DACH:** ~€750 Mio. – €1,9 Mrd./Jahr (Partybedarf + Gastronomie + Eventlocations + Dekoration)
- **Digitales Segment (Tools, Templates, Content):** Noch weitgehend unmonetarisiert, geschätztes Potenzial €15–30 Mio./Jahr bei 1–2 % Penetration mit digitalem Planungstool

Der Markt ist stark saisonal (Peaks: September–November und März–Juni, Tief: Juli/August Ferien und Dezember/Weihnachten).

### 2.3 Das Kernproblem: Fragmentierte Information, kein Workflow

Eltern stehen vor einem wiederkehrenden Planungsproblem, das sie jedes Jahr von Null lösen:

**Informationsquelle-Chaos.** Spiele auf Pinterest, Rezepte auf Chefkoch, Einladungen auf Canva, Einkaufsliste in der Notizen-App, Mengenberechnung im Kopf, 5+ Tools für eine 3-Stunden-Feier.

**Altersgerechte Auswahl.** Was funktioniert mit 4-Jährigen ist für 9-Jährige peinlich. Eltern googeln "Spiele Kindergeburtstag 7 Jahre" und bekommen 200 Ergebnisse ohne Filterung.

**Mengenplanung.** 8 Kinder, 3 Stunden, wie viele Würstchen, Brötchen, Saft, Kuchen? Zu wenig = Chaos, zu viel = Verschwendung. Keine schnelle Berechnung.

**Zeitstruktur fehlt.** Ohne Ablaufplan: Kinder kommen an, 20 Minuten Chaos, dann fällt den Eltern kein Spiel ein, dann essen, dann Geschenke, dann warten auf Abholung. Mit Ablaufplan: strukturierte 3 Stunden mit Ankommen, 3 Spielrunden, Essen, Kuchen, Geschenke, Abschluss.

**Wiederholung ohne Lernen.** Jedes Jahr dasselbe von vorn, weil nichts gespeichert, nichts wiederverwendet wird.

### 2.4 Regulatorischer Kontext

Kein regulatorischer Overhead. Keine personenbezogenen Daten von Kindern in V1 erforderlich (kein Account, kein Upload von Kinderfotos). DSGVO-Anforderungen minimal: Cookie-freies Hosting, keine Tracking-Pixel, kein Drittanbieter-Analytics außer Plausible (EU, cookiefrei).

Quellen: Destatis Bevölkerungsstatistik 2025, Statistik Austria Bevölkerung 2025, BFS Schweiz 2025, Statista Consumer Insights 2025, Forsa Familienstudie 2025, Bitkom Familien-Digital-Index 2025

---

## 3. Wettbewerb

### 3.1 Direkte und indirekte Anbieter

| Anbieter | Art | Stärke | Schwäche / Chance für Geburtstagspilot |
|---|---|---|---|
| **Pinterest** | Plattform | Riesige Inspirationsquelle, visuell | Keine Struktur, kein Workflow, keine Mengenberechnung, Zeitfresser |
| **Mama-Blogs** (z.B. Hallo-Eltern, Familie.de) | Content | Gute Spielideen, SEO-stark | Keine Interaktivität, keine Personalisierung nach Alter/Gästezahl, Werbung |
| **Canva** | Design-Tool | Einladungen gestalten | Nur Einladungen, kein Planungstool, Overkill für einen DIN-A5-Zettel |
| **Kindergeburtstag-Planen.de** | Blog + PDFs | Strukturierte Checklisten | Keine personalisierte Berechnung, PDFs statisch, kein Wizard |
| **Amazon / Partybedarfs-Shops** | E-Commerce | Produkte kaufen | Keine Planung, nur Verkauf |
| **Geburtstagsfee.de** | E-Commerce + Content | Dekoration + Spielideen | Fokus auf Produktverkauf, keine Ablaufplanung |
| **ChatGPT / KI-Assistenten** | Generative AI | Flexible Antworten | Kein strukturierter Workflow, keine Mengenberechnung, kein PDF-Export, Halluzinationen bei Spielregeln |

**Marktlücke:** Kein Anbieter kombiniert **altersgerechte Personalisierung**, **Mengenberechnung**, **Zeitablauf-Generator**, **Einladungs-Template**, **Einkaufsliste** und **PDF-Export** in einem schnellen, mobil-optimierten Wizard ohne Account.

### 3.2 Warum Blog-Content nicht reicht

| Problem mit Blog-Ansatz | Lösung Geburtstagspilot |
|---|---|
| Statische Listen (nicht personalisiert) | Wizard mit Alter × Gästezahl × Motto × Indoor/Outdoor |
| Mengen unklar ("etwas Saft, ein paar Würstchen") | Exakte Berechnung: 12 Kinder × 2 Würstchen = 24 Würstchen |
| Kein Zeitablauf | Automatischer 3-Stunden-Plan mit Minutenangaben |
| Keine Einkaufsliste | 1-Klick-Einkaufsliste nach Kategorie |
| Keine Einladung | Druckfertige Einladung mit allen Infos |
| Werbung, Cookie-Banner, Ablenkung | Clean UI, keine Werbung in Free-Tier, fokussiert |

---

## 4. Zielgruppe

### 4.1 Primäre Zielgruppe

**Eltern mit Kindern im Alter 3–12 Jahre** im DACH-Raum, die den Kindergeburtstag zu Hause oder im Garten feiern.

Vier Nutzerprofile:

**Erstgeburtstags-Mutter/Vater (Kind wird 3–4).** Erste "richtige" Party mit Gästen. Unsicher, was altersgerecht ist. Will nichts falsch machen. Braucht: einfache Spiele, kurzer Ablauf (2 Stunden), wenige Gäste, sichere Essensideen.

**Routine-Eltern (Kind wird 5–8).** Jedes Jahr dasselbe Theater. Suchen Inspiration, die sich vom letzten Jahr unterscheidet. Braucht: neues Motto, andere Spiele, effiziente Planung ("Ich will das in 10 Minuten erledigt haben").

**Motto-Perfektionisten (Kind wird 6–10).** Wollen eine Instagram-würdige Party. Piraten, Einhörner, Detektive, Weltraum, alles muss zum Motto passen. Braucht: thematisch abgestimmte Spiele, Deko-Ideen, Einladungs-Design.

**Last-Minute-Eltern (alle Altersgruppen).** Geburtstag ist in 3 Tagen, nichts geplant. Panik. Braucht: sofort einen Komplettplan mit Einkaufsliste, die sie am gleichen Tag abarbeiten können.

### 4.2 Sekundäre Zielgruppe

- **Großeltern**, die den Geburtstag organisieren (zunehmend, wenn beide Eltern arbeiten)
- **Tagesmütter/Kita-Erzieher**, die Geburtstagsfeiern in der Einrichtung planen
- **Kindergeburtstags-Eventanbieter**, die strukturierte Ablaufpläne als Upsell nutzen

### 4.3 Nicht Zielgruppe

- Teenager-Partys (13+), anderer Bedarf, andere Dynamik
- Professionelle Event-Agenturen, brauchen andere Tools
- Geburtstage in kommerziellen Locations (Indoor-Spielplatz, Kletterhalle). Dort plant die Location

---

## 5. Nutzen

### 5.1 Nutzen für die Nutzer (Eltern)

| Problem heute | Lösung durch Geburtstagspilot | Konkreter Vorteil |
|---|---|---|
| Stundenlange Recherche auf Pinterest/Blogs | Wizard generiert Komplettplan in 5 Minuten | 3–5 Stunden Planungszeit gespart |
| Keine altersgerechte Filterung | Spiele und Ablauf angepasst an exaktes Alter | Keine peinlichen Spiel-Fails |
| Mengenplanung im Kopf → zu viel/zu wenig | Automatische Berechnung auf Gästezahl | Kein Überkauf, keine Unterversorgung |
| Kein Zeitablauf → Chaos auf der Feier | 3-Stunden-Minutenplan mit Puffern | Strukturierte, entspannte Feier |
| Einladungen basteln oder Canva-Kampf | 1-Klick-Einladung als PDF + WhatsApp-Bild | In 60 Sekunden versendet |
| Jedes Jahr von Null anfangen | Bewährte, kuratierte Inhalte | Vertrauen statt Unsicherheit |

### 5.2 Nutzen für die WAMOCON GmbH

**Extrem breite Zielgruppe:** 4,5+ Mio. Kindergeburtstage/Jahr in DACH, jedes Elternteil ist potenzieller Nutzer, ohne Branchen- oder Berufsfilter.

**Virales Wachstum:** Eltern teilen Einladungen → Empfänger-Eltern sehen das Tool → planen ihren nächsten Geburtstag damit. Natürlicher Empfehlungskreislauf.

**Wiederkehrende Nutzung:** Pro Kind mindestens 7–10 Jahre Kindergeburtstage. Bei 2+ Kindern: jahrelange Nutzung.

**SEO-Goldmine:** "Kindergeburtstag Spiele 6 Jahre", "Kindergeburtstag Motto Ideen", "Kindergeburtstag Einkaufsliste", hochvolumige, transaktionsnahe Suchanfragen mit geringem Wettbewerb durch spezialisierte Tools.

**Affiliate- und Lead-Potential:** Einkaufsliste → Affiliate-Links zu Amazon/Partybedarf-Shops. Eventlocations → Lead-Gen.

**Ultra-niedrige Infrastrukturkosten:** 100 % client-seitig in V1. Hosting €0 (Cloudflare Pages / Vercel Hobby). Keine API-Kosten, keine Datenbank.

---

## 6. Abhängigkeiten und Machbarkeit

### 6.1 Technische Services

| Service | Funktion | Abhängigkeit | Kosten V1 |
|---|---|---|---|
| **Cloudflare Pages / Vercel Hobby** | Statisches Hosting, CDN | Keine Exklusiv | €0/Monat |
| **pdf-lib (Open Source)** | PDF-Generierung im Browser | MIT-Lizenz | €0 |
| **html2canvas / dom-to-image** | Einladungs-Bild-Export | Open Source | €0 |
| **Plausible Analytics (EU)** | Cookie-freie Nutzungsstatistik | Optional | €9/Monat |
| **Stripe** | Pro-Tier-Zahlung | Zertifiziert | 1,4 % + €0,25/Tx |

### 6.2 Keine externen APIs in V1

V1 arbeitet komplett ohne externe APIs. Alle Daten (Spiele-Datenbank, Rezepte, Mengenformeln, Einladungs-Templates) sind statisch im Frontend eingebettet. Das bedeutet:

- Keine Laufzeitkosten
- Keine API-Rate-Limits
- Keine Downtime-Abhängigkeiten
- Offline-fähig als PWA (nach erstem Laden)

### 6.3 V2-Abhängigkeiten (Vorausschau)

| Service | V2-Funktion | Kosten |
|---|---|---|
| **OpenWeatherMap API** | Wetter-basierte Spieleempfehlung (Indoor/Outdoor) | Free Tier reicht |
| **OpenAI API / Mistral** | KI-Motto-Generator, personalisierte Spielideen | ~€0,01/Anfrage |
| **Supabase (EU)** | Community-Spielideen, Nutzerkonten | Ab €25/Monat |

### 6.4 Gesamtbewertung

V1 ist ohne jede Partnerschaft, ohne Behördengenehmigung und ohne laufende API-Kosten umsetzbar. Das Produkt kann in **2–3 Wochen** von einem Solo-/Duo-Entwicklerteam gelauncht werden. Kein regulatorisches Risiko, kein Datenschutz-Overhead (kein Account, keine Kinderdaten).

---

## 7. Anforderungen Version 1

### 7.1 Hauptprozesse

#### 7.1.1 Party-Wizard (Kernprozess)

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| PW-01 | Wizard-Schritt 1: Alter des Kindes (3–12 Jahre, Dropdown oder Slider) | Muss | Neu |
| PW-02 | Wizard-Schritt 2: Gästezahl (3–20 Kinder, Dropdown) | Muss | Neu |
| PW-03 | Wizard-Schritt 3: Indoor / Outdoor / Beides | Muss | Neu |
| PW-04 | Wizard-Schritt 4: Motto-Wahl aus kuratierter Liste (Piraten, Prinzessin, Dinos, Weltraum, Fußball, Detektiv, Einhorn, Tiere, Superhelden, Zirkus, Ritter, Meerjungfrau, Dschungel, ohne Motto) | Muss | Neu |
| PW-05 | Wizard-Schritt 5: Dauer (2 / 2,5 / 3 / 3,5 Stunden) | Muss | Neu |
| PW-06 | Wizard-Schritt 6: Budget-Rahmen (optional: €50 / €100 / €150 / €200 / egal) | Soll | Neu |
| PW-07 | Wizard generiert Ergebnis sofort nach letztem Schritt (kein Server-Request) | Muss | Neu |
| PW-08 | Ergebnis-Seite zeigt alle Sektionen übersichtlich mit Tabs oder Akkordeon | Muss | Neu |

#### 7.1.2 Zeitablaufplan

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| ZA-01 | Automatischer Zeitablauf basierend auf gewählter Dauer (z.B. 3h: 14:00–17:00) | Muss | Neu |
| ZA-02 | Phasen: Ankommen & Freispiel (20 Min) → Begrüßung (5 Min) → Spiel 1 (15–20 Min) → Spiel 2 (15–20 Min) → Essen/Kuchen (25 Min) → Spiel 3 (15–20 Min) → Geschenke auspacken (15 Min) → Freispiel/Abholung (15–20 Min) | Muss | Neu |
| ZA-03 | Puffer-Zeiten zwischen Phasen automatisch eingeplant | Muss | Neu |
| ZA-04 | Drag-and-Drop-Reihenfolge anpassen (Spiel 2 vor Kuchen) | Soll | Neu |
| ZA-05 | Startzeit anpassbar (Ergebnis rechnet alle Zeiten automatisch um) | Muss | Neu |
| ZA-06 | PDF-Export des Zeitablaufs (1 Seite, druckbar) | Muss | Neu |

#### 7.1.3 Spiele-Empfehlungen

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| SP-01 | Datenbank mit mindestens 80 Spielen, kategorisiert nach Alter (3–4, 5–6, 7–8, 9–10, 11–12), Indoor/Outdoor, Aktivitätslevel (ruhig/aktiv/wild) | Muss | Neu |
| SP-02 | Jedes Spiel: Name, Beschreibung (3–5 Sätze), Schritt-für-Schritt-Anleitung, benötigtes Material, Dauer, Mindestteilnehmerzahl | Muss | Neu |
| SP-03 | Motto-Filter: Spiele passend zum gewählten Motto (z.B. Piraten → Schatzsuche, Einhorn → Regenbogenlauf) | Muss | Neu |
| SP-04 | 5 Spiele pro Plan vorgeschlagen (Mix aus aktiv + ruhig), davon 3 im Zeitablauf fest und 2 als Reserve | Muss | Neu |
| SP-05 | "Dieses Spiel austauschen" → nächster passender Vorschlag | Muss | Neu |
| SP-06 | Benötigtes Material aus Spielen automatisch in Einkaufsliste übernommen | Muss | Neu |

#### 7.1.4 Kuchen- und Essensvorschläge

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| KE-01 | 1 Kuchen-Rezept passend zum Motto (z.B. Piraten → Schiffskuchen, Dinos → Vulkan-Kuchen) mit Schritt-für-Schritt-Anleitung und Foto-Beschreibung | Muss | Neu |
| KE-02 | Essensvorschläge: Herzhaft (Würstchen, Pizza, Mini-Burger, Gemüsesticks) + Snacks (Popcorn, Obstspieße, Brezeln) + Getränke (Saft, Wasser, Kinderbowle) | Muss | Neu |
| KE-03 | Mengenberechnung pro Gast (z.B. 2 Würstchen/Kind, 0,5L Getränke/Kind, 1 Stück Kuchen + 1 Reserve) | Muss | Neu |
| KE-04 | Allergiker-Hinweis Toggle (glutenfrei, laktosefrei, nussfrei) → alternative Rezepte | Soll | Neu |
| KE-05 | Rezept-Zutaten automatisch in Einkaufsliste | Muss | Neu |

#### 7.1.5 Einkaufsliste

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| EK-01 | Automatisch generierte Einkaufsliste aus: Essen + Spiel-Material + Deko + Goodie-Bags | Muss | Neu |
| EK-02 | Mengen auf Gästezahl berechnet + 10 % Puffer | Muss | Neu |
| EK-03 | Kategorisiert: Lebensmittel / Getränke / Bastelmaterial / Deko / Goodie-Bag-Inhalt | Muss | Neu |
| EK-04 | Abhak-Funktion (Checkbox pro Artikel) | Muss | Neu |
| EK-05 | PDF-Export der Einkaufsliste | Muss | Neu |
| EK-06 | WhatsApp-Share der Liste (als Text) | Soll | Neu |

#### 7.1.6 Einladungs-Generator

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| EI-01 | Einladungs-Template pro Motto (visuell, kindgerecht, A5/A6) | Muss | Neu |
| EI-02 | Felder: Name des Kindes, Alter wird, Datum, Uhrzeit, Adresse, RSVP-Datum, "Bitte mitbringen" (z.B. Regenhose, Schwimmzeug) | Muss | Neu |
| EI-03 | PDF-Export (2× A5 auf A4 zum Drucken) | Muss | Neu |
| EI-04 | WhatsApp-Bild-Export (1080×1080 PNG/JPG) | Muss | Neu |
| EI-05 | QR-Code zur Party-Seite (optional, für digitale Einladung) | Soll | Neu |

#### 7.1.7 Goodie-Bag-Ideen

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| GB-01 | 5 Goodie-Bag-Vorschläge pro Motto + Budget-Stufe (€2/Kind, €5/Kind, €8/Kind) | Muss | Neu |
| GB-02 | Artikelliste mit Mengenberechnung auf Gästezahl | Muss | Neu |
| GB-03 | Goodie-Bag-Material in Einkaufsliste integriert | Muss | Neu |

### 7.2 Basisfunktionalitäten

| ID | Anforderung | Priorität | Status |
|---|---|---|---|
| BF-01 | Kein Account/Login für V1 nötig. Wizard sofort nutzbar | Muss | Neu |
| BF-02 | Ergebnis als Permalink speicherbar (URL mit Parametern oder Hash-basiert) | Muss | Neu |
| BF-03 | Gesamtplan als PDF-Export (alles auf 3–4 Seiten: Ablauf + Spiele + Einkaufsliste + Einladung) | Muss | Neu |
| BF-04 | Responsive Mobile-First-Design | Muss | Neu |
| BF-05 | Offline-fähig als PWA (Service Worker für Wiederöffnen) | Soll | Neu |
| BF-06 | Ladezeit <2 Sekunden (statisches Hosting, keine API-Calls) | Muss | Neu |
| BF-07 | Cookie-freies Tracking (Plausible) | Muss | Neu |
| BF-08 | DSGVO: Datenschutzerklärung, Impressum, kein Tracking ohne Consent | Muss | Neu |
| BF-09 | Deutsche Sprache als Standard, erweiterbar auf AT/CH-Varianten | Muss | Neu |

### 7.3 Preismodell

| Tier | Preis | Inhalt |
|---|---|---|
| **Free** | €0 | 1 Komplettplan/Monat, Basis-Einladung, PDF-Export (mit Branding) |
| **Party-Paket** | €4,99 einmalig | Unbegrenzte Pläne, Premium-Einladungs-Templates (10+ Designs), Einkaufsliste ohne Branding, alle Mottos |
| **Party-Pro** | €9,99 einmalig | Alles aus Party-Paket + Einladungs-Designer (eigene Farben, Foto-Upload), Kosten-Kalkulator, Spiele-Volldatenbank (80+ Spiele mit Varianten) |

### 7.4 Scope: Was ist Version 1 und was nicht

| In Scope Version 1 | Out of Scope, ab V2 |
|---|---|
| Party-Wizard mit 6 Schritten | KI-Motto-Generator aus Interessen |
| Zeitablaufplan mit Drag-and-Drop | Wetter-basierte Spielanpassung (API) |
| 80+ kuratierte Spiele mit Anleitungen | Community-Spielideen von Eltern |
| Kuchen-Rezepte + Essensvorschläge | Rezept-Video-Integration |
| Mengenberechnung auf Gästezahl | Supermarkt-Preisvergleich |
| Einkaufsliste mit PDF-Export | Affiliate-Integration zu Shops |
| Einladungs-Template (PDF + WhatsApp) | Visueller Einladungs-Designer |
| Goodie-Bag-Ideen | Personalisierte Etiketten-Generator |
| Permalink zum Teilen | Nutzerkonten mit gespeicherten Partys |

---

## 8. Anforderungen Version 2 (KI-Erweiterung)

| ID | Anforderung | Priorität | Nutzen |
|---|---|---|---|
| KI-01 | **KI-Motto-Generator:** Kind interessiert sich für X + Y → "Dein Motto: Weltraum-Detektive!" mit passenden Spielen, Deko, Kuchen | Muss | Einzigartige Personalisierung |
| KI-02 | **Wetter-Empfehlung:** PLZ + Datum → Wettervorhersage → "Wahrscheinlich Regen, wir empfehlen Indoor-Spiele" mit automatischem Planswitch | Soll | Weniger Last-Minute-Panik |
| KI-03 | **Einladungs-Designer:** Visueller Editor mit Drag-and-Drop: Hintergrund, Schriftart, Sticker, eigenes Foto-Upload → Export als Print + Digital | Muss | Premium-Feature, hohe Zahlungsbereitschaft |
| KI-04 | **Community-Spiele:** Eltern reichen eigene Spiele ein + bewerten bestehende ("Hat bei 8-Jährigen super funktioniert") | Soll | User-Generated Content, SEO, Bindung |
| KI-05 | **Kosten-Kalkulator:** Alle Einkaufslisten-Artikel mit Durchschnittspreisen hinterlegt → "Dein Geburtstag kostet ca. €120" | Muss | Budget-Transparenz |
| KI-06 | **Mehrere Kinder verwalten:** Nutzer-Account mit gespeicherten Partys pro Kind + "Was haben wir letztes Jahr gemacht?" | Soll | Wiederkehrende Nutzung |
| KI-07 | **Schatzsuche-Generator:** Alter + Motto + Spielort (Wohnung/Garten/Park) → komplett ausformulierte Schnitzeljagd mit Rätseln, Hinweisen und Karte | Muss | Killer-Feature, hoher Wow-Faktor |
| KI-08 | **Foto-Einladung:** KI generiert kindgerechte Illustration aus Motto (z.B. "Ein Piratenschiff mit 8 Kindern") | Kann | Differenzierung, Social-Media-virales Asset |

---

## 9. Zwei Alternativkonzepte in ähnlicher Richtung

### 9.1 Alternative A: SchatzApp (Schatzsuche-/Schnitzeljagd-Generator)

**Kernidee:** Statt gesamter Geburtstagsplanung Fokus auf den beliebtesten Programmpunkt: die Schatzsuche. SchatzApp generiert komplette Schnitzeljagden mit Rätseln, Hinweisen, Karte und Versteck-Anleitung, personalisiert nach Alter, Motto und Spielort.

**V1:** 30 vorgefertigte Schnitzeljagden (thematisch), anpassbar nach Spielort (Wohnung 3 Zimmer / Garten / Park / Wald). Rätsel als druckbare Karten. Schatzkarte als PDF.

**V2:** KI generiert individuelle Rätsel aus Kindernamen und Interessen. GPS-basierte Outdoor-Schnitzeljagd. Augmented Reality (Hinweise per Kamera scannen).

**Pricing:** €3,99 pro Schnitzeljagd oder €9,99/Jahr für unbegrenzt.

**Warum verfolgbar:** Schnitzeljagden sind der Nr.1-Suchanfrage-Treiber bei Kindergeburtstagen (Google Trends DACH 2025). Kann als Standalone oder als Premium-Modul innerhalb von Geburtstagspilot funktionieren.

### 9.2 Alternative B: KinderMenü-Rechner (Party-Essens-Planer)

**Kernidee:** Fokus ausschließlich auf die Mengenberechnung und Essensplanung für Kindergeburtstage und andere Kinderfeste. Keine Spiele, keine Einladungen, nur: "Wie viel von was für wie viele Kinder?"

**V1:** Gästezahl + Essenstyp (Pizza, Würstchen, Buffet, Kuchen) + Dauer → exakte Mengen pro Zutat + Einkaufsliste.

**V2:** Allergie-Manager, Rezept-Vorschläge, Supermarkt-Preisvergleich.

**Pricing:** Free mit Werbung. Pro €1,99 einmalig.

**Warum verfolgbar:** Ultra-schnelle Umsetzung (1 Woche), auch außerhalb von Geburtstagen nutzbar (Kita-Feste, Vereinsfeste), aber limitiertes Monetarisierungspotenzial.

---

## 10. Chancen und Risiken

### 10.1 Chancen

| Chance | Begründung |
|---|---|
| Virales Wachstum über Einladungen | Jede versendete Einladung ist Marketing für die App |
| SEO-Dauerbrenner | "Kindergeburtstag Spiele", "Kindergeburtstag planen" = 150.000+ Suchen/Monat DACH (Sistrix 2025) |
| Saisonales Wiederkehren | Jeden Monat haben Kinder Geburtstag. Nachfrage ganzjährig |
| Affiliate-Potenzial | Einkaufsliste → Amazon/Partybedarf-Links = passive Revenue |
| Erweiterbar auf angrenzende Events | Kita-Feste, Einschulung, Halloween-Party, Osterparty |
| Emotional positive Marke | "Danke, das hat mir den Tag gerettet" → hohe Weiterempfehlung |

### 10.2 Risiken

| Risiko | Gegenmaßnahme |
|---|---|
| Geringe Zahlungsbereitschaft bei Eltern für Tools | Einmalkauf statt Abo (€4,99 = Preis einer Packung Luftballons). Wert klar kommunizieren |
| Content-Aufwand (80+ Spiele kuratieren) | Einmalige Investition, danach Asset. Community-Beiträge ab V2 |
| Saisonale Schwankungen (Ferien/Weihnachten = Tief) | SEO-Content für Nebensaison (Indoor-Geburtstage im Winter, Motto "Weihnachtsparty") |
| Pinterest/Blogs als Gewohnheit | Überlegene UX + Workflow (5 Min vs. 3 Stunden) als Differenzierer |
| ChatGPT als Substitut | Strukturierter Output + PDF-Export + kuratierte Qualität > generischer LLM-Output |

---

## 11. Umsetzungsplan Version 1

### 11.1 Technologiestack

- **Frontend:** Next.js 15 (Static Export) oder Astro, Tailwind CSS, TypeScript
- **PDF-Generierung:** pdf-lib + html2canvas (client-seitig)
- **Bild-Export:** dom-to-image (Einladungen als PNG)
- **Hosting:** Cloudflare Pages (kostenlos, CDN, DACH-PoPs)
- **Analytics:** Plausible EU (cookiefrei)
- **Payment (Pro-Tier):** Stripe Checkout (einmalige Zahlung)
- **PWA:** Service Worker für Offline-Fähigkeit

### 11.2 Umsetzungsplan 5 Werktage

| Tag | Fokus | Inhalt |
|---|---|---|
| Tag 1 | Content-Grundlage | Spiele-Datenbank (80 Spiele, JSON-Struktur), Kuchen-Rezepte (14 Mottos), Mengenformeln, Goodie-Bag-Katalog, Einladungs-Templates (Texte) |
| Tag 2 | Wizard + Logik | 6-Schritt-Wizard-UI, Auswahllogik (Alter × Motto × Indoor/Outdoor → Spiele-Matching), Mengenberechnung, Zeitablauf-Generator |
| Tag 3 | Ergebnis-Seite + PDF | Ergebnis-Anzeige (Tabs/Akkordeon), PDF-Export (Ablauf + Spiele + Einkaufsliste), Permalink-Generierung |
| Tag 4 | Einladungen + Einkaufsliste | Einladungs-Templates (14 Mottos, A5-PDF + WhatsApp-PNG), Einkaufsliste mit Checkbox-UI + PDF + WhatsApp-Text-Share |
| Tag 5 | Pro-Tier, QA, Launch | Stripe-Checkout für Pro-Paket, Paywall für Premium-Einladungen/Spiele, Plausible-Integration, Datenschutz/Impressum, manueller Test aller Flows, Deploy |

---

## 12. Marke, Branding und Marketing

### 12.1 Markenname und Bedeutung

**Geburtstagspilot** ist bewusst gewählt: seriös, klar, DACH-tauglich und sofort verständlich. In einem Markt, der von SEO und Google-Suche lebt, ist ein beschreibender Name ein strategischer Vorteil:

- **SEO-Power:** "Kindergeburtstag planen" und "Kinder Party" sind hochvolumige Keywords. Der Markenname enthält die Suchwörter nativ.
- **Sofortverständlich:** Keine Erklärung nötig. Eltern wissen nach dem Namen, was das Tool tut.
- **WhatsApp-teilbar:** "Ich hab den Geburtstag mit dem Geburtstagspilot geplant, mega!", natürliche Weiterempfehlung.

**Alternative Kurzformen:** GebPilot (fuer Social Media), Pilot (informell).

### 12.2 Positionierung

| Dimension | Ausprägung |
|---|---|
| **Markenversprechen** | "3 Stunden Spaß. 5 Minuten Planung." |
| **Werte** | Einfach · Fröhlich · Verlässlich · Eltern-freundlich |
| **Tonalität** | Warmherzig, humorvoll, verständnisvoll für Elternstress. Nie herablassend, nie perfektionistisch |
| **Sprachregeln** | Du-Ansprache. Kurze Sätze. Emojis erlaubt (🎂🎈🎁). Keine Erziehungsratschläge. |
| **Was Geburtstagspilot nicht ist** | Kein Erziehungs-Blog. Kein Deko-Shop. Keine "perfekte Instagram-Mama"-Marke. |

**Claim-Vorschläge:**
- **"Geburtstagspilot, 3 Stunden Spaß. 5 Minuten Planung."** (Hauptclaim)
- "Geburtstagspilot. Damit du die Party genießen kannst."
- "Geburtstagspilot. Geburtstag planen ohne Stress."

### 12.3 Visuelle Identität

| Element | Empfehlung | Begründung |
|---|---|---|
| **Primärfarbe** | Fröhliches Konfetti-Lila `#7C3AED` | Festlich, kindgerecht, hebt sich von typischem Rosa/Blau ab |
| **Akzentfarbe** | Sonniges Gelb `#FBBF24` | Freude, Geburtstag, Luftballons |
| **Sekundär** | Mintgrün `#34D399`, Koralle `#F87171` | Party-Palette, farbenfroh ohne kitschig |
| **Hintergrund** | Cremeweiß `#FFFDF7` | Warm, einladend, nicht steril |
| **Typografie** | Rounded Sans-Serif (z.B. *Nunito*, *Quicksand*) | Freundlich, kindgerecht, gut lesbar |
| **Bildwelt** | Illustrationen statt Fotos (Vektor-Stil: Luftballons, Kuchen, Girlanden, spielende Kinder) | Universell, inklusiv, lizenzfrei reproduzierbar |
| **Bewegung** | Konfetti-Animation bei Ergebnis-Generierung, sanftes Bounce auf CTAs | Feier-Stimmung, Dopamin beim Ergebnis |

### 12.4 Marketing-Strategie

#### 12.4.1 SEO-Driven Content (Hauptkanal)

| Keyword-Cluster | Suchvolumen DACH/Monat (est.) | Content-Strategie |
|---|---|---|
| "Kindergeburtstag Spiele [Alter]" | 80.000+ | Landingpages pro Alter (3–12) mit 10 Spielen + CTA zum Wizard |
| "Kindergeburtstag Motto Ideen" | 25.000+ | Motto-Galerie-Seite mit Vorschau + Wizard-Einstieg |
| "Kindergeburtstag planen Checkliste" | 15.000+ | Free Checkliste als PDF-Download → E-Mail-Capture → Upsell |
| "Schnitzeljagd Kindergeburtstag" | 30.000+ | Ausführlicher Guide + CTA auf V2-Feature |
| "Kindergeburtstag Essen Mengen" | 8.000+ | Mengenrechner als eingebettetes Tool → Einstieg in Wizard |
| "Einladung Kindergeburtstag Vorlage" | 20.000+ | Einladungs-Galerie mit Vorschau → Free Download 1, mehr im Pro |

Geschätztes organisches Traffic-Potenzial nach 6 Monaten: **30.000–80.000 Besuche/Monat** (Sistrix Sichtbarkeitsschätzung bei 20+ Landingpages mit Long-Tail-Keywords, basierend auf Vergleichsportalen im Eltern-Segment 2025).

#### 12.4.2 Virales Wachstum über Einladungen

Jede generierte Einladung enthält (im Free-Tier) dezent: "Erstellt mit Geburtstagspilot.de 🎈". Bei WhatsApp-Weiterleitung sehen 8–15 Eltern den Markennamen pro Einladung. Bei 1.000 generierten Einladungen/Monat → 8.000–15.000 Brand-Impressions kostenlos.

#### 12.4.3 Social Media (Instagram + Pinterest)

- **Instagram:** "Motto des Monats" Reels (30 Sek: "So planst du eine Piratenparty in 5 Minuten"). Eltern-UGC: "Zeig uns deine Party!" mit Hashtag #Geburtstagspilot
- **Pinterest:** Pins für jedes Motto (Einladungs-Vorschau, Spielideen-Infografik, Kuchen-Bild). Pinterest ist die Nr.1-Plattform für Kindergeburtstags-Inspiration → natürlicher Fit.

#### 12.4.4 Partnerschaften (ab Monat 3)

- **Eltern-Blogs/Influencer:** Kostenloser Pro-Zugang gegen Review/Erwähnung
- **Partybedarf-Shops:** Affiliate-Partnerschaft (Einkaufsliste → Shop-Links)
- **Kita-/Hort-Verteiler:** "Kostenloser Planer für alle Eltern" als Aushang/Flyer in Kitas

#### 12.4.5 Kennzahlen und Ziele (6-Monats-Plan)

| KPI | Monat 1 | Monat 3 | Monat 6 |
|---|---|---|---|
| Generierte Pläne/Monat | 200 | 2.000 | 8.000 |
| Unique Visitors/Monat | 1.000 | 10.000 | 40.000 |
| Pro-Tier-Käufe/Monat | 10 | 150 | 600 |
| MRR (einmalig → annualisiert) | €50 | €750 | €3.000 |
| SEO-Rankings Top-10 | 3 Keywords | 15 Keywords | 40 Keywords |

---

## Quellenverzeichnis

| Quelle | Inhalt |
|---|---|
| Forsa Familienstudie 2025 | Stressfaktoren bei Familienfeiern, forsa.de |
| Destatis Mikrozensus 2025 | Erwerbstätigkeit beider Elternteile, destatis.de |
| Destatis Bevölkerungsstatistik 2025 | Altersstruktur Kinder 3–12 in DE, destatis.de |
| Statistik Austria. Bevölkerung 2025 | Kinder 3–12 in AT, statistik.at |
| BFS Schweiz. Bevölkerung 2025 | Kinder 3–12 in CH, bfs.admin.ch |
| Statista Consumer Insights. Kindergeburtstage DE 2025 | Durchschnittliche Ausgaben pro Feier, statista.com |
| Bitkom Familien-Digital-Index 2025 | Smartphone-Nutzung von Eltern, bitkom.org |
| Sistrix. Keyword-Analyse Eltern-Segment 2025 | Suchvolumen "Kindergeburtstag" Cluster, sistrix.de |
| Google Trends DACH 2025 | Saisonale Suchtrends "Kindergeburtstag", trends.google.de |
| Spielen-und-Feiern.de Branchenreport 2025 | Feierquoten und Partybedarf-Markt |

---

*Dokument erstellt: 6. Mai 2026 | Version 1.0 | Autor: Daniel Moretz | Status: Zur Freigabe eingereicht*
*Alle Marktdaten basieren auf zum Erstellungszeitpunkt öffentlich verfügbaren Quellen.*

## ./HOWTO.md
# Geburtstagspilot - Setup & Deployment Guide

> 📖 **Lies die [AGENTS.md](AGENTS.md) Datei, um GitHub Copilot optimal und produktiv zu nutzen.**
> **Read the [AGENTS.md](AGENTS.md) file to use GitHub Copilot in an optimised and productive way.**

---

## DE Deutsch

---

### Prozessübersicht

Folge diesen Schritten in der angegebenen Reihenfolge, um vom Template zur Produktion zu gelangen:

1. **GitHub Repo erstellen** - Nutze dieses Template, um ein neues Repository in der Wamocon GitHub Organisation zu erstellen.
2. **Repo klonen** - Klone es auf deinen Rechner und führe `npm install` aus.
3. **Pre-commit Hook installieren** - Führe `bash hooks/install.sh` aus. Einmalig nach dem Klonen - schützt dich davor, Geheimnisse versehentlich zu pushen.
4. **GitHub Workflow-Datei überprüfen** - Öffne `.github/workflows/deploy.yml` und `.github/workflows/pr-pipeline.yml`, überprüfe, dass `Wamocon/github_workflow` die korrekte Referenz ist.
5. **`.env.local` aktualisieren & Supabase verbinden** - Kopiere `.env.example` → `.env.local`, erstelle ein Remote-Supabase-Projekt und trage die Zugangsdaten ein.
6. **Lokal starten & Entwicklung beginnen** - Führe `npm run dev` aus und beginne mit der Entwicklung.
7. **GitHub-Organisationseinstellungen: Vercel-App Zugriff gewähren** - Gehe zu den Organisationseinstellungen auf GitHub, suche die Vercel GitHub-App und gewähre ihr Zugriff auf dein neues Repo. Nur so erscheint das Repo in der Vercel-Importliste.
8. **Repo vorübergehend öffentlich machen & bei Vercel importieren** - Stelle das Repo temporär auf öffentlich und importiere es in Vercel.
9. **Vercel Project ID holen** - Kopiere die Vercel Project ID aus den Vercel-Projekteinstellungen.
10. **Vercel Project ID zu GitHub Secrets hinzufügen** - Füge `VERCEL_PROJECT_ID` zu den GitHub Actions Secrets deines Repos hinzu.
11. **Repo auf intern umstellen** - Ändere die Sichtbarkeit des Repos zurück auf intern.
12. **Erstes manuelles Deployment** - Gehe zu `Actions → "Deploy to Vercel" → Run workflow` und wähle `production`.

> 📖 **Für detaillierte Informationen, lies weiter unten.**

---

### 1. Klonen & Einrichten

```bash
# Repository klonen
git clone https://github.com/Wamocon/<dein-repo-name>.git
cd <dein-repo-name>

# Abhängigkeiten installieren
npm install

# Umgebungsvariablen kopieren
cp .env.example .env.local

# Pre-commit Hook installieren (einmalig, direkt nach npm install)
bash hooks/install.sh

# Entwicklungsserver starten (mit Turbopack für schnelles Hot-Reload)
npm run dev
```

Öffne [http://localhost:3000](http://localhost:3000) in deinem Browser.

**Verfügbare Skripte:**

| Befehl | Beschreibung |
|---|---|
| `npm run dev` | Startet den Dev-Server mit Turbopack (Hot Reload) |
| `npm run build` | Erstellt den Produktions-Build |
| `npm run start` | Startet den Produktionsserver |
| `npm run lint` | Führt ESLint aus |
| `npm run typecheck` | Führt TypeScript-Typprüfung aus |

---

### 1b. Git-Workflow & Branch-Strategie

> 💡 **Arbeite nach dem ersten Push immer auf einem Branch - nie direkt auf `main`/`master`.**

**Empfohlener Ablauf:**

```bash
# Einmalig: Ersten Stand auf main/master pushen
git add .
git commit -m "chore: initial setup"
git push origin <main-oder-master>

# Ab jetzt: Immer auf einem Feature-Branch arbeiten
git checkout -b feature/mein-feature

# Änderungen lokal testen, dann committen
npm run dev        # testen
npm run typecheck  # Typfehler prüfen
npm run lint       # Lint prüfen

git add .
git commit -m "feat: beschreibung der Änderung"
git push origin feature/mein-feature
```

**Wichtige Regeln:**

- **Lokal testen, bevor du pushst.** Führe `npm run typecheck` und `npm run lint` aus, bevor du Änderungen pushst.
- **Alle Änderungen vor dem PR-Öffnen pushen.** Jeder neue Push auf einen offenen PR triggert automatisch die GitHub Actions - das verbraucht GitHub Actions-Minuten.
- **Nur einen PR auf einmal offen halten**, bis er gemergt ist.

> ⚠️ **Warum das wichtig ist:** Jeder Push auf einen offenen PR löst die PR Pipeline aus (Auto-Fix + Typecheck + Lint). Teste erst lokal - dann push, dann PR.

---

### 1c. Pre-commit Hook - Geheimnis-Scanner

Der Pre-commit Hook verhindert, dass API-Schlüssel, Tokens, Passwörter oder andere Geheimnisse versehentlich in GitHub eingecheckt werden. Der Hook scannt alle für den Commit vorgesehenen Dateien, **bevor** der Commit abgeschlossen wird.

#### Installation

```bash
# Einmalig nach dem Klonen ausführen - nie wieder nötig:
bash hooks/install.sh
```

> ✅ **Wie oft?** Genau **einmal** - direkt nach `npm install` beim ersten Einrichten des Repos. Nach der Installation läuft der Hook automatisch vor **jedem** `git commit`.

#### Was der Hook prüft

| Muster | Beispiel |
|--------|---------|
| AWS-Schlüssel | `AKIA...`, `aws_secret_access_key = ...` |
| GitHub-Tokens | `ghp_...`, `github_pat_...` |
| Vercel-Token | `VERCEL_TOKEN = abc123...` |
| Private Keys (PEM) | `-----BEGIN PRIVATE KEY-----` |
| Datenbankverbindungen | `postgres://user:password@host` |
| Generische Tokens | `api_key =`, `client_secret =`, `password =` |
| JWT-Tokens | `eyJ...` (vollständige `header.payload.signature`-Form) |
| Supabase Service Role | `service_role = eyJ...` |
| `.env`-Dateien | `.env`, `.env.local`, `.env.production` |

#### Wenn ein Commit blockiert wird

```
[pre-commit] BLOCKED - potential secrets detected
  ✖ src/lib/config.ts:12
    Reason: Generic API key
    Content: const API_KEY = "abc123xyz789..."
```

**Lösung:**
1. Entferne das Geheimnis aus der Datei.
2. Speichere es in deiner `.env.local` (ist bereits in `.gitignore` eingetragen).
3. Nutze GitHub Actions Secrets für CI/CD-Werte.

**Bei einem Falsch-Positiv** (z.B. ein Beispielwert in der Doku):
Füge den Kommentar `# notsecret` am Ende der betroffenen Zeile hinzu.

**Notfall-Bypass** (nur im absoluten Ausnahmefall - niemals für echte Geheimnisse!):
```bash
git commit --no-verify -m "deine Nachricht"
```

---

### 2. Supabase Setup & Warnung

> ⚠️ **KRITISCH: Sobald du einen Supabase-Account hast, speichere alle Testdaten direkt dort.**
>
> **Lege Testdaten NICHT als lokale Dateien im Projektverzeichnis ab** (z.B. JSON-Fixtures, SQL-Dumps). Füge Daten stattdessen direkt in dein Supabase-Projekt ein - über das Dashboard, per MCP-Tool oder per Migrations-Skript.

**Schritte:**

1. Gehe zu [supabase.com](https://supabase.com) und erstelle ein neues Projekt.
2. Kopiere die **Project URL**, den **Anon Key** und den **Service Role Key** aus  
   `Project Settings → API`.
3. Trage sie in deine `.env.local` Datei ein:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=dein-anon-key
   SUPABASE_SERVICE_ROLE_KEY=dein-service-role-key
   ```

---

### 2b. Lokales Supabase Setup via Docker (Optional)

> 💡 **Dieser Schritt ist optional.** Standardmäßig verbindest du dich direkt mit einem Remote-Supabase-Projekt (siehe Abschnitt 2). Nur wenn du lieber vollständig lokal entwickelst, ohne Internetverbindung zu Supabase, verwende dieses Setup.

Für ein vollständig lokales Supabase-Setup mit Docker und einer migrations-basierten Entwicklung, kopiere diesen Prompt in deinen KI-Assistenten (z.B. GitHub Copilot in VS Code):

```
Act as an expert DevOps and database engineer. I am developing an app locally. I need to set up a local Supabase instance via Docker and establish a strict migration-based workflow. Please execute the following:

Setup: Initialize a local Supabase environment using Docker and the Supabase CLI. Check automatically before every task if Docker and the Supabase containers are running. When they are down, start them autonomously.

Initial Schema: Create the initial database schema for the app and save it as a formal Supabase migration file.

Environment Variables: Automatically extract the local Supabase connection details (API URL, anon key, service role key, DB URL) and append them to my local .env file.

Autonomous Development & Schema Versioning: You will develop the entire application based on my prompts. You must autonomously create and update tables, generate schemas, and create timestamped migration files for every change. Ensure strict version history and guarantee that absolutely no functions fail due to database inconsistencies.

Production Deployment via MCP: I use the Supabase MCP to push data to production tables. Do not provide manual push commands. Your only job for production is to verify that all local migrations are completely up to date and error-free so the MCP can handle the live deployment seamlessly.

Automated Testing & Verification: Once the Docker setup is running and the schema is applied, automatically write and execute a small integration test. This test must verify that the app can successfully read from and write to the local Docker database. If any errors or bugs are detected, diagnose and fix them immediately on your own.
```

#### Lokale Supabase-Oberfläche im Browser öffnen

Sobald der lokale Docker-Stack läuft (`npx supabase start`), stellt Supabase eine vollständige Studio-Oberfläche bereit:

| Service | URL | Beschreibung |
|---|---|---|
| **Supabase Studio** | `http://localhost:54323` | Datenbank-UI: Tabellen, SQL-Editor, Auth, Storage |
| **REST API** | `http://localhost:54321` | PostgREST API (dein App-Endpoint) |
| **PostgreSQL** | `localhost:54322` | Direktzugriff (z.B. via pgAdmin, TablePlus) |
| **Inbucket (E-Mail)** | `http://localhost:54324` | Lokaler E-Mail-Dienst für Auth-Mails |

> 💡 Die exakten Ports werden nach `npx supabase start` auch in der Konsole ausgegeben. Der Befehl `npx supabase status` zeigt sie jederzeit an.

**Lokale Umgebungsvariablen:**
```
NEXT_PUBLIC_SUPABASE_URL=http://localhost:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=<aus supabase status kopieren>
SUPABASE_SERVICE_ROLE_KEY=<aus supabase status kopieren>
SUPABASE_DB_URL=postgresql://postgres:postgres@localhost:54322/postgres
```

---

### 3. Supabase MCP & Schemas

#### Supabase MCP für Migrationen verwenden

Der Supabase MCP (Model Context Protocol) Server ermöglicht es deinem KI-Coding-Assistenten (z.B. GitHub Copilot, Cursor), Migrationen und Tabellen direkt zu erstellen und zu verwalten.

- Migrationen werden in `supabase/migrations/` gespeichert.
- Nutze die MCP-Tools, um Tabellen zu erstellen, Schemas zu ändern und Indizes zu verwalten.

#### Arbeiten mit mehreren Schemas

Standardmäßig macht Supabase nur das `public`-Schema über die API verfügbar. Wenn du eigene Schemas brauchst:

**1. Schema erstellen:**
```sql
CREATE SCHEMA IF NOT EXISTS app;
```

**2. Berechtigungen vergeben:**
```sql
GRANT USAGE ON SCHEMA app TO anon, authenticated, service_role;
GRANT ALL ON ALL TABLES IN SCHEMA app TO anon, authenticated, service_role;
ALTER DEFAULT PRIVILEGES IN SCHEMA app
  GRANT ALL ON TABLES TO anon, authenticated, service_role;
GRANT ALL ON ALL SEQUENCES IN SCHEMA app TO anon, authenticated, service_role;
ALTER DEFAULT PRIVILEGES IN SCHEMA app
  GRANT ALL ON SEQUENCES TO anon, authenticated, service_role;
```

**3. Schema über die Supabase API zugänglich machen:**
Gehe zu `Project Settings → API → Exposed schemas` und füge deinen Schema-Namen hinzu.

---

### 4. GitHub Workflow Konfiguration

Dieses Projekt nutzt den **zentralen Wamocon CI/CD-Workflow** aus [`Wamocon/github_workflow`](https://github.com/Wamocon/github_workflow).

#### Übersicht der drei Workflows

| Workflow | Datei | Auslöser | Was es tut |
|---|---|---|---|
| **PR Pipeline** | `pr-pipeline.yml` | **Automatisch** bei jedem PR auf `main`/`master` | Auto-Fix (ESLint + Prettier) → Typecheck + Lint |
| **Deploy** | `deploy.yml` | **Manuell** - kein Auto-Trigger | Baut das Projekt via Vercel CLI und deployed auf Vercel |
| **LP Generator** | `lp-generator.yml` | **Manuell** - kein Auto-Trigger | Generiert eine Landing Page in einem neuen Repo |

> ⚠️ **Kein automatisches Deployment:** Weder ein PR noch ein Push auf `main` startet automatisch ein Deployment. Alle Deployments werden manuell über den Actions-Tab gestartet.

#### Was du tun musst

1. Überprüfe, dass `Wamocon/github_workflow` die korrekte Org/Repo-Referenz ist.
2. Aktiviere Workflow-Schreibrechte:  
   `Settings → Actions → General → Workflow permissions → Allow GitHub Actions to create and approve pull requests`
3. Füge **ein einziges Secret** zu deinem Repository hinzu:
   - Gehe zu `Repository → Settings → Secrets and variables → Actions → New repository secret`
   - Name: `VERCEL_PROJECT_ID`
   - Wert: *(siehe Abschnitt 5 unten)*

> ✅ **Alle anderen benötigten Secrets** (`VERCEL_TOKEN`, `VERCEL_ORG_ID`) sind **bereits auf GitHub-Organisationsebene konfiguriert**.

#### Manuelles Deployment starten

```
Repository auf GitHub → Actions → "Deploy to Vercel" → Run workflow
→ Environment auswählen: production oder preview
→ Run workflow klicken
```

---

### 5. Vercel Deployment-Strategie

#### Schritt 1: GitHub-Org Vercel-App Zugriff gewähren (Einmalig, Kritisch)

> ⚠️ **Dieser Schritt muss VOR dem Vercel-Import durchgeführt werden.** Ohne ihn erscheint dein Repo nicht in der Vercel-Importliste - auch wenn es öffentlich ist.

1. Gehe zu **GitHub → Wamocon Organisation → Settings**  
   `https://github.com/organizations/Wamocon/settings/installations`
2. Suche die **Vercel**-App in der Liste der installierten GitHub Apps.
3. Klicke auf **Configure**.
4. Scrolle zu **Repository access**.
5. Wähle **"Only select repositories"** und füge dein neues Repo hinzu.
6. Klicke **Save**.

#### Schritt 2: Erstmalige Bereitstellung (Einmalig)

1. **Repo vorübergehend öffentlich machen**  
   `Repository → Settings → General → Change visibility → Public`
2. Gehe zu [vercel.com](https://vercel.com) → **Add New Project** → **Import** → dein Repo auswählen.
3. Deploye das Projekt (Vercel erkennt Next.js automatisch).
4. **Vercel Project ID kopieren:**  
   `Vercel Project → Settings → General → Project ID` → ID kopieren.
5. **Zu GitHub Secrets hinzufügen:**  
   `Repository → Settings → Secrets and variables → Actions → New repository secret`  
   Name: `VERCEL_PROJECT_ID` | Wert: die kopierte ID.
6. **Repo auf intern zurücksetzen:**  
   `Repository → Settings → General → Change visibility → Internal`

> 💡 **Nach diesem einmaligen Setup** deployt die GitHub Action via Vercel CLI - Vercel sieht nicht mehr, wer committed, und es gibt keine Team-Seat-Fehler bei einem privaten Hobby-Account.

#### Schritt 3: Umgebungsvariablen in Vercel eintragen

> ⚠️ **WICHTIG:** Gehe zu `Vercel Project → Settings → Environment Variables` und füge **alle** Variablen aus deiner `.env.local` hinzu. Ohne diese wird der Build **fehlschlagen**.

#### Deployment-Ablauf (nach dem Setup)

| Auslöser | Ergebnis |
|---|---|
| PR auf `main`/`master` | PR Pipeline läuft automatisch (kein Deployment) |
| Merge auf `main`/`master` | Kein automatisches Deployment |
| **Manuelles Workflow-Start** | Deployment nach Auswahl: `production` oder `preview` |

**Manuell deployen:**

```
GitHub → Actions → "Deploy to Vercel" → Run workflow
→ environment: production  (für die Live-URL)
→ environment: preview     (für eine Test-URL)
→ db_schema: (leer lassen - Vercel-Umgebungsvariablen werden genutzt)
```

---

### 6. Domain-Verwaltung

1. **Sichere eine Domain** für deine Anwendung über [Strato](https://www.strato.de).
2. Gehe in den Vercel-Projekteinstellungen zu `Settings → Domains` und füge deine Domain hinzu.
3. Konfiguriere die DNS-Einträge bei Strato wie von Vercel angegeben (typischerweise CNAME oder A-Record).

---

### 7. Projekt-Checkliste

- [ ] Landing Page
- [ ] Handbuch / Manual
- [ ] Hauptprozess (Kernfunktion)
- [ ] Video (Demo / Tutorial)
- [ ] Domain (über Strato gesichert)

---

### 8. Landing Page Generator

Das Workflow-File `.github/workflows/lp-generator.yml` generiert eine Landing Page für diese App.

#### Was der Workflow tut

- Liest den Inhalt dieses Repos aus
- Verwendet ein konfigurierbares **Design-Template** als optische Basis
- Lässt GitHub Copilot eine Landing Page generieren und ein neues Repo dafür anlegen

#### Was du ändern kannst

| Eingabe | Standard | Beschreibung |
|---|---|---|
| `custom_template` | `Wamocon/hochzeitsrechner_lp` | Das GitHub-Repo, das als Design-Template dient |
| `custom_name` | `generated_lp` | Name des neu erstellten Landing-Page-Repos |
| `custom_prompt` | *(allgemeiner Prompt)* | Detaillierte Anweisungen für Copilot |

> 💡 **Tipp:** Je spezifischer dein Prompt, desto besser die generierte Landing Page.

#### Wann du den Workflow starten sollst

Starte diesen Workflow **erst dann**, wenn dein Projekt weitgehend fertig dokumentiert ist:
- Handbuch / Manual
- README mit Produktbeschreibung, Features und Zielgruppe
- Rechtstexte / relevante Seiten

> ✅ **Empfehlung:** In der Regel reicht **ein einmaliger Lauf** am Projektende.

#### Manuell ausführen

`Repository → Actions → "🚀 lp-generator" → Run workflow`

1. Wähle in der linken Liste den Workflow **"🚀 lp-generator"**.
2. Klicke rechts auf **"Run workflow"**.
3. Passe Template, Name und Prompt an.
4. Bestätige mit **"Run workflow"**.

#### Wenn der Workflow fehlschlägt

Wenn bereits ein Repository mit gleichem Namen existiert:
1. Ändere den Namen in `custom_name` und starte erneut.
2. Oder lösche das bestehende Ziel-Repo und starte erneut.

---
---

## EN English

---

### Process Overview

Follow these steps in order to go from template to production:

1. **Create GitHub Repo** - Use this template to create a new repository in the Wamocon GitHub organisation.
2. **Clone Repo** - Clone to your local machine and run `npm install`.
3. **Install pre-commit hook** - Run `bash hooks/install.sh`. One-time setup after cloning - protects you from accidentally pushing secrets.
4. **Check GitHub Workflow files** - Open `.github/workflows/deploy.yml` and `.github/workflows/pr-pipeline.yml`, verify that `Wamocon/github_workflow` is the correct reference.
5. **Update `.env.local` & connect Supabase** - Copy `.env.example` → `.env.local`, create a remote Supabase project, and fill in the credentials.
6. **Run locally & start development** - Run `npm run dev` and start building.
7. **GitHub Organisation Settings: Grant Vercel app access** - Go to the organisation settings on GitHub, find the Vercel GitHub App, and grant it access to your new repo. Without this, the repo will not appear in Vercel's import list.
8. **Make repo temporarily public & import in Vercel** - Set the repo to public temporarily and import it in Vercel.
9. **Get Vercel Project ID** - Copy the Vercel Project ID from the Vercel project settings.
10. **Add Vercel Project ID to GitHub secrets** - Add `VERCEL_PROJECT_ID` to your repository's GitHub Actions secrets.
11. **Make repo internal** - Revert the repository visibility to internal.
12. **First manual deployment** - Go to `Actions → "Deploy to Vercel" → Run workflow` and choose `production`.

> 📖 **For detailed information, read below.**

---

### 1. Clone & Setup

```bash
# Clone the repository
git clone https://github.com/Wamocon/<your-repo-name>.git
cd <your-repo-name>

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env.local

# Install pre-commit hook (once, right after npm install)
bash hooks/install.sh

# Start the development server (with Turbopack for fast refresh)
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

**Available scripts:**

| Command | Description |
|---|---|
| `npm run dev` | Start dev server with Turbopack (hot reload) |
| `npm run build` | Create production build |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run typecheck` | Run TypeScript type checking |

---

### 1b. Git Workflow & Branching Strategy

> 💡 **After the first push, always work on a branch - never directly on `main`/`master`.**

**Recommended flow:**

```bash
# One-time: push the initial state to main/master
git add .
git commit -m "chore: initial setup"
git push origin <main-or-master>

# From now on: always work on a feature branch
git checkout -b feature/my-feature

# Test locally, then commit
npm run dev        # test in browser
npm run typecheck  # catch type errors
npm run lint       # catch lint issues

git add .
git commit -m "feat: description of change"
git push origin feature/my-feature
```

**Key rules:**

- **Test locally before pushing.** Always run `npm run typecheck` and `npm run lint` before pushing.
- **Push all changes before opening the PR.** Every new push to an open PR triggers the GitHub Actions pipeline - this consumes GitHub Actions minutes.
- **Keep only one PR open at a time** until it is merged.

> ⚠️ **Why this matters:** Every push to an open PR triggers the PR Pipeline (Auto-Fix + Typecheck + Lint). Test locally first - then push, then open the PR.

---

### 1c. Pre-commit Hook - Secret Scanner

The pre-commit hook prevents API keys, tokens, passwords, or other secrets from accidentally being checked into GitHub. The hook scans all files staged for commit **before** the commit is finalised.

#### Installation

```bash
# Run ONCE after cloning - never needs to run again:
bash hooks/install.sh
```

> ✅ **How often?** Exactly **once** - right after `npm install` when first setting up the repo. After installation, the hook runs automatically before **every** `git commit`.

#### What the hook checks

| Pattern | Example |
|--------|---------|
| AWS keys | `AKIA...`, `aws_secret_access_key = ...` |
| GitHub tokens | `ghp_...`, `github_pat_...` |
| Vercel token | `VERCEL_TOKEN = abc123...` |
| Private keys (PEM) | `-----BEGIN PRIVATE KEY-----` |
| Database connection strings | `postgres://user:password@host` |
| Generic tokens | `api_key =`, `client_secret =`, `password =` |
| JWT tokens | `eyJ...` (full `header.payload.signature` form) |
| Supabase service role | `service_role = eyJ...` |
| `.env` files | `.env`, `.env.local`, `.env.production` |

#### When a commit is blocked

```
[pre-commit] BLOCKED - potential secrets detected
  ✖ src/lib/config.ts:12
    Reason: Generic API key
    Content: const API_KEY = "abc123xyz789..."
```

**How to fix:**
1. Remove the secret from the file.
2. Store it in your `.env.local` (already in `.gitignore`).
3. Use GitHub Actions secrets for CI/CD values.

**False positive** (e.g. an example value in documentation):  
Add the comment `# notsecret` at the end of that line.

**Emergency bypass** (absolute last resort - never for real secrets!):
```bash
git commit --no-verify -m "your message"
```

---

### 2. Supabase Setup & Warning

> ⚠️ **CRITICAL: Once you have a Supabase account, store all test data there directly.**
>
> **Do NOT store test data as local files** (e.g. JSON fixtures, SQL dumps). Insert data directly into your Supabase project - via the Dashboard, an MCP tool, or a migration script.

**Steps:**

1. Go to [supabase.com](https://supabase.com) and create a new project.
2. Copy the **Project URL**, **Anon Key**, and **Service Role Key** from  
   `Project Settings → API`.
3. Paste them into your `.env.local` file:
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   ```

---

### 2b. Local Supabase Setup via Docker (Optional)

> 💡 **This step is optional.** By default you connect directly to a remote Supabase project (see section 2). Only use this setup if you prefer developing fully offline.

For a fully local Supabase setup with Docker and a migration-based development workflow, copy this prompt into your AI assistant (e.g. GitHub Copilot in VS Code):

```
Act as an expert DevOps and database engineer. I am developing an app locally. I need to set up a local Supabase instance via Docker and establish a strict migration-based workflow. Please execute the following:

Setup: Initialize a local Supabase environment using Docker and the Supabase CLI. Check automatically before every task if Docker and the Supabase containers are running. When they are down, start them autonomously.

Initial Schema: Create the initial database schema for the app and save it as a formal Supabase migration file.

Environment Variables: Automatically extract the local Supabase connection details (API URL, anon key, service role key, DB URL) and append them to my local .env file.

Autonomous Development & Schema Versioning: You will develop the entire application based on my prompts. You must autonomously create and update tables, generate schemas, and create timestamped migration files for every change. Ensure strict version history and guarantee that absolutely no functions fail due to database inconsistencies.

Production Deployment via MCP: I use the Supabase MCP to push data to production tables. Do not provide manual push commands. Your only job for production is to verify that all local migrations are completely up to date and error-free so the MCP can handle the live deployment seamlessly.

Automated Testing & Verification: Once the Docker setup is running and the schema is applied, automatically write and execute a small integration test. This test must verify that the app can successfully read from and write to the local Docker database. If any errors or bugs are detected, diagnose and fix them immediately on your own.
```

#### Viewing the local database in the browser

| Service | URL | Description |
|---|---|---|
| **Supabase Studio** | `http://localhost:54323` | Database UI: tables, SQL editor, Auth, Storage |
| **REST API** | `http://localhost:54321` | PostgREST API (your app endpoint) |
| **PostgreSQL** | `localhost:54322` | Direct DB access (e.g. pgAdmin, TablePlus) |
| **Inbucket (email)** | `http://localhost:54324` | Local email service for Auth emails |

**Local environment variables:**
```
NEXT_PUBLIC_SUPABASE_URL=http://localhost:54321
NEXT_PUBLIC_SUPABASE_ANON_KEY=<copy from supabase status output>
SUPABASE_SERVICE_ROLE_KEY=<copy from supabase status output>
SUPABASE_DB_URL=postgresql://postgres:postgres@localhost:54322/postgres
```

---

### 3. Supabase MCP & Schemas

#### Using Supabase MCP for Migrations

The Supabase MCP (Model Context Protocol) server allows your AI coding assistant to create and manage migrations and tables directly.

- Migrations are stored in `supabase/migrations/`.
- Use the MCP tools to create tables, alter schemas, and manage indexes.

#### Working with Multiple Schemas

By default, Supabase only exposes the `public` schema via the API. If you need custom schemas:

**1. Create the schema:**
```sql
CREATE SCHEMA IF NOT EXISTS app;
```

**2. Grant permissions:**
```sql
GRANT USAGE ON SCHEMA app TO anon, authenticated, service_role;
GRANT ALL ON ALL TABLES IN SCHEMA app TO anon, authenticated, service_role;
ALTER DEFAULT PRIVILEGES IN SCHEMA app
  GRANT ALL ON TABLES TO anon, authenticated, service_role;
GRANT ALL ON ALL SEQUENCES IN SCHEMA app TO anon, authenticated, service_role;
ALTER DEFAULT PRIVILEGES IN SCHEMA app
  GRANT ALL ON SEQUENCES TO anon, authenticated, service_role;
```

**3. Expose the schema via the Supabase API:**
Go to `Project Settings → API → Exposed schemas` and add your custom schema name.

---

### 4. GitHub Workflow Configuration

This project uses the **centralized Wamocon CI/CD workflow** from [`Wamocon/github_workflow`](https://github.com/Wamocon/github_workflow).

#### Overview of the three workflows

| Workflow | File | Trigger | What it does |
|---|---|---|---|
| **PR Pipeline** | `pr-pipeline.yml` | **Automatic** on every PR to `main`/`master` | Auto-Fix (ESLint + Prettier) → Typecheck + Lint |
| **Deploy** | `deploy.yml` | **Manual only** - no auto-trigger | Builds and deploys to Vercel via CLI |
| **LP Generator** | `lp-generator.yml` | **Manual only** - no auto-trigger | Generates a landing page in a new repo |

> ⚠️ **No automatic deployment:** Neither a PR nor a push to `main` triggers a deployment automatically. All deployments are started manually from the Actions tab.

#### What you need to do

1. Verify that `Wamocon/github_workflow` is the correct org/repo reference.
2. Enable workflow write permissions:  
   `Settings → Actions → General → Workflow permissions → Allow GitHub Actions to create and approve pull requests`
3. Add **one single secret** to your repository:
   - Go to `Repository → Settings → Secrets and variables → Actions → New repository secret`
   - Name: `VERCEL_PROJECT_ID`
   - Value: *(see section 5 below)*

> ✅ **All other required secrets** (`VERCEL_TOKEN`, `VERCEL_ORG_ID`) are **already configured at the GitHub Organisation level**.

#### Triggering a manual deployment

```
GitHub repo → Actions → "Deploy to Vercel" → Run workflow
→ Choose environment: production or preview
→ Click "Run workflow"
```

---

### 5. Vercel Deployment Strategy

#### Step 1: Grant Vercel GitHub App access in Org Settings (One-time, Critical)

> ⚠️ **This step must be done BEFORE importing in Vercel.** Without it, your repo will not appear in Vercel's import list - even if it is public.

1. Go to **GitHub → Wamocon Organisation → Settings → Installed GitHub Apps**  
   `https://github.com/organizations/Wamocon/settings/installations`
2. Find the **Vercel** app in the list.
3. Click **Configure**.
4. Scroll to **Repository access**.
5. Select **"Only select repositories"** and add your new repo.
6. Click **Save**.

#### Step 2: Initial Deployment (One-Time)

1. **Make the repo public** temporarily  
   `Repository → Settings → General → Change visibility → Public`
2. Go to [vercel.com](https://vercel.com) → **Add New Project** → **Import** → select your repo.
3. Deploy the project (Vercel detects Next.js automatically).
4. **Copy the Vercel Project ID:**  
   `Vercel Project → Settings → General → Project ID` → copy the value.
5. **Add to GitHub secrets:**  
   `Repository → Settings → Secrets and variables → Actions → New repository secret`  
   Name: `VERCEL_PROJECT_ID` | Value: the ID you copied.
6. **Revert the repo to internal:**  
   `Repository → Settings → General → Change visibility → Internal`

> 💡 **After this one-time setup**, the GitHub Action deploys via Vercel CLI - Vercel no longer sees who committed, and there are no team seat errors with a personal Hobby account.

#### Step 3: Add environment variables in Vercel

> ⚠️ **CRUCIAL:** Go to `Vercel Project → Settings → Environment Variables` and add **all** variables from your `.env.local`. Without these, the build **will fail**.

#### Deployment flow (after setup)

| Trigger | Result |
|---|---|
| PR targeting `main`/`master` | PR Pipeline runs automatically (no deployment) |
| Merge / push to `main`/`master` | No automatic deployment |
| **Manual workflow run** | Deploys to the chosen environment: `production` or `preview` |

**How to deploy manually:**

```
GitHub → Actions → "Deploy to Vercel" → Run workflow
→ environment: production  (for the live URL)
→ environment: preview     (for a temporary test URL)
→ db_schema: (leave empty - Vercel env vars are used)
```

---

### 6. Domain Management

1. **Secure a domain** for your application via [Strato](https://www.strato.de).
2. In the Vercel project settings, go to `Settings → Domains` and add your domain.
3. Configure the DNS records at Strato as shown by Vercel (typically a CNAME or A record).

---

### 7. Project Checklist

- [ ] Landing Page
- [ ] Handbuch / Manual
- [ ] Main Process (core feature)
- [ ] Video (demo / tutorial)
- [ ] Domain (secured via Strato)

---

### 8. Landing Page Generator

The workflow file `.github/workflows/lp-generator.yml` generates a landing page for this app by calling a central, reusable Wamocon workflow.

#### What the workflow does

- Reads the contents of this repository
- Uses a configurable **design template** as a visual base
- Lets GitHub Copilot generate a landing page and create a new repository for it

#### What you can change

| Input | Default | Description |
|---|---|---|
| `custom_template` | `Wamocon/hochzeitsrechner_lp` | The GitHub repo used as the design template |
| `custom_name` | `generated_lp` | Name for the newly created landing page repository |
| `custom_prompt` | *(generic prompt)* | Detailed instructions for Copilot |

> 💡 **Tip:** The more specific your prompt, the better the generated landing page.

#### When you should run this workflow

Run this workflow **only after** your project is mostly complete:
- Handbook / Manual
- README with product description, features, and target audience
- Legal pages / relevant links

> ✅ **Recommendation:** In most cases, you only need to run it **once** at the end of the project.

#### Running manually

`Repository → Actions → "🚀 lp-generator" → Run workflow`

1. Select **"🚀 lp-generator"** from the left workflow list.
2. Click **"Run workflow"** on the right.
3. Adjust the input fields (template, name, prompt) as needed.
4. Confirm with **"Run workflow"**.

#### If the workflow fails (repository name already exists)

1. Change the `custom_name` value and run the workflow again.
2. Or delete the existing target repository (if no longer needed) and run again.

## ./IDEA.md
# Projektidee

> Diese Datei beschreibt die Kernidee des Projekts Geburtstagspilot.

---

## Projektname

Geburtstagspilot

---

## Beschreibung

Eine browserbasierte Web-App, die Eltern in unter 5 Minuten einen kompletten
Kindergeburtstag plant: Zeitablauf, Spiele mit Anleitung, Kuchen- und Essensideen,
Einkaufsliste, Einladung und Mitgebsel. Kein Account noetig fuer die Basisnutzung,
sofort Ergebnis. Das Produkt loest ein universelles Elternproblem: die jaehrliche
Stress-Planung eines Kindergeburtstags. Bisher fragmentiert ueber Pinterest,
Mama-Blogs, WhatsApp-Gruppen und improvisierte Listen.

---

## Zielgruppe

Eltern mit Kindern im Alter von 3 bis 12 Jahren im DACH-Raum. Primaer Muetter
und Vaeter, die berufstaetig sind und wenig Zeit fuer die Planung haben.
Sekundaer: Grosseltern, Tanten/Onkel, Tagespflege-Einrichtungen.

---

## Kernproblem

Jedes Jahr, jedes Kind, derselbe Stress: Welches Motto? Welche Spiele passen
zum Alter? Wie viele Wuerstchen fuer 12 Kinder? Was kommt in die Mitgebsel-Tueten?
Bestehende Angebote sind fragmentiert und nicht interaktiv. Es gibt kein Tool,
das den gesamten Planungs-Workflow aus einem Guss liefert.

---

## Gewuenschte Hauptfunktionen (Version 1)

- 7-Schritt Party-Wizard (Alter, Gaeste, Ort, Motto, Dauer, Allergien, Budget)
- Automatischer Zeitablauf mit Minutenplan
- 80+ altersgerechte Spiele mit Anleitung und Material
- Kuchen-Rezepte und Essensvorschlaege mit Mengenberechnung
- Automatische Einkaufsliste nach Kategorien
- Einladungs-Generator mit Themenvorlagen
- Mitgebsel-Ideen nach Budget-Stufen
- Gaesteliste-Verwaltung
- Benutzerkonten mit Free/Pro Modell
- KI-Features (Chat, Spielgenerierung, Einladungstexte)
- Admin-Dashboard

---

## Tech-Stack

Next.js 16, React 19, TypeScript, Supabase, Tailwind CSS v4, Vercel, next-intl, OpenAI

---

## Marktsegment und Branche

Kindergeburtstags-Planungstools, Eltern-SaaS, Family-Tech im DACH-Raum

---

## Bekannte Wettbewerber

- Mama-Blogs (nicht interaktiv)
- Pinterest-Boards (unstrukturiert)
- Einzelne Spiele-Sammlungen ohne Planungsfunktion
- Kein dominanter Anbieter in DACH

---

## Ersteller

Daniel Moretz

---

## Empfaenger (Geschaeftsfuehrung)

Waleri Moretz, CEO WAMOCON GmbH

---

## Welle und Version

10

---

## Zusaetzliche Hinweise (optional)

[Besondere Anforderungen, Einschraenkungen, Deadlines oder andere relevante
Informationen, die im Dokument beruecksichtigt werden sollen.]

## ./docs/IMPLEMENTATION_CONCEPT.md
# Geburtstagspilot - Implementation Concept: Roles, Permissions & Persistence

## 1. Overview

Transform Geburtstagspilot from a stateless one-time browser tool into a persistent SaaS application with user accounts, saved plans, role-based access control, and a free/pro tier model.

---

## 2. Roles & Permissions

### 2.1 Role Model

| Role | Description | Capabilities |
|------|------------|--------------|
| **anonymous** | Unauthenticated visitor | Create plans (sessionStorage), view homepage, use wizard |
| **user (free)** | Registered user, free tier | Save up to 3 plans, view/edit own plans, basic features |
| **user (pro)** | Registered user, pro subscription | Unlimited plans, AI enhancements, PDF export, sharing links, priority support |
| **admin** | Platform administrator | Manage users, plans, roles, content (themes/games/recipes), view analytics |

### 2.2 Permission Matrix

| Action | Anonymous | Free User | Pro User | Admin |
|--------|-----------|-----------|----------|-------|
| Use wizard | Yes | Yes | Yes | Yes |
| Save plan | No | 3 max | Unlimited | Unlimited |
| Load saved plans | No | Yes | Yes | Yes (all) |
| PDF export | No | No | Yes | Yes |
| Share link (persistent) | No | No | Yes | Yes |
| AI enhancements | No | No | Yes | Yes |
| Manage own profile | No | Yes | Yes | Yes |
| Admin dashboard | No | No | No | Yes |
| Manage users | No | No | No | Yes |
| Manage content | No | No | No | Yes |

---

## 3. Free vs. Pro Model

### 3.1 Free Tier
- Account creation (optional)
- Save up to 3 plans
- Basic plan generation (wizard)
- Session-based usage without account

### 3.2 Pro Tier (future: subscription)
- Unlimited plan saving
- AI-powered enhancements (theme suggestions, personalized games)
- PDF export with branding
- Persistent shareable links
- Priority support
- Custom themes (future)

### 3.3 Pricing Model (prepared, not yet active)
- Free: 0 EUR/month
- Pro: 4.99 EUR/month or 39.99 EUR/year
- Implementation: `user_tier` column in profiles table, checked via RLS and middleware

---

## 4. Database Schema (New Tables)

### 4.1 profiles
Extends Supabase auth.users with app-specific data.

```sql
CREATE TABLE public.profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  email TEXT NOT NULL,
  display_name TEXT,
  role TEXT NOT NULL DEFAULT 'user' CHECK (role IN ('user', 'admin')),
  tier TEXT NOT NULL DEFAULT 'free' CHECK (tier IN ('free', 'pro')),
  plan_count INT NOT NULL DEFAULT 0,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

### 4.2 saved_plans
Stores user party plans persistently.

```sql
CREATE TABLE public.saved_plans (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  wizard_data JSONB NOT NULL,
  plan_data JSONB NOT NULL,
  is_shared BOOLEAN NOT NULL DEFAULT false,
  share_token TEXT UNIQUE,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

### 4.3 RLS Policies
- profiles: Users can read/update their own profile. Admins can read/update all.
- saved_plans: Users can CRUD their own plans. Admins can read all. Shared plans readable by anyone via share_token.

---

## 5. Authentication Flow

1. Supabase Auth with email/password
2. Profile auto-created via database trigger on auth.users insert
3. Session managed via @supabase/ssr cookies
4. Middleware checks auth state for protected routes
5. Auth context provider wraps the app for client-side auth state

---

## 6. Implementation Plan

### Phase 1: Database & Auth Infrastructure
- Migration: profiles + saved_plans tables with RLS
- Supabase middleware for auth session
- Auth context provider
- Login/Register/Logout UI components

### Phase 2: Plan Persistence
- Save plan action (Server Action)
- My Plans page (list saved plans)
- Load plan into result view
- Plan count enforcement (free tier limit)

### Phase 3: Admin Dashboard
- Admin layout with sidebar
- User management (list, edit role/tier)
- Plan overview (read-only)
- Content management links

### Phase 4: Free/Pro Tier Enforcement
- Tier check middleware
- Upgrade prompt component
- Feature gating in UI

### Phase 5: Translations
- All new UI strings in de.json and en.json

---

## 7. File Structure (New/Modified)

```
src/
  app/[locale]/
    auth/
      login/page.tsx
      register/page.tsx
      callback/route.ts
    dashboard/
      page.tsx          (My Plans)
    admin/
      page.tsx          (Admin Dashboard)
      users/page.tsx
  components/
    auth/
      AuthProvider.tsx
      LoginForm.tsx
      RegisterForm.tsx
      UserMenu.tsx
    dashboard/
      PlanCard.tsx
      SavePlanButton.tsx
    admin/
      AdminLayout.tsx
      UserTable.tsx
  lib/
    auth.ts             (auth helpers)
    middleware.ts        (Next.js middleware)
  types/
    index.ts            (extended types)
```

---

## 8. Current Implementation Status

| Component | Status |
|-----------|--------|
| Database migration (profiles, saved_plans, is_admin function) | Done |
| RLS policies with SECURITY DEFINER helper | Done |
| Auth proxy (proxy.ts with Supabase session) | Done |
| AuthProvider context (client-side) | Done |
| LoginForm + RegisterForm components | Done |
| UserMenu with dropdown | Done |
| Login page (de/en) | Done |
| Register page (de/en) | Done |
| Auth callback route | Done |
| Save plan functionality (SavePlanButton) | Done |
| My Plans dashboard (list/load/delete) | Done |
| PlanCard component | Done |
| Admin dashboard (stats, links) | Done |
| Admin user management (role/tier editing) | Done |
| Free tier limit enforcement (3 plans max) | Done |
| Pro tier UI + badge | Done |
| Translations (auth, dashboard, admin - de/en) | Done |
| Test users created (admin, free, pro) | Done |
| Typecheck + Lint + Build passing | Done |
| Browser testing (login, dashboard, menu) | Done |

---

## 9. Test Users (Local Supabase)

| Email | Password | Role | Tier |
|-------|----------|------|------|
| admin@geburtstagspilot.de | Admin123! | admin | pro |
| user@geburtstagspilot.de | User123! | user | free |
| pro@geburtstagspilot.de | Pro123! | user | pro |

---

## 10. Files Created/Modified

### New Files
- `supabase/migrations/20260512130000_auth_profiles_plans.sql` - DB migration
- `supabase/seed_test_users.sql` - Test user documentation
- `src/lib/supabase-browser.ts` - Browser Supabase client
- `src/components/auth/AuthProvider.tsx` - Auth context
- `src/components/auth/LoginForm.tsx` - Login form
- `src/components/auth/RegisterForm.tsx` - Registration form
- `src/components/auth/UserMenu.tsx` - User dropdown menu
- `src/components/dashboard/SavePlanButton.tsx` - Save plan button
- `src/components/dashboard/PlanCard.tsx` - Saved plan card
- `src/app/[locale]/auth/login/page.tsx` - Login page
- `src/app/[locale]/auth/register/page.tsx` - Register page
- `src/app/[locale]/auth/callback/route.ts` - Auth callback
- `src/app/[locale]/dashboard/page.tsx` - User dashboard
- `src/app/[locale]/admin/page.tsx` - Admin dashboard
- `src/app/[locale]/admin/users/page.tsx` - User management

### Modified Files
- `src/proxy.ts` - Added auth session refresh + route protection
- `src/app/[locale]/layout.tsx` - Added AuthProvider wrapper
- `src/components/layout/Header.tsx` - Added UserMenu
- `src/components/result/ResultView.tsx` - Added SavePlanButton
- `src/types/index.ts` - Added Profile, SavedPlan, TIER_LIMITS
- `src/messages/en.json` - Added auth, dashboard, admin translations
- `src/messages/de.json` - Added auth, dashboard, admin translations

---

## 11. Future Enhancements

1. **AI Enhancement Engine**: GPT-based plan optimization, personalized suggestions
2. **Stripe Integration**: Payment processing for Pro subscriptions
3. **Social Login**: Google, Apple sign-in
4. **Collaborative Planning**: Share edit access with co-hosts
5. **Push Notifications**: RSVP reminders, party day countdown
6. **Template Marketplace**: Community-created themes and templates

## ./docs/KONZEPT_FREE_PRO_PLAN.md
# Konzept: Free vs. Pro Plan - Geburtstagspilot

Version: 1.0 | Stand: Mai 2026 | Status: Planungsphase

---

## 1. Strategische Grundlage - Was ist ein guter Paywall?

### 1.1 Anti-Bypass-Prinzip

Der entscheidende Filter bei der Feature-Auswahl: **Kann der Nutzer dieses Feature mit einem Screenshot, Browser-DevTools oder einem anderen kostenlosen Tool umgehen?**

| Feature-Typ | Bypass moglich? | Fazit |
|---|---|---|
| PDF-Export / Druck | Ja - window.print() jederzeit | Schlechter Paywall |
| Screenshot der Einladung | Ja - jedes Smartphone | Schlechter Paywall |
| Statische Inhalte (Spiele, Rezepte) | Ja - einfach kopieren | Schlechter Paywall |
| Einkaufsliste exportieren | Ja - Copy/Paste | Schlechter Paywall |
| **Zusammenarbeit mit anderen Eltern** | Nein - benotigt Server-Backend | Starker Paywall |
| **RSVP-Tracking via E-Mail** | Nein - erfordert Server + E-Mail-Service | Starker Paywall |
| **KI-Personalisierung** | Nein - erfordert API-Call mit Kosten | Starker Paywall |
| **Aufgaben-Manager mit Erinnerungen** | Nein - erfordert persistente Datenbankjobs | Starker Paywall |
| **Kinderprofil uber Jahre hinweg** | Nein - erfordert persistente Datenhaltung | Starker Paywall |
| **Unbegrenzte gespeicherte Plane** | Nein - per RLS serverseitig erzwungen | Solider Paywall |
| **Live-Teilen mit Bearbeitungsrechten** | Nein - erfordert Realtime-Backend | Starker Paywall |

### 1.2 Kernprinzip: Wert, nicht Restriktion

Der Free-Tier muss wertvoll genug sein, dass Nutzer registrieren. Der Pro-Tier muss so wertvoll sein, dass soziale und organisatorische Probleme gelost werden - nicht nur Convenience-Features.

**Free = "Ich plane alleine"**
**Pro = "Ich plane gemeinsam und organisiert"**

---

## 2. Feature-Matrix: Free vs. Pro

### 2.1 Vollstandige Ubersicht

| Feature | Anonym | Free | Pro | Begruendung |
|---|:---:|:---:|:---:|---|
| **Party-Wizard (7 Schritte)** | Vollstandig | Vollstandig | Vollstandig | Kern-Conversion-Tool, muss immer frei sein |
| **Ergebnis-Tabs (alle 7)** | Session | Session | Dauerhaft | Free hat Session-Zugriff, Pro persistent |
| **Plane speichern** | 0 | 3 | Unbegrenzt | Naturliche Upgrade-Schwelle |
| **Gespeicherte Plane laden** | - | Ja | Ja | Grundfunktion Pro |
| **Plane loschen** | - | Ja | Ja | Grundfunktion |
| **Basis-Sharing (Link lesen)** | 24h | 7 Tage | Dauerhaft | Zeitlimit erzeugt Upgrade-Druck |
| **--- PRO FEATURES ---** | | | | |
| **Eltern-Kollaboration** | Nein | Nein | Ja | Kern-Pro-Feature |
| **RSVP-Tracking + E-Mail-Einladung** | Nein | Nein | Ja | Kern-Pro-Feature |
| **KI-Personalisierung (Kinderwunsche)** | Nein | Nein | Ja | Hochwertig, kostenintensiv |
| **KI-Chat-Assistent** | Nein | Nein | Ja | Hochwertig, kostenintensiv |
| **Aufgaben-Manager + Erinnerungen** | Nein | Nein | Ja | Benotigt Backend-Jobs |
| **Kindprofile (jahresubergreifend)** | Nein | Nein | Ja | Benotigt persistente Datenhaltung |
| **Budget-Tracker (real)** | Nein | Nein | Ja | Benotigt persistente Datenhaltung |
| **Plan-Versionsgeschichte** | Nein | Nein | Ja | Benotigt Backend-Storage |
| **Exklusive Premium-Themen** | Nein | Nein | Ja | Content-Differenzierung |
| **WhatsApp/E-Mail-Versand (direkt)** | Nein | Nein | Ja | Benotigt E-Mail-Service-API |
| **Mehrere Kinder (Geschwister)** | Nein | Nein | Ja | Benotigt persistente Profile |

### 2.2 Free Tier - Detailbeschreibung

**Ziel:** Nutzer erleben den vollen Wert, werden aber an naturliche Grenzen der "Solo-Planung" stossen.

**Was Free-Nutzer konnen:**
- Den kompletten 7-Schritt-Wizard durchfuhren (keine versteckten Premium-Steps)
- Alle 7 Ergebnis-Tabs in der aktuellen Session sehen und nutzen
- Bis zu **3 Plane dauerhaft speichern** (klar kommuniziert, nicht versteckt)
- Gespeicherte Plane jederzeit laden und bearbeiten
- Gaste zur Liste hinzufugen (nur lokal, kein E-Mail-Versand)
- Einkaufsliste mit Checkboxen nutzen
- Einfache Read-Only-Links teilen (ablaufend nach 7 Tagen)
- Browser-Druck-Funktion (window.print) bleibt immer aktiv - wir verstecken das nicht
- Sprache wechseln (DE/EN)
- Dark/Light Mode

**Was Free-Nutzer nicht konnen:**
- Einen 4. Plan speichern (Upgrade-Prompt erscheint)
- Den Plan mit einem anderen Elternteil zur gemeinsamen Bearbeitung teilen
- E-Mail-Einladungen versenden und RSVP verfolgen
- KI fur personalisierte Empfehlungen nutzen
- Aufgaben und Erinnerungen setzen
- Kindprofile fur nachste Jahr speichern

### 2.3 Pro Tier - Detailbeschreibung

**Ziel:** Pro lost die echten Organisationsprobleme bei einer Kinderparty - Koordination, Kommunikation, Personalisierung.

**Preis:** 4,99 EUR/Monat oder 39,99 EUR/Jahr (sparen 33%)

**Was Pro-Nutzer konnen - jedes Feature einzeln erklart:**

#### Feature A: Eltern-Kollaboration (Bearbeitungs-Sharing)
- Plan mit beliebig vielen Personen teilen (per E-Mail-Einladung)
- Mitbearbeiter konnen Gaste hinzufugen, Spiele andern, Zeitplan anpassen
- Rollenmodell: Host (Vollzugriff), Mithelfer (eingeschrankt), Leser (nur lesen)
- Anderungen werden in Echtzeit synchronisiert (Supabase Realtime)
- **Warum nicht bypassed:** Erfordert serverseitige Authentifizierung, Datenbankoperationen, Realtime-Verbindungen

#### Feature B: RSVP-Tracking mit digitalem Einladungsversand
- Direkt aus der App E-Mail-Einladungen versenden (personalisiert pro Kind)
- Jede Einladung hat einen eindeutigen RSVP-Link
- Eltern klicken "Zusagen" / "Absagen" direkt in der E-Mail
- Dashboard zeigt Live-Status: Wer hat zugesagt, wer noch nicht geantwortet
- Automatische Erinnerungs-E-Mail nach X Tagen ohne Antwort
- Allergie-Informationen der Kinder werden beim RSVP abgefragt und in der App gespeichert
- **Warum nicht bypassed:** Erfordert E-Mail-Service (Resend/SendGrid), persistente Token in der Datenbank, Server-seitige Zustandsverwaltung

#### Feature C: KI-Personalisierung (Kinderwunsche und Interessen)
- Im Wizard: Freitextfeld "Was liebt [Kind] besonders?" (z.B. "Pferdefilme, Zeichnen, Bane Kimi")
- KI generiert personalisierte Spielvorschlage, Dekorationsideen, Kuchendesigns basierend darauf
- Personalisierter Einladungstext der auf das Kind eingeht
- Nicht mehr "Piraten-Standard-Spiel" sondern "Schatzsuche mit Hinweisen die Mias Lieblingsfilme referenzieren"
- **Warum nicht bypassed:** Erfordert LLM-API-Calls (Kosten pro Anfrage), serverseitig verarbeitet

#### Feature D: KI-Chat-Assistent
- Chatfenster in der Ergebnis-Seite: "Frag mich etwas zur Party"
- Beispiele: "Was mache ich wenn es regnet?", "Wie unterhalte ich schuchterne Kinder?", "Ideen fur vegetarische Kuchen zum Dinosaurier-Motto"
- Kontext-bewusst: KI kennt den aktuellen Plan und gibt passende Antworten
- **Warum nicht bypassed:** LLM-API-Kosten, serverseitig

#### Feature E: Aufgaben-Manager mit Erinnerungen
- Automatisch generierte Vorbereitungsaufgaben basierend auf dem Plan (z.B. "8 Wochen vorher: Ort buchen", "2 Wochen vorher: Einladungen verschicken", "3 Tage vorher: Kuchen backen")
- Nutzer kann Aufgaben anpassen, eigene hinzufugen
- E-Mail-Erinnerungen zum konfigurierbaren Zeitpunkt
- Fortschrittsanzeige: wie viel ist erledigt?
- **Warum nicht bypassed:** Erfordert persistente Datenbankjobs (cron), E-Mail-Versand

#### Feature F: Kinderprofile
- Profil fur jedes Kind anlegen (Name, Geburtstag, Interessen, Allergien)
- Beim nachsten Wizard: Kind auswahlen, alle Daten werden automatisch vorausgefullt
- Alter wird automatisch auf das aktuelle Jahr berechnet
- Interessenhistorie: was hat letztes Jahr Spa gemacht?
- **Warum nicht bypassed:** Persistente Datenhaltung uber Sessions hinweg, datenschutzkonform durch Authentifizierung

#### Feature G: Budget-Tracker (reale Ausgaben)
- Neben dem geplanten Budget: tatsachliche Ausgaben erfassen
- Pro Kategorie: geplant vs. ausgegeben
- Belege / Notizen anhangen
- Gesamtubersicht am Ende: "Party hat X EUR gekostet"
- **Warum nicht bypassed:** Persistente Datenhaltung

#### Feature H: Premium-Exklusivthemen
- 5+ zusatzliche Themen, die im Free-Tier nicht erscheinen (z.B. "Barbie", "Minecraft", "Paw Patrol", "Meerjungfrau Deluxe", "Weltraum-Mission")
- Hochwertigere Einladungsvorlagen (animierte CSS-Elemente, professionelles Layout)
- Premium-Rezepte mit detaillierterer Anleitung und Foto-Beschreibungen
- **Warum nicht bypassed:** Serverseitige Content-Filterung per RLS

#### Feature I: Unbegrenzte Shared Links (dauerhaft)
- Free: Links laufen nach 7 Tagen ab
- Pro: Links laufen nie ab, bleiben dauerhaft aktiv
- Planinhalt kann geupdated werden, Link bleibt derselbe
- **Warum nicht bypassed:** Datenbankfeld `expires_at` wird serverseitig gepruft

---

## 3. Pricing-Strategie

### 3.1 Preismodell

```
Free:    0 EUR/Monat    - Fur Eltern die einmal im Jahr planen
Pro:     4,99 EUR/Monat - Fur aktive Eltern / organisierte Familien
Pro:    39,99 EUR/Jahr  - 33% Rabatt, 2 Monate gratis
```

### 3.2 Preispsychologie

- 4,99 EUR ist unter dem "Schmerzpunkt" von 5 EUR - psychologisch wichtig
- Jahresabo preist sich als "Investition fur alle Geburtstage des Jahres"
- Keine Testphase notwendig - Free-Tier ist echte Alternative
- Upgrade-Prompts: kontextuell, nicht aggressiv (erscheinen erst wenn Limit erreicht)

### 3.3 Stripe-Integration

- Zahlungsabwicklung uber Stripe (DSGVO-konform, EU-Server moglich)
- Webhooks: `checkout.session.completed` -> `tier` in `profiles` auf "pro" setzen
- Webhooks: `customer.subscription.deleted` -> `tier` zuruck auf "free"
- Keine eigene Zahlungsverarbeitung - alles uber Stripe Hosted Checkout

---

## 4. Technische Implementierung

### 4.1 Datenbank-Anderungen

#### 4.1.1 Neue Tabellen

```sql
-- Kollaboratoren fur geteilte Plane
CREATE TABLE public.plan_collaborators (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID NOT NULL REFERENCES public.saved_plans(id) ON DELETE CASCADE,
  user_id UUID REFERENCES public.profiles(id) ON DELETE CASCADE,
  invited_email TEXT,
  role TEXT NOT NULL DEFAULT 'viewer' CHECK (role IN ('editor', 'viewer')),
  accepted_at TIMESTAMPTZ,
  invited_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- RSVP-Einladungen
CREATE TABLE public.rsvp_invitations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID NOT NULL REFERENCES public.saved_plans(id) ON DELETE CASCADE,
  guest_id TEXT NOT NULL,
  child_name TEXT NOT NULL,
  parent_email TEXT NOT NULL,
  token TEXT UNIQUE NOT NULL DEFAULT encode(gen_random_bytes(16), 'hex'),
  status TEXT NOT NULL DEFAULT 'pending' CHECK (status IN ('pending', 'accepted', 'declined')),
  child_allergies TEXT,
  notes TEXT,
  sent_at TIMESTAMPTZ,
  responded_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Kinderprofile (Pro only)
CREATE TABLE public.child_profiles (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  name TEXT NOT NULL,
  birth_date DATE,
  interests TEXT[],
  allergies JSONB,
  notes TEXT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Aufgaben-Manager (Pro only)
CREATE TABLE public.party_tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID NOT NULL REFERENCES public.saved_plans(id) ON DELETE CASCADE,
  title_de TEXT NOT NULL,
  title_en TEXT NOT NULL,
  due_days_before INT NOT NULL,
  is_completed BOOLEAN NOT NULL DEFAULT false,
  reminder_sent BOOLEAN NOT NULL DEFAULT false,
  is_custom BOOLEAN NOT NULL DEFAULT false,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Budget-Tracking (Pro only)
CREATE TABLE public.budget_entries (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID NOT NULL REFERENCES public.saved_plans(id) ON DELETE CASCADE,
  category TEXT NOT NULL,
  description TEXT NOT NULL,
  planned_amount NUMERIC(8,2),
  actual_amount NUMERIC(8,2),
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Stripe-Abos (fur Webhook-Verarbeitung)
CREATE TABLE public.stripe_subscriptions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  stripe_customer_id TEXT UNIQUE NOT NULL,
  stripe_subscription_id TEXT UNIQUE,
  status TEXT NOT NULL,
  current_period_end TIMESTAMPTZ,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

#### 4.1.2 Anderungen an bestehenden Tabellen

```sql
-- saved_plans: Ablaufdatum fur geteilte Links
ALTER TABLE public.saved_plans
  ADD COLUMN share_expires_at TIMESTAMPTZ,
  ADD COLUMN party_date DATE;

-- profiles: Stripe-Referenz
ALTER TABLE public.profiles
  ADD COLUMN stripe_customer_id TEXT UNIQUE;

-- Premium-Themes in themes-Tabelle markieren
ALTER TABLE public.themes
  ADD COLUMN is_premium BOOLEAN NOT NULL DEFAULT false;
```

### 4.2 RLS-Policies (Erweiterung)

```sql
-- child_profiles: Nur eigene Profile sichtbar
CREATE POLICY "Users see own child profiles"
  ON public.child_profiles
  FOR ALL USING (auth.uid() = user_id);

-- rsvp_invitations: Planinhaber kann alles, Gaste nur via token
CREATE POLICY "Plan owner manages rsvp"
  ON public.rsvp_invitations
  FOR ALL USING (
    EXISTS (
      SELECT 1 FROM public.saved_plans sp
      WHERE sp.id = plan_id AND sp.user_id = auth.uid()
    )
  );

-- Pro-only content: Premium-Themes nur fur Pro sichtbar
CREATE POLICY "Free users see non-premium themes"
  ON public.themes
  FOR SELECT USING (
    is_premium = false
    OR EXISTS (
      SELECT 1 FROM public.profiles p
      WHERE p.id = auth.uid() AND p.tier = 'pro'
    )
  );
```

### 4.3 Feature-Gate: TypeScript-Pattern

```typescript
// src/lib/feature-gates.ts
// Zentrale Feature-Gate-Konfiguration (neutrales File, kein "use client"/"use server")

export const PRO_FEATURES = [
  'collaboration',
  'rsvp_tracking',
  'ai_personalization',
  'ai_chat',
  'task_manager',
  'child_profiles',
  'budget_tracker',
  'premium_themes',
  'unlimited_plans',
  'persistent_share_links',
] as const;

export type ProFeature = typeof PRO_FEATURES[number];

export function isProFeature(feature: ProFeature): true {
  return true; // type guard, used with profile.tier check
}
```

```typescript
// src/hooks/useFeatureGate.ts
"use client";

import { useAuth } from '@/components/auth/AuthProvider';
import type { ProFeature } from '@/lib/feature-gates';

export function useFeatureGate(feature: ProFeature): {
  hasAccess: boolean;
  tier: 'free' | 'pro';
  showUpgrade: () => void;
} {
  const { profile } = useAuth();
  const tier = profile?.tier ?? 'free';
  const hasAccess = tier === 'pro';

  function showUpgrade() {
    // Global event bus oder Router-Navigation zu /upgrade
    window.dispatchEvent(new CustomEvent('show-upgrade-modal', { detail: { feature } }));
  }

  return { hasAccess, tier, showUpgrade };
}
```

### 4.4 API-Routen (neue Server-seitige Endpunkte)

```
src/app/api/
  stripe/
    checkout/route.ts      - Stripe Checkout Session erstellen
    webhook/route.ts       - Stripe Webhooks empfangen + Tier aktualisieren
    portal/route.ts        - Customer Portal (Abo verwalten)
  rsvp/
    send/route.ts          - E-Mail-Einladungen versenden (Resend API)
    respond/[token]/route.ts - RSVP-Antwort verarbeiten
    remind/route.ts        - Erinnerungen versenden
  collaboration/
    invite/route.ts        - Mitbearbeiter einladen
    accept/route.ts        - Einladung annehmen
  tasks/
    generate/route.ts      - KI/Template-basierte Aufgabenliste generieren
    remind/route.ts        - Cron-Job: Erinnerungen senden
```

### 4.5 UI-Komponenten (neue Dateien)

```
src/components/
  upgrade/
    UpgradeModal.tsx        - Modaler Upgrade-Dialog mit Feature-Highlight
    UpgradeBanner.tsx       - Inline-Banner fur gesperrte Features
    PricingPage.tsx         - Vollstandige Preisseite
    FeatureGate.tsx         - Wrapper-Komponente fur gesperrte Features
  collaboration/
    CollabButton.tsx        - "Mit Partner teilen" Button
    CollabManager.tsx       - Mitbearbeiter-Verwaltung
  rsvp/
    RsvpDashboard.tsx       - RSVP-Ubersicht fur den Gastgeber
    RsvpLandingPage.tsx     - Landing Page fur Gaste-RSVP (offentlich)
    SendInvitationModal.tsx - Modal zum Versenden von Einladungen
  child-profiles/
    ChildProfileCard.tsx    - Kindprofil-Karte
    ChildProfileForm.tsx    - Kindprofil erstellen/bearbeiten
    ChildSelector.tsx       - Kindprofil im Wizard auswahlen
  budget/
    BudgetTracker.tsx       - Budget-Tracker-Komponente
    BudgetEntry.tsx         - Einzelne Ausgabe erfassen
  tasks/
    TaskManager.tsx         - Aufgaben-Liste mit Checkboxen
    TaskReminder.tsx        - Erinnerungseinstellungen
```

### 4.6 Neue Seiten

```
src/app/[locale]/
  upgrade/
    page.tsx               - Preisseite / Upgrade-Seite
  rsvp/
    [token]/
      page.tsx             - Gast-RSVP-Seite (offentlich, kein Login)
  collaborate/
    [planId]/
      page.tsx             - Kollaborations-Landing fur eingeladene Nutzer
```

---

## 5. Upgrade-Conversion-Strategie

### 5.1 Upgrade-Touchpoints (wo und wann erscheinen Upgrade-Prompts)

| Trigger | Wo | Botschaft |
|---|---|---|
| 4. Plan speichern | Dashboard | "Du hast alle 3 kostenlosen Plane genutzt" |
| Teilen-Button (nach 7 Tagen) | Ergebnis-Seite | "Dein Link ist abgelaufen - mit Pro bleibt er dauerhaft" |
| Gastliste: E-Mail-Feld | GuestListTab | "Versende digitale Einladungen und tracke RSVPs" |
| Ergebnis: KI-Button | ResultView | "Personalisiere den Plan mit KI fur [Kindname]" |
| Wizard: Kindprofil-Option | Wizard Step 1 | "Speichere das Profil fur nachste Jahr" |

### 5.2 Upgrade-Modal-Design

Das Upgrade-Modal muss:
- Das konkrete Feature zeigen, das geblockt wurde (kontextuell)
- Den Wert in 1-2 Satzen erklaren (nicht Feature-Liste, sondern Problem-Losung)
- Preis transparent zeigen
- Klaren CTA: "Pro freischalten - 4,99 EUR/Monat"
- Subtile "Nicht jetzt" Option (kein Dark Pattern)

---

## 6. Implementierungsplan (Phasen)

### Phase 1: Foundation (2-3 Tage)
- Feature-Gate Hook (`useFeatureGate`)
- `FeatureGate.tsx` Wrapper-Komponente mit Upgrade-Banner
- `UpgradeModal.tsx` und globaler Event-Listener
- `UpgradeBanner.tsx` fur inline-Hints
- Neue Datenbank-Tabellen: Migrationen erstellen und anwenden
- `TIER_LIMITS` in `src/types/index.ts` erweitern
- RLS-Policies fur neue Tabellen

### Phase 2: Stripe-Integration (2-3 Tage)
- Stripe-Account einrichten (Testmodus)
- `/api/stripe/checkout` Route
- `/api/stripe/webhook` Route (tier-Update)
- `/api/stripe/portal` Route (Abo verwalten)
- Preisseite `/upgrade` mit Stripe Checkout-Integration
- Umgebungsvariablen: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `STRIPE_PRICE_ID_MONTHLY`, `STRIPE_PRICE_ID_YEARLY`

### Phase 3: Kindprofile (1-2 Tage)
- `child_profiles` Tabelle (Migration bereits in Phase 1)
- `ChildProfileForm.tsx` und `ChildProfileCard.tsx`
- `ChildSelector.tsx` in Wizard Step 1 integrieren
- Pro-Gate: nur sichtbar bei Pro-Tier

### Phase 4: Aufgaben-Manager (1-2 Tage)
- `party_tasks` Tabelle
- Standard-Aufgaben-Templates (statisch, kein KI)
- `TaskManager.tsx` in ResultView integrieren (neuer Tab oder Unterabschnitt)
- Erinnerungslogik: Supabase Edge Function oder externe cron-Job-Losung

### Phase 5: Kollaboration (3-4 Tage)
- `plan_collaborators` Tabelle
- `CollabButton.tsx` und `CollabManager.tsx`
- E-Mail-Einladung versenden (Resend API)
- `/collaborate/[planId]` Landing Page fur neue Mitbearbeiter
- Supabase Realtime: Echtzeit-Updates beim gleichzeitigen Bearbeiten
- RLS anpassen fur Mitbearbeiter-Zugriff

### Phase 6: RSVP-Tracking (3-4 Tage)
- `rsvp_invitations` Tabelle
- `RsvpDashboard.tsx` in ResultView (neuer "RSVPs"-Tab, Pro-only)
- `SendInvitationModal.tsx`
- `/api/rsvp/send` Route (Resend API)
- `/rsvp/[token]` offentliche Seite
- E-Mail-Template fur Gaste-Einladung
- Allergie-Erfassung beim RSVP

### Phase 7: Budget-Tracker (1-2 Tage)
- `budget_entries` Tabelle
- `BudgetTracker.tsx` in ResultView (neuer Abschnitt im Plan)
- Pro-Gate

### Phase 8: Premium-Themen (1 Tag)
- `is_premium` Flag in themes-Tabelle
- 5 Premium-Themen hinzufugen
- RLS-Policy fur Premium-Content
- UI: Premium-Badge auf gesperrten Themen im Wizard

---

## 7. Abgrenzung: Was bewusst NICHT in den Paywall kommt

| Feature | Warum frei bleiben? |
|---|---|
| Einkaufsliste | Kernwert, der App Nutzen zeigt |
| Spielempfehlungen (Standard) | Kernwert, Driver fur Registrierung |
| Einladungsvorlagen (Standard) | Kernwert, zeigt Pro-Potential |
| Browser-Druck/Print | Nicht verhinderbar, wware Dark Pattern |
| Sprache wechseln | Zuganglichkeit, kein sinnvoller Paywall |
| Dark Mode | Zuganglichkeit |
| Wizard (alle Schritte) | Ohne guten Wizard kein Nutzer |

---

## 8. Metriken und Erfolgsmessung

### KPIs

| Metrik | Free-Benchmark | Pro-Ziel |
|---|---|---|
| Registrierungsrate (Wizard-Completion -> Register) | >30% | - |
| Free -> Pro Conversion | - | >5% |
| Pro Monthly Retention | - | >85% |
| RSVP-Feature-Nutzung (Pro) | - | >60% der Pro-Nutzer |
| Churn-Grund #1 | - | Keine (messen via Exit-Survey) |

### Tracking-Events (Privacy-first, Plausible Analytics)
- `wizard_completed`
- `plan_saved`
- `plan_limit_reached` (Free)
- `upgrade_modal_shown` + welches Feature
- `upgrade_completed`
- `rsvp_sent`
- `collaboration_invite_sent`

## ./docs/KONZEPT_KI_ENHANCEMENT.md
# Konzept: KI-Enhancement - Geburtstagspilot

Version: 1.0 | Stand: Mai 2026 | Status: Planungsphase
Perspektive: Software-Architekt + Product Owner

---

## 1. Vision und Anforderungsanalyse

### 1.1 Ausgangslage - Was fehlt heute?

Die aktuelle App generiert Partypplane nach einem starren Template-System:
- Spiele kommen aus einer Datenbank mit Filter (Alter, Ort, Thema)
- Rezepte sind 1:1 an ein Motto gebunden
- Einladungstext ist ein unverandertes Template
- Mengenberechnung ist eine lineare Formel
- Der Plan kennt das Kind nicht - es ist nur ein Alter und eine Gasteranzahl

**Zitat eines typischen Nutzers:** *"Der Plan ist gut, aber Mia liebt halt Pferde UND Basteln, und der Piraten-Plan hat nichts davon. Wie passe ich das an?"*

### 1.2 Was KI leisten kann und was nicht

**KI kann:**
- Naturlichsprachliche Eingaben in strukturierte Daten umwandeln
- Kreative und personalisierte Inhalte generieren
- Kontextuelles Wissen uber Kinderpartys einbringen
- Kompromissvorschlage bei Konflikten finden (z.B. Allergie + Lieblingsrezept)
- Unsicherheiten des Nutzers durch Dialog klaren
- Skalierbar personalisierte Texte schreiben

**KI kann nicht (zuverlaessig):**
- Echtzeitdaten liefern (Preise, lokale Anbieter)
- Garantiert korrekte Mengenangaben ohne Validierung
- Medizinische Allergie-Entscheidungen treffen
- Ersatz fur strukturierte Daten sein (Datenbank bleibt Backbone)

### 1.3 Anforderungsanalyse: Use Cases aus Nutzerperspektive

Aus einer hypothetischen Befragung von Eltern ergeben sich folgende Top-Schmerzen:

| Rang | Schmerzpunkt | KI-Losung |
|---|---|---|
| 1 | "Mein Kind hat spezifische Interessen, der Plan passt nicht" | Kinderprofil + KI-Personalisierung |
| 2 | "Ich weiss nicht wo ich anfangen soll" | Naturlichsprachlicher Wizard / KI-Chat |
| 3 | "Die Spiele klingen alle gleich" | KI generiert einzigartige Spiel-Varianten |
| 4 | "Die Einladung klingt generisch" | KI schreibt personalisierte Einladungstexte |
| 5 | "Was ist wenn es regnet?" | KI-Alternativplan / kontextueller Chat |
| 6 | "Wie viel muss ich wirklich kaufen?" | KI-gestutzte Budgetoptimierung |
| 7 | "Ich brauche Ideen fur Themen" | KI-Themen-Vorschlage basierend auf Interessen |
| 8 | "Kann mir jemand beim Planen helfen?" | KI-Chat-Assistent |

---

## 2. KI-Feature-Katalog

### Feature 1: Naturlichsprachliche Eingabe (Conversational Wizard)

**Problem:** Der 7-Schritt-Wizard ist gut, aber es fehlt die Moglichkeit fur Eltern die alles auf einmal sagen wollen.

**Losung:** Ein optionaler "Schnell-Modus" oben im Wizard:

```
"Beschreibe die Party in einem Satz, wir erledigen den Rest."

Eingabe: "Ich plane eine Party fur Lena, sie wird 7, liebt Pferde und Einhorner, 
         wir haben 12 Gaste, Outdoor, ca. 150 EUR"

KI extrahiert:
  - Alter: 7
  - Interessen: Pferde, Einhorner
  - Gasteranzahl: 12
  - Ort: Outdoor
  - Budget: 150 EUR
  - Thema: Einhorn (automatisch gewahlt, aber korrigierbar)
```

**Technisch:**
- `POST /api/ai/parse-wizard-input` - GPT-4o mit strukturiertem JSON-Output
- Validierung des extrahierten Outputs gegen bekannte Wizard-Felder
- Nutzer sieht das vorausgefullte Wizard mit Moglichkeit zur Korrektur
- Kein Blind-Vertrauen in KI-Output - immer menschliche Bestatigung

---

### Feature 2: Kinder-Interessen-Profiler (Deep Personalization)

**Problem:** Das Kind ist aktuell nur Alter + Anzahl. Es hat Personlichkeit, Lieblingsserien, Hobbys.

**Losung:** Ein Freitextfeld im Wizard (Pro-Feature) + KI-Analyse:

**Wizard Step 1 (Pro):**
```
"Was liebt [Kindname] besonders? (optional, aber macht den Plan viel besser)"

Placeholder: z.B. "Mag Dinosaurier, liebt Basteln, hat Angst vor lauten Gerauschen, 
              beste Freundin heisst Sophie, Lieblingsfilm: Das Dschungelbuch"
```

**Was KI damit macht:**
- Erstellt ein internes Kindprofil-Objekt
- Beeinflusst Spiel-Ranking: "Ruhige Bastelspiele" hoher gewichten bei "hat Angst vor lauten Gerauschen"
- Personalisiert Zeitplan-Beschreibungen: "Basteln und entdecken mit Dinos" statt "Spiel 2"
- Generiert personalisierte Einladung: "Komm und feier mit dem großen Dinosaurier-Forscher Luca!"
- Schlagt alternative Themen vor: "Basierend auf Lenas Interessen passen auch: Dschungel-Safari, Naturentdecker"

---

### Feature 3: KI-Spiel-Varianten-Generator

**Problem:** Die Spieldatenbank hat 80+ Spiele - aber nach 3 Jahren Kindergeburtstagen kennen Eltern sie alle.

**Losung:** KI generiert Variationen der Standard-Spiele und neue themenspezifische Ideen:

**Trigger:** Button "Neues Spiel generieren" in GamesTab (Pro)

**Eingabe an KI:**
```json
{
  "theme": "Dinosaurier",
  "age": 6,
  "location": "outdoor",
  "guests": 10,
  "child_interests": ["Basteln", "Fossilien"],
  "existing_games": ["Reise nach Jerusalem", "Sackhupfen"],
  "exclude_materials": ["Schere"],
  "language": "de"
}
```

**KI-Output:**
```json
{
  "name_de": "Fossilien-Ausgraber",
  "name_en": "Fossil Excavation",
  "description_de": "Kleine Paleonteologen graben versteckte Dinosaurier-Fossilien (Gipsabdruecke oder Plastikdinos) im Sandkasten aus...",
  "instructions_de": ["1. Verstecke 10 Dino-Figuren im Sand...", "..."],
  "materials_de": ["Sandkasten oder grosse Kiste mit Sand", "10 Plastik-Dinosaurier", "Pinsel"],
  "duration_minutes": 20,
  "activity_level": "calm"
}
```

**Validierung:** KI-generierte Spiele werden vor Anzeige auf Mindestqualitat gepruft (Completeness-Check), nie blind angezeigt.

---

### Feature 4: KI-Rezept-Generator

**Problem:** Es gibt 1 Rezept pro Thema. Bei Allergien (glutenfrei + laktosefrei + vegan gleichzeitig) sind die Optionen erschopft.

**Losung:** KI generiert themen-passende Rezepte mit Allergie-Berucksichtigung:

**Trigger:** "Alternatives Rezept generieren" Button in FoodTab (Pro)

**Eingabe:**
```json
{
  "theme": "Dschungel-Safari",
  "allergens": {
    "glutenFree": true,
    "vegan": true
  },
  "skill_level": "beginner",
  "servings": 12,
  "available_time_minutes": 60,
  "language": "de"
}
```

**KI-Output:** Vollstandiges Rezept mit Zutaten (mit Mengen fur N Portionen), Schritt-fur-Schritt-Anleitung, Dekortipps passend zum Thema, Allergen-Markierungen.

**Sicherheit:** KI-Rezepte werden mit einem "KI-generiert - bitte prufen" Badge markiert. Kein Ersatz fur medizinische Allergie-Beratung.

---

### Feature 5: KI-Einladungstext-Generator

**Problem:** Die Einladungsvorlagen sind generisch und klingen immer gleich.

**Losung:** KI schreibt personalisierte Einladungstexte:

**Freitext-Eingabe im InvitationTab (Pro):**
```
"Stil: lustig, verspielt
 Besonderes: Lena liebt Dinos, ihre beste Freundin Sophie kommt auch
 Motto: Dino-Party
 Alter wird 7"
```

**KI generiert:**
```
Hey du wildes Dino-Kind!

Lena wird 7 - und das MUSS gefeiert werden!
Komm in die Urzeit-Hohle und feier mit uns:

Wann: Samstag, 14. Juni, 14:00-17:00 Uhr
Wo: Im grossen Garten der Dinos (Musterstrasse 1, 12345 Musterstadt)

Es wird gegraben, gebruellt und gefeiert!
(PS: Sophie freut sich schon auf dich!)

Bitte melde dich bis 7. Juni bei Lenas Mama an.
```

**Varianten:** KI kann 3 Varianten auf einmal generieren (lustig / klassisch / kreativ) zur Auswahl.

---

### Feature 6: KI-Chat-Assistent ("Party-Coach")

**Problem:** Eltern haben viele ad-hoc Fragen die der statische Plan nicht beantworten kann.

**Losung:** Ein Chatfenster in der Ergebnis-Seite, das den aktuellen Plan kennt:

**Kontextuelle Fragen die der Assistent beantwortet:**
- "Was mache ich wenn es regnet?" -> Generiert Indoor-Alternativplan
- "Spiel 2 klingt zu chaotisch fur schuchterne Kinder" -> Schlagt ruhigere Alternativen vor
- "Wie bereite ich den Kuchen einen Tag vorher vor?" -> Anleitungstipps
- "Ich habe nur 80 EUR Wirklichkeit statt 150" -> Budgetoptimierungsvorschlage
- "Was mache ich wenn ein Kind Heulkrampfe bekommt?" -> Krisenmanagement-Tipps
- "Kannst du eine Schatzsuche fur 6-Jahrige erklaren?" -> Detaillierte Spielanleitungen
- "Mein Garten ist nur 30qm" -> Raum-angepasste Spielvorschlage

**Technisch:**
- System-Prompt enthalt den vollstandigen aktuellen Plan als JSON-Kontext
- Antworten auf Deutsch oder Englisch je nach App-Spracheinstellung
- Streaming-Antworten (kein Warten auf komplette Antwort)
- Konversationsverlauf innerhalb der Session (max 10 Nachrichten fur Kosten-Kontrolle)
- Pro-only (Token-Kosten sind real)

---

### Feature 7: KI-Zeitplan-Optimierer

**Problem:** Der aktuelle Zeitplan ist ein linearer Template. Er berucksichtigt nicht:
- Energie-Kurve der Kinder (wild am Anfang, mude nach dem Essen)
- Optimale Spiel-Reihenfolge (aktiv -> ruhig -> aktiv)
- Alter-spezifische Aufmerksamkeitsspannen
- Essen- und Pausen-Rhythmus

**Losung:** KI-Analyse und -Optimierung des Zeitplans:

**Trigger:** "Zeitplan optimieren" Button im ScheduleTab (Pro)

**KI analysiert:**
- Energie-Level der aktuellen Spiel-Reihenfolge
- Ob Essen zwischen zwei sehr aktiven Spielen liegt (schlecht: Erbrechen-Risiko)
- Ob die Gesamtdauer fur das Alter angemessen ist
- Ob Pufferzeiten vorhanden sind

**KI gibt zurück:**
- Optimierten Zeitplan mit Begrundungen
- Warnungen: "Nach 'Laufendes Fangspiel' sollte eine 15-min-Pause vor dem Essen sein"
- Vorschlag: Reihenfolge andern, Puffer einfugen

---

### Feature 8: Themen-Vorschlags-KI

**Problem:** Eltern wissen oft nicht welches Thema zu ihrem Kind passt. Die Liste hat 14 Themen - welches ist das richtige?

**Losung:** KI schlagt Themen basierend auf Kindinteressen vor, noch vor Wizard Step 4:

**Nach Wizard Step 1 (Name + Interessen eingegeben):**
```
KI analysiert Interessen: "Pferde, Zeichnen, Einhorn-Buch"

Themen-Vorschlage:
  1. Einhorn (95% Match) - "Mias Lieblingsmotiv direkt als Partykonzept"
  2. Pferde & Pony (88% Match) - "Echte Pferde als Thema fur den Outdoor-Bereich"
  3. Kunst-Atelier (75% Match) - "Ideal fur kreative Kinder die gerne zeichnen"
  4. Prinzessin (60% Match) - "Passt zum Einhorn-Hintergrund, klassische Variante"
```

**Alternativ:** Freitext-Suche: "Gibt es ein Thema fur ein Kind das Weltraum und Roboter liebt?"
-> KI zeigt "Weltraum-Mission" an und generiert hybride Ideen ("Roboter-Labor im Weltraum")

---

### Feature 9: KI-Budgetoptimierer

**Problem:** Bei einem Budget von 80 EUR und 12 Gasten ist nicht klar wie man optimal verteilt.

**Losung:** KI schlagt Budgetverteilung vor und zeigt Trade-offs:

**Eingabe:** Budget 80 EUR, 12 Gaste, Dino-Theme

**KI-Ausgabe:**
```
Budget-Optimierung fur 80 EUR bei 12 Kindern:

Empfehlung:
  Kuchen (selber backen): 15 EUR (Zutaten)
  Essen/Snacks:           20 EUR (Wurst, Gemuese, Brezeln)
  Getranke:               8 EUR
  Spielmaterial:          12 EUR (Dino-Grabungs-Set)
  Mitgebsel:              18 EUR (1,50 EUR/Kind fur Dino-Figur + Sticker)
  Deko:                   7 EUR (Luftballons, Tischdecke)
  Gesamt:                 80 EUR

Alternative: Kuchen kaufen statt backen (+20 EUR, aber spart 3 Stunden Zeit)

Einsparmoglichkeiten:
  - Mitgebsel: Bastel-Mitgebsel im Spiel erstellen (Gipsabdruck), spart 10 EUR
  - Deko: Girlanden selbst basteln, spart 3 EUR
```

---

### Feature 10: Post-Party-Modul

**Problem:** Nach der Party gibt es keine Folge-Funktionalitat. Aber Eltern haben Feedback: was hat funktioniert, was nicht?

**Losung:** Optional nach dem Party-Datum: KI-gestutzte Retrospektive

**Nutzer beantwortet 3 Fragen:**
- "Was hat super funktioniert?"
- "Was hat nicht funktioniert?"
- "Notizen fur nachstes Jahr?"

**KI verarbeitet das zu:**
- Kindprofil-Update (Interessen bestatigt/widerlegt)
- Notizen im gespeicherten Plan
- Vorschlage fur nachste Party basierend auf Feedback
- (Aggregiert anonym: welche Spiele werden positiv bewertet?)

---

## 3. Technische Architektur

### 3.1 Gesamtubersicht

```
                        ┌────────────────────────────┐
                        │      Next.js App Router     │
                        │                             │
     User Browser ─────>│  Client Components          │
                        │  (Streaming UI, Chat)       │
                        │         │                   │
                        │  Server Components          │
                        │  (Plan Generation)          │
                        └────────────────────────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
          ┌─────────▼──────────┐    ┌──────────▼──────────┐
          │  AI API Routes     │    │  Supabase            │
          │  /api/ai/*         │    │  (PostgreSQL + Auth) │
          │                    │    │                      │
          │  - parse-wizard    │    │  - child_profiles    │
          │  - personalize     │    │  - ai_conversations  │
          │  - generate-game   │    │  - ai_usage_log      │
          │  - generate-recipe │    │  - saved_plans       │
          │  - chat            │    │                      │
          └────────────────────┘    └──────────────────────┘
                    │
          ┌─────────▼──────────┐
          │  LLM Provider      │
          │  OpenAI GPT-4o     │
          │  (Anthropic Backup)│
          └────────────────────┘
```

### 3.2 Provider-Strategie

**Primarer Provider: OpenAI GPT-4o**
- Beste Deutsch-Qualitat
- Structured Outputs (JSON-Modus) fur zuverlaessige Datenextraktion
- Function Calling fur Tool-gestutzte Antworten
- Streaming fur Chat-Antworten

**Backup-Provider: Anthropic Claude 3.5 Haiku**
- Schneller und gunstiger fur einfache Aufgaben
- Guter Fallback bei OpenAI-Ausfallen

**Provider-Abstraktion (Pflicht):**
```typescript
// src/lib/ai/provider.ts
// Neutral - kein "use client"/"use server"

export interface AIProvider {
  complete(prompt: AIPrompt): Promise<string>;
  stream(prompt: AIPrompt): ReadableStream<string>;
  structuredOutput<T>(prompt: AIPrompt, schema: ZodSchema<T>): Promise<T>;
}

// Konkrete Implementierungen:
// src/lib/ai/openai.ts
// src/lib/ai/anthropic.ts
```

**Warum Abstraktion:** Provider konnen jederzeit wechseln ohne App-Code zu andern.

### 3.3 Kostenmodell und Token-Budget

| Feature | Avg. Input Tokens | Avg. Output Tokens | Cost/Call (GPT-4o) | Tier |
|---|---|---|---|---|
| Wizard-Parse (Natural Language) | 200 | 100 | ~$0.003 | Pro |
| Personalisierungs-Analyse | 800 | 300 | ~$0.011 | Pro |
| Spiel generieren | 600 | 400 | ~$0.010 | Pro |
| Rezept generieren | 500 | 600 | ~$0.011 | Pro |
| Einladungstext (3 Varianten) | 400 | 600 | ~$0.010 | Pro |
| Chat-Antwort (mit Plan-Kontext) | 2000 | 500 | ~$0.025 | Pro |
| Budget-Optimierung | 400 | 500 | ~$0.009 | Pro |
| Zeitplan-Optimierung | 1500 | 600 | ~$0.021 | Pro |

**Monatliches Token-Budget pro Pro-Nutzer:**
- Max 500.000 Input-Tokens/Monat (~$1.25)
- Max 200.000 Output-Tokens/Monat (~$2.00)
- Gesamt-Cap: ~$3.25/Monat pro Nutzer (bei Pro-Preis 4,99 EUR = angemessen)

**Rate-Limiting-Strategie:**
```typescript
// src/lib/ai/rate-limiter.ts
export const AI_RATE_LIMITS = {
  chat_messages_per_hour: 20,
  generations_per_day: 30,
  total_tokens_per_month: 500_000,
} as const;
```

### 3.4 Sicherheits-Architektur

**Regel: KI-API-Keys niemals im Client-Code**

```
Client Browser
     │
     ├── NEIN: fetch('https://api.openai.com') mit API-Key -> VERBOTEN
     │
     └── JA: fetch('/api/ai/chat') -> Next.js Server Route -> OpenAI API
```

**Weitere Sicherheitsmassnahmen:**
- Prompt Injection Prevention: Nutzereingaben werden durch ein Sanitization-Layer gefuhrt
- Content Filtering: KI-Output wird auf kindgerechte Inhalte gepruft
- Rate Limiting: Per-User, Per-IP als Doppelschutz
- Input-Validierung: Zod-Schemas fur alle API-Eingaben
- Ausgabe-Validierung: KI-JSON-Output wird gegen erwartetes Schema validiert

**Prompt Injection Beispiel:**
```typescript
// SCHLECHT - direkte Nutzereingabe in System-Prompt
const prompt = `Party planen fuer: ${userInput}`

// GUT - Input wird strukturiert und begrenzt
const sanitized = sanitizeUserInput(userInput, { maxLength: 500, stripHtml: true });
const prompt = buildPartyPlanPrompt({ childInterests: sanitized });
```

### 3.5 Caching-Strategie

Nicht jede KI-Anfrage muss live generiert werden:

```
Caching-Layer:
  L1: Memory Cache (Next.js Request-Level)
      - Themen-Matching-Ergebnisse (gleiche Interessen -> gleicher Score)
  
  L2: Supabase Cache-Tabelle
      - Haufige Spiel-Generierungen (Dino + Outdoor + Alter 6 -> Cache 7 Tage)
      - Budget-Vorschlage fur Standardkombinationen
  
  Nicht gecacht:
      - Chat-Antworten (kontextabhangig)
      - Einladungstexte (personalisiert)
      - Kindprofil-Analysen (individuell)
```

### 3.6 Streaming-Implementierung

Fur Chat und Textgenerierung werden Server-Sent Events (SSE) verwendet:

```typescript
// src/app/api/ai/chat/route.ts
import { OpenAI } from 'openai';

export async function POST(request: Request) {
  // Auth-Check + Rate-Limit-Check
  const user = await getAuthenticatedUser(request);
  if (!user || user.tier !== 'pro') {
    return new Response('Unauthorized', { status: 401 });
  }

  const { message, planContext } = await validateBody(request);

  const stream = new ReadableStream({
    async start(controller) {
      const openai = new OpenAI({ apiKey: process.env.OPENAI_API_KEY });
      const completion = await openai.chat.completions.create({
        model: 'gpt-4o',
        messages: buildChatMessages(planContext, message),
        stream: true,
      });

      for await (const chunk of completion) {
        const text = chunk.choices[0]?.delta?.content ?? '';
        controller.enqueue(new TextEncoder().encode(`data: ${JSON.stringify({ text })}\n\n`));
      }
      controller.enqueue(new TextEncoder().encode('data: [DONE]\n\n'));
      controller.close();
    }
  });

  return new Response(stream, {
    headers: { 'Content-Type': 'text/event-stream', 'Cache-Control': 'no-cache' }
  });
}
```

---

## 4. Datenbankschema-Erweiterungen

### 4.1 Neue Tabellen fur KI-Features

```sql
-- Konversationsverlauf fur KI-Chat
CREATE TABLE public.ai_conversations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  plan_id UUID REFERENCES public.saved_plans(id) ON DELETE SET NULL,
  messages JSONB NOT NULL DEFAULT '[]',
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- KI-Nutzungs-Log fur Rate-Limiting und Abrechnung
CREATE TABLE public.ai_usage_log (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  feature TEXT NOT NULL,
  input_tokens INT NOT NULL DEFAULT 0,
  output_tokens INT NOT NULL DEFAULT 0,
  model TEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- KI-generierte Inhalte-Cache
CREATE TABLE public.ai_content_cache (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  cache_key TEXT UNIQUE NOT NULL,
  content JSONB NOT NULL,
  expires_at TIMESTAMPTZ NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Kindprofile (fur Personalisierung)
CREATE TABLE public.child_profiles (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  name TEXT NOT NULL,
  birth_date DATE,
  interests TEXT[],
  allergies JSONB,
  favorite_theme_slug TEXT REFERENCES public.themes(slug),
  ai_analysis JSONB,
  notes TEXT,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Post-Party-Feedback
CREATE TABLE public.party_feedback (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID NOT NULL REFERENCES public.saved_plans(id) ON DELETE CASCADE,
  user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
  what_worked TEXT,
  what_failed TEXT,
  notes_for_next_year TEXT,
  ai_insights JSONB,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);
```

### 4.2 Erweiterungen der WizardData-Typen

```typescript
// Erweiterung in src/types/index.ts

export interface ChildInterests {
  freeText: string;           // "Liebt Pferde, basteln, die Farbe blau"
  parsedKeywords: string[];   // ["Pferde", "Basteln", "Blau"] - KI-extrahiert
  temperament?: 'calm' | 'active' | 'mixed';
  shyness?: 'shy' | 'social' | 'mixed';
}

export interface WizardData {
  // Bestehende Felder...
  age: number;
  guestCount: number;
  location: LocationType;
  themeSlug: string;
  duration: number;
  budget: string;
  birthdayChildName: string;
  allergens: AllergenPreferences;
  guestNames: string[];

  // NEUE KI-Felder (optional, Pro-only)
  childInterests?: ChildInterests;
  childProfileId?: string;    // Referenz auf child_profiles-Tabelle
  aiPersonalizationEnabled?: boolean;
  partyDate?: string;         // ISO-Datum fur Aufgaben-Manager
}

export interface AIGeneratedContent {
  type: 'game' | 'recipe' | 'invitation' | 'schedule_optimization' | 'theme_suggestion';
  content: unknown;
  generatedAt: string;
  model: string;
  isVerified: boolean;        // true wenn manuell gepruft
}
```

---

## 5. Komponenten-Architektur (neue + geanderte Dateien)

### 5.1 Neue Komponenten

```
src/components/
  ai/
    AiChatPanel.tsx           - Chat-Seitenleiste in ResultView
    AiChatMessage.tsx         - Einzelne Chat-Nachricht (Streaming)
    AiGenerateButton.tsx      - Wiederverwendbarer "KI generieren" Button
    AiLoadingIndicator.tsx    - Animierter Lade-Indikator wahrend KI denkt
    AiContentBadge.tsx        - "KI-generiert" Badge auf Inhalten
    PersonalizationInput.tsx  - Freitextfeld im Wizard fur Kindinteressen
    ThemeRecommendations.tsx  - KI-Themen-Vorschlage nach Interesseneingabe
  child-profile/
    ChildProfileForm.tsx
    ChildProfileCard.tsx
    ChildSelector.tsx
  budget/
    BudgetOptimizer.tsx       - KI-Budgetoptimierung Anzeige
```

### 5.2 Geanderte Komponenten

```
src/components/wizard/PartyWizard.tsx
  - Step 1: PersonalizationInput hinzufugen (Pro, optional)
  - Schnell-Modus Toggle (NLU-Eingabe)
  - ChildSelector integrieren

src/components/result/ResultView.tsx
  - AiChatPanel als ausklappbares Seitenpanel (Pro)
  - KI-Buttons in einzelnen Tabs
  - "KI-generiert" Badge System

src/components/result/tabs/GamesTab.tsx
  - "KI-Spiel generieren" Button (Pro)
  - KI-generierte Spiele mit AiContentBadge

src/components/result/tabs/FoodTab.tsx
  - "KI-Alternatives Rezept" Button (Pro)
  - Allergie-Konfliktwarnungen

src/components/result/tabs/InvitationTab.tsx
  - "KI-Einladung schreiben" Bereich (Pro)
  - 3 Varianten anzeigen, eine auswahlen

src/components/result/tabs/ScheduleTab.tsx
  - "Zeitplan optimieren" Button (Pro)
  - KI-Optimierungshinweise anzeigen
```

### 5.3 Neue API-Routen

```
src/app/api/ai/
  parse-wizard/route.ts       - NLU-Wizard-Parsing
  personalize/route.ts        - Personalisierungsanalyse
  generate-game/route.ts      - Spiel generieren
  generate-recipe/route.ts    - Rezept generieren
  generate-invitation/route.ts - Einladungstext generieren
  optimize-schedule/route.ts  - Zeitplan optimieren
  chat/route.ts               - Chat-Endpunkt (SSE-Streaming)
  suggest-themes/route.ts     - Themen-Vorschlage
  optimize-budget/route.ts    - Budgetoptimierung
```

---

## 6. Implementierungsplan (Phasen)

### Phase 1: KI-Foundation (3-4 Tage)

**Ziel:** Sicheres, kosteneffizientes KI-Fundament aufbauen.

**Tasks:**
1. `npm install openai zod` - Dependencies
2. `src/lib/ai/provider.ts` - Provider-Abstraktion
3. `src/lib/ai/openai.ts` - OpenAI-Implementierung
4. `src/lib/ai/rate-limiter.ts` - Rate-Limiting-Logik
5. `src/lib/ai/prompts.ts` - Alle System-Prompts zentralisiert
6. `src/lib/ai/sanitizer.ts` - Input-Sanitization gegen Prompt-Injection
7. Datenbankmigrationen: `ai_usage_log`, `ai_content_cache`, `child_profiles`, `party_feedback`
8. Umgebungsvariablen: `OPENAI_API_KEY`, `AI_RATE_LIMIT_ENABLED=true`
9. `src/components/ai/AiLoadingIndicator.tsx`
10. `src/components/ai/AiContentBadge.tsx`

**Abnahmekriterium:** Ein Test-API-Call an `/api/ai/generate-game` liefert valides JSON zuruck, Auth wird gepruft, Rate-Limit wird protokolliert.

---

### Phase 2: Kinder-Personalisierung und Themen-Vorschlage (2-3 Tage)

**Ziel:** Wizard wird intelligent - kennt das Kind.

**Tasks:**
1. `PersonalizationInput.tsx` - Freitextfeld in Wizard Step 1
2. `WizardData`-Typ um `childInterests` erweitern
3. `ThemeRecommendations.tsx` - erscheint nach Interesseneingabe
4. `/api/ai/suggest-themes` Route
5. `/api/ai/personalize` Route (analysiert Interessen)
6. `ChildProfileForm.tsx` und `ChildSelector.tsx`
7. Pro-Gate: Personalisierungs-Features hinter `useFeatureGate('ai_personalization')`

**Abnahmekriterium:** Eingabe "Liebt Dinosaurier und Basteln" fuhrt zu Theme-Vorschlag "Dino" (Top 1) und alternativem Custom-Thema.

---

### Phase 3: KI-Spielgenerierung und Rezeptgenerator (2-3 Tage)

**Ziel:** Inhalt ist nicht mehr limitiert auf die Datenbank.

**Tasks:**
1. `/api/ai/generate-game` Route
2. `AiGenerateButton.tsx` wiederverwendbarer Button
3. Integration in `GamesTab.tsx`
4. `/api/ai/generate-recipe` Route
5. Integration in `FoodTab.tsx` (Allergie-Kontext mitgeben)
6. Output-Validierung mit Zod-Schemas
7. Cache-Logik fur haufige Kombinationen

**Abnahmekriterium:** "Dino + Outdoor + 6 Jahre + glutenfrei" liefert ein neues, valides Spiel und ein glutenfreies Dino-Rezept mit vollstandigen Zutaten.

---

### Phase 4: KI-Einladungstext-Generator (1-2 Tage)

**Ziel:** Einladungen werden persoenlich.

**Tasks:**
1. `/api/ai/generate-invitation` Route (3 Varianten)
2. UI-Erweiterung in `InvitationTab.tsx`
3. Varianten-Auswahl-Interface
4. Stil-Auswahl (lustig / klassisch / kreativ)

**Abnahmekriterium:** Drei unterschiedliche Einladungstexte werden generiert, davon mindestens einer mit dem Kindnamen personalisiert.

---

### Phase 5: KI-Chat-Assistent (3-4 Tage)

**Ziel:** Eltern haben immer einen Experten an ihrer Seite.

**Tasks:**
1. `/api/ai/chat` Route mit SSE-Streaming
2. `AiChatPanel.tsx` - ausklappbares Chat-Panel
3. `AiChatMessage.tsx` - mit Streaming-Rendering
4. Session-Konversationsverlauf im React-State
5. System-Prompt mit vollstandigem Plan-Kontext
6. Token-Budget-Anzeige (optional: wie viele Anfragen noch)
7. Integration in `ResultView.tsx` als floating button

**Abnahmekriterium:** Chat-Antwort erscheint streaming (wortweise), kennt den aktuellen Plan, antwortet auf Deutsch wenn App auf Deutsch eingestellt.

---

### Phase 6: Zeitplan-Optimierung und Budgetoptimierung (2-3 Tage)

**Ziel:** Intelligente Planoptimierung uber KI.

**Tasks:**
1. `/api/ai/optimize-schedule` Route
2. `/api/ai/optimize-budget` Route
3. UI in `ScheduleTab.tsx` und Result-Aktionsbereich
4. Optimierungshinweise visuell hervorheben
5. `BudgetOptimizer.tsx`

---

### Phase 7: Post-Party-Modul und Kindprofil-Lernen (2 Tage)

**Ziel:** App wird uber Jahre intelligenter fur jede Familie.

**Tasks:**
1. `/api/ai/post-party-analysis` Route
2. Post-Party-UI (erscheint nach gespeichertem `partyDate`)
3. Kindprofil-Update basierend auf Feedback
4. `party_feedback` Tabelle und Migration

---

## 7. Strukturanderungen aus Softwarearchitekten-Perspektive

### 7.1 Current State (Ist)

```
Frontend-only Logik
  WizardData -> sessionStorage -> Datenbank-Abfragen -> statische Berechnung -> UI

Probleme:
  - Keine Intelligenz: gleiche Inputs -> immer gleicher Output
  - Kein Kontext: App kennt Kind nicht
  - Statische Templates: 14 Themes x 1 Rezept = 14 Rezepte total
  - Keine Lernfahigkeit
```

### 7.2 Target State (Soll)

```
Hybrid Intelligence Architecture
  
  ┌─────────────────────────────────────────────────────────────┐
  │  Data Layer (Supabase)                                       │
  │  Backbone: Themes, Games, Recipes, FoodItems (statisch)      │
  │  + Child Profiles, AI Conversations, AI Usage Log (dynamisch)│
  └─────────────────────────────────────────────────────────────┘
           │                              │
  ┌────────▼──────────┐         ┌────────▼──────────────────┐
  │  Static Engine    │         │  AI Enhancement Layer      │
  │  (bestehend)      │         │  (neu, additiv)            │
  │                   │         │                            │
  │  - Template-      │         │  - Personalisierung        │
  │    Spiele         │         │  - Generierung             │
  │  - Mengen-        │         │  - Optimierung             │
  │    rechnung       │         │  - Chat-Assistent          │
  │  - Schedule-      │         │  - NLU-Parsing             │
  │    Generierung    │         │                            │
  └───────────────────┘         └────────────────────────────┘
           │                              │
           └──────────────┬───────────────┘
                          │
  ┌───────────────────────▼──────────────────────────────────────┐
  │  Result Layer (React UI)                                      │
  │  - Statische Template-Inhalte (immer verfugbar)               │
  │  - KI-Enhanced Inhalte (Pro-Feature, additiv, nicht ersetzend)│
  │  - Klare visuelle Trennung: KI-Badge auf KI-generierten Items │
  └──────────────────────────────────────────────────────────────┘
```

**Schlussel-Designentscheidung:** KI **erganzt** den statischen Engine, ersetzt ihn **nicht**.
- Free-Nutzer sehen immer noch vollstandige, gute Plane (statisch)
- Pro-Nutzer sehen denselben Plan + KI-Verbesserungen
- App funktioniert auch bei KI-API-Ausfall (Fallback auf statisch)

### 7.3 Neue Verzeichnisstruktur

```
src/
  lib/
    ai/                        NEU - KI-Logik (server-only, kein "use client")
      provider.ts              - Provider-Abstraktion
      openai.ts                - OpenAI-Implementierung
      anthropic.ts             - Anthropic-Fallback (optional)
      rate-limiter.ts          - Rate-Limiting
      sanitizer.ts             - Input-Sanitization
      prompts/                 - System-Prompts nach Feature
        game-generator.ts
        recipe-generator.ts
        invitation-writer.ts
        chat-assistant.ts
        wizard-parser.ts
        schedule-optimizer.ts
      schemas/                 - Zod-Schemas fur KI-Outputs
        game.schema.ts
        recipe.schema.ts
        invitation.schema.ts
    data.ts                    UNVERANDERT - Datenbank-Abfragen
    plan-generator.ts          UNVERANDERT - Statische Berechnungen
    feature-gates.ts           NEU - Feature-Gate-Konstanten
  
  app/
    api/
      ai/                      NEU - KI-API-Routen
        parse-wizard/route.ts
        personalize/route.ts
        generate-game/route.ts
        generate-recipe/route.ts
        generate-invitation/route.ts
        optimize-schedule/route.ts
        chat/route.ts
        suggest-themes/route.ts
        optimize-budget/route.ts
      stripe/                  NEU (aus Free/Pro Konzept)
        checkout/route.ts
        webhook/route.ts
  
  components/
    ai/                        NEU - KI-UI-Komponenten
      AiChatPanel.tsx
      AiChatMessage.tsx
      AiGenerateButton.tsx
      AiLoadingIndicator.tsx
      AiContentBadge.tsx
      PersonalizationInput.tsx
      ThemeRecommendations.tsx
    child-profile/             NEU
    upgrade/                   NEU
```

### 7.4 Umgebungsvariablen (neue)

```bash
# .env.local (nie committen)
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4o
AI_RATE_LIMIT_ENABLED=true
AI_MONTHLY_TOKEN_BUDGET_FREE=0       # Free-Nutzer: kein KI-Zugriff
AI_MONTHLY_TOKEN_BUDGET_PRO=500000   # Pro-Nutzer: 500k Tokens/Monat

# Stripe
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
STRIPE_PRICE_ID_MONTHLY=price_...
STRIPE_PRICE_ID_YEARLY=price_...
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...

# Email (fur RSVP und Aufgaben-Erinnerungen)
RESEND_API_KEY=re_...
FROM_EMAIL=noreply@geburtstagspilot.de
```

---

## 8. Qualitats- und Sicherheitsstandards fur KI-Features

### 8.1 KI-Output-Qualitatsstandards

Jeder KI-generierte Inhalt muss folgende Kriterien erfullen:

- **Vollstandigkeit:** Alle Pflichtfelder sind befult (Zod-Validierung)
- **Kindgerechtigkeit:** Keine ungeeigneten Inhalte (System-Prompt-Guardrails)
- **Sprachkorrektheit:** Deutscher Text ist grammatikalisch korrekt (GPT-4o-Standard)
- **Realisierbarkeit:** Rezept-Zutaten sind kauflich, Spiele mit erklartem Material durchfuhrbar
- **Transparenz:** Jeder KI-generierte Inhalt tragt ein `AiContentBadge`

### 8.2 Fallback-Verhalten

```typescript
// Wenn KI-API nicht verfugbar: Fallback auf statischen Content
async function getGameWithAiFallback(params: GameParams): Promise<Game> {
  try {
    const aiGame = await generateAiGame(params);
    return aiGame;
  } catch (error) {
    console.error('AI game generation failed, falling back to database', error);
    return getRandomGameFromDatabase(params);
  }
}
```

### 8.3 Datenschutz und DSGVO

- Kindnamen und Interessen werden **niemals** an OpenAI als identifizierbare Personendaten ubertragen
- Vor API-Call: Pseudonymisierung (Vorname -> "das Geburtstagskind", Interessen bleiben generisch)
- Nutzer muss explizit zustimmen, dass Eingaben zur KI-Verarbeitung gesendet werden (einmalige Zustimmung beim ersten KI-Feature-Aufruf)
- Konversationsverlauf kann jederzeit geloscht werden
- OpenAI-Datenprozessierungsvertrag (DPA) muss abgeschlossen sein

---

## 9. Priorisierung und MVP-KI

Nicht alle 10 Features mussen gleichzeitig implementiert werden. Priorisierung nach Business-Impact:

| Prioritat | Feature | Begrundung |
|---|---|---|
| P1 | KI-Chat-Assistent | Hochste wahrgenommene Wert, starkes Pro-Argument |
| P1 | Kinder-Interessen-Profiler | Loest Problem #1 der Nutzer, differenzierend |
| P2 | KI-Einladungstext | Schnell implementiert, klarer sichtbarer Wert |
| P2 | KI-Spielgenerierung | Loest Problem "immer gleiche Spiele" |
| P3 | Themen-Vorschlage KI | Gut fur Onboarding, nicht kritisch |
| P3 | Zeitplan-Optimierung | Nischenfeature fur organisierte Eltern |
| P4 | Rezept-Generator | Gut fur Allergiker, komplexere Validierung |
| P4 | Budget-Optimierung | Nischenfeature |
| P5 | NLU-Wizard-Modus | Nett to have, erfordert gute UX fur Fallback |
| P5 | Post-Party-Modul | Langfristige Retention, kein sofortiger Wert |

**MVP-KI (Phase 1-4 implementiert):**
- Chat-Assistent + Kinder-Interessen-Profiler + Einladungstext + Spielgenerierung
- Das reicht fur einen starken "KI-powered" Marketing-Claim
- Implementierungszeit: ~10-14 Tage

## ./docs/MARKETINGKONZEPT.md
# Geburtstagspilot - Marketingkonzept

**Erstellt von:** Marketingexperte (Onlinemarketing, 30+ Jahre Erfahrung)
**Stand:** Mai 2026
**Version:** 1.0

---

## 1. Executive Summary

Geburtstagspilot ist eine browserbasierte SaaS-App, die Eltern in unter 5 Minuten einen kompletten Kindergeburtstag plant. Die App adressiert ein universelles, wiederkehrendes Elternproblem im DACH-Raum (ca. 5,8 Mio. Geburtstage pro Jahr, Kinder 3-12).

**Kernversprechen:** "3 Stunden Spass. 5 Minuten Planung."

**Positionierung:** Geburtstagspilot ist kein Blog, keine Ideensammlung, kein Pinterest-Board. Es ist das erste interaktive Planungstool, das den gesamten Kindergeburtstags-Workflow in einem durchgaengigen Wizard abbildet und einen druckfertigen Komplettplan liefert.

---

## 2. Zielgruppenanalyse

### 2.1 Primaere Zielgruppe

| Merkmal | Beschreibung |
|---|---|
| Alter | 28-42 Jahre |
| Geschlecht | 70% Muetter, 30% Vaeter (Planungsverantwortung) |
| Region | DACH (Primaer DE, Sekundaer AT/CH) |
| Einkommen | Mittelschicht, doppelverdienernd |
| Digital-Affinitaet | Hoch, Mobile-First, Social-Media-aktiv |
| Schmerzpunkt | Zeitmangel + Perfektionsdruck + jaehrliche Wiederholung |

### 2.2 Sekundaere Zielgruppen

- Grosseltern (planen fuer Enkel)
- Tanten/Onkel, Paten (unterstuetzen bei der Planung)
- Tagespflege-Einrichtungen, KiTas (Gruppenfeiern)
- Event-Planer (professionelle Kinderpartys)

### 2.3 User Personas

**Persona 1: "Gestresste Sarah" (Kernzielgruppe)**
- 34 Jahre, 2 Kinder (4 + 7), berufstaetig
- Plant den Geburtstag eine Woche vorher
- Hat Pinterest geoeffnet, 47 Tabs, keinen Plan
- Will: Schnelle Loesung, kein Recherche-Aufwand, alles aus einer Hand

**Persona 2: "Perfektionist Thomas"**
- 38 Jahre, 3 Kinder, teilt sich die Planung mit Partnerin
- Will alles durchstrukturiert, zeitlich getaktet
- Schaetzt den Minutenplan, die Einkaufsliste, die Mengenberechnung
- Will: Kontrolle, Anpassbarkeit, Druckfunktion

**Persona 3: "Erstmal-Mama Lisa"**
- 30 Jahre, 1 Kind (wird 4), erster Geburtstag mit Gaesten
- Unsicher, was man braucht, wie viel man kauft
- Will: Orientierung, Vorschlaege, einfache Schritt-fuer-Schritt-Anleitung

---

## 3. Wettbewerbsanalyse

### 3.1 Direkte Wettbewerber

| Anbieter | Staerke | Schwaeche | Differenzierung GP |
|---|---|---|---|
| Pinterest | Inspiration, visuell | Unstrukturiert, kein Planungstool | GP liefert fertigen Plan, nicht Ideen |
| Mama-Blogs | SEO-Traffic, Vertrauen | Fragmentiert, jeder Blog anders | GP buendelt alles in einer App |
| Kindergeburtstag.or.at | Spielesammlung | Nur Spiele, kein Plan | GP deckt 8 Kategorien ab |
| ChatGPT/KI direkt | Flexibel | Keine Struktur, kein Speichern | GP hat DB mit 80+ Spielen, Rezepte, Mengen |

### 3.2 Strategischer Vorteil

**Es gibt keinen direkten Wettbewerber im DACH-Raum**, der den gesamten Planungsprozess (Wizard > Zeitplan > Spiele > Essen > Einkaufsliste > Einladung > Mitgebsel > Gaesteliste) in einer interaktiven Web-App abbildet.

---

## 4. Branding & Visuelle Identitaet

### 4.1 Markenname

**Geburtstagspilot** - stark, einpraegsam, deutsch, sofort verstaendlich.
- "Geburtstag" = Keyword, SEO-relevant
- "Pilot" = Fuehrung, Navigation, Steuerung (Eltern werden durch den Prozess navigiert)

### 4.2 Farbpalette

| Farbe | Hex | Verwendung |
|---|---|---|
| Party-Purple | #7C3AED | Primaerfarbe, CTA-Buttons, Branding |
| Party-Yellow | #FBBF24 | Akzente, Pro-Badge, Dark-Mode-Highlight |
| Party-Mint | #34D399 | Erfolg, abgehakte Items, positive Aktionen |
| Party-Coral | #F87171 | Warnungen, Herz-Icon |
| Party-Cream | #FFFDF7 | Hintergrund Light-Mode (warm, einladend) |
| Party-Pink | #F472B6 | Gradient-Akzent |

**Bewertung:** Die Farbpalette ist festlich, warm und differenziert sich stark von den typischen blauen SaaS-Designs. Party-Purple als Leitfarbe ist einpraegsam und geschlechtsneutral.

### 4.3 Typografie

- **Nunito** (Google Fonts): Rund, freundlich, gut lesbar auf allen Geraeten
- **Bewertung:** Hervorragende Wahl fuer eine Eltern-App. Warm, nicht zu verspielt, professionell genug fuer Pro-Tier.

### 4.4 Logo & Favicon

- Aktuell: Ballon-Emoji (🎈) als SVG-Favicon
- **Empfehlung:** Das Emoji-Favicon ist funktional, aber fuer professionelles Branding sollte ein eigenes SVG-Logo entwickelt werden (Ballon + Kompass/Pilot-Motiv). Fuer V1 ist das Emoji akzeptabel.

---

## 5. Conversion-Funnel & User Journey

### 5.1 AIDA-Modell angewendet

```
ATTENTION   → SEO-Landing, Social Ads, Word-of-Mouth
INTEREST    → Homepage: Hero, Features, Testimonials, Pricing
DESIRE      → Wizard: Sofort loslegen, kein Account noetig
ACTION      → Ergebnis: Plan sehen, speichern (→ Account), upgraden (→ Pro)
```

### 5.2 Conversion-Punkte

| Punkt | Trigger | Ziel |
|---|---|---|
| Homepage → Wizard | CTA "Jetzt planen" | Nutzer startet den Wizard |
| Wizard → Ergebnis | "Plan erstellen!" Button | Nutzer sieht den fertigen Plan |
| Ergebnis → Account | "Plan speichern" Button | Nutzer registriert sich |
| Free → Pro | 3-Plan-Limit erreicht / KI-Feature | Nutzer upgraded |
| Plan → Share | "Plan teilen" Button | Viralitaet, neue Nutzer |

### 5.3 Kritische UX-Metriken

| Metrik | Zielwert | Messung |
|---|---|---|
| Time-to-First-Plan | < 3 Minuten | Analytics: Wizard Start → Result |
| Wizard Completion Rate | > 70% | Step 1 → Step 7 |
| Bounce Rate Homepage | < 40% | GA4 |
| Mobile Usability Score | > 90 | Lighthouse |
| CTA Click Rate | > 8% | "Jetzt planen" Button |

---

## 6. Mobile-First UX-Audit & Redesign-Massnahmen

### 6.1 Identifizierte Probleme

| # | Problem | Schwere | Loesung |
|---|---|---|---|
| M1 | Mobile Hamburger-Menu hat keinen Overlay/Backdrop | Mittel | Fullscreen-Overlay mit Backdrop hinzufuegen |
| M2 | Tab-Leiste im Result scrollt horizontal, Labels versteckt auf Mobile | Hoch | Scrollable mit visuellen Scroll-Hinweisen + Icon-only auf Mobile |
| M3 | Hero-Section CTA-Buttons zu breit auf kleinen Screens | Mittel | Full-width auf Mobile, kompaktere Padding |
| M4 | Wizard Step-Icons Connector-Lines brechen auf Mobile | Niedrig | Connector ausblenden auf < sm |
| M5 | Footer 4-Spalten-Grid auf Mobile nicht optimal | Mittel | Accordion oder 2-Spalten auf Mobile |
| M6 | Result-Actions Buttons wrappen unschoen | Mittel | Sticky Bottom-Bar auf Mobile |
| M7 | Kein "Zurueck nach oben" Button | Niedrig | Scroll-to-Top FAB |
| M8 | Share-URL Box bricht auf kleinen Screens | Niedrig | Besseres Wrapping |

### 6.2 Umgesetzte Redesign-Massnahmen

**M1: Mobile Menu Overlay**
- Fullscreen-Overlay mit semi-transparentem Backdrop
- Smooth Slide-in Animation
- Body-Scroll-Lock wenn Menu offen
- Groessere Touch-Targets (48px)

**M2: Mobile Result-Tab Verbesserung**
- Horizontaler Scroll mit Gradient-Fade als Scroll-Hinweis
- Tab-Labels auf Mobile immer sichtbar (kompakter)
- Aktiver Tab scrollt automatisch in den sichtbaren Bereich

**M6: Sticky Action Bar**
- Fixierte Bottom-Bar mit den 4 Hauptaktionen auf Mobile
- Nur auf der Result-Seite sichtbar
- Verschwindet beim Scrollen nach unten, erscheint beim Hochscrollen

---

## 7. SEO-Strategie

### 7.1 Primaere Keywords (DE)

| Keyword | Suchvolumen (geschaetzt) | Schwierigkeit |
|---|---|---|
| kindergeburtstag planen | 12.000/Monat | Mittel |
| kindergeburtstag spiele | 22.000/Monat | Hoch |
| kindergeburtstag ideen | 18.000/Monat | Hoch |
| kindergeburtstag essen | 8.000/Monat | Mittel |
| kindergeburtstag einladung | 14.000/Monat | Hoch |
| kindergeburtstag einkaufsliste | 2.000/Monat | Niedrig |
| kindergeburtstag zeitplan | 1.500/Monat | Niedrig |
| kindergeburtstag motto | 6.000/Monat | Mittel |

### 7.2 SEO-Massnahmen

- **Meta-Tags:** Title und Description fuer jede Seite optimieren
- **Strukturierte Daten:** FAQ-Schema auf Homepage, HowTo-Schema fuer Wizard
- **Content-Hub (V2):** Blog mit Ratgebern zu jedem Motto (SEO-Traffic)
- **Internal Linking:** Wizard-Schritte → Ergebnis-Tabs → Upgrade
- **Open Graph / Social Cards:** Vorschaubilder fuer geteilte Plaene

### 7.3 Technisches SEO

- Server-side Rendering (Next.js SSR) fuer alle oeffentlichen Seiten
- Sitemap.xml automatisch generieren
- robots.txt konfigurieren
- Core Web Vitals optimieren (LCP < 2.5s, CLS < 0.1)
- Mobile-friendly (responsive, touch-optimiert)

---

## 8. Social-Media-Strategie

### 8.1 Kanalauswahl

| Kanal | Prioritaet | Zielgruppe | Content-Typ |
|---|---|---|---|
| Instagram | Hoch | Muetter 28-38 | Reels, Stories, Carousel |
| Pinterest | Hoch | Planungs-orientierte Eltern | Pins zu Mottos, Spielen, Rezepten |
| Facebook | Mittel | Eltern-Gruppen, 30-45 | Gruppen-Posts, Ads |
| TikTok | Mittel | Juengere Eltern 25-35 | Kurzvideos "5 Minuten Party planen" |
| LinkedIn | Niedrig | B2B (KiTas, Eventplaner) | Produktankuendigung |

### 8.2 Content-Plan (Monatlich)

| Woche | Typ | Beispiel |
|---|---|---|
| 1 | How-To Reel | "So planst du einen Piraten-Geburtstag in 5 Minuten" |
| 2 | User Story | Testimonial-Carousel mit Screenshots |
| 3 | Motto-Highlight | "Top 5 Spiele fuer den Einhorn-Geburtstag" |
| 4 | Product Feature | "Neu: KI-Spielvorschlaege jetzt verfuegbar" |

### 8.3 Paid Ads Strategie

**Budget-Empfehlung Start:** 500 EUR/Monat (Instagram + Facebook)

**Targeting:**
- Eltern mit Kindern 3-12 in DE/AT/CH
- Interessen: Kindergeburtstag, Partyplanung, DIY, Familienaktivitaeten
- Lookalike: Basierend auf registrierten Nutzern (ab 100 Conversions)

**Ad-Formate:**
- Carousel: Feature-Showcase (8 Tabs)
- Video (15s): "Vorher/Nachher" (Chaos → Plan in 5 Min)
- Lead-Ad: "Kostenlos deinen Party-Plan erstellen"

---

## 9. Viralitaets-Mechanismus

### 9.1 Eingebaute Viralitaet

| Mechanismus | Status | Beschreibung |
|---|---|---|
| Share-Link | Implementiert | Geteilte Plaene sind oeffentlich zugaenglich |
| WhatsApp-Teilen | Implementiert | Einladungen per WhatsApp versenden |
| Referral (V2) | Geplant | "Empfehle Geburtstagspilot und erhalte Pro gratis" |
| Social Proof | Implementiert | Testimonials auf Homepage |

### 9.2 Word-of-Mouth Trigger

- Der Plan selbst ist das Marketing: Wenn Eltern den Plan anderen Eltern zeigen, sehen diese die Quelle
- Einladungen tragen ein dezentes "Erstellt mit Geburtstagspilot" Branding
- Geteilte Links fuehren auf eine gebrandete Share-Seite

---

## 10. Monetarisierung & Pricing

### 10.1 Aktuelles Modell

| Tier | Preis | Limits |
|---|---|---|
| Free | 0 EUR | 3 Plaene, Basis-Features |
| Pro | 1,99 EUR/Monat oder 14,99 EUR/Jahr | 50 Plaene, KI-Features, Sharing |

### 10.2 Bewertung

- **Free-Tier ist grosszuegig genug** fuer Single-Use (1 Party = 1 Plan)
- **3-Plan-Limit** trifft Eltern mit mehreren Kindern (natuerlicher Upgrade-Trigger)
- **KI-Features** als Pro-Gating ist stark (nicht bypassbar, hoher wahrgenommener Wert)
- **Preis ist niedrig** (bewusst, Marktdurchdringung vor Margenoptimierung)

### 10.3 Upsell-Strategie

1. **In-App Nudges:** Dezente Hinweise auf Pro-Features beim Nutzen des Free-Plans
2. **Feature Teaser:** Pro-Features sichtbar aber ausgegraut (FOMO)
3. **Limit-Trigger:** Klare Meldung bei 3. Plan gespeichert
4. **Trial (V2):** 7-Tage Pro-Trial nach Registrierung

---

## 11. Launch-Plan

### Phase 1: Soft Launch (Woche 1-2)
- App auf Vercel deployen
- 10-20 Beta-Tester (Freunde, Familie) einladen
- Feedback sammeln, kritische Bugs fixen
- Google Search Console + Analytics einrichten

### Phase 2: Organic Launch (Woche 3-6)
- SEO-optimierte Meta-Tags live
- Instagram/Pinterest Accounts erstellen
- 3-4 Mottobezogene Posts pro Woche
- In 5 relevante Facebook-Gruppen posten (keine Werbung, Mehrwert bieten)

### Phase 3: Paid Launch (Woche 7-12)
- Facebook/Instagram Ads starten (500 EUR/Monat)
- A/B Tests: Verschiedene Ad-Creatives und Landing Pages
- Retargeting: Nutzer die Wizard gestartet aber nicht abgeschlossen haben
- Conversion-Optimierung basierend auf Daten

### Phase 4: Growth (ab Monat 4)
- Content-Marketing (Blog zu jedem Motto)
- Influencer-Kooperationen (Mama-Blogger)
- Referral-Programm implementieren
- PR: Pressemitteilung an Eltern-Magazine

---

## 12. KPI-Dashboard

| KPI | Ziel Monat 1 | Ziel Monat 3 | Ziel Monat 6 |
|---|---|---|---|
| Registrierungen | 100 | 500 | 2.000 |
| Erstellte Plaene | 300 | 1.500 | 6.000 |
| Wizard Completion Rate | 60% | 70% | 75% |
| Pro Conversions | 5 | 25 | 100 |
| MRR | 10 EUR | 50 EUR | 200 EUR |
| Organic Traffic | 500 | 2.000 | 8.000 |
| Social Followers | 100 | 500 | 2.000 |

---

## 13. Technische Marketing-Integration

### 13.1 Analytics

- **Google Analytics 4:** Events fuer Wizard-Steps, Plan-Erstellung, Registrierung, Pro-Upgrade
- **Conversion-Tracking:** Facebook Pixel, Google Ads Tag
- **Heatmaps (V2):** Hotjar oder Microsoft Clarity fuer UX-Optimierung

### 13.2 E-Mail-Marketing (V2)

| Trigger | E-Mail | Ziel |
|---|---|---|
| Registrierung | Willkommen + erster Plan | Aktivierung |
| 3 Tage inaktiv | "Dein Plan wartet" | Re-Engagement |
| 3. Plan gespeichert | "Schalte unbegrenzte Plaene frei" | Upsell |
| Geburtstag in 4 Wochen | "Zeit zu planen!" (wenn Datum bekannt) | Retention |

### 13.3 Open Graph Tags

Jede geteilte Seite sollte optimierte OG-Tags haben:
- `og:title`: "Partyplan fuer [Name]s [Alter]. Geburtstag"
- `og:description`: "Erstellt mit Geburtstagspilot - Kompletter Kindergeburtstag in 5 Minuten"
- `og:image`: Dynamisch generiertes Vorschaubild mit Motto-Emoji und Partyfarben

---

## 14. Zusammenfassung der UX-Redesign-Massnahmen

Folgende Verbesserungen werden im Rahmen dieses Konzepts implementiert:

1. **Mobile Navigation Overlay:** Fullscreen-Menu mit Backdrop statt einfachem Dropdown
2. **Homepage Hero:** Optimierte CTA-Buttons fuer Mobile, besserer visueller Hierarchie
3. **Wizard Step-Indicator:** Bessere Mobile-Darstellung mit kompakten Steps
4. **Result Tabs:** Scrollbare Tab-Leiste mit Gradient-Fade-Hinweisen
5. **Sticky Mobile Actions:** Fixierte Aktions-Leiste am unteren Bildschirmrand
6. **Scroll-to-Top Button:** FAB fuer lange Seiten
7. **Touch-Optimierung:** Mindestgroesse 44px fuer alle interaktiven Elemente (bereits vorhanden)
8. **Smooth Transitions:** Verbesserte Animationen fuer Seitenwechsel

---

*Dieses Konzept wird bei jeder groesseren Aenderung an der App aktualisiert.*

## ./docs/PROGRESS.md
# Geburtstagspilot - Implementierungsfortschritt

## Status: V1 Implementierung abgeschlossen + Auth/Pro Features

Stand: Mai 2026

---

## Umgesetzte Module (V1 + Erweiterungen)

### 1. Party Wizard (7 Schritte)
- Name und Alter (3-12 Jahre)
- Gaestezahl (3-20) mit optionalen Gaestenamen
- Ort (drinnen/draussen/beides)
- Motto (Themen aus Supabase geladen)
- Dauer (1.5-5 Stunden)
- Allergien/Diaeten (Glutenfrei, Vegan etc.) mit Freitextnotizen
- Budget (optional)
- Daten werden in sessionStorage gespeichert

### 2. Ergebnis-Ansicht (8 Tabs)
- **Aufgaben (TodoTab):** Checkliste fuer die Party-Vorbereitung
- **Zeitablauf (ScheduleTab):** Automatischer Minutenplan, farbcodiert, Startzeit anpassbar
- **Spiele (GamesTab):** 80+ Spiele, altersgerecht, aufklappbar, austauschbar
- **Essen & Kuchen (FoodTab):** Rezepte + Essensvorschlaege mit Mengenberechnung
- **Einkaufsliste (ShoppingTab):** Automatisch generiert, kategorisiert, abhakbar
- **Einladung (InvitationTab):** Thematische Vorlagen, Live-Vorschau, PDF/WhatsApp
- **Mitgebsel (GoodiesTab):** Budget-Stufen, Preis- und Mengenberechnung
- **Gaesteliste (GuestListTab):** Gaesteverwaltung

### 3. Authentifizierung & Benutzerverwaltung
- Supabase Auth (E-Mail/Passwort)
- Login/Registrierung/Callback Seiten
- AuthProvider mit Session-Management
- UserMenu mit Logout
- Profiltabelle mit Rollen (user/admin) und Tier (free/pro)

### 4. Dashboard & Planverwaltung
- Gespeicherte Plaene laden und anzeigen (PlanCard)
- Plaene speichern mit Tier-Limits (3 Free, 50 Pro)
- Plan-Sharing mit oeffentlichen Links (ShareToken)

### 5. Free/Pro Modell
- Feature-Gates fuer Pro-Features (feature-gates.ts)
- FeatureGate-Komponente, UpgradeBanner, UpgradeModal
- Pro-Anfrage Workflow (Admin-Genehmigung)
- Upgrade-Seite

### 6. KI-Features (Pro)
- AI Chat-Assistent (AiChatPanel)
- KI-Spielgenerierung (/api/ai/generate-game)
- KI-Einladungstexte (/api/ai/generate-invitation)
- OpenAI API Integration (provider.ts, prompts.ts)

### 7. Admin-Dashboard
- Benutzerstatistiken (Gesamt, Pro, Plaene)
- Pro-Anfragen verwalten (genehmigen/ablehnen)
- Navigation zu Benutzer-, Plan- und Anfragen-Listen

---

## Infrastruktur

### Datenbank (Supabase)
- PostgreSQL mit RLS auf allen Tabellen
- Tabellen: themes, games, recipes, food_items, goodie_bag_items, invitation_templates, profiles, saved_plans, pro_requests
- Custom enums: location_type, activity_level, food_category, budget_tier
- Seed-Daten: 14 Themen, 80+ Spiele, 14 Rezepte, 17 Essens-Artikel, 36+ Mitgebsel, 14 Einladungsvorlagen
- Migrationen in supabase/migrations/

### Internationalisierung (next-intl)
- Deutsch (Standardsprache) und Englisch
- Middleware-basierte Locale-Erkennung
- Alle Texte ueber useTranslations-Hook
- Sprachumschalter im Header

### Theming
- Light/Dark Mode mit localStorage-Persistenz
- Tailwind CSS v4 mit Custom Party-Farben
- Nunito als Schriftart

### Branding
- Party-Purple (#7C3AED) als Primaerfarbe
- SVG Favicon mit Ballon-Emoji
- Professionelle Homepage mit Hero, Features, How-It-Works, Testimonials

### Rechtliche Seiten
- Impressum (WAMOCON GmbH)
- Datenschutzerklaerung
- Allgemeine Geschaeftsbedingungen
- Links im Footer

---

## Verifikation

| Pruefung | Status |
|---|---|
| TypeScript (tsc --noEmit) | Bestanden |
| ESLint | Bestanden |
| Next.js Build | Bestanden |

---

## Bekannte Einschraenkungen / Hindernisse

1. **Middleware-Deprecation**: Next.js 16 zeigt eine Warnung, dass `middleware.ts` zugunsten von `proxy` veraltet ist. next-intl nutzt noch die Middleware-API. Funktioniert weiterhin, sollte aber bei einer next-intl-Aktualisierung migriert werden.

2. **PDF-Export**: Aktuell ueber `window.print()` implementiert. Eine dedizierte PDF-Bibliothek (z.B. pdf-lib) koennte fuer bessere Formatierung integriert werden.

3. **Keine Authentifizierung**: V1 ist ohne Login. Alle Daten sind lokal im Browser (sessionStorage). Fuer V2 koennte Supabase Auth hinzugefuegt werden.

4. **Keine persistente Speicherung**: Party-Plaene werden nicht serverseitig gespeichert. Beim Schliessen des Browsers gehen die Daten verloren.

5. **Supabase Docker muss laufen**: Die App benoetigt eine laufende lokale Supabase-Instanz fuer die Datenbankabfragen. Fuer Produktion muss auf eine gehostete Supabase-Instanz umgestellt werden.

---

## Dateistruktur

```
src/
  app/
    globals.css                    # Tailwind v4 mit Party-Theme
    layout.tsx                     # Root Layout
    page.tsx                       # Root Redirect
    [locale]/
      layout.tsx                   # Locale Layout mit Fonts, Dark Mode
      page.tsx                     # Homepage
      wizard/page.tsx              # Wizard-Seite
      result/page.tsx              # Ergebnis-Seite
      imprint/page.tsx             # Impressum
      privacy/page.tsx             # Datenschutz
      terms/page.tsx               # AGB
  components/
    layout/
      Header.tsx                   # Sticky Header mit Navigation
      Footer.tsx                   # Footer mit Legal-Links
    ui/
      LanguageSwitcher.tsx         # DE/EN Umschalter
      ThemeToggle.tsx              # Light/Dark Umschalter
    wizard/
      PartyWizard.tsx              # 6-Schritt Wizard
    result/
      ResultView.tsx               # Haupt-Ergebnis mit 6 Tabs
      tabs/
        ScheduleTab.tsx            # Zeitplan
        GamesTab.tsx               # Spiele
        FoodTab.tsx                # Essen & Kuchen
        ShoppingTab.tsx            # Einkaufsliste
        InvitationTab.tsx          # Einladung
        GoodiesTab.tsx             # Mitgebsel
  lib/
    supabase.ts                    # Client-seitiger Supabase-Client
    supabase-server.ts             # Server-seitiger Supabase-Client
    data.ts                        # Datenabruf-Funktionen
    plan-generator.ts              # Zeitplan- und Mengenberechnung
  types/
    index.ts                       # Alle TypeScript-Interfaces
  i18n/
    routing.ts                     # next-intl Routing-Konfiguration
    request.ts                     # Server-seitige Locale-Konfiguration
    navigation.ts                  # Navigations-Helfer
  messages/
    de.json                        # Deutsche Uebersetzungen
    en.json                        # Englische Uebersetzungen
  middleware.ts                    # next-intl Locale-Middleware
supabase/
  config.toml                      # Lokale Supabase-Konfiguration
  migrations/
    20260512120000_initial_schema.sql  # Datenbank-Schema
  seed.sql                         # Testdaten (80+ Spiele, etc.)
```

## ./docs/UX_UI_TODO.md
# Geburtstagspilot - UX/UI Todo List

Stand: Mai 2026

## Status-Legende
- ✅ Erledigt
- 🔄 In Arbeit
- ⬜ Offen
- 🔴 Dringend
- 🟡 Mittel
- 🟢 Niedrig

---

## Erledigte Korrekturen (diese Session)

| # | Aufgabe | Prioritaet | Status |
|---|---------|-----------|--------|
| 1 | HTML-Entity Icons (&#128228;) durch echte Emojis ersetzen | 🔴 | ✅ |
| 2 | Einheitlicher Pro-Anfrage-Flow (Admin-Genehmigung statt Stripe-Alert) | 🔴 | ✅ |
| 3 | Preise anpassen (1,99 EUR/Monat, 14,99 EUR/Jahr) | 🟡 | ✅ |
| 4 | "Werbung entfernen" Feature entfernen | 🟡 | ✅ |
| 5 | Gaesteliste: Interne Scrollbar entfernen | 🟡 | ✅ |
| 6 | "Ohne Motto" an erste Stelle setzen | 🟡 | ✅ |
| 7 | Partydauer: Mehr Optionen + Freiauswahl (1.5-8h) | 🟡 | ✅ |
| 8 | Zeitablauf: Gesamtdauer + Endzeit anzeigen | 🟡 | ✅ |
| 9 | Umlaut-Fehler in Seed-Daten korrigieren (Migration) | 🟡 | ✅ |
| 10 | Desktop Tab-Leiste: Kein Scroll, flex-wrap | 🔴 | ✅ |
| 11 | Einladung: Kontrastprobleme bei dunklem Hintergrund beheben | 🔴 | ✅ |
| 12 | Sektionen ein-/ausschaltbar (Essen, Einkaufsliste etc.) | 🟡 | ✅ |
| 13 | pro_requests DB-Tabelle fuer Admin-Workflow | 🟡 | ✅ |

---

## Offene UX/UI Verbesserungen

### Dringend (vor Launch)

| # | Aufgabe | Bereich | Status |
|---|---------|---------|--------|
| 14 | Stripe/Payment-Integration fuer Pro-Plan | Upgrade | ⬜ 🔴 |
| 15 | Admin-Dashboard: Pro-Anfragen verwalten (genehmigen/ablehnen) | Admin | ⬜ 🔴 |
| 16 | E-Mail-Benachrichtigung bei Pro-Statusaenderung | Backend | ⬜ 🔴 |
| 17 | Mobile Navigation: Hamburger-Menu fuer kleine Bildschirme | Layout | ⬜ 🔴 |
| 18 | PWA-Support (installierbar, offline-faehig) | Infra | ⬜ 🟡 |

### Mittel (Qualitaet)

| # | Aufgabe | Bereich | Status |
|---|---------|---------|--------|
| 19 | Drag & Drop fuer Zeitablauf-Reihenfolge | Zeitablauf | ⬜ 🟡 |
| 20 | Druckansicht (Print CSS) optimieren | Result | ⬜ 🟡 |
| 21 | Onboarding-Tour fuer Erstbenutzer | UX | ⬜ 🟡 |
| 22 | Dark Mode: Alle Komponenten visuell pruefen | Design | ⬜ 🟡 |
| 23 | Einladung: Mehr Hintergrund-Vorlagen (themenspezifisch) | Einladung | ⬜ 🟡 |
| 24 | Gaestemanagement: CSV-Import/-Export | Gaesteliste | ⬜ 🟡 |
| 25 | Benachrichtigungen/Toast-System fuer Aktionen | UX | ⬜ 🟡 |
| 26 | Lade-Skeleton fuer alle Seiten statt Spinner | UX | ⬜ 🟡 |
| 27 | Tastaturnavigation und Accessibility (WCAG 2.1) | A11y | ⬜ 🟡 |

### Niedrig (Nice-to-have)

| # | Aufgabe | Bereich | Status |
|---|---------|---------|--------|
| 28 | Animationen/Micro-Interactions verbessern | Design | ⬜ 🟢 |
| 29 | Feedback-Widget (In-App Bug-Report) | UX | ⬜ 🟢 |
| 30 | Mehrere Plaene gleichzeitig vergleichen | Dashboard | ⬜ 🟢 |
| 31 | Social-Media-Share (Instagram Story, Facebook) | Share | ⬜ 🟢 |
| 32 | Foto-Upload fuer Party-Nachbericht | Pro | ⬜ 🟢 |
| 33 | Kalender-Export (ICS-Datei) | Result | ⬜ 🟢 |
| 34 | Spiel-Bewertung nach der Party | Result | ⬜ 🟢 |
| 35 | Favoritenspiele speichern | Dashboard | ⬜ 🟢 |

---

## Architektur-Hinweise

- **Pro-Freischaltung**: Aktuell ueber Admin-Genehmigung. Spaeter Stripe-Integration moeglich.
- **KI-Features**: Benoetigen `OPENAI_API_KEY` Umgebungsvariable. Graceful Fallback wenn nicht gesetzt.
- **Section Toggle**: Zeitablauf ist immer sichtbar (Pflichttab). Alle anderen koennen deaktiviert werden.
- **Einladungskontrast**: Automatische Erkennung + manueller Textfarben-Picker verfuegbar.

## ./legal-docs/agb.md
# Allgemeine Geschäftsbedingungen (AGB)

Stand: {{MONAT}} {{JAHR}}

## § 1 Geltungsbereich

(1) Diese Allgemeinen Geschäftsbedingungen (nachfolgend „AGB") der WAMOCON GmbH, Mergenthalerallee 79 - 81, 65760 Eschborn (nachfolgend „Anbieter"), gelten für alle Verträge über die Nutzung der Software-as-a-Service-Plattform {{PROJEKTNAME}} (nachfolgend „Plattform"), die über die Website {{DOMAIN}} bereitgestellt wird.

(2) Die Plattform richtet sich an Unternehmen und gewerbliche Nutzer (nachfolgend „Auftraggeber") sowie deren Benutzer (nachfolgend „Nutzer"). Es handelt sich um ein B2B-Angebot. Verbraucher im Sinne des § 13 BGB sind nicht Zielgruppe dieses Angebots.

(3) Abweichende, entgegenstehende oder ergänzende AGB des Auftraggebers werden nicht Vertragsbestandteil, es sei denn, der Anbieter stimmt deren Geltung ausdrücklich schriftlich zu.

## § 2 Vertragsschluss

(1) Die Darstellung der Plattform und ihrer Funktionen auf der Website stellt kein verbindliches Angebot im Sinne des § 145 BGB dar, sondern eine Aufforderung zur Abgabe eines Angebots (invitatio ad offerendum).

(2) Der Auftraggeber gibt ein verbindliches Angebot zum Abschluss eines Nutzungsvertrages ab, indem er den Registrierungsprozess auf der Plattform abschließt und diese AGB akzeptiert.

(3) Der Vertrag kommt zustande, wenn der Anbieter das Angebot des Auftraggebers durch Freischaltung des Zugangs annimmt.

## § 3 Leistungsbeschreibung

(1) Der Anbieter stellt dem Auftraggeber die Plattform als Software-as-a-Service (SaaS) über das Internet zur Verfügung.

(2) Der genaue Funktionsumfang ergibt sich aus der jeweils aktuellen Leistungsbeschreibung auf der Website.

(3) Der Anbieter ist berechtigt, die Plattform weiterzuentwickeln, zu erweitern und anzupassen. Wesentliche Einschränkungen des Funktionsumfangs werden dem Auftraggeber vorab mitgeteilt.

## § 4 Nutzungsrechte

(1) Der Anbieter räumt dem Auftraggeber für die Vertragslaufzeit ein einfaches, nicht übertragbares, nicht unterlizenzierbares Recht zur Nutzung der Plattform ein.

(2) Der Auftraggeber darf die Plattform nur für eigene betriebliche Zwecke nutzen.

## § 5 Pflichten des Auftraggebers

(1) Der Auftraggeber ist verpflichtet, seine Zugangsdaten geheim zu halten und vor dem Zugriff Dritter zu schützen.

(2) Der Auftraggeber stellt sicher, dass die Nutzung der Plattform im Einklang mit geltendem Recht erfolgt.

## § 6 Verfügbarkeit

(1) Der Anbieter bemüht sich um eine Verfügbarkeit der Plattform von 99,5 % im Jahresmittel.

(2) Nicht als Ausfallzeit gelten geplante Wartungsarbeiten, die vorab angekündigt werden.

## § 7 Datenschutz

Die Verarbeitung personenbezogener Daten erfolgt gemäß der Datenschutzerklärung des Anbieters und den Bestimmungen der DSGVO.

## § 8 Haftung

(1) Der Anbieter haftet unbeschränkt für Schäden aus der Verletzung des Lebens, des Körpers oder der Gesundheit sowie bei Vorsatz und grober Fahrlässigkeit.

(2) Im Übrigen ist die Haftung auf den vertragstypischen, vorhersehbaren Schaden begrenzt.

## § 9 Vertragslaufzeit und Kündigung

(1) Der Vertrag wird auf unbestimmte Zeit geschlossen und kann von beiden Parteien mit einer Frist von einem Monat zum Monatsende gekündigt werden.

(2) Das Recht zur außerordentlichen Kündigung aus wichtigem Grund bleibt unberührt.

## § 10 Schlussbestimmungen

(1) Es gilt das Recht der Bundesrepublik Deutschland unter Ausschluss des UN-Kaufrechts.

(2) Gerichtsstand ist Eschborn, sofern der Auftraggeber Kaufmann ist.

(3) Sollten einzelne Bestimmungen dieser AGB unwirksam sein, bleibt die Wirksamkeit der übrigen Bestimmungen davon unberührt.

---

> **Hinweis:** Dies ist ein Muster. Ersetze alle `{{PLATZHALTER}}` mit den projektspezifischen Informationen. Lass die AGB vor Veröffentlichung von einem Juristen prüfen.

## ./legal-docs/company-stamp.md
# Firmenstempel / Company Stamp

## Deutsch

### WAMOCON GmbH

**Geschäftsführer:** Dipl.-Ing. Waleri Moretz

**Anschrift:**
Mergenthalerallee 79 - 81
65760 Eschborn
Deutschland

**Kontakt:**
Telefon: +49 6196 5838311
E-Mail: info@wamocon.com

**Registrierung:**
Handelsregister: Eschborn HRB 123666
USt-IdNr.: DE344930486

---

## English

### WAMOCON GmbH

**Managing Director:** Dipl.-Ing. Waleri Moretz

**Address:**
Mergenthalerallee 79 - 81
65760 Eschborn
Germany

**Contact:**
Phone: +49 6196 5838311
Email: info@wamocon.com

**Registration:**
Commercial Register: Eschborn HRB 123666
VAT ID: DE344930486

## ./legal-docs/datenschutzerklaerung.md
# Datenschutzerklärung

Stand: {{MONAT}} {{JAHR}}

## 1. Verantwortlicher

Verantwortlicher im Sinne der Datenschutz-Grundverordnung (DSGVO) und anderer nationaler Datenschutzgesetze ist:

WAMOCON GmbH
Mergenthalerallee 79 - 81
65760 Eschborn
Telefon: +49 6196 5838311
E-Mail: info@wamocon.com
Projektkontakt: {{PROJEKT_EMAIL}}
Geschäftsführer: Dipl.-Ing. Waleri Moretz
Handelsregister: Eschborn HRB 123666
USt-ID: DE344930486

## 2. Überblick über die Datenverarbeitung

Diese Datenschutzerklärung gilt für die Website und Webanwendung {{PROJEKTNAME}} ({{DOMAIN}}).

Wir verarbeiten personenbezogene Daten unserer Nutzer grundsätzlich nur, soweit dies zur Bereitstellung einer funktionsfähigen Plattform sowie unserer Inhalte und Leistungen erforderlich ist.

## 3. Rechtsgrundlagen der Verarbeitung

- **Einwilligung** – Art. 6 Abs. 1 lit. a DSGVO
- **Vertragserfüllung** – Art. 6 Abs. 1 lit. b DSGVO
- **Rechtliche Verpflichtung** – Art. 6 Abs. 1 lit. c DSGVO
- **Berechtigtes Interesse** – Art. 6 Abs. 1 lit. f DSGVO

## 4. Hosting und Infrastruktur

### Vercel Inc.
Die Website und Webanwendung werden über Vercel gehostet. Dabei verarbeitet Vercel technisch notwendige Verbindungsdaten (IP-Adresse, Zeitstempel, Browserinformationen). Rechtsgrundlage: Art. 6 Abs. 1 lit. f DSGVO.

### Supabase Inc.
Für Datenbank, Authentifizierung, Dateispeicher und Teile der Backend-Infrastruktur nutzen wir Supabase. Verarbeitet werden Authentifizierungsdaten, Session-Informationen, Projektdaten sowie gespeicherte Medien. Rechtsgrundlage: Art. 6 Abs. 1 lit. b DSGVO.

## 5. Erhebung personenbezogener Daten

### Registrierung und Nutzerkonto
Bei der Registrierung erheben wir: Name, E-Mail-Adresse und Passwort. Diese Daten sind zur Vertragserfüllung erforderlich (Art. 6 Abs. 1 lit. b DSGVO).

### Server-Logfiles
Bei jedem Zugriff auf unsere Plattform werden automatisch folgende Daten erfasst: IP-Adresse, Datum und Uhrzeit, aufgerufene Seite, Referrer-URL, Browser-Typ und -Version. Rechtsgrundlage: Art. 6 Abs. 1 lit. f DSGVO.

## 6. Cookies und Tracking

Die Plattform verwendet technisch notwendige Cookies für Session-Management und Authentifizierung. Rechtsgrundlage: Art. 6 Abs. 1 lit. f DSGVO.

## 7. Rechte der betroffenen Personen

Sie haben das Recht auf:
- **Auskunft** (Art. 15 DSGVO)
- **Berichtigung** (Art. 16 DSGVO)
- **Löschung** (Art. 17 DSGVO)
- **Einschränkung der Verarbeitung** (Art. 18 DSGVO)
- **Datenübertragbarkeit** (Art. 20 DSGVO)
- **Widerspruch** (Art. 21 DSGVO)
- **Widerruf** erteilter Einwilligungen (Art. 7 Abs. 3 DSGVO)
- **Beschwerde** bei einer Aufsichtsbehörde (Art. 77 DSGVO)

## 8. Datensicherheit

Wir setzen technische und organisatorische Sicherheitsmaßnahmen nach dem Stand der Technik ein, um Ihre Daten gegen zufällige oder vorsätzliche Manipulation, Verlust, Zerstörung oder den Zugriff unberechtigter Personen zu schützen.

## 9. Änderung der Datenschutzerklärung

Wir behalten uns vor, diese Datenschutzerklärung anzupassen, um sie an geänderte Rechtslagen oder bei Änderungen der Plattform anzupassen.

---

> **Hinweis:** Dies ist ein Muster. Ersetze alle `{{PLATZHALTER}}` mit den projektspezifischen Informationen. Lass die Datenschutzerklärung vor Veröffentlichung von einem Juristen prüfen.

## ./legal-docs/impressum.md
# Impressum

Stand: {{MONAT}} {{JAHR}}

## WAMOCON GmbH

Mergenthalerallee 79 - 81
65760 Eschborn
Deutschland

## Kontakt

Telefon: +49 6196 5838311
E-Mail: info@wamocon.com
Projektkontakt: {{PROJEKT_EMAIL}}

## Vertretungsberechtigter Geschäftsführer

Dipl.-Ing. Waleri Moretz

## Registereintrag

Sitz der Gesellschaft: Eschborn
Handelsregister: Eschborn HRB 123666
Umsatzsteuer-Identifikationsnummer: DE344930486

## Angaben zum Angebot

{{PROJEKTNAME}} ist eine webbasierte Software-as-a-Service-Plattform für {{BESCHREIBUNG_DES_ANGEBOTS}}. Das Angebot richtet sich primär an Unternehmen und gewerbliche Nutzer.

---

> **Hinweis:** Ersetze alle `{{PLATZHALTER}}` mit den projektspezifischen Informationen.

## ./legal-docs/imprint.md
# Imprint (Legal Notice)

As of: {{MONTH}} {{YEAR}}

## WAMOCON GmbH

Mergenthalerallee 79 - 81
65760 Eschborn
Germany

## Contact

Phone: +49 6196 5838311
Email: info@wamocon.com
Project Contact: {{PROJECT_EMAIL}}

## Authorized Managing Director

Dipl.-Ing. Waleri Moretz

## Registration

Registered Office: Eschborn
Commercial Register: Eschborn HRB 123666
VAT Identification Number: DE344930486

## About the Service

{{PROJECT_NAME}} is a web-based Software-as-a-Service platform for {{SERVICE_DESCRIPTION}}. The service is primarily aimed at businesses and commercial users.

---

> **Note:** Replace all `{{PLACEHOLDERS}}` with your project-specific information.

## ./legal-docs/privacy-policy.md
# Privacy Policy

As of: {{MONTH}} {{YEAR}}

## 1. Data Controller

The Data Controller as defined by the General Data Protection Regulation (GDPR) is:

WAMOCON GmbH
Mergenthalerallee 79 - 81
65760 Eschborn, Germany
Phone: +49 6196 5838311
Email: info@wamocon.com
Project Contact: {{PROJECT_EMAIL}}
Managing Director: Dipl.-Ing. Waleri Moretz
Commercial Register: Eschborn HRB 123666
VAT ID: DE344930486

## 2. Overview of Data Processing

This Privacy Policy applies to the website and web application {{PROJECT_NAME}} ({{DOMAIN}}).

We process personal data of our users only insofar as this is necessary to provide a functional platform and our content and services.

## 3. Legal Basis for Processing

- **Consent** – Art. 6(1)(a) GDPR
- **Performance of Contract** – Art. 6(1)(b) GDPR
- **Legal Obligation** – Art. 6(1)(c) GDPR
- **Legitimate Interest** – Art. 6(1)(f) GDPR

## 4. Hosting and Infrastructure

### Vercel Inc.
The website and web application are hosted via Vercel. Vercel processes technically necessary connection data (IP address, timestamp, browser information). Legal basis: Art. 6(1)(f) GDPR.

### Supabase Inc.
We use Supabase for database, authentication, file storage, and parts of the backend infrastructure. Authentication data, session information, project data, and stored media are processed. Legal basis: Art. 6(1)(b) GDPR.

## 5. Collection of Personal Data

### Registration and User Account
During registration we collect: name, email address, and password. This data is necessary for the performance of the contract (Art. 6(1)(b) GDPR).

### Server Log Files
Each access to our platform automatically records: IP address, date and time, page accessed, referrer URL, browser type and version. Legal basis: Art. 6(1)(f) GDPR.

## 6. Cookies and Tracking

The platform uses technically necessary cookies for session management and authentication. Legal basis: Art. 6(1)(f) GDPR.

## 7. Rights of Data Subjects

You have the right to:
- **Access** (Art. 15 GDPR)
- **Rectification** (Art. 16 GDPR)
- **Erasure** (Art. 17 GDPR)
- **Restriction of processing** (Art. 18 GDPR)
- **Data portability** (Art. 20 GDPR)
- **Object** (Art. 21 GDPR)
- **Withdraw consent** (Art. 7(3) GDPR)
- **Lodge a complaint** with a supervisory authority (Art. 77 GDPR)

## 8. Data Security

We employ state-of-the-art technical and organisational security measures to protect your data against accidental or intentional manipulation, loss, destruction, or access by unauthorised persons.

## 9. Changes to this Privacy Policy

We reserve the right to amend this Privacy Policy to reflect changes in the law or changes to the platform.

---

> **Note:** This is a template. Replace all `{{PLACEHOLDERS}}` with your project-specific information. Have the Privacy Policy reviewed by a lawyer before publication.

## ./legal-docs/terms-and-conditions.md
# Terms and Conditions

As of: {{MONTH}} {{YEAR}}

## § 1 Scope

(1) These Terms and Conditions (hereinafter "T&C") of WAMOCON GmbH, Mergenthalerallee 79 - 81, 65760 Eschborn (hereinafter "Provider"), apply to all contracts for the use of the Software-as-a-Service platform {{PROJECT_NAME}} (hereinafter "Platform"), provided via the website {{DOMAIN}}.

(2) The Platform is aimed at businesses and commercial users (hereinafter "Client") and their respective users (hereinafter "Users"). This is a B2B offering. Consumers within the meaning of § 13 BGB (German Civil Code) are not the target audience.

(3) Deviating, conflicting, or supplementary terms and conditions of the Client shall not become part of the contract unless the Provider expressly agrees in writing.

## § 2 Conclusion of Contract

(1) The presentation of the Platform and its features on the website does not constitute a binding offer within the meaning of § 145 BGB, but rather an invitation to submit an offer (invitatio ad offerendum).

(2) The Client submits a binding offer by completing the registration process on the Platform and accepting these T&C.

(3) The contract is concluded when the Provider accepts the Client's offer by activating access.

## § 3 Service Description

(1) The Provider makes the Platform available to the Client as Software-as-a-Service (SaaS) via the Internet.

(2) The precise scope of features is set out in the current service description on the website.

(3) The Provider is entitled to further develop, expand, and adapt the Platform. Material restrictions to the scope of features will be communicated to the Client in advance.

## § 4 Usage Rights

(1) The Provider grants the Client a simple, non-transferable, non-sublicensable right to use the Platform for the duration of the contract.

(2) The Client may only use the Platform for its own business purposes.

## § 5 Client Obligations

(1) The Client shall keep its access credentials confidential and protect them from third-party access.

(2) The Client shall ensure that use of the Platform complies with applicable law.

## § 6 Availability

(1) The Provider shall endeavour to maintain an annual average availability of 99.5%.

(2) Scheduled maintenance windows announced in advance shall not count as downtime.

## § 7 Data Protection

The processing of personal data is governed by the Provider's Privacy Policy and the provisions of the GDPR.

## § 8 Liability

(1) The Provider shall be fully liable for damages arising from injury to life, body, or health, as well as for intent and gross negligence.

(2) Otherwise, liability is limited to foreseeable, typically occurring damages.

## § 9 Contract Duration and Termination

(1) The contract is concluded for an indefinite period and may be terminated by either party with one month's notice to the end of a calendar month.

(2) The right to extraordinary termination for good cause remains unaffected.

## § 10 Final Provisions

(1) The law of the Federal Republic of Germany shall apply, excluding the UN Convention on Contracts for the International Sale of Goods.

(2) The place of jurisdiction is Eschborn, provided the Client is a merchant.

(3) Should individual provisions of these T&C be invalid, the validity of the remaining provisions shall remain unaffected.

---

> **Note:** This is a template. Replace all `{{PLACEHOLDERS}}` with your project-specific information. Have the T&C reviewed by a lawyer before publication.

## package.json
{
  "name": "geburtstagspilot",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev --turbopack",
    "build": "next build",
    "start": "next start",
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "typecheck": "tsc --noEmit",
    "verify": "npm run typecheck && npm run lint && npm run build",
    "gen:anforderungsdokument": "node scripts/generate-anforderungsdokument.mjs"
  },
  "dependencies": {
    "@supabase/ssr": "^0.10.3",
    "@supabase/supabase-js": "^2.105.4",
    "docx": "^9.6.1",
    "next": "16.2.1",
    "next-intl": "^4.11.2",
    "openai": "^6.37.0",
    "react": "19.2.4",
    "react-dom": "19.2.4",
    "zod": "^4.4.3"
  },
  "devDependencies": {
    "@tailwindcss/postcss": "^4",
    "@types/node": "^20",
    "@types/react": "^19",
    "@types/react-dom": "^19",
    "eslint": "^9",
    "eslint-config-next": "16.2.1",
    "tailwindcss": "^4",
    "typescript": "^5"
  }
}

