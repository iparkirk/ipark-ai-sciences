---
title: Two Equivalent Formula for Cross Entropy Loss
date: 2025-01-23
summary: Two formulations are mathematically equivalent, but the second one explicitly expands the softmax operation applied to the logits. Let’s break it down to understand why they represent the same thing.
---
### **1. First Formulation**
$$
L_\text{batch} = -\frac{1}{N} \sum_{i=1}^N \sum_{c=1}^C y_{\text{label},i,c} \log(y_{\text{pred},i,c})
$$

- **Explanation**:
  - $ N $: Number of samples in the batch.
  - $ C $: Number of classes.
  - $ y_{\text{label},i,c} $: One-hot encoded true label for the $ i $-th sample and $ c $-th class.
  - $ y_{\text{pred},i,c} $: Predicted probability for the $ c $-th class of the $ i $-th sample.
  - The term $ y_{\text{label},i,c} $ ensures that only the predicted probability of the **true class** contributes to the loss.


### **2. Second Formulation**

$$
L_{\text{batch}} = -\frac{1}{N} \sum_{i=1}^N \log\left(\frac{\exp(y_{\text{pred},i,y_{\text{label}}})}{\sum_{j=1}^C \exp(y_{\text{pred},i,j})}\right)
$$

- **Explanation**:
  - The numerator $ \exp(y_{\text{pred},i,y_{\text{label}}}) $: The unnormalized score (logit) for the true class, exponentiated.
  - The denominator $ \sum_{j=1}^C \exp(y_{\text{pred},i,j}) $: The sum of exponentiated logits for all classes (i.e., the softmax denominator).
  - The term inside the logarithm is the softmax probability $ y_{\text{pred},i,y_{\text{label}}} $, computed for the true class.


### **Why Are They Equivalent?**

#### **Key Observations**:
1. In the first formulation, $ y_{\text{label},i,c} $ is a one-hot encoded vector, meaning only the term corresponding to the true class $ c = y_{\text{label}} $ contributes to the sum:
$$
   \sum_{c=1}^C y_{\text{label},i,c} \log(y_{\text{pred},i,c}) = \log(y_{\text{pred},i,y_{\text{label}}})
$$

2. In the second formulation, the term inside the logarithm:
$$
   \frac{\exp(y_{\text{pred},i,y_{\text{label}}})}{\sum_{j=1}^C \exp(y_{\text{pred},i,j})}
$$
   is exactly the softmax probability of the true class $ y_{\text{pred},i,y_{\text{label}}} $. Therefore:
$$
   \log\left(\frac{\exp(y_{\text{pred},i,y_{\text{label}}})}{\sum_{j=1}^C \exp(y_{\text{pred},i,j})}\right) = \log(y_{\text{pred},i,y_{\text{label}}})
$$

#### **Connection**:
The first formulation directly uses the true class probability after applying softmax, while the second formulation shows the explicit softmax calculation step. Both result in the same value for the loss.
