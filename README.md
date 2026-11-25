# Olist CEO Request: Should We Remove Underperforming Sellers?

A business case on the **Olist** Brazilian e-commerce dataset. The CEO's question: **how many underperforming sellers should Olist remove from its marketplace to maximize profit?**

**Answer:** keep the top **2,021** sellers. Once IT costs are included, the remaining ~460 lowest-profit sellers that looked profitable before cost more than they bring in.

## P&L model
- **Revenues:** 10% commission on each delivered order's product price + 80 BRL monthly subscription per seller
- **Reputation costs:** estimated cost for every bad review (≤ 3 stars), e.g. 100 BRL for a 1-star review
- **IT costs:** grow with scale but not linearly: `α·√n_sellers + β·√n_items`

## Approach
1. Extended the reusable `olist` Python package (`seller_updated.py`) to compute revenues, review costs and profits per seller.
2. **What-if analysis:** sorted sellers by profit and computed cumulative revenues, profits and items sold, i.e. "what if Olist had never accepted the worst sellers?"
3. Added cumulative IT costs and found the number of sellers that maximizes net profit.

## Results

| | Ignoring IT costs | Including IT costs |
|---|---|---|
| Optimal number of sellers | 2,483 | **2,021** |

At the optimum of 2,021 sellers:

| Metric | Value (BRL) |
|---|---|
| Total revenues | 2,147,750 |
| Profit before IT costs | 1,351,940 |
| IT costs | 375,914 |
| **Net profit after IT costs** | **976,026** |

Items sold: 57,209. Ignoring IT costs would have kept ~460 extra sellers who lose money once infrastructure costs are counted. IT costs take 27.8% of the profit.

The notebook also discusses other levers: removing weak product categories, a "honeymoon" period for new sellers, mandatory product information, and restricting slow state-to-state routes.

## Tech
Python · pandas · NumPy · Matplotlib · object-oriented data package (`olist/`)

## Files
- `CEO_request.ipynb` – analysis and recommendations
- `olist/` – data-cleaning and feature classes (`Order`, `Seller`, `Product`, `Review`)

Built during the Workintech Data Science & Machine Learning program.
