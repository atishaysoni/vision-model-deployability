# Comparative Analysis of Deep Learning Models for Image Classification

[cite_start]**Published in:** ICAMC 2026 (Springer) [cite: 1, 282]  
[cite_start]**Authors:** Atishay Soni, Himanshu Jha, Arman Singh, Manoj Kumar [cite: 2]  
[cite_start]**Institution:** Netaji Subhas University of Technology, Delhi, India [cite: 3]  

## Project Overview
[cite_start]This repository contains the training and evaluation notebooks for a comparative deployability study of four vision architectures: MobileNet V2, ResNet-50, EfficientNet-B0, and Vision Transformer ($ViT-B/16$)[cite: 7]. [cite_start]The project moves beyond idealized accuracy benchmarks to evaluate models based on real-world edge deployment constraints[cite: 6, 64]. 

## Key Features & Methodology
* [cite_start]**Complex Feature Extraction:** Models were trained on the CIFAR-100 dataset (resized to 224x224) using transfer learning to evaluate fine-grained classification capabilities[cite: 8, 66, 67].
* [cite_start]**Cross-Domain Generalization:** We utilized linear probing on the STL-10 dataset, keeping the trained feature extraction backbones frozen[cite: 11, 78].
* [cite_start]**Edge Deployability & Quantization:** Native PyTorch models were exported to ONNX FP32 intermediate representation and dynamically compressed via INT8 quantization to simulate realistic CPU inference latencies[cite: 8, 75, 76].
* [cite_start]**Physical Energy Profiling:** The `CodeCarbon` library was integrated into the inference loop to track precise GPU power consumption in Joules over 1,000 consecutive inferences[cite: 10, 77]. [cite_start]Hardware utilized for training was an NVIDIA Tesla P100[cite: 70].
* [cite_start]**Robustness & Calibration:** Evaluated Expected Calibration Error (ECE) via temperature scaling and tested resilience against synthetic image corruptions[cite: 49, 80, 81, 195].
* [cite_start]**Statistical Validation:** Applied McNemar's Test on raw prediction vectors to prove architectural differences were statistically significant ($p<0.05$)[cite: 11, 81, 264, 265].

## Architectures Evaluated
1. [cite_start]**MobileNet V2:** Highly efficient, utilizing depthwise separable convolutions[cite: 18, 31].
2. [cite_start]**ResNet-50:** A deep residual network[cite: 18, 29].
3. [cite_start]**EfficientNet-B0:** Uses a compound method of scaling to optimize depth, width, and resolution[cite: 18, 33].
4. [cite_start]**Vision Transformer ($ViT-B/16$):** An attention-based architecture stabilized using a custom three-epoch linear warm-up and cosine annealing learning rate scheduler[cite: 18, 35, 73].

## Key Results

| Model | CIFAR-100 Accuracy | STL-10 Accuracy | INT8 Latency | Energy (per 1,000 inferences) |
| :--- | :--- | :--- | :--- | :--- |
| **EfficientNet-B0** | [cite_start]84.93% [cite: 85, 90] | [cite_start]82.34% [cite: 90] | [cite_start]11.06 ms [cite: 189] | [cite_start]718.21 Joules [cite: 10, 185, 189] |
| **ResNet-50** | [cite_start]84.02% [cite: 90] | [cite_start]82.43% [cite: 90] | [cite_start]37.58 ms [cite: 189] | [cite_start]2343.14 Joules [cite: 189] |
| **MobileNet V2** | [cite_start]81.52% [cite: 90] | [cite_start]78.94% [cite: 90] | [cite_start]4.89 ms [cite: 184, 189] | [cite_start]312.83 Joules [cite: 184, 189] |
| **ViT-B/16** | [cite_start]52.86% [cite: 9, 86, 90] | [cite_start]59.85% [cite: 90] | [cite_start]125.24 ms [cite: 189] | [cite_start]8172.10 Joules [cite: 10, 186, 189] |

[cite_start]**Conclusion:** EfficientNet-B0 provided the best statistical tradeoff between high accuracy, reliable calibration, and efficient energy usage[cite: 273]. [cite_start]While MobileNet V2 is the most hardware-efficient [cite: 184][cite_start], the $ViT-B/16$ proved unfeasible for battery-constrained edge settings without massive pre-training, though its global attention mechanism displayed high robustness to synthetic corruptions[cite: 9, 186, 196].