# FPE indexing fix plan for Codex

## Goal

Make Google stop treating most of the site as duplicates of the homepage.

## Scope

Only do the changes that directly help indexing.

- [x] Fix canonical tags
- [x] Verify generated HTML
- [x] Add a regression check so this cannot silently ship again

## Current phase

- [x] Convert this plan into a live checklist and track progress
- [x] Fix the shared canonical logic in `src/website/layouts/SiteLayout.astro`
- [x] Verify `GuideLayout.astro` and `GodotAPILayout.astro` inherit the shared fix
- [x] Rebuild the site and inspect generated canonical tags

## 1) Fix the shared canonical logic

**File to edit:** `src/website/layouts/SiteLayout.astro`

Right now the canonical tag is hard-coded to the homepage. That causes many pages to declare the homepage as their canonical URL.

### Required change

Generate the canonical URL from the current page path instead of hard-coding it.

### Requirements

- [x] Homepage canonical must be `https://fpe.papercraft.games`
- [x] Every other page canonicalizes to itself
- [x] Docs pages do not point to the homepage as canonical
- [x] API pages do not point to the homepage as canonical
- [x] Use `Astro.site` plus the current pathname
- [x] Normalize the homepage so it does not end with a trailing slash

### Implementation shape

Use logic equivalent to this:

```ts
const canonicalUrl = new URL(Astro.url.pathname, Astro.site);
const canonical = canonicalUrl.toString().replace(/\/$/, "");
```

Then render:

```astro
<link rel="canonical" href={canonical} />
```

## 2) Make sure all layout consumers inherit the fix

**Files to verify:**

- [x] `src/website/layouts/GuideLayout.astro`
- [x] `src/website/layouts/GodotAPILayout.astro`

These should continue using `SiteLayout` so the canonical fix automatically applies everywhere.

Do not add page-specific canonical hacks unless a page truly needs a different canonical.

## 3) Rebuild and verify actual output HTML

After the code change, build the site and verify the generated files.

### Must pass

- [x] `dist/website/index.html` canonical is `https://fpe.papercraft.games`
- [x] A docs page canonical points to its own docs URL
- [x] A Godot API page canonical points to its own API URL
- [x] No non-home page canonical points to the homepage

### Suggested checks

```bash
yarn build:web

grep -R "<link rel=\"canonical\"" -n dist/website/index.html

grep -R "<link rel=\"canonical\"" -n dist/website/docs/*.html | head

grep -R "<link rel=\"canonical\"" -n dist/website/godot-api-docs/*.html | head
```

## Done criteria

This task is done when all of the following are true:

- [x] The shared layout no longer hard-codes the homepage canonical
- [x] Built HTML shows self-canonicals for non-home pages
- [~] The deployed fix causes non-home pages to stop declaring the homepage as canonical

## Non-goals

Do not spend time on these in this task:

- backlink work
- content marketing
- social promotion
- generic SEO cleanup unrelated to indexing
- speculative fixes with no clear indexing impact
