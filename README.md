# Real-World E-Commerce Dataset Analysis

## Project Overview

This project analyzes the **Brazilian E-Commerce Public Dataset by Olist** to understand sales patterns, delivery performance, and customer satisfaction.

The analysis focuses on relationships between order characteristics, delivery performance, product categories, regional differences, freight costs, and customer review scores.

The project follows a complete real-world data analysis workflow, including:

- Dataset exploration
- Data quality assessment
- Data cleaning and preprocessing
- Feature engineering
- Exploratory data analysis
- Statistical analysis
- Data visualization
- Anomaly and outlier investigation
- Business-oriented interpretation
- Conclusions and recommendations

---

## Problem Statement

E-commerce businesses need to understand how operational performance and order characteristics relate to customer satisfaction.

This project investigates the following problem:

> **Analyze the Olist Brazilian E-Commerce dataset to understand sales, delivery performance, and customer satisfaction, with particular attention to factors associated with delayed deliveries and lower review scores.**

The analysis focuses on the following questions:

1. How do order volumes and sales vary over time?
2. How does delivery performance change over time?
3. Is late delivery associated with lower customer review scores?
4. Do larger delivery delays correspond to lower review scores?
5. Which product categories show longer delivery times or higher late-delivery rates?
6. How do order value and freight cost relate to customer satisfaction?
7. How does delivery performance vary across customer regions?
8. Are higher regional late-delivery rates associated with lower customer review scores?
9. What unusual or extreme observations exist in delivery time, order value, and freight cost?

---

## Dataset

### Brazilian E-Commerce Public Dataset by Olist

The dataset contains approximately 100,000 orders from the Brazilian Olist e-commerce platform and includes multiple interconnected tables covering:

- Customers
- Orders
- Order items
- Payments
- Reviews
- Products
- Sellers
- Geolocation
- Product category translations

The dataset covers orders from approximately 2016 to 2018.

### Dataset Source

Kaggle:

**Brazilian E-Commerce Public Dataset by Olist**

https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

The dataset is provided under the **CC BY-NC-SA 4.0** license.

The raw dataset is not included in this repository because of repository size and dataset licensing considerations.

---

## Project Structure

```text
Real-World-Dataset-Analysis/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── data/
│   └── raw/
│       ├── archive.zip
│       ├── olist_customers_dataset.csv
│       ├── olist_geolocation_dataset.csv
│       ├── olist_order_items_dataset.csv
│       ├── olist_order_payments_dataset.csv
│       ├── olist_order_reviews_dataset.csv
│       ├── olist_orders_dataset.csv
│       ├── olist_products_dataset.csv
│       ├── olist_sellers_dataset.csv   
│       └── product_category_name_translation.csv
│
└── notebooks/
    └── real_world_dataset_analysis.ipynb
```

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Jupyter Notebook

---

## Analysis Workflow

### 1. Data Loading and Exploration

All nine dataset tables were loaded independently and examined before integration.

The initial exploration included:

- Dataset dimensions
- Column names
- Data types
- Sample records
- Missing values
- Duplicate records
- Basic data-quality assessment

### 2. Data Cleaning

The cleaning process included:

- Removing exact duplicate records from the geolocation dataset
- Converting date and timestamp fields to datetime format
- Handling missing product categories
- Handling missing review text
- Preserving meaningful missing delivery timestamps
- Investigating missing values according to their semantic meaning

No values were automatically imputed when doing so could introduce unsupported assumptions.

### 3. Feature Engineering

Several analysis-ready features were created, including:

- Delivery time in days
- Delivery delay in days
- Late-delivery indicator
- Total order value
- Total freight value
- Total number of items
- Average review score
- Review count
- Delivery-delay groups
- Translated product categories

Order-item data was aggregated appropriately when order-level analysis was required, while item-level data was retained for category-level analysis.

---

## Exploratory Data Analysis

### Sales and Order Activity

Monthly order volume and sales value were analyzed to understand changes in e-commerce activity over time.

The dataset shows substantial growth in order activity during the main observation period, with particularly high order volume and sales during late 2017 and 2018.

The sparse observations at the beginning and end of the dataset were treated cautiously rather than interpreted as normal monthly activity.

### Delivery Performance

Delivery performance was analyzed using:

- Average delivery time
- Median delivery time
- Late-delivery rate
- Delivery delay
- Monthly trends
- Regional comparisons
- Product-category comparisons

Delivery performance varied considerably over time, across product categories, and across customer states.

### Delivery and Customer Satisfaction

One of the strongest patterns in the analysis was the relationship between delivery performance and customer review scores.

Orders delivered on time had an average review score of approximately **4.29**, compared with approximately **2.57** for late orders.

This represents an observed difference of approximately **1.73 review points**.

The relationship became even stronger for severe delays:

| Delivery Delay | Average Review Score |
|---|---:|
| 1–3 days late | ~3.77 |
| 4–7 days late | ~2.32 |
| 8–14 days late | ~1.75 |
| 15+ days late | ~1.71 |

These findings indicate a strong association between delivery delays and lower observed customer satisfaction.

They do not establish a causal relationship.

### Product Categories

Product categories showed meaningful differences in delivery performance.

Office furniture had a particularly high average delivery time of approximately **20.84 days** among the frequently represented categories.

At the category level:

- **Pearson correlation between average delivery time and average review score:** -0.7804
- **After excluding office furniture:** -0.5415

The relationship therefore remained substantial even without the most extreme category.

### Regional Analysis

Delivery performance varied significantly across customer states.

Among the 17 states with at least 500 orders:

- **Pearson correlation between late-delivery rate and average review score:** -0.9076
- **Spearman correlation:** -0.8946

States with higher observed late-delivery rates generally had lower average review scores.

These are aggregated regional associations and should not be interpreted as evidence that location or delivery delay independently causes lower satisfaction.

### Order Value and Freight Cost

Order value did not show a simple monotonic relationship with customer review scores.

However, order value and freight cost showed a moderate positive association:

- **Pearson correlation:** 0.4128
- **Spearman correlation:** 0.4690

This indicates that higher-value orders generally tended to have higher freight costs, while also showing substantial variation that cannot be explained by order value alone.

### Customer Review Distribution

The original review-score distribution was examined using the 1–5 customer rating scale.

Out of **99,224 reviews**:

| Review Score | Number of Reviews |
|---:|---:|
| 1 | 11,424 |
| 2 | 3,151 |
| 3 | 8,179 |
| 4 | 19,142 |
| 5 | 57,328 |

Approximately **77.1%** of reviews were 4 or 5 stars.

The distribution is therefore strongly concentrated toward positive ratings, while the 1-star group still represents a substantial minority of customer experiences.

---

## Anomaly and Outlier Investigation

Real-world datasets often contain extreme observations that may represent genuine business cases rather than data errors.

The analysis investigated extreme values in:

- Delivery time
- Delivery delay
- Order value
- Freight value

Examples of observed extremes included:

- **Maximum delivery time:** approximately 209.63 days
- **Orders delivered more than 60 days after purchase:** approximately 0.32% of delivered orders
- **Maximum order value:** 13,440
- **Maximum freight value:** 1,794.96

Extreme records were inspected individually rather than removed automatically.

No definitive evidence was found that these observations were invalid. Therefore, the extreme observations were retained.

---

## Key Findings

- Delivery performance is strongly associated with customer satisfaction.
- Late orders had substantially lower average review scores than orders delivered on time.
- More severe delays were associated with progressively lower review scores.
- Product categories showed meaningful differences in delivery performance.
- Office furniture had particularly long observed delivery times.
- Regional delivery performance varied considerably.
- States with higher late-delivery rates generally showed lower average review scores.
- Order value alone did not explain customer satisfaction.
- Freight cost showed a moderate positive association with order value, but substantial variation remained.
- The dataset contains meaningful extreme observations that should not be removed solely because they are statistically unusual.

---

## Business Recommendations

Based on the observed patterns, the following areas could be prioritized for further operational investigation:

- Reduce the frequency of late deliveries.
- Monitor severe delivery delays separately from normal late deliveries.
- Investigate product categories with consistently long delivery times.
- Examine regional logistics performance and delivery networks.
- Investigate the relationship between seller location, customer location, and shipping distance.
- Analyze freight-cost variation using additional logistics information.
- Monitor customer review scores alongside operational delivery metrics.

These recommendations are based on observed associations and should be validated using additional operational data before implementing major business decisions.

---

## Limitations

- The analysis is observational and identifies associations rather than causal relationships.
- The dataset represents a historical period and may not reflect current e-commerce behavior.
- Delivery performance can be influenced by factors not represented in the dataset.
- Customer reviews are subjective and may reflect factors beyond delivery performance.
- Review scores are strongly concentrated toward higher ratings.
- Several variables contain highly skewed distributions and extreme values.
- Regional comparisons were restricted to states with at least 500 orders to reduce instability from very small samples.
- The available data does not provide enough information to determine the causes of individual delivery delays.

---

## Additional Data That Could Improve the Analysis

Future analysis could be strengthened by including:

- Shipping distance
- Seller and warehouse locations
- Product weight and dimensions
- Logistics provider
- Shipping method
- Delivery attempts
- Detailed shipping costs
- Cancellation and return reasons
- Customer purchase history
- Customer complaints and support interactions
- Regional logistics infrastructure
- Promotional periods and major shopping events

These variables could provide additional explanations for differences in delivery performance and customer satisfaction.

---

## How to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/kartikeysharma2645/Real-World-Dataset-Analysis
cd Real-World-Dataset-Analysis
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv .venv
```

**Windows:**

```bash
.venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Download the Dataset

Download the **Brazilian E-Commerce Public Dataset by Olist** from Kaggle and place the CSV files inside:

```text
data/raw/
```

The expected dataset files include:

```text
olist_customers_dataset.csv
olist_geolocation_dataset.csv
olist_order_items_dataset.csv
olist_order_payments_dataset.csv
olist_order_reviews_dataset.csv
olist_orders_dataset.csv
olist_products_dataset.csv
olist_sellers_dataset.csv
product_category_name_translation.csv
```

### 5. Run the Notebook

Open:

```text
notebooks/real_world_dataset_analysis.ipynb
```

and execute the notebook from top to bottom.

### Author

**Kartikey Sharma**  
B.Tech in Artificial Intelligence & Machine Learning

If you found this project useful, consider giving the repository a ⭐ on GitHub!