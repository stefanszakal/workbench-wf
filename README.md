# Workbench WF

A Claude Code skill for generating high-fidelity wireframes as self-contained HTML files.

## What it does

- Generates wireframes through conversation: idea → requirements → HTML output
- Produces clean, black-and-white wireframes optimized for developer handoff
- Includes desktop and mobile component libraries
- Uses shadcn/Radix naming conventions for easy translation to production code

## Installation

Clone this repo to your Claude Code skills directory:

```bash
git clone https://github.com/stefanszakal/workbench-wf ~/.claude/skills/workbench-wf
```

Or download and unzip to `~/.claude/skills/workbench-wf/`.

## Usage

In any Claude Code conversation:

```
/workbench-wf
```

Then describe what you want to wireframe:

- "Wireframe a dashboard for a project management app"
- "Design a checkout flow for mobile"
- "Sketch out a settings page with user preferences"

## Visual Language

All wireframes follow a consistent style:

| Element | Specification |
|---------|---------------|
| Borders | 1.5px solid black |
| Corners | `rounded-md` (avatars: `rounded-full`) |
| Colors | Black, white, grays only |
| Typography | System fonts, weight-based hierarchy |
| Shadows | Simple offset, no blur |

## Included Assets

```
workbench-wf/
├── SKILL.md                          # Skill instructions
├── README.md                         # This file
└── assets/
    └── workbench-template/
        ├── index.html                # Workbench documentation template
        └── pages/
            ├── components.html       # Desktop component library
            ├── components-mobile.html # Mobile component library
            ├── home.html             # Sample web page
            └── mobile-app.html       # Sample mobile app
```

## Part of the Workbench Series

| Skill | Stage | Purpose |
|-------|-------|---------|
| **workbench-wf** | Wireframe | Structure, layout, flow (this skill) |
| workbench-staging | Front-end | Component code, styling, interactions |
| workbench-prod | Full-stack | Back-end integration, ship-ready |

## License

MIT
