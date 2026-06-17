# Comparative Analysis of Deep Learning Models for Image Classification

**Published in:** ICAMC 2026 (Springer)  
**Authors:** Atishay Soni, Himanshu Jha, Arman Singh, Manoj Kumar  
**Institution:** Netaji Subhas University of Technology, Delhi, India  

## Project Overview
This repository contains the training and evaluation notebooks for a comparative deployability study of four vision architectures: MobileNet V2, ResNet-50, EfficientNet-B0, and Vision Transformer (ViT-B/16). The project moves beyond idealized accuracy benchmarks to evaluate models based on real-world edge deployment constraints. 

## Key Features & Methodology
* **Complex Feature Extraction:** Models were trained on the CIFAR-100 dataset (resized to 224x224) using transfer learning to evaluate fine-grained classification capabilities.
* **Cross-Domain Generalization:** We utilized linear probing on the STL-10 dataset, keeping the trained feature extraction backbones frozen.
* **Edge Deployability & Quantization:** Native PyTorch models were exported to ONNX FP32 intermediate representation and dynamically compressed via INT8 quantization to simulate realistic CPU inference latencies.
* **Physical Energy Profiling:** The CodeCarbon library was integrated into the inference loop to track precise GPU power consumption in Joules over 1,000 consecutive inferences. Hardware utilized for training was an NVIDIA Tesla P100.
* **Robustness & Calibration:** Evaluated Expected Calibration Error (ECE) via temperature scaling and tested resilience against synthetic image corruptions.
* **Statistical Validation:** Applied McNemar's Test on raw prediction vectors to prove architectural differences were statistically significant (p<0.05).

## Architectures Evaluated
1. **MobileNet V2:** Highly efficient, utilizing depthwise separable convolutions.
2. **ResNet-50:** A deep residual network.
3. **EfficientNet-B0:** Uses a compound method of scaling to optimize depth, width, and resolution.
4. **Vision Transformer (ViT-B/16):** An attention-based architecture stabilized using a custom three-epoch linear warm-up and cosine annealing learning rate scheduler.

## Key Results

| Model | CIFAR-100 Accuracy | STL-10 Accuracy | INT8 Latency | Energy (per 1,000 inferences) |
| :--- | :--- | :--- | :--- | :--- |
| **EfficientNet-B0** | 84.93% | 82.34% | 11.06 ms | 718.21 Joules |
| **ResNet-50** | 84.02% | 82.43% | 37.58 ms | 2343.14 Joules |
| **MobileNet V2** | 81.52% | 78.94% | 4.89 ms | 312.83 Joules |
| **ViT-B/16** | 52.86% | 59.85% | 125.24 ms | 8172.10 Joules |

**Conclusion:** EfficientNet-B0 provided the best statistical tradeoff between high accuracy, reliable calibration, and efficient energy usage. While MobileNet V2 is the most hardware-efficient, the ViT-B/16 proved unfeasible for battery-constrained edge settings without massive pre-training, though its global attention mechanism displayed high robustness to synthetic corruptions.