# EUR/USD Receivable Hedge Model — Technical Specification

**Created by:** Arlen Dreewes  
**Updated by:** Arlen Dreewes  
**Date Created:** April 3, 2026  
**Date Updated:** April 24, 2026  
**Version:** 1.0  
**LLM Used:** None (Stage 2); Claude Sonnet 4 (Stage 3 documentation)

**Role:** Treasury / Risk Management  
**Audience:** CFO or Director of Treasury

**Purpose:** Document the analytical structure of the Stage 2 Excel hedge model, record design decisions and limitations, and specify an improved version suitable for AI-assisted reconstruction or audit.

---

## 1. Problem Statement

Our firm expects to receive **EUR 5,000,000** from a European customer on **August 1, 2026** — approximately **120 days** from the model inception date of April 3, 2026. The receivable is invoiced in euros, exposing the firm to full EUR/USD translation risk over that period.

At the current spot rate of **1.0820 USD/EUR**, the receivable carries a USD equivalent of approximately **$5,410,000**. Every one-cent move in EUR/USD shifts proceeds by **$50,000**. Over a 120-day horizon with EUR/USD historical volatility of roughly 7% annualized, a ±5% spot move ($±270,000) is a realistic planning range.

The objective is to evaluate four positions — no hedge, forward hedge, money market hedge, and EUR put option hedge — and provide a quantitative basis for a CFO-approved hedging decision. The decision context is corporate treasury; the criterion is protecting USD revenue while preserving a reasonable degree of upside optionality.

---

## 2. Inputs (Known Variables)

| Named Range   | Description                              | Unit       | Value      | Source                              |
|---------------|------------------------------------------|------------|------------|-------------------------------------|
| `FC_AMT`      | EUR receivable notional                  | EUR        | 5,000,000  | Contract / company data             |
| `S0_in`       | EUR/USD spot rate at inception           | USD/EUR    | 1.0820     | Bloomberg, April 3, 2026            |
| `F0_in`       | EUR/USD 120-day forward rate             | USD/EUR    | 1.0750     | Bloomberg indicative, April 3, 2026 |
| `R_USD`       | USD interest rate (annualized)           | Decimal    | 0.0525     | Fed Funds effective rate, Apr 2026  |
| `R_FC`        | EUR interest rate (annualized)           | Decimal    | 0.0390     | ECB deposit rate, Apr 2026          |
| `T_DAYS`      | Days to settlement                       | Days       | 120        | Derived from contract date          |
| `K_PUT`       | EUR put strike price                     | USD/EUR    | 1.0750     | Set at-the-money-forward            |
| `PREM_PUT`    | EUR put premium per EUR                  | USD/EUR    | 0.0120     | Indicative bank quote (~1.1% of notional) |
| `K_CALL`      | EUR call strike price (reference only)  | USD/EUR    | 1.0900     | OTM reference; not in primary hedge |
| `PREM_CALL`   | EUR call premium per EUR                 | USD/EUR    | 0.0090     | Indicative bank quote               |

**Derived Inputs (calculated from the above):**

| Derived Variable | Formula                         | Value      |
|------------------|---------------------------------|------------|
| `T` (years)      | `T_DAYS / 360`                  | 0.3333     |
| USD equiv. @ spot | `FC_AMT × S0_in`               | $5,410,000 |
| 1-cent sensitivity | `FC_AMT × 0.01`               | $50,000    |

---

## 3. Assumptions & Constraints

- **Day count:** ACT/360 throughout. All interest accruals are computed as `rate × (T_DAYS / 360)`, consistent with FX and money market convention.
- **Interest rate basis:** Both `R_USD` and `R_FC` are quoted as simple (not compounded) annual rates.
- **Forward rate:** Treated as a market-given input; independently verifiable via covered interest parity (`F0 = S0 × (1 + R_USD × T) / (1 + R_FC × T)`) but not derived from rates in the model.
- **Option premium timing:** `PREM_PUT` is paid upfront in USD and future-valued to settlement using `R_USD × T` to express cost on a consistent maturity basis.
- **Put strike:** Set at-the-money-forward (`K_PUT = F0_in = 1.0750`), which is standard market convention for vanilla hedging puts.
- **Bid-ask spreads:** Excluded. All spot, forward, and option prices treated as mid-market. Real execution will reduce proceeds modestly across all strategies.
- **Counterparty credit risk:** Not modeled. Forward contracts assume a bank-grade counterparty operating under an ISDA master agreement.
- **Margin/collateral:** No margin calls or collateral posting modeled for any strategy.
- **Call option:** Included as a reference input (`K_CALL`, `PREM_CALL`) but not incorporated into hedge outcome calculations; reserved for a future collar analysis.
- **No dynamic hedging:** All strategies are static (set-and-hold to maturity). Delta hedging and rolling hedges are excluded.

---

## 4. Calculation Flow

### 4.1 Forward Hedge

1. Multiply `FC_AMT` by `F0_in` to obtain locked-in USD proceeds.  
   → `USD_forward = FC_AMT × F0_in = 5,000,000 × 1.0750 = $5,375,000`  
2. This result is fixed regardless of future spot (`S_T`). No further inputs required.

### 4.2 Money Market Hedge

1. **Borrow PV of receivable in EUR:** Divide `FC_AMT` by `(1 + R_FC × T)` to obtain the EUR amount to borrow today such that the loan principal + interest equals the receivable at maturity.  
   → `EUR_borrow = 5,000,000 / (1 + 0.039 × 0.3333) ≈ EUR 4,935,834`

2. **Convert to USD at spot:** Multiply `EUR_borrow` by `S0_in`.  
   → `USD_spot = EUR_borrow × 1.0820 ≈ $5,340,573`

3. **Invest USD proceeds:** Multiply `USD_spot` by `(1 + R_USD × T)` to accumulate to maturity.  
   → `USD_mm = USD_spot × (1 + 0.0525 × 0.3333) ≈ $5,434,033`

4. **Parity check:** Compute `|USD_mm − USD_forward|`. Under covered interest parity this should be near zero; a divergence greater than $1,000 flags a rate-basis inconsistency.  
   → Current divergence: **$59,033** *(see Section 6 — model improvement required)*

### 4.3 EUR Put Option Hedge

1. **Total premium outlay:** `PREM_PUT × FC_AMT = 0.012 × 5,000,000 = $60,000`

2. **Future value of premium at maturity:** `$60,000 × (1 + R_USD × T) = $61,050`  
   This aligns the premium cost with the settlement date for consistent comparison.

3. **Payoff at maturity by scenario:**  
   - If `S_T < K_PUT` (put in-the-money): exercise put, sell EUR at strike.  
     → `USD_put = FC_AMT × K_PUT − FV_premium = $5,375,000 − $61,050 = $5,313,950` (floor)  
   - If `S_T ≥ K_PUT` (put out-of-the-money): let put expire, sell EUR at market.  
     → `USD_put = FC_AMT × S_T − FV_premium`

### 4.4 No-Hedge (Benchmark)

`USD_unhedged = FC_AMT × S_T` — computed for each scenario in the sensitivity table as a baseline.

---

## 5. Outputs

| Output Label               | Description                                                          | Format        |
|----------------------------|----------------------------------------------------------------------|---------------|
| `USD_forward`              | Locked-in USD proceeds under forward hedge                          | Single value  |
| `USD_mm`                   | USD proceeds under money market hedge                               | Single value  |
| `USD_put_floor`            | Minimum net proceeds with put exercised                             | Single value  |
| `USD_put_upside`           | Net proceeds at +5% spot (put expires)                              | Single value  |
| `USD_unhedged_downside`    | No-hedge proceeds at −5% spot (worst case)                          | Single value  |
| `Parity_gap`               | Absolute difference between MM and forward results                  | Single value  |
| **Sensitivity Table**      | USD proceeds for all four strategies across 11 `S_T` scenarios      | 11-row × 4-col table |
| **Chart: Hedge Outcomes**  | Line chart of USD proceeds vs. `S_T` for all four strategies        | Line chart    |
| **Summary KPI Block**      | Six key metrics with labels and notes for executive review           | Formatted table |

---

## 6. Model Review — What Worked & What to Improve

### What Worked

- **Named ranges** (`FC_AMT`, `S0_in`, `F0_in`, etc.) are implemented consistently and correctly referenced throughout calculations.
- **Color coding** (yellow inputs, green formulas, gray outputs) follows industry convention and makes the model auditable at a glance.
- **Option floor calculation** correctly future-values the premium to maturity before subtracting, yielding an apples-to-apples comparison with the forward.
- **Sensitivity table** spans a realistic ±5% range in equal steps, enabling clean chart production.
- **Notes & Assumptions sheet** documents all rate sources, day-count basis, and simplifications — a significant audit-trail benefit.

### What Should Be Improved

1. **Parity gap is too large ($59,033).** A correct money market hedge should produce a result within ~$100 of the forward hedge under covered interest parity. The current divergence suggests a rate-basis mismatch — likely that the 120-day forward rate provided (1.0750) is not consistent with the ACT/360 spot-and-rates combination. The improved model should derive `F0_implied = S0 × (1 + R_USD × T) / (1 + R_FC × T)` endogenously and flag if it diverges from the market forward by more than a defined tolerance (e.g., 10 pips).

2. **Call option is not integrated.** `K_CALL` and `PREM_CALL` are inputs but produce no outputs. The improved model should include a **zero-cost collar** section: buy put at `K_PUT`, sell call at `K_CALL`, net premium = `PREM_PUT − PREM_CALL`, with payoff logic for three regions: `S_T < K_PUT`, `K_PUT ≤ S_T ≤ K_CALL`, `S_T > K_CALL`.

3. **Sensitivity step size is irregular.** The current 11-scenario table uses a step of 0.01082 (1% of S₀), which produces uneven, hard-to-read spot rates. The improved model should use a clean step — e.g., 0.01 per step — producing round numbers for presentation.

4. **No break-even analysis.** The improved model should calculate and highlight the `S_T` at which the option hedge equals the forward hedge (i.e., the premium break-even rate), giving the CFO a concrete threshold for the hedge decision.

5. **Summary section lacks recommendation logic.** The CFO row is currently blank ("PENDING STAGE 4"). The improved model should include a conditional recommendation cell driven by a user-settable risk-preference input (e.g., "Protection-First" vs. "Cost-Minimizing").

---

## 7. Sensitivity Plan

The sensitivity table varies the future EUR/USD spot rate `S_T` across **11 scenarios**, centered on the current spot `S0_in = 1.0820`, spanning ±5%:

- **Range:** `S0_in × 0.95` to `S0_in × 1.05` (approximately 1.0279 to 1.1361)
- **Step size:** `S0_in × 0.01` per step (~108 pips) — *to be revised to a clean $0.01 step in the improved model*
- **Strategies compared:** (0) No hedge, (1) Forward, (2) Money Market, (3) EUR Put

The resulting line chart plots USD proceeds on the y-axis versus `S_T` on the x-axis. The most decision-relevant comparisons are:

- **No hedge vs. Forward:** illustrates the cost of certainty at varying spot outcomes
- **Forward vs. Put (floor):** shows where the premium cost exceeds the protection benefit
- **Put vs. No hedge at upside scenarios:** demonstrates retained upside from optionality

The ±5% range reflects approximately one standard deviation of EUR/USD movement over 120 days (7% annualized vol × √(120/365) ≈ 3.9%), making it a realistic rather than stress-test range.

---

## 8. Limitations & Next Steps

**Analytical exclusions:**
- Implied volatility and volatility smile effects on option pricing are not modeled; the premium is treated as a given input.
- Transaction costs, bid-ask spreads, and bank credit lines are excluded; real-world proceeds will be modestly lower across all strategies.
- Dynamic (delta) hedging, rolling hedges, and partial-hedge ratios are outside scope.
- FAS 133 / IFRS 9 hedge accounting treatment is not addressed.
- Correlation risk (e.g., EUR/USD moving in tandem with the underlying contract value) is not modeled.

**How this feeds Stage 4:**  
This specification will serve as the primary input to the Stage 4 AI prompt. The named ranges in Section 2 will become standardized variable names in the prompt. The calculation flow in Section 4 will become the instruction block for model generation. The improvement items in Section 6 will direct the AI to build the *enhanced* version — including the parity fix, collar strategy, clean step size, and break-even analysis — rather than replicate the Stage 2 prototype. The output table in Section 5 will define the exact deliverables the AI is expected to produce.
