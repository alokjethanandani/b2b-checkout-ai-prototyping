# B2B Checkout POC — Fog City Food Distributor

## About the author

**Alok** — Lead Product Designer, 15+ years in B2B FinTech, currently focused on agentic AI workflows, AP/AR automation, and product design for complex financial workflows (exception handling, trust calibration, back-office automation).

[LinkedIn](https://linkedin.com/in/alokjethanandani) · [Portfolio](https://madebyalok.com)

## What it is

A public "learn in public" portfolio prototype demonstrating **AI-assisted, design-to-code prototyping**: a Figma design system handed to Claude Code via Figma's Dev Mode MCP server, generating a working B2B ordering + checkout flow directly from structured design context (tokens, layout, components) rather than a screenshot.

> Fictional brand, mock data, no real payments or backend — this is a public learning artifact, not production software. See [`PRD.md`](PRD.md) for full scope, decisions, and the user-story backlog.

## Scope

An interactive click-through prototype for a fictional SF food distributor (**Fog City Food Distributor**) selling to **Jaffa Hummus**, a restaurant pre-authenticated as the buyer persona. 

In scope:

- **Product catalog** — browse by category, with B2B unit types (case / lb / each)
- **Cart** — add, edit quantity, remove line items, running subtotal
- **Checkout** — choose credit card (with processing-fee disclosure) or ACH (with settlement-time disclosure); delivery date picker constrained by a cutoff rule and order minimum
- **Confirmation** — summary of the submitted order

No login/signup (pre-authenticated start), no real payment processing, no supplier-side admin.

## Why it exists

Two learning goals in one project:

1. **Figma Dev Mode MCP → Claude Code** — assemble a themeable design system in Figma (tokens + components adapted from Community kits), then generate the frontend from structured design context via MCP.
2. **A designed, rules-based B2B checkout flow** — payment-method tradeoffs (CC vs. ACH) and delivery-constraint UX, as a portfolio artifact for B2B FinTech / design-engineering roles.

## Tech

- Frontend: React + Tailwind (generated via Claude Code from Figma Dev Mode MCP context)
- Local persistence: IndexedDB via [Dexie.js](https://dexie.org/), behind a repository/data-access layer, with a one-action "reset to seed" for demos and usability studies
- Design: Figma, Dev Mode MCP server
- Runs **local only** — no deployment, no server process; demoed via screen recording or live walkthrough

## Getting started

Setup instructions will be added once the frontend scaffold lands (see `PRD.md` Phase 3). Expected shape:

```bash
npm install
npm run dev
```

## Project docs

- [`PRD.md`](PRD.md) — problem statement, scope, architecture decisions, and the full user-story backlog
- [`Operating-Instructions.md`](Operating-Instructions.md) — collaboration/working-style notes for this project
- [`LICENSE`](LICENSE) — MIT

## Status

Phase 0 (setup) complete. Target ship: **Aug 10, 2026**.
