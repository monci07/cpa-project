# Customer Personality Analysis (cpa-project)

Project to analyze customer personalities based on products and generate a predictive model.

## Overview

Customer personality analysis helps a business modify its products based on its target customers across different customer segments. Instead of spending money marketing a new product to every customer in a company's database, a company can analyze which customer segment is most likely to buy the product and market it only to that segment. It helps a business better understand its customers and makes it easier to tailor products to the specific needs, behaviors, and concerns of different types of customers.

This project is used as a training case for a clustering model based on patterns found in customers' purchase history. It also serves as a practice exercise for data presentation, feature engineering, model selection, hyperparameter tuning, and the interpretation of results through data visualization.

## Dataset

The data is a dataset of 2,240 rows of individual customers, where each feature column is part of a simplified group of characteristics for each customer. The groups are: **People**, **Products**, **Promotion**, and **Place**.

- Source: [Customer Personality Analysis — Kaggle](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis)
- The dataset's stated objective is to perform clustering to summarize customer segments — there is no predefined target variable.

## Methodology

1. **Data exploration** — reviewed column structure, data types, and null values (`Income` had 24 missing values, filled using the median grouped by education level).
2. **Feature engineering**:
   - `Year_Birth` → converted to `Age`.
   - `AcceptedCmp1-5` and `Response` → consolidated into a single `Campaign` feature.
   - Added `NumDependents` as a numeric representation of dependents per client.
   - Filtered out customers older than 100 and uncommon marital statuses ("Alone", "Absurd", "YOLO") with very low representation.
   - `Education` encoded as an ordinal variable (1–5) based on its hierarchy.
   - `Marital_Status` encoded using label encoding (performed marginally better than one-hot encoding in testing; the one-hot version is kept in the notebook for comparison).
   - All numeric features standardized (z-score) before clustering.
3. **Exploratory visualization** — custom reusable plotting functions to show percentage-based distributions of spending and purchase channels across age ranges, education levels, and marital status.
4. **Clustering**:
   - Model: **K-Means**.
   - `k` selection supported by the **elbow method** (distortion/inertia) and the **silhouette score**.
   - Both k=2 and k=4 were tested and compared in detail; k=4 was selected as the final value based on how much more useful and interpretable the resulting segments were, despite k=2 scoring higher on silhouette.
5. **Cluster interpretation** — each resulting group was described and given a name based on income, age, household dependents, education/marital composition, shopping tendencies, channel preference, and deal responsiveness.

## Results

Four customer segments were identified:

| Cluster | Name | Summary |
|---|---|---|
| 1 | The low-income occasional customer | Lower income, moderate purchases, buys mainly when there's a deal of interest. |
| 2 | The high-income bulk buying loyal customer | Smallest group, highest spending, buys at full price without relying much on deals. |
| 3 | The average loyal customer | Represents the "average" customer — moderate income and spending, responsive to deals. |
| 4 | The deal-seeking customer | A single-client group; buys mainly driven by deals rather than store loyalty or income. |

## Limitations & Future Work

- The dataset is relatively small (~2,240 rows), and one of the four resulting clusters is represented by a single client, limiting how much can be generalized from it.
- K-Means was used as a standard/default clustering approach; future iterations could explore other algorithms (e.g., DBSCAN, GMM) or a larger dataset to validate or refine the segments found here.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
