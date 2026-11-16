# I can design — config

Values marked `<<FILL>>` are required. Setup asks for them in one message.

## Required

workspace_root: <<FILL>>

projects: <<FILL>>
<!-- one per line: name | path | stack | design system
     e.g. web | /path/to/web | Next.js + Tailwind | tokens in src/styles/tokens.css, components in src/ui
     A project with no design system yet: write `none`. -->

## Optional

report_language: English
<!-- language for interview questions, briefs and reviews -->

viewports: desktop 1440x900, mobile 390x844
<!-- evidence captures; add `tablet 834x1194` when the brief targets tablets -->

browser_tool: auto
<!-- auto = chrome-devtools MCP, else ux-ui-agent-skills gates (Playwright), else ask the user for screenshots -->

dev_url: none
<!-- e.g. http://localhost:3000; per project when different: web=http://localhost:3000 -->

team_rules: none
<!-- design and commit rules every build follows, one per line, e.g.
     "WCAG 2.2 AA minimum"
     "no new font files without design approval"
     "no AI attribution in commits" -->
