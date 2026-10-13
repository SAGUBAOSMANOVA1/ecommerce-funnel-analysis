# E-Commerce Funnel Analysis – View to Purchase

## 1. Project Overview

This project analyzes e-commerce event data for January and February 2020. The goal is to understand user behavior across product views, cart activity, and purchases, compare monthly performance, identify category and brand conversion patterns, and detect unusual purchase prices.

## 2. Dataset

- **January:** 4,264,752 events
- **February:** 4,156,682 events
- **Combined dataset:** 8,421,434 events
- **Columns:** `event_time`, `event_type`, `product_id`, `category_id`, `category_code`, `brand`, `price`, `user_id`, `user_session`

The data contains four event types: `view`, `cart`, `remove_from_cart`, and `purchase`.

## 3. Data Preparation

- Combined the January and February CSV files into one DataFrame.
- Converted `event_time` to a UTC datetime format.
- Created a `month` column for monthly comparisons.
- Checked missing values and data types.
- Retained records with missing category and brand information for analyses where those fields were not required.

Missing values were concentrated in `category_code` (98.20%), `brand` (42.77%), and `user_session` (0.03%). Category and brand analyses excluded records with missing values in the corresponding field.

## 4. Key Results

### Overall Funnel

| Stage | Unique users | Percentage of view users |
|---|---:|---:|
| View | 716,987 | 100.00% |
| Cart | 162,035 | 22.60% |
| Purchase | 49,473 | 6.90% |

### Monthly Conversion

| Month | Unique view users | Unique purchase users | View-to-purchase ratio |
|---|---:|---:|---:|
| January 2020 | 397,775 | 28,220 | 7.09% |
| February 2020 | 379,246 | 25,759 | 6.79% |

The view-to-purchase ratio decreased by 0.30 percentage points from January to February.

Purchase events declined from 263,797 in January to 241,993 in February, a decrease of 8.27%.

### Category Analysis

Among the eight categories selected by unique view-user count, `apparel.glove` had the highest view-to-purchase ratio at 38.91%, while `accessories.bag` had the lowest at 1.43%.

### Brand Analysis

Among the ten brands selected by purchase-event count, `bpw.style` had the highest view-to-purchase ratio at 22.95%. `kapous` had the lowest ratio at 7.14%.

### Purchase Price Outliers

The IQR method identified 34,947 purchase events as price outliers, representing 6.91% of purchase events.

- Q1: 1.59
- Q3: 5.56
- IQR: 3.97
- Lower bound: -4.37
- Upper bound: 11.52

These observations are statistical outliers and are not necessarily data errors.

### Bonus: Time from View to Purchase

For 182,132 purchase events, a previous view of the same product by the same user was identified.

- Mean time: 2,069.81 minutes
- Median time: 34.22 minutes

The mean is substantially higher than the median, indicating that some view-to-purchase intervals were very long.

### Bonus: High-View, Low-Conversion Products

Product `5915337` had 4,818 unique view users and 5 unique purchase users, giving a view-to-purchase ratio of 0.10%. Product `5808664` had 10,426 unique view users and 22 unique purchase users, giving a ratio of 0.21%.

These products may warrant further investigation into price, availability, product-page quality, or checkout friction. The current dataset does not establish the cause.

## 5. Business Insights

1. **Monthly performance weakened:** Purchase events decreased by 8.27% in February, while the view-to-purchase ratio declined from 7.09% to 6.79%. Investigate whether the change is associated with traffic quality, product availability, or checkout performance.
2. **Category performance varies substantially:** `apparel.glove` showed a much higher view-to-purchase ratio than `accessories.bag`. Investigate differences in pricing, demand, and product presentation before reallocating marketing resources.
3. **Brand conversion varies:** `bpw.style` had the highest view-to-purchase ratio among the selected top brands, while `kapous` had the lowest. Compare product mix, pricing, and traffic sources to understand the difference.
4. **Some highly viewed products convert poorly:** Products such as `5915337` and `5808664` receive many unique views but few unique purchase users. Prioritize these products for a product-page and availability review.
5. **Purchase prices include a notable outlier group:** 6.91% of purchase events fell outside the IQR thresholds. Inspect high-priced observations and verify whether they represent premium products or data-quality issues before making pricing decisions.

## 6. Visualizations

The notebook includes the following visual analyses:

- Overall funnel bar chart
- View-to-purchase conversion by top eight categories
- January versus February conversion comparison
- Horizontal view-to-purchase conversion chart for the top ten brands
- Purchase-price boxplot for IQR outliers
- Low-conversion chart for high-view products

## 7. Methodology and Limitations

- Funnel and conversion calculations use unique users at each event stage. They measure stage presence, not necessarily a verified sequential journey from view to cart to purchase.
- Category and brand ratios compare unique users associated with view and purchase events for each category or brand. They do not prove that every purchasing user previously viewed the same item.
- The view-to-purchase time calculation matches a purchase to the most recent preceding view of the same product by the same user in the available dataset. Earlier views outside the dataset's date range cannot be observed.
- Missing category and brand values reduce the coverage of category and brand analyses.
- Observational data can identify patterns but cannot independently establish why conversion changed.

## 8. Conclusion

The analysis identifies a decline in purchase-event volume and a small reduction in the monthly view-to-purchase ratio from January to February 2020. Conversion also varies considerably by category, brand, and product. These findings can guide further investigation into product presentation, availability, pricing, and the checkout journey.