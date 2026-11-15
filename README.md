# Machine Learning-Based Buyer Segmentation and Investment Profiling for Real Estate Market Intelligence

Buyer segmentation for a real estate platform using K-Means and Ward hierarchical clustering. The project links 2,000 clients to 7,305 sold property units, finds four buyer segments, and delivers the results as a dashboard and a research paper.

Prepared for **Unified Mentor** and **Parcl Co. Limited**.

## Problem

Real estate companies often treat all buyers the same. This leads to inefficient marketing, generic property recommendations and poor investor targeting. This project uses clustering to find hidden buyer segments and describe their investment behaviour, financing patterns and geography.

## Data

| File | Description |
|---|---|
| `clients.csv` | 2,000 clients: type, gender, country, region, date of birth, acquisition purpose, loan applied, referral channel, satisfaction score |
| `properties.csv` | 10,000 listings (7,305 sold) with unit category, floor area, sale price, status, transaction date and buyer reference |

## Methodology

1. **Cleaning:** standardised labels, checked missing values and duplicates, parsed mixed date formats, calculated age.
2. **Linking:** joined sold units to clients to create units purchased, total spend, average price and office units per client.
3. **Encoding:** one-hot encoding for client type, acquisition purpose and referral channel; country grouped as USA or international; binary flags for loan, investment and corporate.
4. **Scaling:** `StandardScaler` on age, satisfaction, units and total spend, followed by feature weighting.
5. **Models:** K-Means (k = 4, initialised from the brief's buyer archetypes) and Ward hierarchical clustering as a cross-check.
6. **Choosing k:** elbow method and silhouette score for k = 2 to 8.
7. **Interpretation:** each cluster profiled by age, purpose, loans, spend, units and geography.

## Results

| ID | Buyer type | Clients | Avg age | Loan % | Investment % | Avg units | Avg spend |
|---|---|---|---|---|---|---|---|
| C1 | Global Investors | 676 | 71.1 | 33.6 | 29.4 | 3.4 | $1.09M |
| C2 | First-Time Buyers | 793 | 39.7 | 40.0 | 33.9 | 3.5 | $1.17M |
| C3 | Corporate Buyers | 103 | 47.6 | 41.7 | 35.0 | 3.7 | $1.26M |
| C4 | Luxury Investors | 428 | 62.6 | 34.8 | 25.9 | 4.4 | $1.71M |

Key findings:
- First-Time Buyers are the largest segment and provide 36.7% of sales value.
- Luxury Investors buy the most per client ($1.71M, 35% above average).
- Corporate Buyers are few but clearly distinct.
- The United States holds 76.9% of clients; California alone holds 41% of US clients.

## Limitations

- The data has no income field, so "high income" in C1 cannot be measured.
- The silhouette score is about 0.21 for k = 3 to 8, so segments are soft groupings and not tight clusters. C1 is the weakest label.
- The choice of k = 4 and the feature weights rely on judgement.

## Repository contents

```
data/
  dim_clients_segmented.csv     cleaned clients with segment labels
  fact_property_sales.csv       listings joined to buyer segment
  dim_segments.csv              segment lookup (C1 to C4)
  segment_profile.csv           segment averages
  model_k_evaluation.csv        elbow and silhouette values
dashboard/
  buyer_segmentation_dashboard.html   interactive dashboard
  PowerBI_Build_Guide.md              Power BI model, DAX measures and page layouts
paper/
  Buyer_Segmentation_Paper_Compressed.docx
```

## Dashboard

Four modules: Buyer Segmentation Overview, Investor Behaviour, Geographic Buyer Analysis and Segment Insights. Filters: country, region, acquisition purpose and client type. To rebuild it in Power BI, follow `PowerBI_Build_Guide.md`.

## Tech stack

Python (pandas, scikit-learn), Power BI, DAX, HTML and Chart.js.

## Author

Add your name and contact details here.
