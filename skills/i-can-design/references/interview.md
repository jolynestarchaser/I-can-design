# Step 3 — The design interview

The interview is the product. Its job: turn "make it look good" into decisions the person owns, so the build has a point of view that is theirs, not the model's average.

## How to ask

Load `grilling` and run its rounds: this file is the **design tree** it walks (job → feeling → references → constraints), and the rounds below are its usual frontiers. A later branch opens as soon as its prerequisites are settled, so a short request can cover two rounds at once.

- At most **four questions** per round, in `report_language`. Each question opens with the decision in plain words, then a **recommended answer** with a one-line reason drawn from what you already know (input, project, earlier answers). The user can reply "ok" to take every recommendation.
- Facts are your job, decisions are theirs. Anything you can read from the project (stack, existing tokens, fonts in use, component library) you look up and state as a fact in the round, not a question.
- After each round, say in one line what the answers settled and what is still open.
- When the user says "you decide", take the recommendation and record it as an **assumption** in the brief. Assumptions are shown back at approval.
- Stop when every section of the brief has an answer or an assumption. Typical: three or four rounds; a small component can finish in one.

## Round 1 — the job

1. **What and where**: the screen(s) or component, the project (from config), new or redesign.
2. **Who and the one action**: the main audience, and the single thing they should do or understand on this surface.
3. **Content**: real copy, data and images available, or placeholders now?
4. **Done looks like**: how the person will judge it (ship to production, pitch to a client, explore a direction).

## Round 2 — the feeling

The heart of it. Ask for **three feeling words** (e.g. calm, confident, warm). Then, for each word, propose what it means *on screen*, using the feeling dictionary below as a starting point, and ask the user to confirm or correct:

> "Calm" for this page would mean: one accent colour, generous spacing (section padding ≥ 96px desktop), motion only on user action, under 200ms. Right, or calmer / livelier?

Each confirmed word becomes one or more **criteria**: things a reviewer can observe in a screenshot, the code or a measurement. A word that cannot be made observable is not done; ask again with a concrete pair ("closer to A or B?").

Also ask the **opposite**: "What should it never feel like?" (e.g. corporate, cheap, busy). Each answer becomes a guardrail criterion.

## Round 3 — references

1. **Likes**: up to three products, sites, Dribbble/Behance shots or screenshots, and *what exactly* about each (the type, the density, the motion), not the whole thing.
2. **Anti-references**: one or two things it must not look like, and why.
3. **Slop check**: show the slop list below and ask which of these the person actually wants. Every item they keep needs a reason in the brief; the rest are banned for this design.

Open URLs and screenshots the user gives and describe back what you see in them before writing it down; a misread reference poisons the brief.

## Round 4 — constraints

1. **System**: the existing design system wins (precedence 3). Confirm what may change: nothing (use it as is), extend (new tokens or components allowed), or new.
2. **Accessibility**: WCAG level (default 2.2 AA), reduced-motion behaviour, minimum target size.
3. **Themes and devices**: light, dark or both; which viewports matter most.
4. **Motion appetite**: none, functional only, or expressive (and where).

## Feeling dictionary

Starting points to make words observable. Adjust to the product; never paste a row unchanged without the user confirming it.

| Word | Observable on screen |
|---|---|
| calm | 1 accent hue; spacing in ≥ 8px steps with large section gaps; motion only on user action, ≤ 200ms, ease-out; no autoplay |
| premium | restrained palette (≤ 2 neutrals + 1 accent); display type with tight tracking and a clear scale jump; real photography or none; no stock-icon grids |
| trustworthy | plain verbs in buttons; proof the user supplies (real logos, real numbers) or none; one consistent alignment grid; AA contrast or better on all text |
| playful | one unexpected element per section (shape, rotation, illustration); springy motion on interaction (overshoot ≤ 10%); radii ≥ 12px |
| technical / precise | monospace for data only; dense but aligned tables; 1px hairlines; numbers right-aligned with tabular figures |
| editorial | strong type hierarchy with a serif or high-contrast display face; measure 60–75ch; images with captions; asymmetric layout |
| energetic | high-contrast accent; hero type ≥ 64px; one signature scroll move, nothing else animates on scroll |
| warm | warm neutrals (not pure #fff / #000); human imagery; softer radii; friendly microcopy |

## Slop list

Defaults that read as AI-generated when they appear without a reason. Present them neutrally; the user decides which stay.

- Purple-to-blue or rainbow gradients, gradient text on headlines.
- One default sans (often Inter) for everything with no scale contrast.
- Centered hero, then three identical feature cards, then a CTA band.
- Emoji or generic line icons as feature illustrations.
- Glassmorphism and glow on every surface.
- Invented testimonials, logos, user counts or star ratings.
- Decorative step numbers (01 / 02 / 03), uppercase tracked eyebrows over every heading.
- "Tasteful AI" palettes picked by reflex: cream with terracotta, near-black with acid green.
- Every element fading up on scroll.
- Lorem ipsum or vague copy ("Unlock your potential", "Seamless experience").
