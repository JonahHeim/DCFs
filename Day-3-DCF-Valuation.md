# Day 3 — DCF Valuation Deep Dive

> **Key Summary (re-read until it sticks):** A Discounted Cash Flow (DCF) values a company as the sum of all the cash it will generate in the future, translated into today's dollars. Why translate? Because a dollar next year is worth less than a dollar today — you could invest today's dollar and grow it. So we **project** free cash flow for ~5–10 years, **discount** each year back to today using **WACC** (the blended cost of the company's debt and equity), then add a **Terminal Value** to capture everything beyond the projection window. Sum it all up and you get **Enterprise Value**; subtract net debt and you get **Equity Value**, then divide by shares for a per-share price. A DCF is an *intrinsic* value — what the business is truly worth based on its cash, independent of what the market says today.

**Time today:** ~100 min (15 morning read + 15 mental drills + 70 screen — this is a heavy day). Do the walk-through in Excel.

---

> 🧮 **Today's Excel problem:** open `FMI_Excel_Problems.xlsx` → **D3 Problem** tab. Discount the projected FCFs, build the terminal value both ways, bridge to a per-share value, and fill the sensitivity grid. Check against **D3 Answer**.

---

## 1. Lecture Notes

### 1.1 The one idea underneath everything: the time value of money

$100 today ≠ $100 in a year. If you can earn 10%, then $100 today becomes $110 next year — so $110 next year is only worth $100 today. To reverse it: **Present Value = Future Value ÷ (1 + r)^n**, where r is the discount rate and n is years out.

- $110 one year out at 10%: PV = 110 / 1.10 = $100.
- $121 two years out at 10%: PV = 121 / 1.10² = $100.

That division by (1 + r)^n is "discounting." A DCF does this to every future year of cash flow.

### 1.2 The DCF in 6 Steps (know this ladder cold)

1. **Project Unlevered Free Cash Flow** for an explicit forecast period (usually 5, sometimes 10 years).
2. **Calculate WACC** — the discount rate (the blended required return of all investors).
3. **Discount** each year's FCF back to present value using WACC.
4. **Calculate Terminal Value** — the value of all cash flows *after* the projection window — then **discount it** back too.
5. **Sum** the discounted FCFs + discounted Terminal Value = **Enterprise Value.**
6. **Bridge to Equity Value / share price:** Enterprise Value − Net Debt = Equity Value; ÷ diluted shares = value per share.

### 1.3 Step 1 — Projecting Unlevered FCF (from Day 2)

```
Unlevered FCF = EBIT × (1 − tax) + D&A − CapEx − Increase in NWC
```
You build this from revenue assumptions: grow revenue, apply margins to get EBIT, tax it, add back D&A, subtract CapEx and working-capital investment. Garbage assumptions = garbage valuation — this is why interviewers probe your assumptions.

### 1.4 Step 2 — WACC (Weighted Average Cost of Capital)

WACC is the blended rate the company must earn to satisfy *both* lenders and shareholders. It's the discount rate for unlevered FCF.

```
WACC = (E/V) × Cost of Equity + (D/V) × Cost of Debt × (1 − tax)
```
where E = market value of equity, D = market value of debt, V = E + D.

- **Cost of Debt** is roughly the interest rate on the company's debt. It's multiplied by (1 − tax) because interest is tax-deductible — the government subsidizes debt. This is the **"tax shield on debt."**
- **Cost of Equity** — what shareholders demand. Computed with **CAPM**:
  ```
  Cost of Equity = Risk-Free Rate + Beta × Equity Risk Premium
  ```
  - **Risk-free rate:** yield on a 10-year US Treasury (~4% in 2026).
  - **Beta:** how volatile the stock is vs. the market. Beta of 1 = moves with the market; >1 = riskier/more volatile; <1 = more stable.
  - **Equity Risk Premium (ERP):** the extra return investors demand for holding stocks over Treasuries (~5–6% historically).

**Why cost of equity > cost of debt:** equity holders are last in line if the company fails (debt gets paid first), so they demand a higher return for that risk. Debt is also cheaper because of the tax shield.

### 1.5 Step 3 — Discounting the projected years

Each year's FCF gets divided by (1 + WACC)^n. Year 1 FCF ÷ (1+WACC)¹, Year 2 ÷ (1+WACC)², etc. (The "discount factor.")

### 1.6 Step 4 — Terminal Value (TWO methods — know both)

You can't project forever, so after the explicit period you capture "everything after" as a Terminal Value (TV), calculated at the *end* of the final projection year, then discounted back.

**Method A — Gordon Growth / Perpetuity Growth Method:**
Assumes FCF grows at a small constant rate forever.
```
TV = [ Final Year FCF × (1 + g) ] / (WACC − g)
```
where **g** = perpetual growth rate (must be modest — usually 2–3%, never higher than long-run GDP growth, or the math implies the company eventually eats the whole economy).

**Method B — Exit Multiple Method:**
Assumes you "sell" the company at the end at a market multiple of its final-year EBITDA.
```
TV = Final Year EBITDA × Exit EV/EBITDA Multiple
```
The multiple comes from comparable companies (Day 4).

> **Interview gold:** Terminal Value is usually **60–80% of the total DCF value.** That's a feature *and* a warning — the answer is highly sensitive to your terminal assumptions, which is why you run a sensitivity table. Good analysts sanity-check the two methods against each other: the implied growth rate from an exit multiple should be reasonable, and the implied exit multiple from Gordon Growth should look like the comps.

**Don't forget to discount TV** back to today with the same (1 + WACC)^n as the final year.

### 1.7 Step 5 & 6 — Enterprise Value → Equity Value → per share

```
Enterprise Value (EV) = Σ (discounted FCFs) + (discounted Terminal Value)

Equity Value = Enterprise Value − Net Debt
             where Net Debt = Total Debt − Cash

Value per Share = Equity Value / Diluted Shares Outstanding
```

**Why subtract net debt?** The unlevered FCF belonged to *all* investors (the whole enterprise). To get what belongs to *shareholders*, you remove what's owed to lenders. You subtract debt and add back cash (cash could pay down debt or be distributed).

### 1.8 Sensitivity Analysis

Because the output swings on WACC and g (and the exit multiple), you build a **sensitivity table** (a data table in Excel) showing the share price across a grid of WACC (columns) × terminal growth or exit multiple (rows). You present a *range*, not a false-precision single number. FMI loves candidates who say "the DCF gives a range of roughly $X–$Y depending on assumptions" rather than "the answer is $43.17."

---

## 2. Worked DCF Walk-Through (simple company)

**Company: "MowCo."** All numbers in $millions. Do this alongside the Excel model (`build_model.py`).

**Assumptions:**
- Year 0 (last actual) Revenue = $1,000, growing 8% → 6% → 5% → 4% → 3% over 5 years.
- EBIT margin flat at 20%.
- Tax rate = 25%.
- D&A = 5% of revenue. CapEx = 6% of revenue. Increase in NWC = 2% of revenue.
- WACC = 9%.
- Terminal growth g = 2.5% (Gordon Growth method).

**Step 1 — Project revenue and unlevered FCF:**

| Year | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Growth | 8% | 6% | 5% | 4% | 3% |
| Revenue | 1,080 | 1,145 | 1,202 | 1,250 | 1,288 |
| EBIT (20%) | 216 | 229 | 240 | 250 | 258 |
| EBIT×(1−.25) | 162 | 172 | 180 | 188 | 193 |
| + D&A (5%) | 54 | 57 | 60 | 63 | 64 |
| − CapEx (6%) | (65) | (69) | (72) | (75) | (77) |
| − ΔNWC (2%) | (22) | (23) | (24) | (25) | (26) |
| **Unlevered FCF** | **129** | **137** | **144** | **150** | **155** |

*(Rounding to whole numbers; the Excel model carries full precision.)*

**Step 2 — WACC** is given as 9%.

**Step 3 — Discount each FCF at 9%:**

| Year | FCF | Discount factor 1/(1.09)^n | PV of FCF |
|---|---|---|---|
| 1 | 129 | 0.917 | 118 |
| 2 | 137 | 0.842 | 115 |
| 3 | 144 | 0.772 | 111 |
| 4 | 150 | 0.708 | 106 |
| 5 | 155 | 0.650 | 101 |
| | | **Sum of PV(FCF)** | **≈ 551** |

**Step 4 — Terminal Value (Gordon Growth):**
```
TV = [155 × (1 + 0.025)] / (0.09 − 0.025)
   = 158.9 / 0.065
   = 2,445  (value as of end of Year 5)
```
Discount TV back 5 years: 2,445 × 0.650 = **≈ 1,589.**

Notice: TV present value (1,589) is ~74% of total value — textbook.

**Step 5 — Enterprise Value:**
```
EV = 551 (sum of PV FCFs) + 1,589 (PV of TV) ≈ 2,140
```

**Step 6 — Equity Value & per share.** Say MowCo has $300 debt, $100 cash (Net Debt = $200), and 100 million shares:
```
Equity Value = 2,140 − 200 = 1,940
Value per share = 1,940 / 100 = $19.40
```

**Sanity check with Exit Multiple method:** Year 5 EBITDA = EBIT + D&A = 258 + 64 = 322. If comps trade at ~7.5x EV/EBITDA: TV = 322 × 7.5 = 2,415 — very close to the 2,445 from Gordon Growth. Cross-check passes. ✅

---

## 3. Practice Questions

**⚠️ How to answer these:** Q1–Q6 are **calculation problems** — write the formula, plug in the numbers, state the figure (show the arithmetic). Q7–Q8 are **concept questions** — answer in 1–2 sentences that name the *why*, the way you would out loud in an interview. Round money to the cent where relevant.

Example of the format wanted:
> *PV of $800 in 4 years at 8%:*  PV = FV/(1+r)^n = 800/(1.08)⁴ = 800/1.3605 = **$588.03.**

> 🔒 **Solutions are in `Day-3-Solutions.md`.** Work all eight, then check.

### Q1 — Present value basics
What's the PV of $500 received in 3 years at a 10% discount rate?

### Q2 — Cost of equity (CAPM)
Risk-free = 4%, Beta = 1.2, Equity Risk Premium = 5.5%. Cost of equity?

### Q3 — WACC
Equity = $800 (cost 10.6%), Debt = $200 (cost 5%), tax = 25%. WACC?

### Q4 — Terminal Value, Gordon Growth
Final year FCF = $200, WACC = 9%, g = 3%. TV?

### Q5 — Terminal Value, Exit Multiple
Final year EBITDA = $400, exit multiple 8x. TV?

### Q6 — EV to equity bridge
Enterprise Value = $5,000, total debt = $1,200, cash = $300, shares = 200M. Price per share?

### Q7 — Sensitivity intuition
If WACC rises, what happens to the DCF value, and why?

### Q8 — Why unlevered, not levered?
Why does a standard DCF discount *unlevered* FCF at WACC rather than levered FCF?

---

## 4. Anki Card Ideas

1. What is a DCF? → Values a company as the PV of its future free cash flows.
2. Why discount? → Time value of money — a future dollar is worth less than today's.
3. Present value formula? → PV = FV / (1 + r)^n.
4. The 6 DCF steps? → Project FCF, find WACC, discount, terminal value, sum to EV, bridge to equity.
5. WACC formula? → (E/V)×CoE + (D/V)×CoD×(1−t).
6. CAPM / cost of equity? → Risk-free + Beta × Equity Risk Premium.
7. Why (1−t) on cost of debt? → Interest is tax-deductible (debt tax shield).
8. Gordon Growth TV? → [Final FCF × (1+g)] / (WACC − g).
9. Exit Multiple TV? → Final EBITDA × exit EV/EBITDA multiple.
10. Typical TV as % of DCF value? → 60–80%.
11. Constraint on terminal growth g? → Must be modest (≤ long-run GDP, ~2–3%).
12. EV to equity value? → Subtract net debt (debt − cash).
13. Why subtract net debt? → Unlevered FCF belongs to all investors; remove lenders' claim to isolate equity.
14. Effect of higher WACC on value? → Lower value (inverse).
15. Two TV methods should be cross-checked how? → Implied growth from exit multiple and implied multiple from Gordon Growth should look reasonable vs comps.

---

## 5. Mental Drill for Today (screen-free — say it out loud or think it through)

**The DCF Ladder + WACC recall.** Out loud or in your head, five times each:
- "Project free cash flow… calculate WACC… discount each year… add terminal value… sum to enterprise value… subtract net debt for equity value."
- "WACC is weight of equity times cost of equity, plus weight of debt times cost of debt times one minus tax."
- "Cost of equity is risk-free plus beta times the equity risk premium."

Then do mental PV math: "A dollar in one year at 10% is worth about 91 cents today. In two years, about 83 cents. In three, about 75." Get a feel for how fast money shrinks.

---

## 6. End-of-Day Check

- [ ] Recite the 6 DCF steps from memory.
- [ ] Write out WACC and CAPM formulas without notes.
- [ ] Do both Terminal Value methods on a given number.
- [ ] Explain why TV dominates the answer and why you subtract net debt.
- [ ] Reproduce this hand-walk (~$19.40) — it uses a simplified ΔNWC of 2% of revenue for teaching. *(Note: the fuller Excel model on Day 5 derives ΔNWC precisely from the balance-sheet lines, so its answer-key price is ~$22.18 — same method, more exact inputs. Don't be thrown by the difference.)*

Log confidence in `Progress-Tracker.md`. Tomorrow: the market-based cousin of the DCF — comps and multiples.
