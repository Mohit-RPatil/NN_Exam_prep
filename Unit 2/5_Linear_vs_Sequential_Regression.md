
# Linear Regression vs. Sequential Regression

While both terms relate to regression analysis, "Linear Regression" refers to a specific statistical model, whereas "Sequential Regression" describes a *methodology* for selecting variables to build a regression model. They are not directly comparable as different types of models but rather as a model versus a model-building strategy.

---

## Linear Regression

**Linear Regression** is a statistical modeling technique used to establish a linear relationship between a dependent variable (the outcome you want to predict) and one or more independent variables (the predictors). It assumes that the relationship between these variables can be best described by a straight line (or a hyperplane in the case of multiple independent variables).

### Key Characteristics:

-   **Nature:** A statistical model.
-   **Objective:** To predict the value of a continuous dependent variable based on the values of one or more independent variables. It aims to find the "best-fit" line that minimizes the sum of squared differences between the observed and predicted values.
-   **Equation:** For simple linear regression: `Y = β0 + β1X + ε`
    *   `Y`: Dependent variable
    *   `X`: Independent variable
    *   `β0`: Y-intercept (bias)
    *   `β1`: Slope (weight)
    *   `ε`: Error term
-   **Assumptions:** Assumes linearity, independence of errors, homoscedasticity (constant variance of errors), and normality of errors.
-   **Output:** Provides coefficients (weights) that quantify the strength and direction of the relationship between each independent variable and the dependent variable.

### Advantages:

-   **Simplicity and Interpretability:** Easy to understand and interpret the coefficients.
-   **Computational Efficiency:** Relatively fast to compute, especially for large datasets.
-   **Foundation:** Forms the basis for many other advanced statistical and machine learning models.

### Disadvantages:

-   **Assumes Linearity:** Performs poorly if the true relationship between variables is non-linear.
-   **Sensitive to Outliers:** Outliers can significantly impact the regression line and model performance.
-   **Limited Predictive Power:** May not capture complex patterns as effectively as non-linear models.

### Example:

Predicting house prices (`Y`) based on square footage (`X`). A linear regression model would find a line that best describes how price changes with square footage.

---

## Sequential Regression (Stepwise Regression / Hierarchical Regression)

**Sequential Regression** is not a type of regression model itself, but rather a **methodology or procedure for selecting predictor variables** to be included in a multiple regression model (often a multiple linear regression model). Its goal is to build a more parsimonious and effective model by identifying the most relevant features from a larger set of potential predictors.

### Key Characteristics:

-   **Nature:** A variable selection technique or model-building strategy.
-   **Objective:** To identify an optimal subset of independent variables for a regression model, typically based on statistical criteria (e.g., p-values, R-squared change).
-   **Process:** Involves adding or removing variables from the model in a step-by-step fashion. Common approaches include:
    *   **Forward Selection:** Starts with no variables and adds the most significant variable at each step until no remaining variable significantly improves the model.
    *   **Backward Elimination:** Starts with all potential variables and removes the least significant variable at each step until all remaining variables are significant.
    *   **Stepwise Selection:** A combination of forward and backward, adding and removing variables at each step.
    *   **Hierarchical Regression:** Variables are added in blocks based on theoretical or practical considerations, and the change in R-squared is assessed.

### Advantages:

-   **Model Simplification:** Helps in creating simpler models by removing irrelevant or redundant predictors.
-   **Feature Selection:** Useful for identifying important features from a large pool of candidates.
-   **Exploratory Tool:** Can be used as an exploratory tool to understand the relative importance of different predictors.

### Disadvantages:

-   **Can Lead to Biased Coefficients:** The coefficients of variables selected through stepwise methods can be biased.
-   **Inflated R-squared:** Can lead to an inflated R-squared value, making the model appear better than it is.
-   **P-value Misinterpretation:** The p-values reported for variables in a stepwise model are often not reliable due to the multiple comparisons made during the selection process.
-   **Order Dependence:** The final model can depend on the order in which variables are considered (especially in forward selection).
-   **Risk of Omitting Important Variables:** May exclude variables that are theoretically important but do not meet the statistical criteria at a particular step.

### Example:

Building a linear regression model to predict house prices, but you have many potential predictors (square footage, number of bedrooms, bathrooms, age, location, garden size, etc.). Sequential regression would help you decide which of these predictors to include in your final linear regression model.

---

## Comparison Summary

| Feature             | Linear Regression                                  | Sequential Regression                                     |
| :------------------ | :------------------------------------------------- | :-------------------------------------------------------- |
| **What it is**      | A statistical model                                | A variable selection methodology for building a model     |
| **Primary Goal**    | Predict a continuous outcome                       | Select optimal predictors for a regression model          |
| **Output**          | Model coefficients, predictions                    | A subset of chosen predictor variables                    |
| **Process**         | Fits a line/hyperplane to data                     | Iteratively adds/removes variables based on criteria      |
| **Relationship**    | The model itself                                   | A technique *applied to* (e.g.) multiple linear regression |
| **Assumptions**     | Statistical assumptions about data and errors      | Relies on statistical tests at each step                  |
