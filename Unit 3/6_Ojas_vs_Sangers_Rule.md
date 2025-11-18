
# Oja's Rule vs. Sanger's Rule (Generalized Hebbian Algorithm - GHA)

Oja's Rule and Sanger's Rule (also known as the Generalized Hebbian Algorithm, GHA) are both unsupervised local learning rules that are extensions of the classical Hebbian learning rule. They are primarily used for **Principal Component Analysis (PCA)**, enabling neural networks to extract principal components from input data. While both aim to address the instability of basic Hebbian learning and perform PCA, they differ in their scope and the number of principal components they can extract.

---

## Oja's Rule

**Oja's Rule** is a modification of the Hebbian learning rule that incorporates a normalization term to prevent weights from growing indefinitely. It is typically applied to a **single neuron** and allows that neuron's weight vector to converge to the **first principal component** of the input data.

### Core Idea:

The standard Hebbian rule can lead to unbounded weight growth. Oja's rule introduces a multiplicative term that effectively normalizes the weight vector, ensuring its stability. This normalization forces the neuron to learn the direction of maximum variance in the input data, which corresponds to the first principal component.

### Update Rule:

For a single neuron with weight vector `W` and input vector `X`, the update rule is:

`ΔW = η * y * (X - y * W)`

Where:
*   `ΔW`: Change in the weight vector.
*   `η`: Learning rate.
*   `y`: Output of the neuron (`y = W^T * X`).
*   `X`: Input vector.
*   `W`: Current weight vector.

The term `(X - y * W)` can be interpreted as subtracting the component of the input that is parallel to the current weight vector, effectively pushing the weight vector towards the direction of the residual input variance.

### Characteristics:

-   **Single Neuron:** Designed for a single output neuron.
-   **First Principal Component:** Learns only the first principal component.
-   **Stability:** Prevents unbounded weight growth.
-   **Online Learning:** Suitable for online learning scenarios.

### Advantages:

-   **Simplicity:** Relatively simple extension of Hebbian learning.
-   **Stability:** Solves the weight explosion problem of basic Hebbian learning.
-   **PCA Capability:** Effectively extracts the first principal component.

### Disadvantages:

-   **Limited Scope:** Cannot extract multiple principal components with a single neuron.
-   **Linearity:** Assumes linear relationships in the data.

---

## Sanger's Rule (Generalized Hebbian Algorithm - GHA)

**Sanger's Rule**, also known as the **Generalized Hebbian Algorithm (GHA)**, is a further generalization of Oja's rule. It is designed for **networks with multiple output neurons** and allows these neurons to extract **multiple principal components** in a hierarchical and ordered manner.

### Core Idea:

Sanger's rule extends Oja's rule by introducing an inhibitory or "decorrelation" term. This term ensures that each subsequent neuron learns a principal component that is orthogonal to the principal components already learned by the preceding neurons. This prevents all neurons from converging to the same first principal component.

### Update Rule:

For the `j`-th neuron with weight vector `W_j` and input vector `X`, the update rule is:

`ΔW_j = η * y_j * (X - Σ_{k=1}^{j} y_k * W_k)`

Where:
*   `ΔW_j`: Change in the weight vector of the `j`-th neuron.
*   `η`: Learning rate.
*   `y_j`: Output of the `j`-th neuron (`y_j = W_j^T * X`).
*   `X`: Input vector.
*   `W_k`: Weight vector of the `k`-th neuron.

The term `Σ_{k=1}^{j} y_k * W_k` represents the sum of the components of the input that have already been captured by the first `j` neurons. By subtracting this from `X`, the `j`-th neuron is forced to learn from the residual input, thus extracting a new, orthogonal principal component. This is an implicit Gram-Schmidt orthogonalization process.

### Characteristics:

-   **Multiple Neurons:** Designed for networks with multiple output neurons.
-   **Multiple Principal Components:** Extracts multiple principal components in descending order of variance.
-   **Orthogonality:** Ensures that the learned principal components are orthogonal to each other.
-   **Online Learning:** Suitable for online learning.

### Advantages:

-   **Full PCA Capability:** Can extract all desired principal components.
-   **Decorrelation:** Explicitly decorrelates the outputs of the neurons.
-   **Stability:** Inherits the stability improvements over basic Hebbian learning.

### Disadvantages:

-   **Complexity:** More complex to implement than Oja's rule due to the summation term.
-   **Linearity:** Still a linear method, limited to finding linear principal components.

---

## Comparison and Contrast

| Feature                 | Oja's Rule                                     | Sanger's Rule (GHA)                                    |
| :---------------------- | :--------------------------------------------- | :----------------------------------------------------- |
| **Number of Neurons**   | Typically for a single neuron                  | For networks with multiple output neurons              |
| **PCA Extraction**      | Extracts only the **first** principal component | Extracts **multiple** principal components in order    |
| **Mechanism**           | Multiplicative normalization                   | Multiplicative normalization + inhibitory/decorrelation term |
| **Orthogonality**       | Implicitly learns the first PC                 | Explicitly enforces orthogonality between learned PCs |
| **Relationship**        | Sanger's rule is a generalization of Oja's rule; the first neuron in a Sanger network behaves like an Oja neuron. |
| **Complexity**          | Simpler                                        | More complex due to the summation term                  |

---

## Conclusion

Both Oja's rule and Sanger's rule are significant advancements in unsupervised learning, particularly for PCA. Oja's rule provides a stable way to extract the most dominant feature, while Sanger's rule extends this to extract a full set of ordered principal components, making it a powerful tool for dimensionality reduction and feature extraction in various applications.
