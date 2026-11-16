# Step 6 — Review

Judges the UI against the brief with evidence a person can open. Runs inside `build`, alone as `/i-can-design review <slug> [before|after]`, or as `before` at the start of a redesign.

## 1. Capture

Tool from `browser_tool` (setup check 4). Target: `dev_url` for the project, or a local file for static pages; ask the user to start their app when it is not running. Never start it yourself unless the user asks.

For every screen in the brief, every viewport in config, and dark mode when the brief has it:

- Screenshot to `evidence/<before|after>/<screen>-<viewport>[-dark].png`. Same names before and after, so they pair.
- Key states the brief lists (focus, error, empty) as separate captures: `<screen>-<state>-<viewport>.png`.
- When the brief has motion criteria: a short note of what moved, measured duration and easing from the code or the DevTools animation panel.

No browser: ask the user for screenshots and say which render criteria become `unmeasured`. `before` stops here; write nothing else.

## 2. Measure

- ux-ui gates (`ux-ui-agent-skills:gate`): contrast, a11y (axe), target size, overflow. A gate that prints `SKIPPED` is `unmeasured`, not a pass.
- Code facts per criterion: token use, number of type families, accent hues, durations.

## 3. Judge

Write `designs/<slug>/review.md`:

```markdown
# Review — <slug> — 2026-01-31

| ID | Criterion | Verdict | Evidence |
|---|---|---|---|
| F1 | one accent hue | Met | after/pricing-desktop.png; tokens.css:12 |
| A1 | WCAG 2.2 AA contrast | Unmeasured | no browser (gate SKIPPED) |

## Slop scan
| Pattern | Present? | Allowed by brief? | Evidence |

## Critic
<summary of the independent critique and what was done about each point>

## Not verified
- <each check that did not run and why>
```

Verdicts: `Met`, `Not met`, `Unmeasured`. Each cites a file, a line, a measured value, or the reason it could not be measured. A redesign compares before and after in the Evidence column.

## 4. Independent critic

One fresh-eyes critique, so the reviewer is not only the builder. Prefer the ux-ui `design-critic` agent (or ux-ui `critique`); otherwise impeccable `critique`. Give it the brief and the `after` captures, **not** your verdict table, and ask it to argue for rejection against the brief. Treat its points as claims: check each against the captures before acting on it.

## 5. Fix round

`Not met` verdicts and confirmed critic points go into **one** batch of fixes, then recapture only what changed and update the table. Stop after that round; anything still open goes to the hand-off as a named open item rather than another loop.

Set brief `Status: reviewed` and add a Log line.
