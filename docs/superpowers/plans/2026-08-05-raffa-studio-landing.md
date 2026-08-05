# Raffa Studio landing page implementation plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a responsive Raffa Studio landing page that presents applications and can grow into a product ecosystem.

**Architecture:** Next.js renders a static-first marketing surface from typed local content. Shared components consume a small token system and application records so new products do not require duplicated page markup.

**Tech Stack:** Next.js, React, TypeScript strict, Tailwind CSS, Framer Motion, Lucide Icons, Vercel, GitHub Actions.

## Global Constraints

- Use the locked palette from the design specification.
- Use Sora for headings and Inter for body text.
- Keep application content in typed local data.
- Do not publish personal contact data until it is provided.
- Respect `prefers-reduced-motion`.
- Do not add credentials or tokens to source control.

---

### Task 1: Create the application shell

**Files:**
- Create: `package.json`
- Create: `next.config.ts`
- Create: `tsconfig.json`
- Create: `src/app/layout.tsx`
- Create: `src/app/page.tsx`
- Create: `src/app/globals.css`
- Create: `public/favicon.svg`

**Interfaces:**
- Produces: a Next.js application that renders `HomePage` at `/`.

- [ ] **Step 1: Create the Next.js application with TypeScript and Tailwind.**

Run: `npx create-next-app@latest . --ts --tailwind --eslint --app --src-dir --use-npm --import-alias "@/*" --yes`

- [ ] **Step 2: Confirm the development build works.**

Run: `npm run build`

Expected: the build completes with exit code 0.

- [ ] **Step 3: Configure global font variables and palette tokens.**

Implement `--color-background: #050505`, `--color-surface: #0B0B0B`, `--color-border: #1E1E1E`, `--color-accent: #00E676`, `--color-accent-secondary: #00C853`, `--color-text: #FFFFFF`, and `--color-text-muted: #BDBDBD` in `src/app/globals.css`.

- [ ] **Step 4: Rebuild after the token change.**

Run: `npm run build`

Expected: the build completes with exit code 0.

- [ ] **Step 5: Commit the shell.**

Run: `git add package.json next.config.ts tsconfig.json src/app public/favicon.svg && git commit -m "chore: scaffold Raffa Studio landing page"`

### Task 2: Model the application catalog

**Files:**
- Create: `src/content/apps.ts`
- Create: `src/types/app.ts`
- Create: `src/components/apps/app-card.tsx`
- Test: `src/content/apps.test.ts`

**Interfaces:**
- Produces: `AppRecord` and `apps: readonly AppRecord[]`.
- Consumes: `AppRecord` in `AppCard`.

- [ ] **Step 1: Write a failing catalog test.**

```ts
import { apps } from "@/content/apps";

it("includes MinhaRota as an application in development", () => {
  expect(apps).toEqual(expect.arrayContaining([
    expect.objectContaining({ slug: "minha-rota", status: "em-desenvolvimento" }),
  ]));
});
```

- [ ] **Step 2: Run the test and confirm it fails.**

Run: `npm test -- apps.test.ts`

Expected: FAIL because `@/content/apps` does not exist.

- [ ] **Step 3: Implement the typed record and MinhaRota content.**

```ts
export type AppStatus = "em-desenvolvimento" | "disponivel";

export interface AppRecord {
  slug: string;
  name: string;
  status: AppStatus;
  summary: string;
  platforms: readonly string[];
  capabilities: readonly string[];
  downloadUrl?: string;
}
```

- [ ] **Step 4: Run the catalog test.**

Run: `npm test -- apps.test.ts`

Expected: PASS.

- [ ] **Step 5: Commit the catalog.**

Run: `git add src/types/app.ts src/content/apps.ts src/content/apps.test.ts src/components/apps/app-card.tsx && git commit -m "feat: add typed application catalog"`

### Task 3: Build the landing sections

**Files:**
- Create: `src/components/sections/hero.tsx`
- Create: `src/components/sections/ecosystem.tsx`
- Create: `src/components/sections/about.tsx`
- Create: `src/components/sections/commitments.tsx`
- Create: `src/components/sections/technology.tsx`
- Create: `src/components/sections/contact.tsx`
- Create: `src/components/site/header.tsx`
- Create: `src/components/site/footer.tsx`
- Modify: `src/app/page.tsx`

**Interfaces:**
- Consumes: `apps` from `@/content/apps`.
- Produces: a semantic one-page document with navigation anchors.

- [ ] **Step 1: Write a failing page test for the main landmarks.**

```ts
expect(screen.getByRole("main")).toBeInTheDocument();
expect(screen.getByRole("navigation", { name: /principal/i })).toBeInTheDocument();
expect(screen.getByRole("contentinfo")).toBeInTheDocument();
```

- [ ] **Step 2: Run the test and confirm it fails.**

Run: `npm test -- page.test.tsx`

Expected: FAIL because the landmarks are not rendered.

- [ ] **Step 3: Compose the documented sections in `src/app/page.tsx`.**

Use one `main` landmark and sections with IDs `aplicativos`, `ecossistema`, `sobre`, `tecnologias` and `contato`.

- [ ] **Step 4: Run the page test.**

Run: `npm test -- page.test.tsx`

Expected: PASS.

- [ ] **Step 5: Commit the page sections.**

Run: `git add src/components src/app/page.tsx src/app/page.test.tsx && git commit -m "feat: add Raffa Studio landing sections"`

### Task 4: Add production checks and Vercel configuration

**Files:**
- Create: `.github/workflows/ci.yml`
- Create: `vercel.json`
- Create: `src/app/robots.ts`
- Create: `src/app/sitemap.ts`
- Modify: `next.config.ts`

**Interfaces:**
- Produces: lint, test and build checks for pull requests and secure production headers.

- [ ] **Step 1: Add a GitHub Actions workflow that runs lint, tests and build.**

```yaml
name: CI
on: [pull_request, push]
jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 22, cache: npm }
      - run: npm ci
      - run: npm run lint
      - run: npm test
      - run: npm run build
```

- [ ] **Step 2: Add CSP and related headers in `next.config.ts` after confirming all asset origins.**

Run: `npm run build`

Expected: the build completes with exit code 0.

- [ ] **Step 3: Validate SEO routes.**

Run: `npm run lint && npm test && npm run build`

Expected: all commands complete with exit code 0.

- [ ] **Step 4: Connect the GitHub repository to the Raffa Sutdio Vercel team and verify the preview deployment.**

Expected: a preview URL renders the landing page with no build error.

- [ ] **Step 5: Commit the deployment configuration.**

Run: `git add .github/workflows/ci.yml vercel.json next.config.ts src/app/robots.ts src/app/sitemap.ts && git commit -m "chore: add release checks and deployment configuration"`

