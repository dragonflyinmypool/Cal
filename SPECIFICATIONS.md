# Real Estate Profit Calculator - Specifications (MVP - First-Time Buyers)

## Tab Structure

### Tab 1: Buying the House
**Purpose**: Help first-time buyers understand the real cost of buying and selling a home

**Language**: Use simple, everyday terms. Example: "What does it cost to buy and sell?" rather than "capital gains analysis"

#### Input Fields (Simplified)
| Field | Type | Default | Help Text |
|-------|------|---------|-----------|
| Home Price | Currency | $200,000 | What are you paying for the house? |
| Closing Costs | Currency | $5,000 | Costs at signing (usually 2-5% of price) - includes inspections, title, recording, etc. |
| Repairs/Upgrades | Currency | $20,000 | *Optional* - How much will you spend fixing/improving it? |
| Estimated Sale Price | Currency | $280,000 | What do you think you'll sell it for in the future? |

**Why we removed:**
- Separate "Closing Costs (Buy)" and "Closing Costs (Sell)" - too detailed for MVP, confuses buyers
- Kept single field that's easier to estimate

#### Calculations
```
What You Put In = Home Price + Closing Costs + Repairs
What You'll Get Back = Estimated Sale Price
Your Gain/Loss = What You'll Get Back - What You Put In
```

#### Display (Big, Clear, Obvious)
```
┌─────────────────────────────────────┐
│ BUYING THE HOUSE                    │
├─────────────────────────────────────┤
│ What You Put In:        $225,000    │
│ What You'll Get Back:    $280,000    │
├─────────────────────────────────────┤
│ YOUR GAIN/LOSS:         +$55,000 ✓  │
│                         (green if    │
│                          positive)   │
└─────────────────────────────────────┘
```

#### Chart
Horizontal bar showing the journey:
```
[Cost: $225k] ────→ [Gain: $55k] ────→ [Sale: $280k]
```

---

### Tab 2: Monthly Costs/Profit
**Purpose**: Help buyers understand ongoing monthly costs vs. income (whether renting it out or living there)

**Language**: Keep it simple: "Is this house profitable month-to-month?"

#### Input Fields (Simplified)
| Field | Type | Default | Help Text |
|-------|------|---------|-----------|
| Monthly Income | Currency | $2,500 | *Optional* - Leave blank if you're living here. If renting it out, what's the monthly rent? |
| Monthly Costs | Currency | $1,500 | Your monthly costs: mortgage + insurance + taxes + maintenance (roughly) |
| How Many Months | Number | 12 | How long will you own this house? (1 year = 12 months) |

**Why we simplified:**
- One "Monthly Costs" field instead of separating mortgage, taxes, etc. (buyers don't need that breakdown)
- One "Monthly Income" field - either they're renting or they're not
- Users can estimate monthly costs roughly - precision isn't critical for MVP

#### Calculations
```
Total Income Over Period = Monthly Income × How Many Months
Total Costs Over Period = Monthly Costs × How Many Months
Monthly Profit/Loss = Total Income - Total Costs
Average Per Month = Monthly Profit/Loss ÷ How Many Months
```

#### Display (Simple & Clear)
```
┌─────────────────────────────────────┐
│ MONTHLY COSTS/PROFIT                │
├─────────────────────────────────────┤
│ Total Income (over period):  $30,000│
│ Total Costs (over period):   $18,000│
├─────────────────────────────────────┤
│ YOUR PROFIT/LOSS:            +$12,000✓
│ Average per month:           +$1,000 │
│                         (green if    │
│                          positive)   │
└─────────────────────────────────────┘
```

#### Chart
Horizontal bar showing monthly balance:
```
[Costs: $18k] ───→ [Profit: $12k] ───→ [Income: $30k]
```

---

### Tab 3: Your Investment Summary
**Purpose**: The "big picture" - answer the simple question: "Is this a good investment?"

**Language**: Use plain language and reassuring framing. This is where it all comes together.

#### Display (SIMPLE - Three Numbers)

```
┌──────────────────────────────────────────┐
│ YOUR INVESTMENT SUMMARY                  │
├──────────────────────────────────────────┤
│                                          │
│ Profit from Buying & Selling:            │
│ + $55,000                                │
│                                          │
│ Profit from Monthly Operations:          │
│ + $12,000                                │
│                                          │
├──────────────────────────────────────────┤
│ YOUR TOTAL GAIN/LOSS:                    │
│ ✓ $67,000 PROFIT ✓                       │
│   (BIG, GREEN, obvious if positive)      │
│                                          │
└──────────────────────────────────────────┘
```

#### What We Removed (MVP Simplification)
- ❌ Separate ROI/Margin calculations (too technical for first-time buyers)
- ❌ Detailed breakdowns (too much information)
- ❌ Complex metrics (confusing without education)

**Why?** First-time buyers want ONE answer: "Am I making or losing money?" Not: "What's my 15% IRR vs. 8% ROI?"

#### Visualization (The Chart)
A single, clean horizontal bar showing all components:

```
From Buying:    [RED or GREEN bar: $55k]
From Monthly:   [RED or GREEN bar: $12k]
Total:          [BOLD LARGE: $67k PROFIT]
```

Colors:
- GREEN = positive (making money)
- RED = negative (losing money)
- Size = magnitude (bigger bar = bigger impact)

#### Interactions
- **Automatic Updates**: As user changes numbers in Tabs 1 & 2, this tab updates instantly
- **No interaction needed here** - just visualization

---

## Visual Design Principles (MVP)

**Keep it super simple:**
- Large, readable numbers
- Clear color coding (GREEN = profit, RED = loss)
- ONE chart per tab, not multiple
- Labels that use "you" language ("Your Gain/Loss" not "Net Proceeds")
- Minimal technical jargon

---

## Color Scheme

- **Profit (Positive)**: #10b981 (Green) - feels good
- **Loss (Negative)**: #f43f5e (Red) - warning
- Keep charts minimal - don't need rainbow of colors
- Reuse existing theme from current design

---

## Data Flow (Simple)

1. User enters numbers in Tab 1 → Auto-calculates → Shows result
2. User enters numbers in Tab 2 → Auto-calculates → Shows result
3. Tab 3 automatically pulls both results → Shows total
4. All updates happen instantly as user types

---

## Input Validation

- Keep it forgiving for MVP (users can leave fields blank = $0)
- All currency fields: Non-negative (no negative prices)
- Month fields: Positive only (at least 1 month)
- Display $0 if empty

---

## Real-time Updates

- Fast: Calculate on every keystroke (oninput event)
- Smooth: No delays or lag
- All tabs update instantly when switching
