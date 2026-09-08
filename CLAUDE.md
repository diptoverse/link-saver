# Link Saver — Claude Code Instructions

## What this app is

A personal tool for saving links you want to revisit. You paste a URL, it pulls the title, platform, and creator automatically so you don't have to type them. You add a topic and rate the link yourself. Later you browse, search, and filter what you saved.

That's it. No social features, no sharing, no accounts. Just a fast personal library.

---

## Code quality rules

Write code a competent human engineer would write. These rules are not suggestions.

- No comments that explain what code does. Only add one if the *why* is genuinely non-obvious.
- No over-abstraction. No helpers, utilities, or wrapper components without a real reason.
- No defensive coding for things that cannot happen. Trust internal code and framework guarantees.
- No excessive error handling. Validate at system boundaries only — user input, external API responses.
- Short, honest variable names. `url`, `links`, `priority` — not `currentUrlInputValue`.
- Small, focused components. If a component does two unrelated things, split it.
- No redundant state. Derive values from existing state instead of duplicating.
- No placeholder comments — no `// TODO`, `// handle later`, `// add error handling here`.
- No leftover `console.log` calls.

## UI copy rules

All text the user sees — labels, buttons, empty states, errors, placeholders — must sound like a real person wrote it.

- No em dashes (—) in UI text.
- No AI words: "utilize", "leverage", "seamlessly", "robust", "comprehensive", "streamline", "provide", "ensure", "facilitate".
- No stiff phrasing: "Please enter a valid URL", "An error has occurred", "No items to display".
- Write like you'd say it out loud. "Something went wrong, try again." "No links yet." "Save link."

## Priority rating

Priority is always set manually by the user. Never pre-fill it, never default it, never suggest a value. The user decides.

---

## Conventions

**Branches:** `feature/<name>`, `fix/<name>`, `chore/<name>`

**Commits:** Conventional Commits — `feat:`, `fix:`, `chore:`, `refactor:`

**Workflow:** one sprint = one branch = one PR = squash merge to `main`

## File structure

```
src/
  components/
  lib/
    supabase.js
  App.jsx
  main.jsx
```

## Hard constraints

- Never hardcode secrets. Everything sensitive comes from `import.meta.env`.
- Never commit `.env`. It is gitignored. `.env.example` is the committed placeholder.
- `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` are the only required env vars.
- `main` branch must always build and deploy cleanly.

---

## How every sprint runs

This is the exact workflow to follow for every sprint, every time, without the user having to ask.

---

### Step 1 — Sprint briefing

When a sprint starts, give this before touching any code:

- **What** — what this sprint builds, from the user's perspective
- **Why** — why it's needed now, what it unlocks for later sprints
- **Sub-tasks** — the full ordered list of sub-tasks to complete this sprint
- **Deliverables** — concrete, testable things that confirm the sprint is done

Wait for the user to say they're ready before moving on.

---

### Step 2 — Sub-tasks one by one

Go through each sub-task in order. For every sub-task:

1. Tell the user **what** the sub-task is
2. Tell the user **why** we're doing it — plain language, 1-2 sentences
3. Ask: "Do you want to do this or should I?"

If user says **"me"** — tell them exactly what to run or do, then wait for confirmation before moving to the next sub-task.

If user says **"you"** — explain how you will implement it (which file, what change, why that approach), wait for the user to confirm, then write the code.

Never skip the what/why. Never write code without being asked. Never move to the next sub-task without confirmation the current one is done.

---

### Step 3 — Sprint completion check

After all sub-tasks are done, go through the sprint's deliverables checklist one by one and confirm each is met. Fix anything missing before closing the sprint.

---

### Step 4 — Commit, push, PR, merge

Only after the completion check passes:

1. Commit with the correct conventional commit message
2. Push the branch
3. Open a PR on GitHub
4. Confirm CI passes and Vercel preview looks correct
5. Squash merge the PR
6. Pull main locally

---

### Step 5 — Handoff (automatic, every sprint)

After the sprint is fully merged, without the user asking:

1. Mark all checklist items as done in the sprint deliverables section below
2. Add a handoff block under the sprint with the exact prompt the user can copy-paste into a new session to start the next sprint — with full context baked in, no assumptions

---

## Sprint handoffs

After each sprint is fully done (all checklist items checked), the following handoff block is added below that sprint. Use it to start the next sprint in a new session — copy the prompt exactly.

The prompt is designed to:
- Tell Claude which sprint we're on and what was already done
- Re-anchor the code quality and UI copy rules
- Give the exact task without needing to re-read the full plan
- Keep the same standards across sessions

---

## Sprint deliverables

A sprint is done only when every item is checked.

---

### Sprint 0 — Scaffold + CI/CD
- [x] Vite React scaffold created
- [x] `.gitignore` includes `.env`
- [x] `README.md` written
- [x] `.github/workflows/ci.yml` — build gate on PRs
- [x] `npm run build` passes locally
- [x] `git init` + initial commit pushed
- [x] GitHub repo created and code pushed
- [x] Vercel project connected to GitHub, auto-deploy on `main` confirmed

---

#### Sprint 0 handoff — use this to start Sprint 1

```
Sprint 0 is done. The project is a Vite React app at /Users/dipto/Code/pet-projects/1-linksaver.
It has a GitHub repo (public), Vercel auto-deploy on main, and a GitHub Actions CI build gate on PRs.
CLAUDE.md has all code quality rules, UI copy rules, and sprint deliverable checklists — read it first.

We are starting Sprint 1: Tailwind CSS setup.
Create a branch feature/tailwind-setup, install tailwindcss and @tailwindcss/vite, wire it into
vite.config.js and index.css, and update App.jsx with a simple centered layout and heading to prove
it works. Follow all rules in CLAUDE.md. Go through the Sprint 1 checklist item by item before
calling it done.
```

---

### Sprint 1 — Tailwind CSS
- [x] `tailwindcss` and `@tailwindcss/vite` installed
- [x] `vite.config.js` updated with Tailwind plugin
- [x] `index.css` imports Tailwind
- [x] `App.jsx` styled: centered layout, heading — visible proof Tailwind works
- [x] `npm run dev` shows a styled page
- [x] `npm run build` passes

---

#### Sprint 1 handoff — use this to start Sprint 2

```
Sprint 1 is done. Tailwind CSS is set up and working. The project is at /Users/dipto/Code/pet-projects/1-linksaver on the main branch.

Completed so far:
- Sprint 0: Vite React scaffold, GitHub repo (public), Vercel auto-deploy, GitHub Actions CI gate
- Sprint 1: Tailwind CSS installed, wired into vite.config.js and index.css, App.jsx cleaned up

Read CLAUDE.md before doing anything. It has the code quality rules, UI copy rules, sprint workflow protocol, and all deliverable checklists. Follow the sprint workflow exactly as described there — briefing first, then sub-tasks one by one, then completion check, then commit/push/PR/merge, then update CLAUDE.md.

We are starting Sprint 2: Supabase schema and client setup.
```

---

### Sprint 2 — Supabase schema + client
- [ ] `links` table created in Supabase dashboard with correct schema
- [ ] RLS enabled, "allow all" policy in place
- [ ] `@supabase/supabase-js` installed
- [ ] `src/lib/supabase.js` exports a working Supabase client
- [ ] `.env.example` has `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` as placeholders
- [ ] Local `.env` filled with real keys (not committed)
- [ ] Vercel env vars set for both keys
- [ ] `npm run build` passes

---

### Sprint 3 — Add-link form
- [ ] `LinkForm` component built
- [ ] URL input + submit button
- [ ] On submit: fetches `https://noembed.com/embed?url=<encoded>`
- [ ] `provider_name` → platform, `title` → title, `author_name` → creator pre-filled as editable inputs
- [ ] Falls back to domain-guessed platform if noembed returns nothing
- [ ] Topic field (always manual)
- [ ] Priority field — user sets it manually, no default or suggestion
- [ ] On save: inserts row into Supabase `links` table
- [ ] Test: YouTube URL auto-fills platform + title + creator
- [ ] Test: unknown blog URL falls back without breaking
- [ ] `npm run build` passes

---

### Sprint 4 — Link list (MVP)
- [ ] `LinkList` component built
- [ ] Fetches all rows from `links`, ordered by `created_at` descending
- [ ] Each card shows: title, platform badge, creator, topic, priority
- [ ] Delete button removes row from Supabase and updates UI without full reload
- [ ] `App.jsx` wires `LinkForm` + `LinkList` — form at top, list below
- [ ] List refreshes after a new link is added
- [ ] Test: add a link, it appears immediately
- [ ] Test: delete a link, it disappears immediately
- [ ] `npm run build` passes

---

### Sprint 5 — Inline editing
- [ ] Priority on each card is editable
- [ ] Editing priority updates Supabase immediately
- [ ] UI reflects change without reload
- [ ] Pencil icon toggles edit mode for title, creator, topic
- [ ] Checkmark saves to Supabase
- [ ] Closing edit mode without saving discards changes
- [ ] `npm run build` passes

---

### Sprint 6 — Search, filter, sort
- [ ] Search bar filters cards by title, creator, topic (case-insensitive substring)
- [ ] Platform dropdown lists distinct platforms from loaded links
- [ ] Selecting a platform filters the list
- [ ] Sort control: newest first / priority high to low
- [ ] All filtering and sorting is client-side
- [ ] Filters combine correctly
- [ ] `npm run build` passes

---

### Sprint 7 — Extras (decide per feature)
One branch per extra. Repeat the pattern: branch → build → checklist → PR → merge.

---

### Sprint 8 — Production hardening
- [ ] Failed Supabase request shows a visible, human-worded error
- [ ] Failed noembed fetch handled — form still usable for manual entry
- [ ] Empty link list shows a real empty state, not a blank page
- [ ] Loading states shown while fetching and saving
- [ ] No hardcoded secrets anywhere in source
- [ ] No leftover `console.log` calls
- [ ] `npm run build` passes with no warnings
