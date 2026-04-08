# Executive Summary
## Whiskique's E-Commerce Analytics — Profit, Shipping & Basket Intelligence
**Prepared for:** Commercial Leadership & Operations Management
**Dataset:** 24,404 transactions · 11,427 invoices · 3,141 customers
**Period:** Full transactional history (point-in-time snapshot)
**Anaytical tool:** Power BI — 3 page interactive report

---

## Situation 

Whiskique operates as a multi-category pet products retailer across U.S. regions. While transaction data was being collected, the business lacked a structured analytical layer to answer three critical questions:

1. **Profitability:** What are actual margins after accounting for landed costs and shipping — not just top-line revenue?
2. **Shipping efficiency:** How do current shipping cost structures scale with order quantity, and what would optimized bulk pricing look like?
3. **Purchasing patterns:** Which products are bought together, and how can that intelligence drive bundling and cross-sell strategy?

This report provides the analytical foundation to answer all three.

---

## Key Findings

**1. Electronics is the highest-margin category at 44.28%.**
Despite not being the highest revenue category, Electronics generates the best return per dollar of sales. This margin profile makes it a priority for promotional investment and inventory expansion.

**2. The top-selling product drives disproportionate volume.**
Sheba Perfect Portions Pet Wet Cat Food leads in sales with an average quantity of 7.07 units per transaction — significantly higher than other products. It is the natural anchor for bundle promotions and loyalty program incentives.

**3. Shipping costs are structurally skewed toward heavy products.**
The cost differential between the highest shipping product (Taste of the Wild 40lb at $20/1,000 miles) and the lowest (Sheba at \$2.50/1,000 miles) is 8x. This creates a significant drag on margins for bulk pet food orders that is invisible in top-line revenue figures.

**4. The current shipping model penalizes multi-item orders.**
The baseline shipping model adds a 70% surcharge per additional unit beyond the first. At a What-if quantity of 9 or more, a blended discount  factor of 0.3 would reduce per-unit shipping costs 70% — a lever that could incentivize bulk purchases while improving net margins.

**5. Customers cluster in 2-4 item baskets.**
The most frequent transaction sizes are 2 items (7.22%), 3 items (6.68%), and 4 items (6.52%). This clustering suggests that bundle promotions targeting 2-4 product combinations would align with existing purchasing behavior rather than asking customers to change habits.

**6. California, Texas, New York, and Florida drive regional concentration.**
Four states account for a disproportionate share of the customer base.
California alone holds 419 customers — 13.3% of the total.
Regional marketing budgets should reflect this geographic concentration.

**7. Average Customer LTV of \$494.72 sets the retention investment ceiling**
Any customer acquisition or retention program with a cost below $494.72 per customer is potentially ROI-positive. This benchmark should be the reference point for loyalty program design.

---

## Recommendations

| Priority | Recommendation | Owner | Timeline |
|----------|----------------|-------|----------|
| 🔴 High | Launch a 2-4 item bundle promotion anchored on Sheba as the lead product | Commercial / Marketing | 30 days |
| 🔴 High | Introduce a bulk shipping incentive for orders ≥ 9 units using the 0.3 blended factor as the ceiling | Operations / Pricing | 45 days |
| 🔴 High | Expand Electronics inventory and promotional visibility — highest margin category at 44.28% | Merchandising | 30 days |
| 🟡 Medium | Review Indoor Pet Camera positioning: lowest-selling product warrants a pricing or placement audit | Product / Commercial | 60 days |
| 🟡 Medium | Design a California-specific retention program: largest customer concentration, highest strategic risk if churned | Marketing / Regional | 60 days |
| 🟡 Medium | Introduce a weight-based shipping surcharge or free shipping threshold for heavy products (>10 lbs) to protect margins on bulk pet food | Operations / Finance | 90 days |
| 🟢 Ongoing | Use Market Basket Analysis cross-filter interactivity in weekly commercial reviews to identify emerging co-purchase patterns | Commercial Analytics | Weekly |

---

## Impact Estimate

**Shipping optimizations scenario:**
If bulk discount incentives shift 10% of customers to ≥ 9-item orders, applying the 0.3 blended shipping factor:

- Shipping baseline: **$385,150**
- Potential reduction at 0.3 factor on 10% of volume: **~$27,000/year**
- Net effect: lower operating costs with higher average order value

**Bundle promotion scenario:**
If 2-item bundle promotions increase average basket size from 2.0 to 2.5 items for 20% of transactions:

- Additional units sold: ~**1,143 incremental units**
- At average unit price of ~\$25: **~$28,575 in incremental revenue**
- At blended margin of ~35%: **~$10,000 in incremental profit**

---

## How to use this report

| If you need to... | Go to... | Use this feature... |
|---|---|---|
| Review top-line performance | Executive Summary | Product slicer to filter by category |
| Model a shipping cost scenario | Shipping Metrics | What-if Quantity slicer (1-20) |
| Identify products bought together | Market Basket Analysis | Click a product in the table to filter the bar chart |
| Analyze a specific state or region | Shipping Metrics | Map: Shippipng cost by State and Region |
| Compare margin across products | Executive Summary | Treemap: Profit % by Category |

---

*Full interactive report available on Power BI Service -> [View Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODA2NzA5ZGEtNTk3Mi00ZjI0LWJkY2UtMDgwNDczYWMwNjYwIiwidCI6IjRkYTFiNTk3LTkyOGEtNGVkZi04Y2MwLTcwMmFiNjA1NjYyMSIsImMiOjR9)*

---


