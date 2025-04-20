# Market Basket Analysis for Grocery Retail

This project implements association rule mining using the Apriori algorithm to analyze grocery shopping patterns and identify item relationships in retail transaction data.

## Overview

Market Basket Analysis (MBA) is a data mining technique that discovers relationships between products that customers purchase together. This project applies MBA to grocery retail data to uncover hidden patterns in customer purchasing behaviors that can inform store layout, inventory management, and targeted marketing strategies.

## Features

- **Transaction Data Processing**: Load and preprocess grocery transaction data
- **Apriori Analysis**: Discover frequent itemsets and association rules with customizable parameters
- **Visualization Tools**: Generate multiple visualization types to analyze results:
  - Frequent itemsets bar charts
  - Association rules scatter plots
  - Rule metrics correlation heatmaps
  - Top rules by lift visualization
  - Support distribution histograms

## Installation

### Prerequisites

- Python 3.8 - 3.11
- Required libraries listed in `requirements.txt`

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/market-basket-analysis.git
   cd market-basket-analysis
   ```

2. Create and activate a virtual environment (optional but recommended):
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Basic Usage

```python
from market_basket_analysis import load_and_preprocess_data, apriori_analysis

# Load and preprocess data
dataset_path = 'Groceries_dataset.csv'
transactions = load_and_preprocess_data(dataset_path)

# Run analysis with default parameters
frequent_itemsets, rules = apriori_analysis(transactions)

# Display results
print("Frequent Itemsets:")
print(frequent_itemsets.sort_values(by='support', ascending=False).head())

print("\nAssociation Rules:")
print(rules.sort_values(by='confidence', ascending=False).head())
```

### Visualization

```python
from market_basket_analysis import (
    plot_frequent_itemsets,
    plot_association_rules_scatter,
    plot_rule_metrics_heatmap,
    plot_top_rules_by_lift,
    plot_support_distribution
)

# Generate visualizations
plot_frequent_itemsets(frequent_itemsets)
plot_association_rules_scatter(rules)
plot_rule_metrics_heatmap(rules)
plot_top_rules_by_lift(rules)
plot_support_distribution(rules)
```

### Parameter Customization

You can adjust support and confidence thresholds to control the number and quality of rules:

```python
# For broader, less strict results (more rules)
frequent_itemsets, rules = apriori_analysis(transactions, min_support=0.001, min_confidence=0.02)

# For more focused, higher quality results (fewer rules)
frequent_itemsets, rules = apriori_analysis(transactions, min_support=0.01, min_confidence=0.1)
```

## Key Findings

Our analysis of grocery transaction data revealed:

- Whole milk appears in 15.79% of all transactions, making it a central product
- Strong associations between:
  - Sausage + yogurt → milk (25.58% confidence, 1.62 lift)
  - Sausage + rolls/buns → milk (21.25% confidence, 1.35 lift)
  - Yogurt + tropical fruit → milk (18.73% confidence, 1.19 lift)
- Identifiable meal-pattern clusters for breakfast, quick meals, and family dinners

## Practical Applications

Insights from this project can be applied to:

- **Store Layout Optimization**: Strategic product placement based on association patterns
- **Targeted Promotions**: Create bundled offers for high-lift product combinations
- **Inventory Management**: Coordinate replenishment of frequently paired items
- **Customer Experience**: Improve shopping convenience by anticipating needs

## Project Structure

```
market_basket_analysis/
├── data/
│   └── Groceries_dataset.csv
├── notebooks/
│   └── market_basket_analysis.ipynb
├── market_basket_analysis/
│   ├── __init__.py
│   ├── data_processing.py
│   ├── analysis.py
│   └── visualization.py
├── README.md
├── requirements.txt
└── .gitignore
```

## Acknowledgments

- Dataset source: [Kaggle Groceries Dataset](https://www.kaggle.com/datasets/heeraldedhia/groceries-dataset)
- Based on academic research by Agrawal, Imielinski, & Swami (1993) on association rule mining
