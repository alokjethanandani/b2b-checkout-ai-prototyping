# Mini-PRD — B2B FinTech Flow Rebuild: SF Food Distributor Ordering & Checkout

**Portfolio Project** · **Owner:** Alok · **Drafted:** July 26, 2026 · **Status:** Phase 0 complete (Jul 26) — starting Phase 1

> Public project demonstrating AI-assisted prototyping — a Figma design system handed to Claude Code via Dev Mode MCP. Target ship **Aug 10, 2026**.

---

## 0. TL;DR

Build an interactive, business-customer-facing B2B ordering + checkout prototype: a fictional SF food distributor selling to SF restaurants. Flow: product catalog → cart (editable) → checkout with credit card or ACH payment + delivery scheduling. Built in two learning motions — (a) assemble a themeable design system in Figma, adapted from free Community kits, and (b) use Figma's Dev Mode MCP server to hand that system to Claude Code, generating the working frontend directly from structured design context instead of a screenshot.

No production backend, no real payment processing, no proprietary/employer IP — fictional brand and mock data only. **Local-only mock persistence is in scope** (see §5) — needed for CRUD on cart/order data during usability studies and demos; this is not a "real backend" (no server code to write or infra to run), same spirit as the mock JSON product catalog.

## 1. Why this artifact

- **Learning:** hands-on, end-to-end with the Figma MCP pipeline — Dev Mode → Claude Code — plus building a token-based design system rather than one-off screens. This is the **AI-assisted design-to-code** proof point of this project: pairing a Figma design system with Claude Code via Dev Mode MCP.
- **Positioning:** demonstrates B2B FinTech breadth into B2B receivables-adjacent checkout — payment-method choice (CC vs ACH), delivery-constrained commerce. A distinct payment-design decision — real-time capture vs. deferred/policy-gated — worth surfacing in the design story.
- **Content:** a "learn in public" piece on the Figma MCP workflow itself — free Community kit → adapted design system → generated code — focused on the design-tooling workflow.

## 2. Success criteria

- **Learning:** can explain and demo the Dev Mode → MCP → Claude Code pipeline — a Figma frame becomes structured tokens/layout that Claude reads directly, not a screenshot it has to guess from.
- **Artifact:** demoable end-to-end click-through — browse products → add to cart → edit cart → checkout (choose CC or ACH) → pick delivery date → confirmation. Real design tokens driving the UI, not hardcoded hex/px values.
- **Content:** one build-in-public article + 2–3 LinkedIn posts + a portfolio case study with explicit decision rationale (CC-vs-ACH tradeoff, delivery-constraint handling).
- **Definition of done:** demoable click-through prototype, a presentable Figma design-system file, one article live. Not production-hardened; no real payments.

## 3. Scope

**In scope (v1):**

- Fictional supplier — **Fog City Food Distributor** (SF food distributor); restaurant-customer persona **Jaffa Hummus**, **pre-authenticated** (skip login/signup — start "signed in as Jaffa Hummus").
- Product catalog: food items with realistic B2B units (case / lb / each), category browse.
- Add to cart; cart review page with quantity edit, remove line item, subtotal.
- Checkout:
  - Payment method choice — **credit card** (mock card form + processing-fee disclosure) or **ACH** (mock "connect bank" instant-verification flow, no fee, settlement-time disclosure). **ACH selection pushes the earliest available delivery date out by a mocked clearing-time rule** (default: 3 business days, reflecting real-world standard ACH settlement of 1–3 business days) — food doesn't ship before payment clears. Checkout and confirmation copy discloses that delivery is contingent on the ACH payment settling and **subject to cancellation** if it fails to clear.
  - Delivery scheduling: date picker constrained by a mocked cutoff rule (e.g., orders after 2pm push to next available date) + a case-minimum or order-minimum rule + the ACH clearing-time push-out above (CC checkout is unaffected — its earliest date reflects only the cutoff/minimum rules).
  - Order confirmation screen.
- Figma design system: tokens (color, type, spacing) + core components (product card, cart line item, payment-method selector, date picker, buttons/forms) — adapted from a fintech kit + an ecommerce/checkout kit, then handed to Claude Code via Dev Mode MCP. Token structure built theming-ready (so a second supplier's palette could drop in later), but only one brand designed in v1.

**Non-goals (v1):**

- Real payment processing — no live Stripe/Plaid, mocked only.
- Login/signup, account management, order history/reorder, saved payment methods.
- Supplier-side admin/dashboard, multi-supplier marketplace.
- Invoicing, net payment terms, credit lines — excluded by design; CC/ACH only.
- Agentic behavior — this is a rules-based prototype, not an agent (that's artifacts #1 and #3).
- Multi-tenant theming *built out* — token structure is theming-ready, but only one brand is designed in v1.
- Login/signup screen — pre-authenticated start only.

## 4. Constraints & guardrails

- **No proprietary/employer IP.** Fictional brand, mock data only — framed publicly as "how I'd approach this today."
- **No real financial or irreversible actions** — all payment capture mocked.
- **Scope discipline** — v1 targets an **Aug 10** ship date; resist adding accounts, multi-supplier, or a real backend.
- Fits Mon/Tue "Learn & Build" blocks per the weekly cadence.

## 5. Architecture

- **Design system in Figma:** foundation from a fintech kit (tokens/components) + a checkout/ecommerce kit (cart/checkout interaction patterns), reskinned for food distribution (case-pack quantities, CC/ACH only, delivery scheduling). No B2B-specific Community kit exists for this — this is an adapted hybrid, not a straight reskin.
- **Figma Dev Mode MCP server** enabled on that file → connected to **Claude Code** → frames read as structured tokens/layout, not screenshots.
- **Frontend** generated via Claude Code from the Figma context — likely React + Tailwind (or plain HTML/CSS/JS), single-page prototype, mock JSON product catalog seeded into local storage on first load.
- **Local persistence (decided):** IndexedDB via Dexie.js, behind a thin repository/data-access module (e.g. `lib/data/*`) so the storage engine is swappable later. Chosen over a local API server (e.g. `json-server`) because it needs zero process management — one `npm run dev` command, nothing extra to remember to start before a live usability study or leadership demo. Include a **"reset mock data"** dev action that restores the seed dataset to a known state, so repeat demo/test runs don't drift.
  - *Alternative considered:* `json-server` (or a tiny Express + SQLite API) — would demonstrate real REST calls in the Network tab, a stronger "full-stack" interview beat, at the cost of a second process to run and more moving parts during a live session. Worth revisiting post-v1 if the interview story needs it; not the v1 default given the operational risk during live demos.
- Runs **local only** — demoed via screen recording or live walkthrough. No deployment step, no server process.

## 6. Learn-then-build ramp

1. Set up Figma Dev Mode + MCP server; confirm Claude Code can read a single frame's structured context (vs. a screenshot).
2. Assemble the design-system foundation (tokens, then 3–4 core components) in Figma.
3. Design the four screens (catalog, cart, checkout, confirmation) using those components.
4. Hand each frame to Claude Code via MCP; generate and wire up the click-through.

## 7. Phased build plan

- **Phase 0 — Setup (½ day): ✅ Done Jul 26.** Figma file created — [Fog City Provisions — B2B Checkout POC](https://www.figma.com/design/b5nyoACZ9hClgt96XWeKov) (fileKey `b5nyoACZ9hClgt96XWeKov`). ⚠️ **Rename pending:** supplier brand was renamed to **Fog City Food Distributor** (§9) after this file was created — the Figma file title still reads "Fog City Provisions." Rename the file in Figma before/during Phase 1 so doc and artifact stay in sync (Figma MCP tools weren't authenticated in this session to do it here). Dev Mode MCP confirmed live via the remote connector (no desktop toggle needed — auth was already in place). Verified end-to-end: created a test frame, read it back via `get_metadata` (structured XML) and `get_design_context` (React+Tailwind + node IDs + screenshot) — confirms Claude reads structured layout/tokens, not a screenshot guess. Test frame node `1:2`, ready to delete before Phase 1 design work starts.
- **Phase 1 — Design-system foundation (1–2 sessions):** tokens + core components, sourced/adapted from the two Community kits.
- **Phase 2 — Screen design (2 sessions):** catalog, cart review, checkout, confirmation frames built from the component set.
- **Phase 3 — MCP → code (2–3 sessions):** generate the frontend from Figma via Claude Code; wire cart state + mock checkout logic + delivery-cutoff rule + ACH clearing-time push-out rule.
- **Phase 4 — Polish + mock data (1 session):** realistic product catalog, case-pack units, fee/settlement disclosures.
- **Phase 5 — Demo + content (1–2 sessions):** screen-record the click-through, write the MCP-workflow article, cut LinkedIn posts.

## 8. The design story to capture (interview gold)

- **CC vs. ACH:** the fee-vs-speed tradeoff surfaced to the customer at the moment of choice — business-model fluency made visible. Sharpened by the clearing-time rule: ACH isn't just "no fee, slower disclosure copy" — it visibly pushes the delivery date out and carries a cancellation-if-payment-fails condition, so the tradeoff has real stakes attached, not just a line of fine print.
- **Delivery-constraint UX:** how a cutoff rule / order minimum shows up without feeling like a wall — trust calibration in a non-agentic UI. The ACH clearing-time push-out is the same problem in a second guise: communicating a payment-driven schedule constraint (and its cancellation risk) without making the customer feel penalized for choosing the no-fee option.
- **Editable cart before commit:** the "confirm, don't just submit" pattern — the same trust-calibration muscle as your agentic work, applied to a plain rules-based flow.
- **The MCP workflow itself:** tokens-in-Figma → structured context → generated code, and where it actually saved (or cost) time vs. hand-coding from a screenshot.

## 9. Open questions

_None outstanding — both resolved 2026-07-26, see §10._

## 10. Decisions (locked)

- Vertical: SF food distributor → SF restaurants, B2B online ordering. CC/ACH only — no invoicing, no net terms.
- Supplier brand: **Fog City Food Distributor** (supersedes earlier "Fog City Provisions" proposal — Figma file from Phase 0 still needs renaming to match, see §7).
- Restaurant-buyer persona: **Jaffa Hummus** — the pre-authenticated "signed in as" identity throughout the flow.
- No proprietary/employer IP; fictional brand + mock data only.
- Non-agentic — a designed, rules-based prototype (by design, distinct from agent-building work elsewhere in this portfolio).
- Target ship: **Aug 10**.
- Pre-authenticated start; no login screen in v1.
- Token structure theming-ready; single brand designed in v1.
- Runs local only, no deployment.
- MCP client: **Claude Code**.
- Local persistence: **IndexedDB (Dexie.js)** behind a repository layer, with a reset-to-seed dev action. No local API server in v1.

## 11. User Stories — Build & Test Backlog (for Claude Code)

Meta-instruction for Claude Code on this repo: **for each story below, implement the flow, then write a test that exercises the acceptance criteria before marking it done.** Prefer component/integration tests over pure unit tests where the story involves user interaction. Flag any story that can't be tested as written rather than skipping the test silently.

**Epic A — Product Catalog**
- **US-1:** As a restaurant buyer, I can browse the catalog by category, so I can find products without scrolling one long list.
  *AC:* categories render from mock data; selecting a category filters the grid; "All" shows everything. *Test:* filtering returns the correct product count per category.
- **US-2:** As a restaurant buyer, I can see each product's unit type (case / lb / each) on its card, so I understand what I'm ordering in.
  *AC:* unit type is visible on the card and carries through to cart/checkout unchanged.

**Epic B — Cart (CRUD)**
- **US-3:** As a restaurant buyer, I can add a product to my cart, so I can build an order.
  *AC:* add creates a new line item or increments quantity if already present. *Test:* adding the same product twice results in one line item with quantity 2, not two rows.
- **US-4:** As a restaurant buyer, I can edit a line item's quantity in the cart, so I can correct an order before checkout.
  *AC:* quantity input accepts only valid values for the unit type; subtotal recalculates on change. *Test:* editing quantity updates both the line total and cart subtotal.
- **US-5:** As a restaurant buyer, I can remove a line item from the cart, so I can drop something I don't want.
  *AC:* removal updates the cart list and subtotal immediately; removing the last item shows an empty-cart state. *Test:* removing an item drops it from persisted storage, not just the UI.
- **US-6:** As a restaurant buyer, my cart persists if I reload the page mid-session, so I don't lose my order.
  *AC:* cart state is read from IndexedDB on load and matches what was there before reload. *Test:* add → reload → cart contents unchanged.

**Epic C — Checkout: Payment**
- **US-7:** As a restaurant buyer, I can choose credit card or ACH at checkout and see the relevant disclosure (processing fee for CC, settlement time for ACH), so I understand the tradeoff before committing.
  *AC:* switching payment method updates the visible fee/settlement copy and any total shown; no real payment fields are transmitted anywhere. *Test:* selecting each method renders its specific disclosure text.

**Epic D — Checkout: Delivery Scheduling**
- **US-8:** As a restaurant buyer, I can pick a delivery date constrained by a cutoff rule (e.g. orders after 2pm push to next available date), so I can't select a date the supplier can't fulfill.
  *AC:* date picker disables/greys out invalid dates based on current mock time; rule is configurable, not hardcoded per-date. *Test:* mock "order placed at 2:01pm" scenario disables same-day delivery.
- **US-9:** As a restaurant buyer, I'm blocked from checking out below the order/case minimum, so I understand the supplier's ordering constraints.
  *AC:* checkout CTA is disabled with an explanatory message below minimum; enables once met. *Test:* cart below minimum cannot reach confirmation.
- **US-10:** As a restaurant buyer paying by ACH, my delivery date reflects ACH clearing time, so the supplier isn't shipping food before payment clears.
  *AC:* selecting ACH pushes the earliest available delivery date out by a configurable clearing-time rule (default: 3 business days), layered on top of the existing cutoff/minimum rules; selecting CC leaves the earliest date unaffected by this rule. Checkout and confirmation screens both disclose that delivery is contingent on the ACH payment settling and subject to cancellation if it fails to clear. *Test:* an otherwise-identical order shows a later earliest-delivery date under ACH than under CC; the cancellation-risk disclosure text is present on both the checkout and confirmation screens when ACH is selected, absent when CC is selected.

**Epic E — Confirmation**
- **US-11:** As a restaurant buyer, I see an order confirmation summarizing items, payment method, and delivery date, so I have a record of what I submitted.
  *AC:* confirmation reflects the exact cart/payment/delivery state at submit time, not live state. *Test:* placing an order and then editing "cart" (if reachable) doesn't retroactively change a past confirmation.

**Epic F — Demo & Test Infrastructure**
- **US-12:** As Alok running a usability study or leadership demo, I can reset mock data to its seed state with one action, so every session starts from a known baseline.
  *AC:* a dev-only "reset data" control clears IndexedDB and reseeds the catalog/cart/orders. *Test:* reset after a modified state returns storage to the exact seed snapshot.
- **US-13:** As Alok, every CRUD flow above has an automated test I can point to, so the prototype is demonstrably AI-built and tested, not just AI-styled.
  *AC:* test suite covers US-1 through US-12; `npm test` runs clean. *Test:* this is the meta-check — CI/local test run passes before a story is marked done.

---