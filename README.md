# MLB Game Outcome Prediction Project

## Project Overview

This project aims to participate in a competition to predict the winning team for each MLB game. The task is divided into two stages:
- **Stage 1:** Use first-half season data to predict second-half game outcomes.
- **Stage 2:** Predict the outcomes for the entire 2024 season.

To improve prediction accuracy, we employed data augmentation, feature engineering, and various modeling techniques including Logistic Regression, Decision Trees, Random Forest, XGBoost, and Neural Network. Overall, XGBoost demonstrated the best balance across both stages, while the Neural Network showed notable performance in Stage 2 under certain settings.

---

## Model Overview

### Logistic Regression
- **Objective:** Build a baseline model and perform feature importance analysis.
- **Key Points:** Explore various missing value imputation methods (mean, median, mode, zero imputation) and improve model performance with polynomial transformations and blending techniques.

### Decision Tree and Random Forest
- **Objective:** Capture nonlinear features using Decision Trees and Random Forest.
- **Key Points:** Analyze Gini and Entropy as splitting criteria, and adjust tree depth and the number of features to observe their impact on model accuracy.

### XGBoost
- **Objective:** Leverage the efficiency and regularization capabilities of XGBoost to handle complex data relationships.
- **Key Points:** Use Optuna for hyperparameter tuning. The final model achieved a public test accuracy of 0.59167 in Stage 1, demonstrating its advantage in handling nonlinear interactions and high-dimensional features.

### Neural Network (My Primary Area of Responsibility)
- **Objective:** Develop a multilayer neural network that uses nonlinear activation functions to capture complex data relationships, with the addition of a "Home-Away Average Difference" feature to enhance predictive power.
- **Methodology:**
  - **Data Processing:** In addition to standard data preprocessing, we applied time-weighted processing for game data by using a Time-Weighted Loss. This approach assigns higher weights to more recent game samples.
  - **Hyperparameter Optimization:** We used Optuna to automatically tune the network architecture and training parameters—including the number of layers, hidden layer sizes, dropout rates, learning rate, weight decay, and activation function. Among various optimizers (AdamW, RAdam, AdaBound), AdaBound demonstrated faster convergence and greater stability.
  - **Model Performance:** Although the Neural Network achieved promising public test accuracy (0.58554) in Stage 2, it is more sensitive and computationally intensive compared to XGBoost. The model also exhibited a risk of overfitting, so an early stopping strategy was employed to mitigate excessive training.
- **Key Note:** Given the relatively small dataset (approximately 11,000 samples), the neural network may not capture high-dimensional features as efficiently as tree-based models. However, with careful hyperparameter tuning and feature engineering, it remains competitive in Stage 2.

---

## Results and Conclusions

- **Stage 1:** The XGBoost model achieved the best public test accuracy of 0.59167. The comparative results illustrate the strengths and weaknesses of different approaches when handling nonlinear data.
- **Stage 2:** Although the Neural Network achieved a public test accuracy of 0.58554 under specific settings, its performance on the private test set was less stable (private score: 0.53349) due to the limited data and sensitivity to noise.
- **Final Recommendation:** Considering all models, XGBoost offers the best balance of accuracy, scalability, and efficiency, making it the recommended approach for MLB game predictions. Nonetheless, the Neural Network—with its specialized time-weighting and additional feature engineering—has potential advantages in capturing complex relationships.
