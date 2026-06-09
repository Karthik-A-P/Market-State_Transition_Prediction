# Stock Market State Transition Prediction using Markov Models and Machine Learning

## Overview

This project explores whether stock market behavior can be represented as a sequence of discrete market states and whether future states can be predicted using probabilistic and machine learning approaches.

Using 10 years of NASDAQ-100 historical data, continuous market variables such as price levels, volatility, and daily returns are transformed into categorical states. These states are then used to:

* Model market dynamics using Markov Chains.
* Analyze transition probabilities between market regimes.
* Predict future market states using probabilistic methods.
* Compare Markov-based forecasting against Random Forest classification.

---

## Objectives

* Convert continuous market data into interpretable market regimes.
* Study how market states evolve over time.
* Build a transition probability matrix describing regime shifts.
* Evaluate the predictive power of Markov Models.
* Benchmark against machine learning approaches.

---

## Dataset

Historical NASDAQ-100 (NDX) daily data covering:

* Open Price
* Close Price
* High Price
* Low Price
* Trading Date

Derived features:

* Daily Percentage Change
* Daily Volatility (High − Low)

Time Period:

2015 – 2025

---

## Methodology

### 1. Feature Engineering

Additional market indicators were generated:

#### Daily Return


(Close - Open) / Open × 100


#### Daily Volatility

High - Low


### 2. State Generation

Continuous variables were converted into categorical states using percentile-based discretization.

For price and volatility variables:

* Low
* Medium
* High

For percentage change:

* High Decrease
* Decrease
* Increase
* High Increase
* Consistent

Example state:


Open=High

High=High

Low=Medium

Close=High

Volatility=Low

Return=Increase


Each unique combination was assigned a symbolic state label:


A, B, C, D, ... AA, AB, AC ...

### 3. Markov Chain Construction

A first-order Markov Chain was built from the training dataset.

For every state:


Current State → Next State


transition frequencies were computed and normalized into probabilities.

This produced a transition matrix:


P(State_t+1 | State_t)


which describes the probability of moving from one market regime to another.

---

### 4. Market Persistence Analysis

State transition matrices were also generated for:

* Open Price Category
* Close Price Category
* Volatility Category
* Return Category

to measure regime persistence and switching behavior.

---

### 5. Feature Dependency Analysis

Cramér's V statistics were used to quantify associations between categorical market variables.

Examples:

* Open vs Close
* Open vs Volatility
* Volatility vs Returns
* Close vs Returns

This helped identify redundant and strongly related features.

---

### 6. Probabilistic Forecasting

The simplest prediction strategy:

Predicted Next State =
Most Probable Transition


For each current state, the next state with the highest transition probability was selected.

---

### 7. Machine Learning Model

A Random Forest Classifier was trained using:

Features:

* Open
* Close
* High
* Low
* Volatility
* Percent Change
* Year
* Month

Target:


Next Market State

Hyperparameters were optimized through experimentation and validation.

---

## Results

### Markov Model

Predicts future market regimes using transition probabilities learned from historical data.

Advantages:

* Highly interpretable
* Captures market persistence
* Easy to visualize and analyze

---

### Random Forest Model

Learns nonlinear relationships between market features and future states.

Advantages:

* Handles complex interactions
* Provides feature importance estimates
* Can capture patterns beyond first-order transitions

---

## Key Findings

* Market regimes exhibit strong persistence.
* Open and Close categories show extremely high association.
* Volatility displays moderate state memory.
* Market behavior can be represented as transitions between discrete states.
* Probabilistic state models provide interpretable insight into regime evolution.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* SciPy
* Matplotlib

---

## Future Improvements

* Higher-order Markov Models
* Hidden Markov Models (HMMs)
* Regime-switching models
* LSTM and Transformer-based forecasting
* Rolling-window state generation
* Elimination of state-definition data leakage
* State clustering and dimensionality reduction
