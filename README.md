[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mobasserulHaque/Mechanistic_Interpretability/blob/main/Mechanistic_Interpretability.ipynb)


## Attribution (Use of AI Citation)  

>The README was generated with assistance from an AI system (GPT-5 Thinking) and subsequently reviewed/edited by the author, who is responsible for the final content.

>Remaining parts of assignment LLMs have not been used. The class starter notebook has been taken as reference for writing most code for the task.

# 🧠 Mechanistic Interpretability: Investigating a Tiny Neural Network on 5-Bit Palindromes

This repository contains a complete mechanistic interpretability project exploring how a small neural network internally represents the structure of a simple task: detecting whether a **5-bit binary string is a palindrome**.  
All experiments, visualizations, and analysis are contained in a Google Colab notebook, including training, probing, and interpreting internal neuron behavior.


## 📌 Project Overview

The purpose of this project is to *open up the tiny brain* of a neural network and identify how individual neurons encode meaningful structure.  
To keep everything interpretable, both the task and the model are intentionally tiny.

### **Task**
- Binary classification:  
  **Is a 5-bit sequence a palindrome?**

### **Model**
- A small **MLP (Multi-Layer Perceptron)**
- **1 hidden layer**
- **6 hidden neurons**
- **Tanh activation**
- Small enough to manually inspect weights, activations, and circuits

### **Dataset**
- All **32 possible** 5-bit binary sequences  
- Fully enumerable → allows complete analysis with no sampling uncertainty

### **Interpretability Focus**
- Mechanistic interpretability of a **single key neuron**
- How hidden neurons encode:
  - symmetry,
  - positional relationships,
  - equality between bits,
  - and task-relevant circuits

Because the model is small and deterministic, we can inspect *every input pattern*, *every intermediate activation*, and *every learned weight*   enabling full neuron-level interpretability.

---

## 🚀 Key Components of the Analysis

### **1. Tiny Task: 5-Bit Palindrome Detection**

We define a 5-bit sequence

$$
[b_0, b_1, b_2, b_3, b_4]
$$

as a **palindrome** when:

$$
b_0 = b_4
$$

$$
b_1 = b_3
$$

This simple, symmetric structure encourages the network to learn **equality** and **mirror-pattern** relationships between bit positions.

---

### **2. Tiny Model**

A deliberately small neural network designed for full interpretability:

- **Input:** 5 bits  
- **Hidden Layer:** 6 neurons, **Tanh** activation  
- **Output Layer:** 1 unit with **Sigmoid** (binary classification)

The compact architecture lets us analyze each neuron individually and inspect how information flows through the network.

---

### **3. Exploring the Network’s Internals**

The notebook walks through a suite of mechanistic interpretability tools, including:

- Extracting **hidden activations** for all 32 possible input sequences  
- Computing correlations with interpretable, human-defined features:
  - **Outer symmetry:**
    $$
    b_0 = b_4
    $$
  - **Inner symmetry:**
    $$
    b_1 = b_3
    $$
- Visualizing neuron activations using **heatmaps**
- Comparing activation patterns for palindrome vs non-palindrome inputs
- Inspecting **top-activating** and **bottom-activating** input sequences
- Examining **learned weights** and biases for each neuron
- Running **input manipulations** to probe feature selectivity
- Analyzing **pre-activation** distributions to understand Tanh saturation

Each technique helps reveal what internal computations each neuron has specialized to represent.

---

### **4. Case Study: Neuron 2**

A detailed neuron-level investigation shows that:

- **Neuron 2 is strongly correlated with inner symmetry**
  $$
  b_1 = b_3
  $$
- It activates most when the inner bits contain at least one `1`
- It becomes strongly negative when both inner bits are `0`
- Its learned weights confirm this specialization:

  ```text
  b1 → +4.38
  b3 → +5.67
  b2 → minimal influence
```

- The Tanh nonlinearity pushes its output toward –1 or +1, creating an almost binary “inner-match detector”

### Conclusion:

Neuron 2 functions as an inner-bit feature detector, playing a key role in how the network distinguishes palindromes from non-palindromes.