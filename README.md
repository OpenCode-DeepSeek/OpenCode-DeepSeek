### OC · OpControl's agentic build system

OC is the coding agent behind OpControl IT Solutions projects. It runs **stock, unmodified OpenCode** on our self-hosted AI Homelab PC. Everything that makes it "OC" lives around it: a custom launcher, a multi-agent Dev Studio mode, persistent memory and private search.

#### The stack

- **OC Launcher** (Textual TUI): the front door to every session. User selection with PIN, then a choice of mode:
  - **Normal mode**: one agent, pick the model (day to day: DeepSeek V4.1 Flash).
  - **Dev Studio mode**: the full multi-agent team below, for larger builds.
  - Session-lock recovery, so a crashed or stuck session never leaves a dead terminal, and a clean return to the menu after each session.
- **MemPalace**: persistent memory across sessions, so project context survives restarts.
- **SearXNG**: private, self-hosted web search for research.
- **Image generation MCP**: design assets, icons and artwork from inside a build.
- **Job prompts and reports**: every build starts from a structured markdown prompt (scope, rules, non-goals, "done when" checklist) and ends with a written report.

#### Dev Studio team

| Agent | Role | Model |
|---|---|---|
| Orchestrator | Runs the precheck, plans the build, coordinates the team, deploys | DeepSeek V4 Pro |
| Researcher | Looks up docs, versions and best practices before anything is built | Inkling (Thinking Machines) |
| Explorer | Maps the existing codebase and infrastructure | DeepSeek Flash |
| Designer | UI/UX layouts and visual design | Kimi K2.6 |
| Builder | Writes and wires the code | DeepSeek V4 Pro |
| Reviewer | Tests and reviews; nothing ships without a pass | Qwen 3.6 Plus |
| Artist | Images and visual assets | Gemini 3.5 Flash |

Every Dev Studio build follows the same phases: **precheck** (ping every agent, verify tools, load memory) → research → map → design → plan → build → review → assets → deploy, with a build diary kept along the way. The model lineup changes as better models come out.

#### How we work

Ziur decides what to build. Claude handles planning, design and review, and writes the job prompts. OC builds, tests on staging first, deploys with backups, and reports back. Each job report is reviewed before the next job starts.
