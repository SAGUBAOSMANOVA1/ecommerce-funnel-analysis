# E-Commerce Funnel Analysis — View to Purchase

## Project Overview

This project analyzes e-commerce user behavior using event-level data from January and February 2020. The main objective is to examine the conversion funnel, identify potential drop-off points, compare performance across months, product categories, and brands, and investigate product pricing outliers.

## Dataset

- **Period:** January–February 2020
- **Total events:** 8,421,434
- **January events:** 4,264,752
- **February events:** 4,156,682
- **Columns:** `event_time`, `event_type`, `product_id`, `category_id`, `category_code`, `brand`, `price`, `user_id`, `user_session`

The dataset contains product views, cart additions, cart removals, and purchases.

## Tools and Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Data Preparation

The January and February datasets were combined into one DataFrame. Event timestamps were validated, and a month column was used to support monthly comparisons.

Missing values were examined:
- `category_code`: 98.20%
- `brand`: 42.77%
- `user_session`: 0.03%

Missing category and brand values were considered during interpretation. Negative prices were identified and excluded from the cleaned price-analysis dataset; zero prices were retained.

## Event Distribution

| Event Type | Event Count | Percentage |
|---|---:|---:|
| View | 3,991,194 | 47.39% |
| Cart | 2,297,017 | 27.28% |
| Remove from cart | 1,627,433 | 19.32% |
| Purchase | 505,790 | 6.01% |

Views account for the largest share of recorded events. Cart removals also represent a substantial portion of activity, suggesting that cart abandonment and product-selection behavior deserve further investigation.

## User-Level Funnel

The number of unique users recorded at each event type was:

| Event Type | Unique Users | Percentage of View Users |
|---|---:|---:|
| View | 716,987 | 100.00% |
| Cart | 162,035 | 22.60% |
| Purchase | 49,473 | 6.90% |

These figures represent unique users associated with each event type. They do not necessarily mean that every user progressed sequentially through the funnel stages.

## Session-Level Sequential Funnel

A separate session-based analysis examined sessions containing the stages in the required chronological order: view, cart, and purchase.

| Funnel Stage | Number of Sessions | Conversion from View |
|---|---:|---:|
| View | 1,784,916 | 100.00% |
| View → Cart | 220,441 | 12.35% |
| View → Cart → Purchase | 28,179 | 1.58% |

The results indicate that 12.35% of view-containing sessions also contained a cart event after a view, while 1.58% reached the complete view-to-cart-to-purchase sequence under the implemented session-based method.

## Monthly Comparison

### Unique-User Conversion

| Month | View Users | Purchase Users | View-to-Purchase Rate |
|---|---:|---:|---:|
| January 2020 | 397,775 | 28,220 | 7.09% |
| February 2020 | 379,246 | 25,759 | 6.79% |

The unique-user view-to-purchase rate decreased slightly from January to February.

### Event-Based Comparison

The purchase-event-to-view-event ratios were 12.95% in January and 12.39% in February. These are event-count ratios, not unique-user conversion rates.

## Category Analysis

The category analysis compared view, cart, and purchase events across product categories with available category codes.

Examples of event-based purchase-to-view ratios include:

- `stationery.cartrige`: 23.77%
- `apparel.glove`: 38.91%
- `appliances.environment.vacuum`: 8.85%
- `furniture.living_room.cabinet`: 2.21%

These ratios are calculated from event counts. They should not be interpreted as sequential user conversion rates. Since most records lack a category code, the results describe only the records with available category information.

## Brand Analysis

The top 10 brands by the selected analysis criteria were compared using view and purchase activity.

The highest event-based purchase-to-view ratio among the displayed brands was:

- `bpw.style`: 22.95%

This is an event-based ratio rather than the percentage of unique viewers who purchased. Brand-level results should also be interpreted in light of missing brand values and differences in event volume.

## Product-Level Analysis

Products with at least 1,000 view events were examined to identify products with low event-based purchase-to-view ratios.

Examples included:
- Product `27759`: 1,062 views and no purchase events.
- Product `5915337`: 5,900 views and 5 purchase events.
- Product `5688835`: 1,135 views and 1 purchase event.

These products may warrant further investigation into pricing, product descriptions, availability, and user experience. The results indicate candidates for further review, not proof of why conversion was low.

## Price Outlier Analysis

The Interquartile Range (IQR) method was used to identify potential price outliers among purchase events.

- First quartile (Q1): 1.59
- Third quartile (Q3): 5.56
- IQR: 3.97
- Upper IQR boundary: 11.52
- Potential purchase-price outliers: 34,876

The lower IQR boundary was negative, so the upper boundary was the relevant threshold for identifying high-price observations among non-negative prices. Statistical outliers are not necessarily data errors and should be reviewed before removal.

## Bonus Analysis 1: Time from View to Purchase

The analysis matched purchase events to a preceding view of the same product by the same user.

- Matched purchase records: 182,132
- Mean time to purchase: 2,069.81 minutes
- Median time to purchase: 34.22 minutes

The mean is much higher than the median, indicating a right-skewed distribution. Because the matching method does not require the view and purchase to occur in the same session, long intervals may include activity separated by days or weeks.

## Bonus Analysis 2: High-View, Low-Conversion Products

Products with high view counts and low event-based purchase-to-view ratios were identified. This analysis can help prioritize products for additional investigation and potential conversion improvements.

The analysis is exploratory. Low ratios alone do not establish the causes of poor performance.

## Visualizations

The notebook includes the following charts:

1. Event Distribution
2. Unique Users by Stage
3. Monthly View-to-Purchase Conversion Rate
4. Category View-to-Purchase Conversion Rate
5. Brand View-to-Purchase Conversion Rate
6. Purchase Price Outliers
7. Sequential E-commerce Funnel

## Key Findings

- Views represented 47.39% of all recorded events.
- The unique-user view-to-purchase rate decreased from 7.09% in January to 6.79% in February.
- The session-based complete view-to-cart-to-purchase funnel contained 28,179 sessions, representing 1.58% of sessions with a view.
- Category and brand conversion patterns varied considerably.
- Some products attracted many views but recorded very few purchases.
- Purchase-price outliers and long view-to-purchase intervals require careful interpretation.
- Missing category codes limit the coverage of category-level analysis.

## Conclusion

This project demonstrates an end-to-end exploratory analysis of e-commerce event data, including data preparation, funnel measurement, monthly comparison, category and brand analysis, product-level investigation, and price outlier detection.

The findings help identify where further investigation may improve the customer journey. More detailed session-level validation and additional business context would be useful before making operational decisions.

