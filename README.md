# Limit Order Book Simulation using Poisson Processes

This project simulates the evolution of a **limit order book (LOB)** at the best bid using Poisson-driven order arrivals and the inverse transform method. The goal is to create a synthetic market environment and study queue dynamics and liquidity risk.

## Overview

Modern electronic markets exhibit stochastic order arrivals that can be approximated by Poisson processes at short time scales. This project:

* Simulates buy and market sell order arrivals
* Generates discrete order sizes
* Constructs best-bid queue dynamics
* Tracks liquidity depletion events
* Visualizes queue depth over time


## Model Assumptions

**Time horizon:** 1 hour

**Arrival intensities:**

* Buy limit orders: λB = 12 per hour
* Sell limit orders: λS = 15 per hour
* Market sell orders: λM = 8 per hour

**Order size distribution:**

* P(Y = 1) = 0.5
* P(Y = 2) = 0.3
* P(Y = 3) = 0.2

**Initial best bid depth:**
[
Q(0) = 20
]


## Methodology

### 1. Arrival Simulation

Inter-arrival times are generated using the inverse transform method:

[
T = -\frac{1}{\lambda}\ln(U), \quad U \sim \text{Uniform}(0,1)
]

Separate Poisson streams are simulated for:

* Buy limit orders
* Market sell orders


### 2. Order Size Simulation

Discrete inverse transform is used:

| Uniform range | Size |
| ------------- | ---- |
| [0, 0.5)      | 1    |
| [0.5, 0.8)    | 2    |
| [0.8, 1]      | 3    |


### 3. Queue Dynamics

The best bid evolves as:

[
Q(t) = Q(0) + \sum \text{Buy Sizes} - \sum \text{Market Sell Sizes}
]

Rules:

* Buy limit orders increase depth
* Market sells consume depth
* Queue is floored at zero


## Simulation Results

From the sample run:

* **Buy arrivals:** 10
* **Market sell arrivals:** 5
* **Liquidity depletions:** 0

The queue remained strictly positive throughout the simulation horizon.


## Author

**Swapnil Saha**
MSc Data Science, Madras School of Economics

---

## Notes
This is an educational simulation and does **not** represent a production-grade market microstructure model.





