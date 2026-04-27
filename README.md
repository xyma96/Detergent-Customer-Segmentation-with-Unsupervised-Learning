# Detergent Customer Segmentation

## Project Summary

The business question is whether the market should receive one broad pricing strategy or differentiated promotion strategies. The analysis finds four price-response segments and recommends a simple rule: **do not discount everyone**.

| Cluster | Segment | Approx. size | Core behavior | Recommended action |
|---:|---|---:|---|---|
| 0 | Deal Hunters | 38% | Buy only at low prices | Deprioritize paid marketing; use email-only or low-cost offers |
| 1 | Selective Spenders | 15% | Higher willingness to pay, moderate price sensitivity | Use differentiation, bundles, loyalty perks, and light promotions |
| 2 | Practical Value Seekers | 22% | Medium willingness to pay, responsive to value | Test 10-20% coupons and price thresholds |
| 3 | Premium Minimalists | 25% | Very high willingness to pay, low price sensitivity | Avoid discounts; focus on upsell, launches, and loyalty |

## Dataset

The dataset is [`pricing_application_conjoint.csv`](pricing_application_conjoint.csv). Each row is a household-price observation:

- `purchase`: 1 if the household would buy at the shown price, 0 otherwise
- `price`: tested detergent price
- `household_id`: household identifier
- `age`, `family_size`, `prev_interactions`: numeric household characteristics
- `income_bracket`, `state`, `sex`, `race`: categorical household characteristics

The same household appears multiple times because each household is evaluated at several prices.

## Notebook Workflow

The notebook is structured as a standalone clustering exercise:

1. Executive summary and business problem
2. Household-level feature construction
3. Candidate model comparison
   - Baseline K-means on household features
   - Drop-off-price clustering
   - Price-response-curve K-means
   - GMM robustness check
4. K selection across K=3, K=4, and K=5
5. Final four-segment interpretation
6. Marketing strategy and caveats

## How to Run

Open `detergent_customer_segmentation.ipynb` in Jupyter, VS Code, or Google Colab with the CSV file in the same folder.

Required Python packages:

```bash
pip install pandas numpy matplotlib scikit-learn
```

The notebook reads the local CSV first, so it does not require network access.

## Caveats

- The data reflects stated purchase intent, not actual transactions.
- Discount decisions should be validated using incremental profit, not purchase lift alone.
- Segment membership must be predicted from observable customer signals before deployment.
- K=4 is chosen for business actionability, not because it is a universal statistical truth.
- Better deployment would use transaction history, coupon redemption, channel, geography, competitor pricing, and product margin.
