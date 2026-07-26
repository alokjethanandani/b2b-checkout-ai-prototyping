# Operating Instructions — B2B Checkout POC

*Scoped to this project only (`b2b-checkout-poc-learn`). Finalized 2026-07-26.*

## 1. About Me

- **Name:** Alok
- **Role:** Lead Product Designer, 15+ years in B2B FinTech.
- **This project:** a public portfolio piece — a fictional SF food distributor B2B ordering/checkout prototype, built via a Figma design-system → Dev Mode MCP → Claude Code pipeline, to demonstrate AI-assisted prototyping and Figma MCP fluency. Target ship Aug 10, 2026. See `PRD.md` for full scope.
- **Pain points this project exists to close:**
  1. **Prototyping speed:** limited hands-on experience with Figma MCP + Claude Code makes high-fidelity prototyping slow. Expect me to need more explanation/checkpoints early on than a fluent user would.
  2. **Interview credibility gap:** I can't market myself as a "design engineer" or AI-native designer without a real, demoable, AI-built coded prototype to point to. This project *is* that proof point — treat polish and demoability as first-class, not nice-to-have.
  3. **Live demo reliability:** I need to run this in front of leadership and in usability studies with mock data that supports real CRUD (add/edit/delete), and reset cleanly between sessions. Fragile or manual-reset-required states are a real cost, not a minor inconvenience.
- **Tools:**
  - Figma (Dev Mode MCP) → Claude Code, for design-to-code generation.
  - Local persistence: **IndexedDB via Dexie.js**, behind a repository layer, with a one-action reset-to-seed for demo/test repeatability. (Decision + rationale logged in `PRD.md` §5 and §10; `json-server`/local API was considered and set aside for v1 — see PRD for why.)
  - **Version control / publishing: GitHub.** `PRD.md` (and this file) live in this repo and get pushed to a GitHub remote — GitHub is the source of truth, not just a local file. [Correction 2026-07-26: originally drafted as "no PM tool, PRD.md is local source of truth" — superseded by this.]

## 2. Building Anything

- PRD first, always: problem, success criteria, scope (in/out), constraints, plan, open questions. For this project, `PRD.md` is that document — extend it, don't fork a parallel one.
- New features or user stories get added to `PRD.md` §11 (User Stories backlog) before code is written against them.
- No code, no file, no design work starts until you've signed off on the relevant PRD section.
- Before proposing anything custom: check what's already in this repo and in `PRD.md` first. Don't reinvent what's already decided.

## 3. Pushback

- Vague requests get interrogated before I act on them, not guessed at.
- If something looks off — scope creep past the Aug 10 target, a weak assumption, a framing that doesn't hold up — I say so and explain why, before proceeding.
- If a new instruction contradicts something already decided in `PRD.md` (e.g. its Decisions or Non-goals sections), I flag the contradiction explicitly and ask which one wins. I never silently overwrite a locked decision.
- No reflexive agreement. If I think you're wrong, I say so.

## 4. Reversibility

- Before anything destructive or hard to undo in this repo or its data — deleting files, overwriting `PRD.md` content wholesale, bulk edits to seed/mock data, anything that would need to be reconstructed from memory — I show the plan, name what's irreversible, and wait for an explicit "proceed."
- Resetting mock/demo data via the dev "reset" action is expected and safe by design — that's a feature, not a destructive op requiring sign-off.

## 5. Note-Taking

- Capture decisions and open threads in `PRD.md` as they happen (Decisions, Open Questions sections), not after the fact.
- Checkpoint before switching between design work (Figma) and build work (Claude Code), or when a session runs long, so nothing gets lost in the handoff between modes.

## 6. Working Style

- Show reasoning, not just conclusions — especially on architecture calls like the persistence approach.
- Given the prototyping-speed pain point, default to the simplest path that still hits the "real, demoable, tested" bar — not the most impressive-looking one. Flag when a shortcut would compromise the interview-demo goal.
- If you say "things changed," treat that as a cue to re-check scope against `PRD.md`, not to patch silently around it.
