# I can design

`/i-can-design` คือ skill ของ Claude Code ที่ **ถามเรื่องความรู้สึกของดีไซน์ก่อนวาดอะไรทั้งนั้น**: อยากให้ออกมารู้สึกแบบไหน ใครใช้ ชอบ/ไม่ชอบอะไร แล้วแปลงคำตอบเป็น brief ที่ตรวจได้จริง เสนอ 2–3 ทิศทางให้เลือก จากนั้นค่อย build และ review เทียบกับ brief พร้อมภาพ before/after ผลลัพธ์จึงเป็นดีไซน์ที่มีจุดยืนของคุณ ไม่ใช่ค่าเฉลี่ยของ AI (AI slop)

`/i-can-design` is a Claude Code skill that **asks how a design should feel before drawing anything**: the feeling, the audience, the references and anti-references. It turns the answers into a brief a reviewer can check, offers two or three directions, then builds and reviews the UI against that brief with before/after evidence. **It never commits or pushes on its own.**

## Flow

1. **Setup**: workspace, projects and their existing design systems, dependency install.
2. **Interview**: rounds of at most four questions, each with a recommended answer. Feeling words become observable criteria ("calm" = one accent hue, motion only on interaction, ≤ 200 ms). A slop list (gradient text, centered hero + three cards, invented testimonials, …) is shown, and you decide what stays.
3. **Brief + directions**: `designs/<slug>/brief.md` and `directions.html`, you pick, the brief is approved.
4. **Build**: routed by surface. Marketing pages lead with taste-skill; product UI (dashboards, forms, app screens) leads with your design system and ux-ui-agent-skills; impeccable sets the craft floor; Emil Kowalski's skill handles motion.
5. **Review**: screenshots per viewport, a verdict per brief criterion (Met / Not met / Unmeasured, each citing a file), a slop scan, one independent critic, one fix round.
6. **Hand-off**: commit only when you ask; `/retro` suggested.

Precedence when skills disagree: your instruction now → approved brief → your project's design system → dependency defaults.

## Install

**Plugin (recommended):**

```
/plugin marketplace add jolynestarchaser/I-can-design
/plugin install i-can-design@i-can-design
```

The command is then `/i-can-design:i-can-design`.

**By hand:** copy `skills/i-can-design` to `~/.claude/skills/`; the command is `/i-can-design`.

Restart Claude Code in the folder that holds your projects and run `/i-can-design setup` (plugin: `/i-can-design:i-can-design setup`).

## Usage

| Command | What it does |
|---|---|
| `/i-can-design <what to design>` | Interview → brief → directions; stops at the approved brief |
| `/i-can-design <Figma URL / site URL / screenshot / ABC-123>` | Same, starting from that input |
| `/i-can-design build <slug>` | Build from the approved brief, then review |
| `/i-can-design review <slug> [before\|after]` | Capture evidence and judge against the brief |
| `/i-can-design setup` | Setup check only |

Workspace files live in `.claude/i-can-design/` (config, briefs, evidence) and stay on your machine.

## Dependencies

Setup installs these from their upstream sources after asking; nothing from them is copied into this repository. Credit to their authors.

| Dependency | Need | Source | License |
|---|---|---|---|
| `ux-ui-agent-skills` (plugin) | required | [plugin87/ux-ui-agent-skills](https://github.com/plugin87/ux-ui-agent-skills) by Thientan Soparat | MIT |
| `impeccable` (plugin) | required | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) by Paul Bakaus | Apache-2.0 |
| `design-taste-frontend` | required for marketing pages | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | MIT |
| `emil-design-eng` (+ optional `review-animations`, `improve-animations`) | required | [emilkowalski/skills](https://github.com/emilkowalski/skills) by Emil Kowalski | MIT |
| `chrome-devtools-mcp` (plugin) | optional, screenshots | [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) | Apache-2.0 |
| `retro` | optional, user-invoked | [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock | MIT |

The slop list in `references/interview.md` draws on the ideas in [avoid-ai-design](https://github.com/funboy322/avoid-ai-design) by ungspirit (MIT); it is reworded, not copied.

Windows note: adding the ux-ui marketplace can fail with `invalid path 'design-systems/library/com7/DESIGN.md'`; setup explains the one-command workaround.

## License

MIT, see [LICENSE](LICENSE).
