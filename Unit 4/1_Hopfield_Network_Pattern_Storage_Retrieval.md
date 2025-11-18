
# Hopfield Network: Pattern Storage and Retrieval

A **Hopfield network** is a type of recurrent artificial neural network that functions as a content-addressable memory system. Invented by John Hopfield in 1982, it is primarily used for storing and retrieving binary patterns. It's a classic example of an associative memory model, meaning it can retrieve a complete, stored pattern even when presented with a partial or noisy version of that pattern.

---

## Architecture of a Hopfield Network

1.  **Single Layer of Neurons:** A Hopfield network consists of a single layer of `N` interconnected neurons.
2.  **Fully Connected:** Every neuron is connected to every other neuron.
3.  **Recurrent Connections:** The connections are recurrent, meaning the output of a neuron can feed back as input to other neurons, and the network's state evolves over time.
4.  **Symmetric Weights:** The connections are bidirectional and symmetric. This means the weight of the connection from neuron `i` to neuron `j` (`W_ij`) is equal to the weight from neuron `j` to neuron `i` (`W_ji`).
5.  **No Self-Connections:** Neurons do not connect to themselves (`W_ii = 0`).
6.  **Binary/Bipolar Neurons:** Neurons typically have binary activation states, either `{-1, 1}` (bipolar) or `{0, 1}` (binary). Bipolar states are often preferred for mathematical simplicity.
7.  **Energy Function:** A key characteristic is the existence of a global energy function (Lyapunov function) that always decreases as the network updates its state. This ensures that the network will eventually converge to a stable state, which corresponds to a local minimum of this energy function.

---

## How it Works for Pattern Storage (Learning/Training)

Patterns are "stored" in a Hopfield network by adjusting the connection weights between neurons. The network is trained in an unsupervised manner, typically using a variant of Hebbian learning.

1.  **Representing Patterns:** Each pattern to be stored is represented as a binary (or bipolar) vector. For example, an image could be flattened into a vector of pixel values.
2.  **Weight Calculation (Hebbian Learning):** Given `M` patterns to be stored, `S^1, S^2, ..., S^M`, where each `S^p` is a vector of `N` elements (e.g., `S^p = [s_1^p, s_2^p, ..., s_N^p]`), the weights `W_ij` between neuron `i` and neuron `j` are calculated as:

    `W_ij = (1/N) * Σ_{p=1}^{M} (s_i^p * s_j^p)` for `i ≠ j`
    `W_ii = 0` (no self-connections)

    This formula essentially strengthens connections between neurons that are active together across the stored patterns. The `1/N` term is a scaling factor.

---

## How it Works for Pattern Retrieval

Once the weights are set (patterns are stored), the network can retrieve patterns. When a partial, noisy, or distorted input pattern is presented, the network iteratively updates its neuron states until it settles into a stable state, which ideally corresponds to one of the stored patterns.

1.  **Initialization:** An initial input pattern (the query pattern) is presented to the network, setting the initial states of the neurons.
2.  **Asynchronous Update (or Synchronous):**
    *   **Asynchronous:** A single neuron `i` is randomly selected at each step. Its new state `s_i(t+1)` is calculated based on the weighted sum of the current states of all other neurons.
    *   **Synchronous:** All neurons update their states simultaneously at each step. Asynchronous updates are generally preferred as they guarantee convergence to a stable state.
3.  **Activation Rule:** The new state of a neuron `i` is determined by its net input and an activation function (typically a sign function for bipolar states):

    `Net_input_i = Σ_{j≠i} (W_ij * s_j(t))`

    `s_i(t+1) = 1` if `Net_input_i > 0`
    `s_i(t+1) = -1` if `Net_input_i < 0`
    `s_i(t+1) = s_i(t)` if `Net_input_i = 0` (or randomly chosen)

4.  **Convergence:** This update process continues until the network reaches a stable state, meaning no neuron changes its state during an update cycle. This stable state represents the retrieved pattern, which is the stored pattern closest to the initial query pattern in terms of Hamming distance. The network acts as an energy minimization system, where stable states correspond to local minima of its energy function.

---

## Advantages of Hopfield Networks

-   **Content-Addressable Memory:** Can retrieve a complete pattern from a partial or corrupted input, making it robust to noise and incomplete information.
-   **Associative Memory:** Associates an input with a stored pattern.
-   **Simple Architecture:** Relatively simple to understand and implement.
-   **Parallel Processing:** Neuron updates can be performed in parallel.
-   **Energy Minimization:** Guaranteed to converge to a stable state due to the existence of an energy function.

---

## Disadvantages of Hopfield Networks

-   **Limited Storage Capacity:** The number of patterns that can be reliably stored is limited (approximately `0.138 * N` for bipolar neurons, where `N` is the number of neurons). Beyond this capacity, the network starts retrieving spurious patterns or fails to retrieve stored ones.
-   **Spurious States:** The network can converge to "spurious" stable states that are not among the original stored patterns.
-   **Binary/Bipolar Inputs:** Primarily designed for binary or bipolar patterns, limiting its direct application to continuous data without preprocessing.
-   **No Learning After Training:** Once weights are set, the network typically doesn't learn new patterns without recalculating the entire weight matrix.

---

## Applications

-   **Pattern Recognition:** Recognizing noisy or incomplete patterns (e.g., characters, images).
-   **Image Restoration:** Reconstructing corrupted images.
-   **Optimization Problems:** Solving combinatorial optimization problems (e.g., Traveling Salesperson Problem) by mapping the problem to the energy function.
-   **Error Correction:** Correcting errors in transmitted data.

Hopfield networks, while having limitations, provided significant insights into associative memory and the dynamics of recurrent neural networks, influencing subsequent research in neural computation.
