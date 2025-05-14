# Jailbreaking Deep Models: Adversarial Attacks on Image Classifiers

## Overview

This project explores the vulnerability of deep convolutional neural networks, specifically ResNet-34 and DenseNet-121, to adversarial attacks. Using a subset of the ImageNet dataset (100 classes), we generate and evaluate both pixel-wise (FGSM, PGD) and patch-based adversarial attacks. We also analyze how these attacks transfer across different model architectures.

---

## Introduction

Deep neural networks like ResNet-34 and DenseNet-121 achieve high accuracy on image classification tasks but are surprisingly vulnerable to adversarial attacks. In these attacks, small, carefully crafted changes to input images can cause models to make incorrect predictions with high confidence. This project tests the robustness of a pre-trained ResNet-34 model against such attacks and examines how well adversarial examples transfer to DenseNet-121.

---

## Methods

- **Pixel-wise Attacks (L∞):**
  - **FGSM (Fast Gradient Sign Method):** Single-step attack with ε = 0.02.
  - **PGD (Projected Gradient Descent):** Multi-step attack (10 steps, step size 0.005, ε = 0.02).
- **Patch-based Attack (L0):**
  - PGD-style attack applied to a random 32x32 patch (10 steps, step size 0.03, ε = 0.3).

All attacks are constrained to keep changes visually imperceptible or localized.

---

## Results

### Accuracy Comparison Before Transfer (Evaluated on ResNet-34)

| Dataset        | Model      | Top-1 Accuracy | Top-5 Accuracy |
|----------------|------------|:--------------:|:--------------:|
| Original       | ResNet-34  |    0.7600      |    0.9420      |
| FGSM Attack    | ResNet-34  |    0.2640      |    0.5060      |
| PGD Attack     | ResNet-34  |    0.0040      |    0.0640      |
| Patch Attack   | ResNet-34  |    0.1620      |    0.5000      |

### Transferability Evaluation (Evaluated on DenseNet-121)

| Dataset        | Model         | Top-1 Accuracy | Top-5 Accuracy |
|----------------|---------------|:--------------:|:--------------:|
| Original       | DenseNet-121  |    0.7480      |    0.9360      |
| FGSM Attack    | DenseNet-121  |    0.4880      |    0.7780      |
| PGD Attack     | DenseNet-121  |    0.4920      |    0.7940      |
| Patch Attack   | DenseNet-121  |    0.7120      |    0.9080      |

---

## Observations

- All adversarial attacks caused significant drops in accuracy for ResNet-34, with PGD being the most effective.
- Attacks generated for ResNet-34 also reduced DenseNet-121’s accuracy, showing strong transferability for pixel-wise attacks.
- Patch-based attacks were less transferable, with DenseNet-121 retaining higher accuracy on these images.
- These results highlight the need for robust defense strategies, as even small or localized perturbations can compromise model reliability.

---

## Lessons Learned

- Deep models are highly vulnerable to both global and localized adversarial attacks.
- Iterative attacks like PGD are especially effective.
- Adversarial examples often transfer between models, posing a real-world security risk.
- Careful tuning of attack parameters is crucial for balancing effectiveness and imperceptibility.

---

## Conclusion

Adversarial attacks can dramatically reduce the accuracy of state-of-the-art image classifiers, and many attacks transfer across different architectures. This underscores the urgent need for developing more robust and secure AI systems.

