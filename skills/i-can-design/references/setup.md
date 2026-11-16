# Step 0 — Setup Check

Run before every I can design run (and alone for `/i-can-design setup`). The person running it installed the skill; interview them for anything you cannot find. Report one line per check: `OK`, `FIXED`, `WARNING` or `MISSING`. Do not start step 1 while a `MISSING` is open.

## 1. Workspace and config

File: `<workspace>/.claude/i-can-design/config.md` (workspace = the folder Claude Code was started in).

1. When `config.md` does not exist, ask first, before creating any file:

   ```text
   I can design keeps its config, briefs and evidence in <current folder>/.claude/i-can-design/.
   1. Is <current folder> your workspace (the folder you will start Claude Code in for design work)?
   2. Which folder holds your projects? (suggested: <current folder>)
   ```

   - No to 1: create nothing; tell the user to restart Claude Code in the folder they name and run `/i-can-design setup` there, then stop.
   - Yes: create `config.md` from `config.template.md` (in this skill's folder).
2. Collect every `<<FILL>>` in **one** message, with suggestions the user confirms or corrects:
   - `projects`: list folders under `workspace_root` (depth 1–2) holding a `package.json`, `pubspec.yaml`, `*.xcodeproj` or `build.gradle*`. For each, suggest the stack from its manifest and the design system from what exists: token files (`tokens*.json`, `*tokens*.css`, `theme.*`, Tailwind `@theme` / config), a component folder, `DESIGN.md` / `PRODUCT.md`, Storybook.
   - Optional fields: show the default and say the user may keep it.
3. Write the answers, show the final file. Never guess a required value. An older `config.md` missing template keys gets them added with defaults; say which.

## 2. Dependency skills and plugins

A skill counts as installed when it appears in this session's skill list (plugin skills carry a prefix, e.g. `ux-ui-agent-skills:design-review`) or its `SKILL.md` exists in `~/.claude/skills/<name>/` or `<workspace>/.claude/skills/<name>/`.

| Dependency | Need | Used for | Install |
|---|---|---|---|
| `ux-ui-agent-skills` (plugin) | required | tokens, components, a11y, quality gates, `design-critic` agent | `/plugin marketplace add plugin87/ux-ui-agent-skills`, then `/plugin install ux-ui-agent-skills@ux-ui-agent-skills` |
| `impeccable` (plugin) | required | craft floor, critique, audit, polish, harden | `/plugin marketplace add pbakaus/impeccable`, then `/plugin install impeccable@impeccable` |
| `design-taste-frontend` | required for marketing surfaces | art direction, layout and copy for landing pages and portfolios | `https://github.com/Leonxlnx/taste-skill` → `skills/taste-skill`, copied to `~/.claude/skills/design-taste-frontend` |
| `emil-design-eng` | required | motion, interaction and polish decisions | `https://github.com/emilkowalski/skills` → `skills/emil-design-eng` |
| `review-animations`, `improve-animations` | optional | deeper motion review | `https://github.com/emilkowalski/skills` → `skills/<name>` |
| `chrome-devtools-mcp` (plugin) | optional | screenshots for evidence | `/plugin install chrome-devtools-mcp@claude-plugins-official` |
| `retro` | optional, user-invoked | improve the environment after a design | `https://github.com/mattpocock/skills` → `skills/engineering/retro` |

If any are missing:

1. Show one list: each missing dependency, required or optional, what it is for, its source. Ask which to install; default is all required ones.
2. Folder skills: install with Bash (Git Bash, macOS, Linux). Clone each source once, copy only the listed folders, never overwrite an existing folder:

   ```bash
   tmp="$(mktemp -d)"
   git clone --depth 1 https://github.com/Leonxlnx/taste-skill.git "$tmp/taste"
   cp -r "$tmp/taste/skills/taste-skill" ~/.claude/skills/design-taste-frontend
   git clone --depth 1 https://github.com/emilkowalski/skills.git "$tmp/emil"
   cp -r "$tmp/emil/skills/emil-design-eng" ~/.claude/skills/
   ```

3. Plugins: give the user the `/plugin` commands to type; a session cannot run slash commands for them. On Windows, `/plugin marketplace add plugin87/ux-ui-agent-skills` can fail with `invalid path 'design-systems/library/com7/DESIGN.md'` (`com7` is a reserved name for Git on Windows). Tell the user and offer the workaround, which they choose: clone it once with `git -c core.protectNTFS=false clone https://github.com/plugin87/ux-ui-agent-skills.git <folder>` and add that folder as the marketplace (`/plugin marketplace add <folder>`). The setting applies to that one command only; it lets Git write the `com7` folder, which some Windows versions still refuse, so treat it as a best effort.
4. ux-ui render gates need a browser: inside the plugin folder `npm install && npx playwright install chrome`. Without it they print `SKIPPED`; report that as a `WARNING` and treat every render check as `unmeasured`.
5. Confirm each install; newly installed skills and plugins appear after a Claude Code restart.
6. A declined required dependency: continue only with the user's agreement and name the fallback (write the route's rules from the brief alone; mark the review "no <dependency>").

## 3. Projects

For each project in config: the path exists; the design-system entry still points at files that exist. A project whose design system is `none` gets a `WARNING`: the build will create tokens first (ux-ui `brandkit` or `design-tokens`).

## 4. Evidence tool

Resolve `browser_tool`: the chrome-devtools MCP responds (`list_pages`), else the ux-ui gates have a browser, else `WARNING — no browser: evidence comes from user screenshots, render checks unmeasured`.
