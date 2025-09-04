# Oncosoft Frontend Style Guide (Svelte 5 + TypeScript)

**Project:** `onco-rpt-frontend`  
**Audience:** Contributors + Gemini Review Bot ("bot")  
**Status:** v1.2 (2025-08-21, aligned with README.md)

---

## 0) Purpose & Scope

This guide defines **how we write, structure, and review code** in the frontend project.  
Rules use RFC-2119 keywords (**MUST / SHOULD / MAY**) and unique IDs (e.g., **SG-001**) so the bot can check compliance
and auto-suggest fixes.

> **Applies to:** Svelte 5, SvelteKit, TypeScript, Stores, Vitest, Playwright, ESLint, Prettier.

---

## 1) Project Structure

* **SG-001 (MUST):** Follow this layout:

  ```
  src/
    lib/
      components/
      utils/
      apis/
      stores/
    routes/
  static/
    css/
    font/
    js/
  ```

* **SG-002 (SHOULD):** One component per file. Place tests (`*.test.ts`) and stories (`*.stories.ts`) alongside the
  component.
* **SG-003 (MUST):** Public APIs in `src/lib/**` must be stable and typed. Avoid deep imports.

---

## 2) Naming & Files

* **SG-010 (MUST):** Components → **PascalCase**, utilities → **camelCase**, types → **PascalCase**, constants → *
  *UPPER_SNAKE_CASE**, stores → **camelCase**.
* **SG-011 (MUST):** File suffixes: `.svelte`, `.store.ts`, `.service.ts`, `.utils.ts`.
* **SG-012 (SHOULD):** Route filenames reflect URL. Use `[id]` for dynamic params.

---

## 3) Svelte Component Conventions

* **SG-020 (MUST):** Use `<script lang="ts">`. Ordering:  
  imports → props (`$props`, `$bindable`) → local state (`$state`) → derived (`$derived`) → side effects (`$effect`) →
  functions/events.
* **SG-021 (MUST):** Define props with `interface` and assign defaults via destructuring.
* **SG-022 (SHOULD):** Use `$bindable` only when parent mutation is required.
* **SG-030 (MUST):** Props are immutable; upward communication via typed events only.
* **SG-031 (SHOULD):** Event names in kebab-case; dispatch with type safety.
* **SG-040 (MUST):** Prefer `$derived` or `$:` over `$effect`.
* **SG-041 (SHOULD):** Keep `$effect` pure, avoid unnecessary dependencies.
* **SG-050 (MUST):** All interactive elements must meet accessibility (a11y).
* **SG-051 (MUST):** Ensure keyboard operability.
* **SG-052 (SHOULD):** Use `aria-*` attributes when needed.

---

## 4) State Management

* **SG-060 (MUST):** Shared state managed with Svelte stores (`writable`, `$state`, or class-based).
* **SG-061 (SHOULD):** Scope stores by feature or under `lib/stores`.
* **SG-062 (MUST):** Avoid global singletons for ephemeral state.

---

## 5) Data & API Layer

* **SG-070 (MUST):** Place HTTP calls only in `lib/apis/*.ts`.
* **SG-071 (MUST):** Define request/response types explicitly.
* **SG-072 (SHOULD):** Handle loading/error states clearly.

---

## 6) Styling

* **SG-080 (MUST):** Use scoped `<style>` inside `.svelte` or global styles in `static/css/`.
* **SG-081 (SHOULD):** Define design tokens via CSS variables.
* **SG-082 (SHOULD):** Support dark mode via `data-theme`.

---

## 7) Performance

* **SG-090 (MUST):** No blocking work in top-level scope.
* **SG-091 (MUST):** Always provide keys in `{#each}`.
* **SG-092 (SHOULD):** Lazy-load rarely used components.
* **SG-093 (MUST):** Optimize images.

---

## 8) Security & Privacy

* **SG-100 (MUST):** Do not log PHI/PII.
* **SG-101 (MUST):** Escape/encode all user input.
* **SG-102 (MUST):** Use secure cookies and CSRF protection.

---

## 9) Testing

* **SG-110 (MUST):** Unit tests with Vitest + Testing Library.
* **SG-111 (SHOULD):** E2E tests with Playwright.
* **SG-112 (MUST):** Follow Arrange-Act-Assert pattern.

---

## 10) Linting & Formatting

* **SG-120 (MUST):** Prettier formats all files.
* **SG-121 (MUST):** ESLint with Svelte + TS rules.
* **SG-122 (SHOULD):** Run lint/format via commit hooks.

---

## 11) Git & PRs

* **SG-130 (MUST):** Follow Conventional Commits.
* **SG-131 (MUST):** Keep PRs small with clear description and screenshots.
* **SG-132 (SHOULD):** Use draft PRs early.

---

## 12) Internationalization

* **SG-140 (MUST):** No hardcoded user-facing strings.
* **SG-141 (SHOULD):** Use ICU pluralization.

---

## 13) Error Handling & UX

* **SG-150 (MUST):** Distinguish user vs. system errors.
* **SG-151 (SHOULD):** Show transient success with toasts.

---

## 14) Documentation

* **SG-160 (MUST):** Each feature must include `README.md`.
* **SG-161 (SHOULD):** Public components must document props.

---

## 15) Bot Checks

* Typed props/events.
* No `any`.
* a11y compliance.
* Stores isolation.
* No fetch in `.svelte`.
* Keys in `{#each}`.
* No PHI/PII in logs.
* Conventional commits.
* Prettier/ESLint configs present.

---

## 16) SvelteKit Usage

* **SG-200 (SHOULD):** Use SvelteKit’s standard routing, endpoints, and form actions.
* **SG-201 (MUST):** Do not bypass routing/server load without justification.
* **SG-202 (SHOULD):** Separate server/client code into `+page.server.ts` and `+page.svelte`.

---

## 17) Icon Management

* **SG-084 (SHOULD):** Store icons under `src/lib/assets/icons/` as `.svg` or `.svelte`.
* **SG-085 (MUST):** Color changes via `currentColor` and CSS variables only.
* **SG-086 (MUST):** Use `:global()` styles only under a wrapper class.

---

## 18) Exceptions

* **SG-900 (MUST):** All deviations require PR justification.

---

## 19) Adoption Plan

1. Ensure ESLint, Prettier, and commitlint configs.
2. Enable CI checks for §15 rules.
3. Adopt rules incrementally as code is touched.  

## 20) HTML Conventions
* **SG-210 (MUST):** All interactive HTML elements must have appropriate ARIA attributes (e.g., `aria-label`, `role`) to ensure accessibility (SG-050).