# Real Estate Profit Calculator - Specifications (First-Time Buyers)

**Purpose**: Help first-time buyers understand the real cost of buying, owning, and selling a home as an investment.

**Language**: Simple, everyday terms. "What does it cost?" not "capital gains analysis."

---

## Tab Structure

### Tab 1: Buy

What it costs to get into the house. Includes a mortgage calculator so buyers can see their monthly payment.

#### Input Fields

| Field | Type | Default | Smart Default? | Help Text |
|-------|------|---------|----------------|-----------|
| Home Price | Currency | $300,000 | No | What are you paying for the house? |
| Down Payment | Currency/% | 10% | No | Toggle between $ and %. Shows calculated $ amount either way |
| Interest Rate | Percent | 6.5% | No | Your mortgage interest rate |
| Loan Term | Dropdown | 30 years | No | 15 or 30 years |
| → Monthly Mortgage | Display | *calculated* | Always | Auto-calculated, display-only |
| Closing Costs | Currency | *3% of home price* | **Yes** | Costs at signing (inspections, title, etc.) |
| Repairs / Upgrades | Currency | $0 | No | _Optional_ - How much will you spend fixing it up? |

#### Results

```
Total Cash Needed = Down Payment + Closing Costs + Repairs
```

Displayed clearly at the bottom of the tab: **"Cash You Need: $XX,XXX"**

---

### Tab 2: Sell

What you get when you eventually sell.

#### Input Fields

| Field | Type | Default | Smart Default? | Help Text |
|-------|------|---------|----------------|-----------|
| Years Owned | Number | 5 | No | How many years before you sell? |
| Estimated Sale Price | Currency | $360,000 | No | What do you think you'll sell it for? |
| Selling Costs | Currency | *6% of sale price* | **Yes** | Agent fees, closing costs, etc. |
| → Remaining Mortgage | Display | *calculated* | Always | What you still owe on the loan |

#### Results

```
Net Sale Proceeds = Sale Price - Selling Costs - Remaining Mortgage
```

Displayed clearly: **"What You Walk Away With: $XX,XXX"**

---

### Tab 3: Monthly Costs

Broken-out monthly costs so buyers see where the money goes. Mortgage flows in from the Buy tab.

#### Input Fields

| Field | Type | Default | Smart Default? | Help Text |
|-------|------|---------|----------------|-----------|
| Mortgage Payment | Display | *from Buy tab* | Always | Read-only, calculated in Buy tab |
| Property Tax | Currency | *1.1% of home price / 12* | **Yes** | Monthly property tax |
| Insurance | Currency | $150 | No | Homeowner's insurance per month |
| HOA | Currency | $0 | No | Homeowner's association fee (if any) |
| Maintenance | Currency | *1% of home price / 12* | **Yes** | Budget for upkeep and repairs |
| Monthly Income | Currency | $0 | No | _Optional_ - Rental income, if renting it out |

#### Results

```
Total Monthly Costs = Mortgage + Tax + Insurance + HOA + Maintenance
Monthly Cash Flow = Monthly Income - Total Monthly Costs
Total Over Ownership = Monthly Cash Flow × (Years Owned × 12)
```

Displayed clearly: **"Monthly Cash Flow: +/- $X,XXX"** and **"Total Over X Years: +/- $XX,XXX"**

---

### Tab 4: Total Profit

The big picture — everything combined. No inputs here, just the answer.

#### Display

```
Cash to Buy:              -$XX,XXX   (from Buy tab)
What You Walk Away With:  +$XX,XXX   (from Sell tab)
Monthly Cash Flow Total:  +/- $XX,XXX (from Monthly tab)
─────────────────────────────────────
TOTAL PROFIT/LOSS:        +/- $XX,XXX
```

Big, bold, color-coded: GREEN if profit, RED if loss.

---

## Smart Default System

Some fields auto-calculate from Home Price or Sale Price so buyers don't have to guess.

### How It Works

1. Smart default fields start with an auto-calculated value (e.g., Closing Costs = 3% of Home Price)
2. If the user edits the field, their value sticks — it switches to "manual mode"
3. A reset button (↺) appears next to manually-edited fields
4. Clicking reset restores the auto-calculated value

### Smart Default Fields

| Field | Derives From | Formula |
|-------|-------------|---------|
| Closing Costs | Home Price | 3% of Home Price |
| Selling Costs | Sale Price | 6% of Sale Price |
| Property Tax | Home Price | 1.1% of Home Price / 12 |
| Maintenance | Home Price | 1% of Home Price / 12 |

---

## Formulas

### Mortgage Payment (standard amortization)

```
Monthly Payment = P × [r(1+r)^n] / [(1+r)^n - 1]

Where:
  P = Loan Amount (Home Price - Down Payment)
  r = Monthly interest rate (Annual Rate / 12)
  n = Total payments (Loan Term in years × 12)
```

### Remaining Mortgage Balance

```
Remaining Balance = P × [(1+r)^n - (1+r)^t] / [(1+r)^n - 1]

Where:
  t = Payments made (Years Owned × 12)
```

### Profit Calculation

```
Cash to Buy = Down Payment + Closing Costs + Repairs
Net Sale Proceeds = Sale Price - Selling Costs - Remaining Mortgage
Monthly Cash Flow Total = (Monthly Income - Total Monthly Costs) × Months Owned
Total Profit = Net Sale Proceeds - Cash to Buy + Monthly Cash Flow Total
```

---

## Data Flow

1. **Home Price** drives smart defaults across all tabs (closing costs, property tax, maintenance)
2. **Buy tab** calculates mortgage payment → flows into Monthly Costs tab
3. **Sale Price** drives selling costs smart default
4. **Buy + Sell tabs** feed loan info → remaining mortgage calculation
5. **Tab 4** pulls results from all other tabs → shows total profit
6. All updates happen instantly as user types

---

## Visual Design Principles

- Large, readable numbers
- Clear color coding (GREEN = profit, RED = loss)
- Labels that use "you" language ("Cash You Need" not "Total Acquisition Cost")
- Minimal technical jargon
- Reuse existing theme from current design

## Color Scheme

- **Profit (Positive)**: #10b981 (Green)
- **Loss (Negative)**: #f43f5e (Red)
- Reuse existing theme from current design

## Input Validation

- All currency fields: non-negative
- Interest rate: 0-100%
- Years owned: at least 1
- Down payment: can't exceed home price
- Empty fields treated as $0

## Real-time Updates

- Calculate on every input change (oninput event)
- No delays or lag
- All tabs update instantly when switching
