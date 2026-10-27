# Valuation workflow

Valuation is an estimate conditional on assumptions. Show enough arithmetic that a reader can reproduce the main bridge and see which inputs drive the result.

## 1. Set the valuation date and share basis

Record the analysis date and quote source/timestamp. Use the latest verified diluted share count available at that date. State the filing date for shares, and adjust for material issuance, buybacks, conversions, splits, or equity awards after that date when evidence supports it. Do not mix a current share price with an old share count without disclosure.

Define enterprise value consistently:

```text
Enterprise value = market capitalization
                 + debt
                 + preferred equity
                 + noncontrolling interests
                 - cash and cash equivalents
                 - clearly identified non-operating investments (if appropriate)
```

Explain whether lease liabilities are treated as debt; use consistent numerator/denominator definitions across company and peers. Decide whether restricted cash, excess cash, pensions, minority interests, and other claims require adjustment. Avoid double counting.

## 2. Normalize the operating picture

Build a table of at least three to five fiscal years where available, plus the latest reported quarter and TTM where meaningful. Show revenue, growth, gross/operating margins, diluted shares, GAAP operating income/net income, cash from operations, capex, free cash flow, cash, and debt. Note acquisitions, divestitures, unusual tax items, impairments, accounting changes, cyclicality, and restatements.

Reconcile company-adjusted metrics to GAAP. Evaluate whether exclusions recur (for example, stock-based compensation, restructuring, acquisition costs, or recurring “one-time” charges). State which figures are reported and which are normalized estimates.

For share-based compensation, show share-count dilution and consider the economic cost. If using an adjusted cash-flow measure that adds back stock compensation, also model dilution or another explicit compensation cost; do not count the same cost twice or omit it silently.

## 3. Cash-flow valuation

### FCFF discounted cash flow

Use an unlevered free-cash-flow model when revenue, reinvestment, margins, and capital structure can be modeled with reasonable discipline:

```text
FCFF = EBIT × (1 − normalized cash tax rate)
     + depreciation and amortization
     − capital expenditures
     − change in operating working capital
```

Forecast key drivers (revenue growth, operating margin, cash taxes, D&A, capex, and working capital) over an explicit period, commonly five to ten years depending on the business. Tie assumptions to historical performance, company guidance, competitive position, and reinvestment needs. Do not extrapolate one unusually strong or weak quarter as a permanent rate.

Discount FCFF at WACC:

```text
WACC = equity weight × cost of equity
     + debt weight × after-tax cost of debt
Cost of equity = risk-free rate + beta × assumed equity risk premium
PV(explicit FCFF) = Σ FCFF_t / (1 + WACC)^t
Terminal value = FCFF_(n+1) / (WACC − perpetual growth)
Enterprise value = PV(explicit FCFF) + PV(terminal value)
```

The risk-free rate, beta, equity risk premium, cost of debt, and capital weights are assumptions with source and date, not immutable facts. A beta from a public quote site can be method-dependent; disclose the source or avoid implying precision. Use a normalized cash tax rate. Ensure WACC exceeds perpetual growth and use a terminal growth assumption that is economically defensible for the currency and market. Show how much of EV comes from terminal value.

Bridge enterprise value to equity value:

```text
Equity value = enterprise value
             + cash and non-operating assets included in the bridge
             − debt and debt-like claims
             − preferred equity and noncontrolling interests
Per-share value = equity value / diluted shares
```

Keep the bridge consistent with whether leases, pensions, restricted cash, and investments were included in enterprise value or forecast cash flows.

### Owner earnings cross-check

An owner-earnings style check can be useful when cash conversion is central:

```text
Owner earnings ≈ net income
               + non-cash charges
               − maintenance capital expenditures
               − normalized working-capital investment
```

Maintenance capex is rarely reported separately. Label it as an analyst estimate, explain how it was inferred, and compare it with total capex. Avoid assuming all current capex is growth capex or all is maintenance capex.

## 4. Relative valuation

Select a small, defensible peer set based on business model, growth, margin, capital intensity, geography, cyclicality, and accounting where possible. Explain why each peer is comparable and identify material differences. Use the same measurement period and valuation definitions.

Potential multiples include:

- P/E or P/FCF for profitable businesses with interpretable earnings/cash generation.
- EV/EBITDA as a rough operating comparison when depreciation and capex burdens are reasonably comparable. It is not a substitute for cash flow.
- EV/EBIT, EV/FCF, P/B, dividend yield, or sector measures when they better fit economics.
- EV/revenue only as a limited cross-check when profits are negative or immature; pair it with a credible path to sustainable margins and cash generation.

Show the company's current multiple, peer median/range, relevant historical range if available, and the operating assumptions implicit in the selected multiple. Historical multiples can be affected by rates, business mix, or accounting changes; explain the comparison window. Do not select only the highest-multiple peers.

## 5. Sector-specific adjustments

- **Banks:** Focus on capital, asset quality, deposits/funding, net interest income, credit losses, and sustainable return on tangible/common equity. P/TBV or P/B relative to sustainable ROE may help. Industrial FCFF/EV-to-EBITDA is usually a poor default because interest is an operating input.
- **Insurers:** Examine underwriting economics, reserves, investment portfolio, solvency/capital, book value, and normalized returns. Distinguish life, property/casualty, and other models.
- **REITs:** Use FFO/AFFO definitions and reconciliations, same-property operating trends, occupancy, debt maturity/refinancing, cap rates, and NAV where useful. AFFO is not standardized across issuers; inspect the calculation. Treat lease and property-level debt consistently.
- **Commodity producers:** Use mid-cycle commodity prices, cost curves, reserve lives, sustaining capex, and balance-sheet resilience. Avoid valuing a cyclical peak or trough as a permanent earnings base.
- **Early-stage or unprofitable growth:** Use explicit scenarios and milestones; treat EV/revenue as a rough contextual measure. Make dilution, funding needs, and failure risk visible. Do not manufacture a mature-company DCF from unsupported margins.
- **Conglomerates or multi-segment firms:** Consider a sum-of-the-parts only when segment disclosure supports it; state corporate costs, net debt, and any holding-company discount assumptions.

## 6. Scenarios and sensitivity

Present low/base/high cases with visible, internally consistent assumptions. Vary the few drivers that matter most: sales growth, steady-state margin, reinvestment/capital intensity, discount rate, terminal growth, normalized commodity prices, or valuation multiple. Give the per-share range and, where relevant, the implied current-price assumptions.

At minimum, include a two-variable sensitivity for WACC versus terminal growth or for the most relevant operating driver versus valuation multiple. Avoid false decimal precision. Explain whether the current quote lies below, within, or above the modeled range and what might make the model wrong. A margin of safety is a discipline for handling uncertainty, not a guarantee that a price is safe.

If discussing return from a current quote, state the horizon and scenario assumptions, include dividends only if relevant and sourced, and label the result as an illustration rather than a forecast. Do not present a single point estimate as a price target without its range and assumptions.

## 7. Cross-checks before publishing

- Are income-statement periods and balance-sheet dates aligned?
- Are basic/diluted shares and per-share amounts on the correct split-adjusted basis?
- Did you distinguish TTM from fiscal-year data and GAAP from adjusted figures?
- Are cash, debt, leases, pension obligations, and noncontrolling interests handled consistently?
- Are working capital, taxes, capex, and stock compensation economically plausible?
- Does terminal value dominate the answer? If so, state that sensitivity clearly.
- Does the peer set fit the business, and are definitions comparable?
- Did you show contrary evidence and a downside case?
- Can a reader follow each critical assumption to a source or see that it is analyst judgment?
