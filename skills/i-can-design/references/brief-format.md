# Step 4 — Brief and directions

## brief.md

Write `designs/<slug>/brief.md` in `report_language`. Every criterion is something a reviewer can check from a screenshot, the code or a measurement; that is what step 6 judges.

```markdown
# <Design name>

Status: draft | approved | built | reviewed
Date: 2026-01-31
Slug: <slug>
Project: <name> (<path>) · Surface: marketing | product | redesign
Source: <request / Figma node / URL / Jira key>

## Job
- Audience: <who>
- One action: <the single thing they should do or understand>
- Content: real | placeholders (`TODO(content)` marks each)

## Feeling
| Word | Criteria (observable) |
|---|---|
| calm | F1 one accent hue (#...); F2 section gap ≥ 96px desktop / 56px mobile; F3 motion only on interaction, ≤ 200ms ease-out |
| never: busy | G1 ≤ 2 type families; G2 ≤ 1 primary CTA per viewport |

## References
- Like: <ref> — <what exactly>
- Not like: <ref> — <why>

## Slop decisions
- Banned: <items from the slop list>
- Kept on purpose: <item> — <reason>

## Constraints
- Design system: <use as is | extend | new> — <paths>
- Accessibility: A1 WCAG 2.2 AA; A2 reduced motion: <behaviour>; A3 targets ≥ 24px
- Themes: <light/dark>; viewports: <from config>
- Motion appetite: <none | functional | expressive (where)>

## Direction
<chosen direction name and its summary, copied from directions.html, plus any mix the user asked for>

## Screens
| # | Screen / component | Path (existing or new) | States to cover |
|---|---|---|---|

## Assumptions
- <what was decided for the user, shown at approval>

## Decisions
- <precedence calls and conflicts settled, with the rule that decided>

## Log
- 2026-01-31 brief approved
```

Criterion IDs (`F1`, `G1`, `A1`, …) are what the review cites.

## directions.html

Before approval, show **two or three directions** that all satisfy the criteria but differ in point of view. Write them to `designs/<slug>/directions.html`: one static, self-contained file (inline CSS, no scripts; fonts from Google Fonts only), one panel per direction with:

- name and a one-line point of view;
- type pairing rendered as a heading and a paragraph;
- palette swatches with hex values and the contrast ratio of text on background;
- one representative block of the real surface (the hero, the key table row, the form) in that direction, with the user's content;
- the motion signature in words (what moves, how long, which easing).

Give its absolute path so the user can open it. When the project already has a design system, directions vary only what the system leaves open (layout, density, imagery, motion), and say so.

The user picks, mixes or asks for another round. Record the result under **Direction**.

## Grill the direction

Before approval, load `grilling` once more and walk the chosen direction screen by screen. The tree per screen: each state in its row (empty, loading, error, long content, no image), the mobile layout of its key block, dark mode when in scope, where motion happens and what reduced motion shows, and every `TODO(content)` still open (who supplies it, by when). Look up what the project already decides; ask only what it leaves open. Answers fill the **Screens** table and **Decisions**. Done when the frontier is empty.

Then show the full brief and set `Status: approved` only on the user's confirmation.
