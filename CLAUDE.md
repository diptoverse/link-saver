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

## Sprint deliverables

A sprint is done only when every item is checked.

---

### Sprint 0 — Scaffold + CI/CD
- [x] Vite React scaffold created
- [x] `.gitignore` includes `.env`
- [x] `README.md` written
- [x] `.github/workflows/ci.yml` — build gate on PRs
- [x] `npm run build` passes locally
- [ ] `git init` + initial commit pushed
- [ ] GitHub repo created and code pushed
- [ ] Vercel project connected to GitHub, auto-deploy on `main` confirmed

---

### Sprint 1 — Tailwind CSS
- [ ] `tailwindcss` and `@tailwindcss/vite` installed
- [ ] `vite.config.js` updated with Tailwind plugin
- [ ] `index.css` imports Tailwind
- [ ] `App.jsx` styled: centered layout, heading — visible proof Tailwind works
- [ ] `npm run dev` shows a styled page
- [ ] `npm run build` passes

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
