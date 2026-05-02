# STAGE 4 — FX HEDGE FINAL ANALYSIS & RECOMMENDATION

| | |
|---|---|
| **TO** | Chief Financial Officer |
| **FROM** | Arlen Dreewes, Treasury / Risk Management |
| **DATE** | May 1, 2026 |
| **RE** | Final Hedge Recommendation — EUR 5,000,000 Receivable Due August 1, 2026 |
| **CLASSIFICATION** | Internal — Confidential |

---

## A. Exposure Summary

Our firm holds a confirmed EUR **5,000,000** receivable from a European customer, due **August 1, 2026** — approximately **120 days** from model inception (April 3, 2026). The invoice is denominated in euros, so we carry full EUR/USD translation risk until settlement.

At the April 3 spot rate of **1.0820**, the receivable carried a USD equivalent of **$5,410,000**. The key risk metric: **every one-cent move in EUR/USD shifts USD proceeds by $50,000**. Over a 120-day horizon with EUR/USD historical volatility of approximately 7% annualized, a ±5% spot move represents a realistic planning range of **±$270,000** — a range that is not immaterial relative to operating margins.

The firm's objective is to protect USD cash flows while retaining some degree of upside optionality if the euro appreciates. The following analysis evaluates four strategies: no hedge, forward contract, money market hedge, and EUR put option.

---

## B. Summary of Hedge Outcomes

The Stage 2 model evaluated each strategy at a spot rate of 1.0820 and across an 11-scenario sensitivity table (S_T ranging from 1.0279 to 1.1361). Key results:

| Strategy | USD Outcome | Nature of Result |
|---|---|---|
| **Forward Hedge** | **$5,375,000** | Certain; locked in regardless of S_T |
| **Money Market Hedge** | **$5,434,033** | Synthetic forward; modeled divergence noted |
| **Put Option (floor)** | **$5,313,950** | Minimum if EUR depreciates below 1.0750 |
| **Put Option (upside @ +5%)** | **$5,619,450** | Net of premium FV; upside fully retained |
| **No Hedge (worst case, −5%)** | **$5,139,500** | Fully exposed; $235,500 below forward |

**Forward Hedge:** Selling EUR forward at 1.0750 locks in $5,375,000 unconditionally. The CFO can budget this figure with certainty. The trade-off is forfeiting any appreciation if EUR/USD rises above 1.0750 — at +5% spot (1.1361), the no-hedge outcome ($5,680,500) would exceed the forward by $305,500.

**Money Market Hedge:** Borrowing the present value of the receivable in EUR, converting to USD at spot, and investing USD yields approximately $5,434,033 — theoretically equivalent to the forward under covered interest parity (CIP). However, the model flags a **$59,033 parity gap**, which indicates the market-given forward rate of 1.0750 is not fully consistent with the 5.25%/3.90% interest rate inputs. In a real execution, a treasury team would reconcile this before executing; the divergence suggests either the forward is slightly stale or the rates reflect different day-count bases. The money market hedge also requires drawing on a credit facility and tying up a USD investment position for 120 days — a meaningful liquidity consideration.

**EUR Put Option:** Purchasing a 120-day EUR put at the at-the-money-forward strike of 1.0750 costs $60,000 upfront ($61,050 future-valued to maturity). This provides a floor of $5,313,950 if EUR weakens, while preserving the full upside if EUR strengthens. At +5% spot, net proceeds reach $5,619,450 — over $244,000 above the forward outcome. The premium represents approximately **1.1% of notional** and is the explicit cost of optionality.

**No Hedge:** Unhedged proceeds equal FC_AMT × S_T. This is the baseline risk position. At the current spot of 1.0820, proceeds are $5,410,000 — $35,000 above the forward. But downside is uncapped: at 1.0279 (−5%), proceeds fall to $5,139,500, a $235,500 shortfall versus the forward with zero premium protection.

---

## C. Sensitivity Interpretation

The sensitivity table spans S_T from **1.0279 (−5%)** to **1.1361 (+5%)**, producing the following strategic picture:

**EUR Depreciation Scenarios (S_T < 1.0750):**
- The forward hedge and money market hedge hold constant at $5,375,000 and $5,434,033 respectively, regardless of how far EUR falls.
- The put option activates its floor at $5,313,950, protecting against further depreciation at the cost of the $61,050 premium.
- The no-hedge position deteriorates linearly; at the −5% scenario it reaches only $5,139,500 — the worst outcome across all strategies.
- **Key takeaway:** The forward dominates the put in pure downside protection because the put floor ($5,313,950) is $61,050 below the forward ($5,375,000). The premium is the explicit price of optionality.

**EUR Appreciation Scenarios (S_T > 1.0750):**
- The forward hedge remains fixed at $5,375,000, meaning all appreciation upside is forfeited once EUR strengthens past the forward rate.
- The put option expires worthless, and net proceeds = FC_AMT × S_T − $61,050. At S_T = 1.0820 (current spot), this yields $5,348,950; at S_T = 1.1361 (+5%), it yields $5,619,450.
- The no-hedge position outperforms all hedged strategies in appreciation scenarios, reaching $5,680,500 at +5%.
- **Key takeaway:** The put option is the only strategy that participates in upside while still providing a floor. The break-even S_T relative to the forward is approximately **1.0872** — the spot rate at which the put's net proceeds (S_T × FC_AMT − $61,050) equals the forward's $5,375,000. Above this rate, the option is superior to the forward; below it, the forward provides better net proceeds.

**Summary of trade-offs across the ±5% range:**

| Scenario | No Hedge | Forward | Put Option |
|---|---|---|---|
| −5% (1.0279) | $5,139,500 | $5,375,000 | $5,313,950 |
| Spot (1.0820) | $5,410,000 | $5,375,000 | $5,348,950 |
| +5% (1.1361) | $5,680,500 | $5,375,000 | $5,619,450 |
| **Range** | **$541,000** | **$0** | **$305,500** |

The option compresses the outcome range to $305,500 while preserving meaningful upside — roughly 56% of the unhedged range, at a cost of $61,050.

---

## D. Strategic Recommendation

**Recommended Strategy: EUR Put Option (at-the-money-forward strike, 1.0750)**

The EUR put option best serves our risk profile given the following model-supported rationale:

1. **Downside floor is adequate.** The option floor of $5,313,950 is $174,450 above the worst-case unhedged outcome at −5% ($5,139,500). The $61,050 premium buys $174,450 of downside protection — a 2.86:1 protection ratio.

2. **Upside is material.** The current macro environment features genuine EUR/USD uncertainty — diverging Fed/ECB policy, ongoing trade tariff discussions, and Eurozone growth uncertainty. EUR appreciation is a credible scenario, not a remote tail event. The put preserves full participation in this upside.

3. **Break-even is achievable.** EUR/USD need only move approximately 50 pips above the current forward (to ~1.0872) for the put to match forward proceeds. This is well within the expected volatility range.

4. **The forward's certainty is valuable but costly in this context.** A forward hedge is optimal when upside optionality has no strategic value and budget certainty is paramount. In our case, the contract proceeds are not tied to a fixed-price commitment that would make a $305,000 upside swing irrelevant. The option preserves value in scenarios that are reasonably probable.

5. **The money market hedge is not recommended.** The $59,033 parity gap raises execution confidence concerns, and the strategy requires drawing on credit lines and maintaining a USD investment for 120 days — adding liquidity complexity without meaningful benefit over the forward.

---

## E. Executive Justification

**Cash Flow Stability:** The put option guarantees a minimum USD receipt of $5,313,950, providing a reliable floor for budgeting and cash planning purposes. This figure should be used as the conservative planning figure in the FY2026 revenue forecast.

**Budget Certainty vs. Optionality:** Unlike a forward contract, the put allows treasury to capture additional USD revenue if EUR strengthens beyond the 1.0872 break-even. In a year with elevated macro uncertainty, this optionality carries real value. The $61,050 premium is a modest and bounded cost to preserve it.

**Liquidity Impact:** The put requires a $60,000 upfront cash outlay — a manageable and predictable cost. In contrast, the money market hedge draws on a credit facility for 120 days, which has implicit cost (line fee, opportunity cost) and balance sheet implications that are excluded from the model but real in execution.

**Optionality Value:** The option's asymmetric payoff profile is particularly well-suited to the current FX environment. The put provides insurance against EUR weakness while retaining full exposure to EUR strength — a profile that a forward contract structurally cannot replicate.

**Premium Costs:** The $61,050 FV premium (1.1% of notional) is within normal market range for an ATM put on EUR/USD with a 120-day tenor. It should be treated as a cost of doing business and expensed in the current period, consistent with hedge accounting treatment for options not designated under ASC 815.

**Accounting Implications (Note):** If the firm elects to designate this as a cash flow hedge under ASC 815 (FAS 133), the option's intrinsic value changes would flow through OCI, with time value changes in P&L. A formal hedge designation memo would need to be prepared at inception. If not designated, mark-to-market changes go through P&L immediately. Treasury should consult with the Controller on designation election prior to execution.

---

## F. Structured AI Prompt

### Appendix: AI Prompt for FX Hedge Spreadsheet Regeneration

---

```
# GOAL

Create a complete Excel workbook (fx_hedge_model.xlsx) modeling four FX hedging 
strategies for a EUR receivable: No Hedge, Forward Hedge, Money Market Hedge, and 
EUR Put Option Hedge. The model must include an input section with named ranges, 
four calculation sections, an 11-scenario sensitivity table, a summary KPI block, 
and verification checks. Follow all formatting, naming, and calculation conventions 
exactly as specified below.

---

# INPUT VARIABLES

Use these exact named ranges and values. Do not infer missing data.

| Named Range  | Value       | Description                              | Unit    |
|--------------|-------------|------------------------------------------|---------|
| FC_AMT       | 5,000,000   | EUR receivable notional                  | EUR     |
| S0_in        | 1.0820      | EUR/USD spot rate at model inception     | USD/EUR |
| F0_in        | 1.0750      | EUR/USD 120-day forward rate             | USD/EUR |
| R_USD        | 0.0525      | U.S. interest rate, annualized           | Decimal |
| R_FC         | 0.0390      | EUR interest rate, annualized            | Decimal |
| T_DAYS       | 120         | Days to settlement                       | Days    |
| K_PUT        | 1.0750      | EUR put strike price (ATM-forward)       | USD/EUR |
| PREM_PUT     | 0.0120      | EUR put premium per EUR                  | USD/EUR |
| K_CALL       | 1.0900      | EUR call strike (reference only)         | USD/EUR |
| PREM_CALL    | 0.0090      | EUR call premium per EUR                 | USD/EUR |

Derived inputs (use Excel formulas, do not hardcode):
- T = T_DAYS / 360         (label: "Time Horizon in Years")
- USD_spot_equiv = FC_AMT × S0_in   (label: "USD Equivalent @ Spot")
- cent_sensitivity = FC_AMT × 0.01  (label: "1-Cent Move Impact")

---

# MODEL LOGIC

## SECTION 1 — INPUTS
Place all named ranges in a formatted table with columns: [Label | Value | Named Range | Source/Notes].
Apply YELLOW background fill to all input value cells.
Apply BLUE background fill to all assumption/derived input cells.

## SECTION 2 — FORWARD HEDGE
Formula: USD_forward = FC_AMT × F0_in
Label result "Locked-In USD Proceeds." Mark as GREEN (formula).
Note: This value is constant regardless of future spot rate.

## SECTION 3 — MONEY MARKET HEDGE (3 steps)
Step [a]: EUR_borrow = FC_AMT / (1 + R_FC × T)
  → Label: "Borrow PV of EUR Receivable"
Step [b]: USD_spot = EUR_borrow × S0_in
  → Label: "Convert EUR Loan to USD at Spot"
Step [c]: USD_mm = USD_spot × (1 + R_USD × T)
  → Label: "Invest USD to Maturity"

Parity Check: =ABS(USD_mm − USD_forward)
  → Label: "Parity Check |MM − Forward| (target: < $1,000)"
  → Apply conditional formatting: RED fill if value > 1000, GREEN fill if ≤ 1000.

Also compute the CIP-implied forward for comparison:
  F0_implied = S0_in × (1 + R_USD × T) / (1 + R_FC × T)
  → Label: "CIP-Implied Forward Rate"

## SECTION 4 — EUR PUT OPTION HEDGE
Step [a]: PREM_TOTAL = FC_AMT × PREM_PUT
  → Label: "Total Put Premium (upfront USD)"
Step [b]: FV_PREM = PREM_TOTAL × (1 + R_USD × T)
  → Label: "FV of Premium at Maturity"
Step [c]: PUT_FLOOR = FC_AMT × K_PUT − FV_PREM
  → Label: "Floor: Minimum USD Proceeds (put exercised)"
Step [d]: PUT_UPSIDE = FC_AMT × S0_in − FV_PREM
  → Label: "Net Proceeds at Current Spot (put expires)"

Break-even spot rate:
  S_BREAKEVEN = (USD_forward + FV_PREM) / FC_AMT
  → Label: "Break-Even S_T vs. Forward"
  → Note: "Above this rate, put outperforms forward on net proceeds"

## SECTION 5 — SENSITIVITY TABLE
Build an 11-row × 5-column table.

Columns: [S_T | No Hedge | Forward Hedge | Money Market | Put Option]
Rows: S_T from (S0_in × 0.95) to (S0_in × 1.05) in equal steps of (S0_in × 0.01)
  → Use a formula: first row = S0_in × 0.95; each subsequent row = prior row + S0_in × 0.01

Formulas for each strategy at each S_T:
  - No Hedge:      FC_AMT × S_T
  - Forward:       USD_forward (constant)
  - Money Market:  USD_mm (constant)
  - Put Option:    IF(S_T < K_PUT, PUT_FLOOR, FC_AMT × S_T − FV_PREM)

Apply alternating row shading (light gray / white) for readability.
Mark the row where S_T is closest to S0_in with a BOLD border.

## SECTION 6 — SUMMARY OUTPUT (KPI Block)
Build a 7-row summary table with columns: [Metric | Value | Notes]
Apply GRAY background to all cells in this section.

Rows:
1. Forward Hedge — Locked USD          | =USD_forward       | "Certain; no upside"
2. Money Market Hedge — Locked USD     | =USD_mm            | "Should ≈ Forward (see parity check)"
3. Put Option Floor (put exercised)    | =PUT_FLOOR         | "Minimum net proceeds"
4. Put Option Upside @ +5% Spot        | [S_T=S0×1.05 put]  | "Put expires; upside retained"
5. No Hedge @ −5% Spot (worst case)   | [S_T=S0×0.95]      | "Unprotected downside"
6. Put Premium Cost (upfront USD)      | =PREM_TOTAL        | "Cash outlay for option"
7. CFO Recommendation                  | "EUR Put Option"   | "ATM-F put; floor + upside retained"

---

# VERIFICATION

Include a dedicated VERIFICATION section with the following checks:

1. Parity Check: =ABS(USD_mm − USD_forward)
   → Pass condition: < $1,000
   → Flag: "REVIEW RATE INPUTS" if > $1,000

2. CIP Consistency: =ABS(F0_implied − F0_in)
   → Pass condition: < 0.0010 (10 pips)
   → Flag: "FORWARD RATE INCONSISTENT WITH RATES" if > 0.0010

3. Put Floor Logic: =IF(PUT_FLOOR < USD_forward − FV_PREM − 1, "CHECK", "OK")
   → Verifies: Put floor = Forward − premium FV (approximately)

4. Sensitivity Row Count: =COUNTA(S_T column)
   → Should equal 11

---

# FORMATTING STANDARDS

## Color Coding
- YELLOW (#FFFF00): All input cells (manually entered values)
- BLUE (#BDD7EE): All assumption/derived cells
- GREEN (#E2EFDA): All formula output cells
- GRAY (#D9D9D9): All summary/KPI output cells

## Font & Layout
- Font: Calibri 11pt throughout
- Section headers: Bold, 12pt, dark navy fill (#1F3864), white text
- Column widths: Label columns ≥ 35 characters wide; value columns 18 characters wide
- All USD values: format as $#,##0 (no decimals)
- All rates: format as 0.0000
- All percentages: format as 0.00%

## Sheet Structure
- Sheet 1: "FX Hedge Model" (all sections above)
- Sheet 2: "Notes & Assumptions" (day count basis, rate sources, model limitations, 
  parity explanation, option premium source, bid-ask exclusion note)

---

# EXPORT

Save as: fx_hedge_model_enhanced.xlsx
Ensure all named ranges are registered (Name Manager) and all formulas recalculate 
correctly. Zero formula errors (#REF!, #DIV/0!, #VALUE!, #NAME?) are required 
before delivery.
```

---

## Extra Credit: Areas for Further Study & Improvement

### 1. AI Skills & Automation

The most significant enhancement to this workflow would be connecting a live market data feed to the model's input cells. An AI tool such as Claude with a financial data MCP connector (Bloomberg, Refinitiv, or even a free FX API) could be configured to pull the current EUR/USD spot, the 120-day forward implied by current rates, and an indicative ATM option premium automatically at model open. Combined with a Monte Carlo simulation layer — where the AI generates 10,000 random EUR/USD paths using the input volatility and time horizon, then computes expected proceeds and value-at-risk for each hedge strategy — this model could move from a static snapshot to a live decision-support tool. The structured prompt in Section F would serve as the template for this regeneration, with only the variable block updated each run.

### 2. GitHub & Version Control

Committing each stage of this project to GitHub — the Stage 1 memo, Stage 2 model, Stage 3 specification, and this Stage 4 deliverable — creates an auditable, reproducible record of the entire analytical process. For hedge accounting purposes under ASC 815 or IFRS 9, this matters: auditors and regulators require contemporaneous documentation that the hedge was designated, the risk was identified, and the model logic was specified *before* execution. A GitHub commit timestamp on the Stage 1 memo (April 3, 2026) establishes that the exposure was identified and documented prior to any hedging transaction. The Stage 3 specification commit demonstrates that the model logic was peer-reviewable. If a question ever arises about how the forward rate or option premium was sourced, the git history and Bloomberg source annotations in the named range table provide a defensible audit trail. This is the workflow that Big 4 accounting firms and well-governed treasury teams increasingly require.

### 3. Accounting & Audit Integration

If the EUR put option is designated as a cash flow hedge under ASC 815, the accounting treatment bifurcates: changes in the option's *intrinsic value* (the difference between spot and strike) accumulate in Other Comprehensive Income (OCI) and reclassify to revenue when the hedged transaction affects earnings on August 1. Changes in *time value*, however, must be recognized immediately in P&L unless the firm elects the "aligned" method under ASU 2017-12, which permits time value to follow the hedged item into OCI as well. The $61,050 future-valued premium represents time value at inception; documenting this in the Stage 3 specification and tying it to the Bloomberg quote date (April 3, 2026) satisfies the contemporaneous documentation requirement. GitHub version control of the specification and model creates the reproducible audit trail that allows an external auditor to trace the hedge effectiveness assessment from original designation through settlement — a workflow that is increasingly being asked for by audit committees and external reviewers alike.

---

*Prepared by Arlen Dreewes, Treasury / Risk Management.*
*Model source: Stage 2 Excel (Dreewes-Arlen-stage2-model.xlsx). Specification: stage3-spec-Dreewes.md.*
*All market data as of April 3, 2026. For internal use only.*
