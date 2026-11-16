# Step 5 — Build

Needs `designs/<slug>/brief.md` with `Status: approved`. Without it, refuse and point to `/i-can-design <request>`.

## Before the first edit

1. Re-read the brief. List the criteria; they are the build's acceptance test.
2. Read the project's `CLAUDE.md` / `AGENTS.md`, the design-system files named in the brief, and 2–3 existing screens or components nearest to the target. Reuse their components, tokens and patterns before creating new ones.
3. Redesign: confirm `evidence/before/` holds captures (else run review `before` first).
4. Dirty working tree in the target project: show `git status` and ask. Never stash or reset.

## Route by surface

| Surface | Leads | Supports | Not used |
|---|---|---|---|
| marketing | `design-taste-frontend` (art direction, layout, copy density, imagery) | impeccable craft floor, `emil-design-eng` motion, ux-ui `design-tokens` / `a11y-audit` | — |
| product | the project's design system, then ux-ui (`design-screen`, `data-dashboard` for dense data, `design-component`, `design-code`) | impeccable (`harden`, `clarify`, `polish`), `emil-design-eng` for interactions | `design-taste-frontend` (it covers landing pages, not app UI) |
| redesign | ux-ui `redesign` or impeccable `audit` to find what to change; keep functionality | the route of the underlying surface | — |
| no design system yet | ux-ui `brandkit` (or `design-tokens`) from the brief's direction first, then the surface route | | |

How to use each dependency inside this step:

- **design-taste-frontend**: skip its own brief inference; the approved brief is the brief. Apply its layout, typography and content rules that match the chosen direction.
- **impeccable**: read its `craft-floor` reference before UI edits. When it asks for `PRODUCT.md` / `DESIGN.md`, write them from the brief rather than re-interviewing the user, and only in the project when the user agrees (they are files in their repo).
- **ux-ui-agent-skills**: load `design-doctrine` first. Its rules (no emoji, tokens by intent, the eight states) apply unless the brief says otherwise.
- **emil-design-eng**: invoke it with a concrete question ("how should the plan-switch toggle animate for a calm feel?"); invoked bare, it only greets.

When two dependencies disagree, the brief decides; when the brief is silent, the project's existing system decides; record the call under **Decisions** in the brief.

## Build order

1. **Tokens**: map every colour, type size, space, radius, shadow and duration in the direction to existing tokens; add new ones only where the brief allows extending the system. No raw hex or px in components when the project uses tokens.
2. **Structure**: layout and content for each screen in the brief, with real content or `TODO(content)`.
3. **States**: every state listed per screen (default, hover, focus-visible, active, disabled, loading, empty, error as they apply).
4. **Motion**: only what the brief's motion appetite allows; `prefers-reduced-motion` honoured per A2.
5. **Self-check against the brief** in one batch: walk every criterion, fix what the code alone shows wrong, then go to review. Bounded: one pass here; rendering and judging belong to step 6.

## Checks

Run the project's own lint, type check and tests on changed files (its `package.json` scripts or equivalent), and the ux-ui gates when installed (`ux-ui-agent-skills:gate`). Report each command and its exit code; one that could not run is named with the reason. Update the brief: `Status: built`, a Log line with the date and changed paths.
