# Space Debris Trajectory Prediction using AI/ML

## Objective

The primary objective of this project is to improve the accuracy of space debris trajectory prediction in Low Earth Orbit (LEO) by combining traditional physics-based models with machine learning.

Specifically, the project aims to:

* Model and correct the **residual error of SGP4 (analytical propagator)**
* Use **LSTM-based deep learning** to learn temporal error patterns
* Evaluate whether AI can enhance or match traditional orbital prediction methods

---

## Core Technologies Used

### Physics-Based Model

* **SGP4 (Simplified General Perturbations 4)**

  * Standard industry model for satellite orbit prediction
  * Fast but limited accuracy due to simplified physics

### Machine Learning Model

* **LSTM (Long Short-Term Memory)**

  * Captures temporal dependencies in orbital data
  * Used for time-series prediction of error

### Hybrid Approach

* Combines:

  * **SGP4 predictions**
  * **LSTM-predicted residual errors**

Final Prediction:
Corrected Position = SGP4 Output + LSTM Error Prediction

---

## System Workflow

1. Parse TLE (Two-Line Element) data
2. Generate orbital predictions using SGP4
3. Compute residual error between predicted and actual positions
4. Preprocess and scale data
5. Train LSTM on time-series error sequences
6. Apply correction to improve trajectory prediction

---

## Experiment Comparison

### 1 Satellite Model

* Trained on a single satellite
* **Observation:**

  * Severe overfitting
  * Training loss → near zero
  * Validation loss → constant

Model memorizes instead of learning

---

### 100 Satellites Model

* Trained on large-scale dataset (100 satellites)

**Improvements:**

* Better generalization
* More stable training behavior
* Reduced overfitting

**Performance:**

* SGP4 baseline error ≈ **0.55 km**
* Hybrid model error ≈ **0.57 km**

Matches baseline but does not outperform

---

## Key Difference: 1 vs 100 Satellites

| Aspect            | 1 Satellite  | 100 Satellites |
| ----------------- | ------------ | -------------- |
| Learning Behavior | Memorization | Generalization |
| Overfitting       | High         | Reduced        |
| Stability         | Poor         | Stable         |
| Data Diversity    | Very low     | High           |
| Performance       | Misleading   | Realistic      |

Conclusion:
Scaling data is essential for learning real-world orbital patterns.

---

## Feature Combinations Analysis

The **Feature_combinations.ipynb** explores how different orbital parameters affect model performance.

### Features Used

* Mean Motion
* Eccentricity
* Bstar Drag
* Inclination
* RAAN (Right Ascension)
* Argument of Perigee
* Mean Anomaly

---

### Key Observations

* Individual features give **limited predictive power**
* Combining features improves results slightly
* No combination significantly outperforms baseline SGP4

Best performance observed when:

* Multiple orbital parameters are combined
* Temporal context is preserved

---

### Insight

The model struggles because:

* TLE data lacks **external environmental factors**
* Missing key variable:
   **Space weather (Solar Flux, atmospheric drag variations)**

---

## Limitations

* No space weather data included
* Limited dataset (~100 satellites)
* LSTM relies only on historical motion, not external physics

---

## Future Work

* Integrate **Solar Flux and geomagnetic indices**
* Use **Physics-Informed Neural Networks (PINNs)**
* Scale dataset to thousands of satellites
* Improve feature engineering with environmental data

---

## Conclusion

This project demonstrates that:

* AI models (LSTM) can **match traditional physics models (SGP4)**
* However, without domain-specific inputs (like space weather), they cannot surpass them

key takeaway:
**Data quality and domain knowledge matter more than model complexity**

---

## Authors

* Pratyush Negi
* Team Members, University of Delhi

---
