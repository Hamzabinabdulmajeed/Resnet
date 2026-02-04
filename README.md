# ResNet Family Benchmarking on CIFAR-10

This project provides a comprehensive structural and performance analysis of the **Residual Network (ResNet)** family. By training five different architectures—from the lightweight **ResNet-18** to the massive **ResNet-152**—on the **CIFAR-10** dataset, this benchmark explores the trade-offs between model depth, training time, and predictive accuracy.

## Project Overview

The goal of this study was to observe the "Depth vs. Trainability" paradox in a controlled environment using a **Kaggle P100 GPU**. We specifically analyzed how adding layers impacts the vanishing gradient problem and whether deeper models always translate to significantly better results on low-resolution (32x32) images like those in CIFAR-10.

### Key Findings

* **The Accuracy Ceiling:** On CIFAR-10, ResNet-18 achieves ~88% accuracy in just 23 minutes, while ResNet-152 takes over 5 hours to reach ~91%.
* **Diminishing Returns:** Increasing depth by 8x (18 to 152 layers) only yielded a ~3.7% increase in accuracy.
* **Optimization Gap:** Deeper models (ResNet-101/152) require significantly more epochs to fully converge compared to shallower variants.

---

## Performance Comparison

| Model | Layers | Params | Runtime (P100) | Epochs | Accuracy |
| --- | --- | --- | --- | --- | --- |
| **ResNet-18** | 18 | ~11M | 23m 38s | 100 | 87.92% |
| **ResNet-34** | 34 | ~21M | 28m 44s | 100 | 86.41% |
| **ResNet-50** | 50 | ~25M | 1h 35m | 150 | 87.93% |
| **ResNet-101** | 101 | ~44M | 3h 39m | 200 | 88.17% |
| **ResNet-152** | 152 | ~60M | 5h 12m | 250 | **91.68%** |

---

## Implementation Links

Each model was implemented and trained in its own environment. You can view the full code, logs, and loss curves below:

* [ResNet-18 Notebook](https://www.kaggle.com/code/hamzabinbutt/resnet-18)
* [ResNet-34 Notebook](https://www.kaggle.com/code/hamzabinbutt/resnet-34)
* [ResNet-50 Notebook](https://www.kaggle.com/code/hamzabinbutt/resnet-50)
* [ResNet-101 Notebook](https://www.kaggle.com/code/hamzabinbutt/resnet-101)
* [ResNet-152 Notebook](https://www.kaggle.com/code/hamzabinbutt/resnet-152)

---

## Architecture Analysis

The transition from ResNet-34 to ResNet-50 marks a shift in internal structure:

1. **BasicBlock (18 & 34):** Uses two  convolutional layers.
2. **BottleneckBlock (50, 101, & 152):** Uses a  stack. The  layers reduce and then restore dimensions, making the deeper models more computationally efficient than if they used standard blocks.

---

## How to Run

1. Clone the repository or open any of the Kaggle links above.
2. Ensure you have `torch`, `torchvision`, and `matplotlib` installed.
3. Set your accelerator to **GPU** (P100 or T4 recommended).
4. Run the cells to begin training and validation.

---

Would you like me to add a **Future Improvements** section to this README, focusing on techniques like Data Augmentation or Learning Rate Schedulers?
