# E-commerce Funnel Analysis

## Project Overview

This project analyzes e-commerce user behavior using event data from January and February 2020. The goal is to understand how users interact with products, identify conversion patterns, and discover opportunities to improve the customer journey.

## Objectives

- Analyze user activity across different event types.
- Measure view-to-cart and view-to-purchase conversion rates.
- Compare conversion performance between January and February.
- Identify high-view products with low purchase conversion.
- Explore purchase price outliers.
- Estimate the time between product views and purchases.

## Tools & Technologies

- Python
- Pandas
- Matplotlib
- Jupyter Notebook
- Git & GitHub

## Dataset

The analysis uses e-commerce event data from January and February 2020.

- **January:** 4,264,752 events
- **February:** 4,156,682 events
- **Total:** 8,421,434 events

The dataset includes event timestamps, event types, product IDs, category information, brands, prices, user IDs, and user sessions.

## Key Findings

### 1. User Funnel

| Funnel Stage | Unique Users |
|---|---:|
| Product View | 716,987 |
| Add to Cart | 162,035 |
| Purchase | 49,473 |

- 22.60% of users who viewed products also had an add-to-cart event.
- 6.90% of users who viewed products also had a purchase event.

*Note: These are stage-presence ratios based on unique users, not strictly sequential funnel conversion rates.*

### 2. Monthly Conversion

| Month | View Users | Purchase Users | View-to-Purchase Rate |
|---|---:|---:|---:|
| January 2020 | 397,775 | 28,220 | 7.09% |
| February 2020 | 379,246 | 25,759 | 6.79% |

The view-to-purchase ratio decreased by approximately 0.30 percentage points in February.

### 3. Category Performance

Conversion performance varied considerably across product categories.

- **Apparel gloves:** 38.91% view-to-purchase ratio.
- **Accessories bags:** 1.43% view-to-purchase ratio.

These differences may help identify categories for further investigation. Category comparisons should be interpreted with the available sample sizes in mind.

### 4. Brand Performance

Among the selected brands analyzed:

- **bpw.style:** 22.95% view-to-purchase ratio.
- **kapous:** 7.14% view-to-purchase ratio.

The results can help identify brands that may benefit from further product-page, pricing, or marketing analysis.

### 5. High-View, Low-Conversion Products

Products with at least 1,000 unique viewers were examined to identify products with relatively low purchase activity.

Product **5915337** had 4,818 unique viewers and 5 unique purchasing users, resulting in an approximate view-to-purchase ratio of 0.10%.

These products may warrant further investigation into pricing, product descriptions, availability, and customer experience.

### 6. Purchase Price Outliers

The Interquartile Range (IQR) method was used to identify unusual purchase-event prices.

- **Q1:** 1.59
- **Q3:** 5.56
- **IQR:** 3.97
- **Upper outlier threshold:** 11.52
- **Detected outliers:** 34,947 purchase events (approximately 6.91%)

These observations were flagged for investigation rather than automatically removed.

### 7. Time