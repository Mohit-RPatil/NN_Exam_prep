
# Activation Functions in Neural Networks

Activation functions are a crucial component of neural networks. They determine the output of a node given a set of inputs. These functions introduce non-linearity into the network, which allows it to learn complex patterns in the data.

---

## Types of Activation Functions

Here are some of the most common types of activation functions used in neural networks:

### 1. Sigmoid Function

The sigmoid function is a smooth, S-shaped function that squashes the input values into a range between 0 and 1.

- **Formula:** `f(x) = 1 / (1 + exp(-x))`
- **Advantages:**
    - The output is in the range (0, 1), which can be interpreted as a probability.
    - It is differentiable, which is necessary for backpropagation.
- **Disadvantages:**
    - **Vanishing Gradient:** For very high or very low input values, the gradient of the sigmoid function is close to zero. This can slow down or even stop the learning process.
    - **Not zero-centered:** The output is not centered around zero, which can make training more difficult.

### 2. Hyperbolic Tangent (Tanh) Function

The Tanh function is similar to the sigmoid function, but it squashes the input values into a range between -1 and 1.

- **Formula:** `f(x) = (exp(x) - exp(-x)) / (exp(x) + exp(-x))`
- **Advantages:**
    - **Zero-centered:** The output is centered around zero, which can help to speed up convergence.
    - It is differentiable.
- **Disadvantages:**
    - **Vanishing Gradient:** Like the sigmoid function, the Tanh function also suffers from the vanishing gradient problem.

### 3. Rectified Linear Unit (ReLU) Function

The ReLU function is one of the most popular activation functions in deep learning. It outputs the input directly if it is positive, and zero otherwise.

- **Formula:** `f(x) = max(0, x)`
- **Advantages:**
    - **Computationally efficient:** It is very simple to compute.
    - **Avoids vanishing gradient:** For positive inputs, the gradient is always 1, which helps to prevent the vanishing gradient problem.
- **Disadvantages:**
    - **Dying ReLU:** If the input to a ReLU neuron is negative, it will output zero. This means that the neuron will not be activated and will not learn. This is known as the "dying ReLU" problem.
    - **Not zero-centered:** The output is not centered around zero.

### 4. Leaky ReLU Function

The Leaky ReLU function is a variation of the ReLU function that is designed to address the "dying ReLU" problem. It has a small positive slope for negative inputs.

- **Formula:** `f(x) = max(0.01*x, x)`
- **Advantages:**
    - **Prevents dying ReLU:** The small slope for negative inputs ensures that the neuron will always have a non-zero gradient.
- **Disadvantages:**
    - The results are not always consistent.

### 5. Softmax Function

The softmax function is a generalization of the sigmoid function that is used for multi-class classification problems. It converts a vector of real numbers into a probability distribution.

- **Formula:** `f(x_i) = exp(x_i) / sum(exp(x_j))` for all j
- **Advantages:**
    - The output is a probability distribution, which is useful for multi-class classification.
- **Disadvantages:**
    - It can be computationally expensive.

---

## Summary

| Activation Function | Formula | Range | Advantages | Disadvantages |
|---|---|---|---|---|
| Sigmoid | `1 / (1 + exp(-x))` | (0, 1) | Probabilistic output, differentiable | Vanishing gradient, not zero-centered |
| Tanh | `(exp(x) - exp(-x)) / (exp(x) + exp(-x))` | (-1, 1) | Zero-centered, differentiable | Vanishing gradient |
| ReLU | `max(0, x)` | [0, inf) | Computationally efficient, avoids vanishing gradient | Dying ReLU, not zero-centered |
| Leaky ReLU | `max(0.01*x, x)` | (-inf, inf) | Prevents dying ReLU | Inconsistent results |
| Softmax | `exp(x_i) / sum(exp(x_j))` | (0, 1) | Probabilistic output for multi-class | Computationally expensive |
