# DECISION MEMO

| | |
|---|---|
| **TO** | Chief Financial Officer |
| **FROM** | Treasury / Risk Management |
| **DATE** | April 3, 2026 |
| **RE** | FX Receivable Exposure — EUR 5,000,000 Due August 1, 2026 |
| **CLASSIFICATION** | Internal — Confidential |

---

## 1. The Exposure

Our firm expects to receive **€5,000,000 (EUR)** from a European customer on **August 1, 2026** — approximately 120 days from today. At the current EUR/USD spot rate of **~1.0820**, this receivable has a USD equivalent of roughly **$5,410,000**.

Because the invoice is denominated in euros, we bear full currency risk between now and the settlement date. Every 1-cent move in EUR/USD shifts our USD proceeds by approximately **$50,000**.

---

## 2. Why This Is Risky

The EUR/USD pair can move materially in 120 days. Over the past two years the pair has traded in a range of roughly 1.02–1.12 — a 10-cent band worth **±$500,000** on our position. Key risk drivers include:

- **U.S. Federal Reserve policy** diverging from the ECB, driving dollar strength
- **Eurozone growth or inflation surprises** weakening the euro
- **Geopolitical shocks** (energy prices, trade tariffs) that historically spike EUR/USD volatility

**Downside scenario:** If EUR/USD depreciates to 1.03 by August, we would receive only ~$5,150,000 — a **$260,000 shortfall** versus today's rate. That is not immaterial relative to our operating margin on this contract.

---

## 3. Three Hedge Families — Quick Comparison

| Strategy | Mechanism | Pros | Cons |
|---|---|---|---|
| **Forward Contract** | Lock in a fixed EUR/USD rate today for Aug 1 delivery | Certainty; zero premium; simple execution | No upside if EUR strengthens; counterparty credit risk |
| **FX Options (Put on EUR)** | Buy the right to sell EUR at a strike rate | Full downside protection; retain upside if EUR rallies | Premium cost (~0.5–1.5% of notional); requires options desk |
| **Natural Hedge / Netting** | Offset EUR receivable by incurring EUR payables (e.g., EUR-denominated vendor payments) | No derivatives needed; reduces net exposure | Requires operational flexibility; rarely covers full exposure |

Each strategy produces a different risk/return profile. The right choice depends on our risk appetite, budget for premium costs, and CFO-approved hedging policy limits.

---

## 4. Next Steps — Analysis Roadmap (Stages 2–4)

| Stage | Deliverable | Purpose |
|---|---|---|
| **Stage 2 — Excel Model** | `.xlsx` scenario model | Compute hedge outcomes (forward, option, unhedged) across a rate range; show P&L sensitivity and break-even levels |
| **Stage 3 — Technical Spec** | Design document (`.md`) | Precisely document model logic; specify an improved version suitable for AI-assisted reconstruction or audit |
| **Stage 4 — Final Recommendation** | CFO presentation + structured AI prompt | Select optimal hedge strategy from model results; draft Board-ready recommendation and AI prompt for ongoing scenario analysis |

**Requested authorization:** Approval to proceed to Stage 2 modeling and to engage our banking counterparties for indicative forward and option quotes on the €5M Aug 1 position.

---

*Prepared by Treasury/Risk Management. Model outputs, market quotes, and final recommendation to follow in subsequent stages.*
