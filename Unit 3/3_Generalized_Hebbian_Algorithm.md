
# Generalized Hebbian Algorithm (GHA)

The **Generalized Hebbian Algorithm (GHA)**, also known as **Sanger's Rule**, is an unsupervised learning algorithm used in artificial neural networks. It is a direct extension of the classical Hebbian learning rule and is primarily employed for **Principal Component Analysis (PCA)**, enabling dimensionality reduction and feature extraction. GHA is particularly valuable for its ability to extract principal components from data without explicitly computing the covariance matrix, making it computationally efficient for large datasets.

---

## Core Principle

The classical Hebbian learning rule states that "neurons that fire together, wire together," meaning the connection strength (weight) between two neurons increases if they are simultaneously active. GHA extends this by introducing a mechanism to decorrelate the outputs of the neurons, ensuring that each neuron learns a different principal component.

GHA aims to find the principal components (eigenvectors) of the input data's autocorrelation matrix. These principal components represent the directions of maximum variance in the data, and projecting the data onto these components reduces dimensionality while retaining most of the information.

---

## Algorithm

Consider a single-layer feedforward network with `N` inputs and `M` outputs, where `M < N`. Each output neuron `j` has a weight vector `W_j`.

The GHA learning rule for updating the weight vector `W_j` of the `j`-th output neuron, given an input vector `X`, is:

1.  **Calculate Output:** For each output neuron `j` (from 1 to `M`), calculate its output `y_j`:
    `y_j = W_j^T * X`

2.  **Update Weights:** The weight vector `W_j` is updated using the following rule:
    `W_j(t+1) = W_j(t) + η * y_j(t) * [X(t) - Σ_{k=1}^{j} y_k(t) * W_k(t)]`

    Where:
    *   `t` is the current iteration.
    *   `η` is the learning rate.
    *   `y_j(t)` is the output of the `j`-th neuron at time `t`.
    *   `X(t)` is the input vector at time `t`.
    *   `W_k(t)` is the weight vector of the `k`-th neuron at time `t`.

The crucial part of this rule is the term `[X(t) - Σ_{k=1}^{j} y_k(t) * W_k(t)]`. This term effectively subtracts the components of the input that have already been "explained" by the previous principal components (learned by neurons `1` to `j-1`). This ensures that each subsequent neuron learns a new, orthogonal principal component. This is often referred to as the **Gram-Schmidt orthogonalization process** being implicitly performed.

---

## Advantages

1.  **Principal Component Extraction:** Effectively extracts the principal components of the input data in an unsupervised manner.
2.  **Computational Efficiency:** Avoids the explicit computation and inversion of the covariance matrix, which can be computationally expensive for high-dimensional data. It directly learns from the data.
3.  **Online Learning Capability:** GHA is well-suited for online learning, where data arrives sequentially, and weights can be updated continuously without needing to store the entire dataset.
4.  **Parallel Implementation:** The updates for different neurons can be performed in parallel, making it suitable for parallel computing architectures.
5.  **Biologically Plausible:** It is a biologically inspired algorithm, extending the Hebbian learning rule.

---

## Disadvantages

1.  **Linearity Assumption:** GHA, like PCA, is a linear method. It can only find linear principal components and may not be effective for extracting features from data with complex non-linear structures.
2.  **Sensitivity to Learning Rate:** The choice of learning rate `η` is critical for stable convergence.
3.  **Order Dependence:** The order in which neurons learn principal components can sometimes be influenced by initialization, though the final set of components should be the same.
4.  **Requires Orthogonality:** The algorithm implicitly enforces orthogonality between the learned principal components, which is a characteristic of PCA.

---

## Applications

-   **Dimensionality Reduction:** Reducing the number of features in a dataset while retaining most of the variance, which is useful for visualization and speeding up subsequent learning algorithms.
-   **Feature Extraction:** Extracting the most salient features from raw data.
-   **Data Compression:** Compressing data by representing it with fewer principal components.
-   **Noise Reduction:** Filtering out noise by focusing on the principal components that capture the signal.

GHA provides an elegant and efficient neural network approach to PCA, offering a powerful tool for unsupervised learning and data preprocessing.
