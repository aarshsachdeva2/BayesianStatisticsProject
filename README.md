# Instacart Customer Purchase Behavior: Hierarchical Bayesian Modeling

## Overview

This project analyzes customer purchase and reorder behavior using the Instacart Online Grocery Shopping Dataset. The objective was to model both product reordering probability and shopping cart size while accounting for customer-level and product-level heterogeneity through Bayesian hierarchical models.

Traditional machine learning models were used as benchmarks and compared against Bayesian approaches to evaluate the benefits of incorporating uncertainty estimates and hierarchical structures.

---

## Dataset

* **Source:** Instacart Online Grocery Shopping Dataset
* **Type:** Transactional retail purchase data
* **Size:** Over 3 million grocery orders from more than 200,000 users
* **Target Variables:**

  * Product reorder probability
  * Cart size (number of products purchased per order)

---

## Methodology

### Data Preparation

The dataset was cleaned and validated through:

* Missing value analysis
* Duplicate detection
* Garbage value identification
* Product name standardization
* Data integrity checks across all tables

Feature engineering included:

* Order number
* Day of week
* Hour of day
* Historical customer purchasing behavior
* Average cart size
* User and product identifiers

---

## Model 1: Hierarchical Bayesian Logistic Regression

### Objective

Predict the probability that a customer will reorder a product.

### Model Structure

The model incorporates:

* Global intercept
* User-specific random effects
* Product-specific random effects
* Fixed effects for:

  * Order number
  * Day of week
  * Hour of day

### Why Hierarchical Modeling?

Customer purchasing behavior varies significantly across users and products.

A hierarchical framework allows:

* Partial pooling of information
* User-specific behavior modeling
* Product-specific preference modeling
* Improved generalization for sparse observations

### Bayesian Inference

The model was implemented in Stan using MCMC sampling to estimate posterior distributions for all parameters.

Outputs include:

* Posterior means
* Credible intervals
* Effective sample sizes
* Convergence diagnostics

---

## Model 2: Bayesian Poisson Regression

### Objective

Predict shopping cart size for a given order.

### Predictors

* Order number
* Day of week
* Hour of day
* Average historical cart size

### Model Structure

Cart size was modeled as a count variable using Bayesian Poisson regression.

Posterior inference provides:

* Parameter uncertainty
* Predictive distributions
* Probabilistic forecasts for cart size

---

## Model Comparison

### Frequentist Benchmarks

#### Logistic Regression

Used as a baseline model for reorder prediction.

Advantages:

* Fast training
* Easy interpretation

Limitations:

* No uncertainty quantification
* Unable to model user-level and product-level heterogeneity

#### Poisson Regression

Used as a baseline count model for cart size prediction.

Limitations:

* Assumes a fixed parameter estimate
* Does not provide full posterior uncertainty

---

### Bayesian Models

Advantages observed:

* Quantification of parameter uncertainty
* User-specific behavioral effects
* Product-specific purchasing effects
* Improved interpretability through posterior distributions
* More realistic representation of customer behavior

---

## Results

### Hierarchical Bayesian Logistic Regression

Successfully captured:

* Customer-level reorder tendencies
* Product-specific reorder behavior
* Temporal effects of ordering patterns

Posterior analysis showed substantial variation across both users and products, validating the use of hierarchical modeling.

### Bayesian Poisson Regression

Successfully modeled:

* Cart size distributions
* Expected basket sizes
* Uncertainty around purchase volume

Posterior predictive checks indicated reasonable alignment between observed and predicted cart-size distributions.

---

## Diagnostics and Insights

The notebook includes:

### Posterior Diagnostics

* Posterior density plots
* Parameter distributions
* Credible intervals

### Random Effects Analysis

* User-level intercept distributions
* Product-level intercept distributions
* Behavioral heterogeneity visualization

### Posterior Predictive Checks

* Observed vs predicted distributions
* Predictive uncertainty analysis
* Cart size forecasting validation

---

## Project Structure

```text
InstBay.ipynb          # Data cleaning, feature engineering, Bayesian modeling, and evaluation
hier_logit.stan        # Hierarchical Bayesian logistic regression model
poisson_reg.stan       # Bayesian Poisson regression model
```

---

## How to Run

1. Clone the repository
2. Download the Instacart dataset
3. Install dependencies including CmdStanPy and Stan
4. Open the notebook
5. Run all cells sequentially

---

## Key Learnings

* Hierarchical models capture customer behavior more effectively than global models
* Bayesian methods provide uncertainty estimates unavailable in traditional approaches
* Random effects are valuable when modeling customer-product interactions
* Posterior predictive checks are essential for validating Bayesian models
* Customer purchasing behavior exhibits substantial heterogeneity across both users and products

---

## Future Work

* Implement Hierarchical Bayesian Negative Binomial models
* Incorporate product category and department-level effects
* Develop recommendation and next-purchase prediction systems
* Build a prediction API for real-time inference
* Deploy models using a scalable MLOps pipeline
* Explore variational inference for faster posterior estimation

---

## Key Takeaway

Customer purchase behavior is inherently hierarchical. Treating all customers and products identically can mask important behavioral patterns. Hierarchical Bayesian models provide a principled framework for capturing individual differences while quantifying uncertainty, leading to more realistic and interpretable predictions.
