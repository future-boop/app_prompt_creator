# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Project Is

A web application that guides users through a 4-step pre-prompting workflow and produces a copy-paste master prompt for building webapps with Bolt, v0.dev, Lovable, or Google AI Studio.

The skill that defines the **complete interaction model** already exists at:
`C:\Users\usuario\Domingo-Miguel-AIOS\.claude\skills\webapp-prompt\SKILL.md`

That file is the canonical specification for the logic, questions, sector suggestions, and final prompt template. Read it before implementing any feature.

## Architecture Decision

Three UX approaches were brainstormed (see `.superpowers/brainstorm/`):

- **A — Conversational Chat**: AI asks questions, user types free-form. Requires AI backend.
- **B — Step-by-Step Wizard**: Multi-step form with progress bar, no AI backend needed.
- **C — Hybrid** (recommended): Structured steps with clickable options; AI generates the 5 sector-specific suggestions and compiles the final master prompt. Needs API key only for those two AI calls.

## Core Workflow (4 Steps)

1. **Step 0**: Sector pick → 5 app ideas → solution brief → optional URL style extraction
2. **Step 1 — Define the Project**: Problem statement, users, must-have features, what to skip
3. **Step 2 — Data Structure**: Main entity, schema generation with 5–6 sample rows, optional free API suggestion
4. **Step 3 — Features & UI**: Operations (CRUD options), layout, color style, UI extras
5. **Step 4 — Generate Master Prompt**: Compile everything into the structured template and output in a code block

## Six Supported Sectors

Food & Drinks, Furniture, Ceramic Tiles (B2B), Toys, Accounting, AI Automations

Each sector has 5 static webapp ideas in the skill file. The "Other" path uses AI to generate 5 custom ideas.

## Key Constraints

- The final prompt must always go in a code block (triple backticks) for clean copy
- Free tools (Bolt, v0.dev, Google AI Studio) listed before paid ones in the closing
- Sample data must be realistic and sector-specific — no "John Doe" or "example@email.com"
- MVP scope: no payments, no auth, no email/SMS notifications, no analytics in the generated prompt
- If a URL is provided for style extraction, skip the manual color question in Step 3

## Source Documents

- `The app prompt generator.md` — lesson content explaining the 4-step methodology and context engineering concepts (course material, not the app spec)
- `.superpowers/brainstorm/157-1781502574/content/interaction-model.html` — visual mockups of the three UX approaches
