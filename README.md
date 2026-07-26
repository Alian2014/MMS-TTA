# Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation

[![Paper](https://img.shields.io/badge/Paper-PDF-red.svg)](Link_to_your_paper)
[![Conference](https://img.shields.io/badge/Conference-ACM_MM_2026-blue.svg)](Link_to_conference)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Authors:** Guohao Jiang, Zhiheng Ma, Chenhao Ding, SongLin Dong, Qiang Wang, Yuhang He, Yihong Gong
> 
> **Institutions:** Xi'an Jiaotong University, Shenzhen University of Advanced Technology, The University of Tokyo

This is the official PyTorch implementation of the ACM MM 2026 paper [**Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation**](Link_to_your_paper). 

## Abstract
Test-Time Adaptation (TTA), particularly the training-free paradigm, has garnered widespread attention due to its significant advantages in addressing test-time distribution shifts in Vision-Language Models. However, existing training-free approaches are often constrained by the inherent limitations caused by an over-reliance on a single textual or visual modality, resulting in suboptimal performance and robustness. To address this issue, we propose a novel training-free dynamic multimodal synergy strategy (**MMS-TTA**).

## Highlights

*   **Hierarchical Retrieval-Augmented (RA) Paradigm:** We construct a cache-based, hierarchical RA mechanism to extract textual modality features with enhanced robustness, effectively alleviating the blind confidence commonly found in text-reliant methods.
*   **Dynamic Multimodal Synergy:** We introduce a negative-entropy-driven dynamic synergy mechanism that adaptively fuses the optimized textual modality, the visual modality, and the original CLIP modality to yield a highly robust and confident predictive distribution.
*   **State-of-the-Art Performance and Efficiency:** MMS-TTA consistently outperforms state-of-the-art approaches across diverse Out-of-Distribution (OOD) and cross-domain tasks. It operates efficiently, requiring only 1.2 GB of memory with an inference speed of 10.77 fps on a single NVIDIA 3090 GPU.

## Methodology

Our framework overcomes the performance ceiling imposed by unimodal reliance through two core designs:

### 1. Training-Free Textual Adaptation via Hierarchical RA
To address the pathological concentration issue in text-only methods, we leverage an LLM-generated description pool and employ a coarse-to-fine Hierarchical RA paradigm. This structured matching mechanism filters out noisy semantic features and quantifies cross-modal alignment via an Optimal Transport (OT) distance.

### 2. Dynamic Multimodal Synergy and Fusion
We intelligently aggregate the original zero-shot prediction ($P_{clip}$), the cache-based visual prediction ($P_{vis}$), and the hierarchical RA textual prediction ($P_{txt}$). We establish an Instance-level Consensus Anchor grounded in Jensen-Shannon divergence:

$$P_{cons}=\frac{1}{3}(P_{clip}+P_{vis}+P_{txt})$$

This consistency-aware design adaptively rewards multimodal consensus and suppresses isolated overconfidence. The framework dynamically heavily penalizes the weights of modalities exhibiting high uncertainty and severe consensus divergence, mitigating unimodal predictive biases without requiring iterative optimization.

## Main Results

MMS-TTA demonstrates superior robustness and accuracy compared to 12 state-of-the-art baselines. 

### Cross-Dataset Benchmark (ViT-B/16 Backbone)
*Performance evaluated across 9 diverse image classification datasets.*

| Method | Aircraft | Caltech101 | DTD | Flowers102 | OxfordPets | SUN397 | UCF101 | **Average** |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| CLIP | 23.22 | 93.55 | 45.04 | 66.99 | 86.92 | 65.63 | 65.16 | 66.16 |
| TPT | 24.78 | 94.16 | 47.75 | 68.98 | 87.79 | 65.50 | 68.04 | 67.62 |
| DPE | 28.95 | 94.81 | 54.20 | 75.07 | 91.14 | 70.07 | 70.44 | 70.91 |
| BoostAdapter| 27.45 | 94.77 | 45.69 | 71.66 | 89.51 | 68.09 | 71.93 | 69.51 |
| **MMS-TTA (Ours)**| **30.81** | **95.13** | **58.92** | **78.36** | **92.45** | **70.44** | **73.59** | **73.00** |

### Out-of-Distribution (OOD) Benchmark (ViT-B/16 Backbone)
*Performance evaluated on ImageNet variants under severe distribution shifts.*

| Method | ImageNet-A | ImageNet-R | ImageNet-Sketch | ImageNet-V2 | **Average** |
| :--- | :---: | :---: | :---: | :---: | :---: |
| CLIP | 49.89 | 77.65 | 48.24 | 61.88 | 59.42 |
| DiffTPT | 55.68 | 75.00 | 46.80 | 65.10 | 60.65 |
| CuPL | 50.23 | 78.16 | 49.60 | 63.00 | 60.25 |
| BoostAdapter| 60.11 | 80.24 | 50.54 | 64.67 | 63.89 |
| **MMS-TTA (Ours)**| **64.31** | **81.15** | **52.41** | **65.96** | **65.96** |

## Quick Start

### 1. Requirements
Ensure the necessary environment dependencies are installed prior to execution.
```bash
git clone [https://github.com/YourUsername/MMS-TTA.git](https://github.com/YourUsername/MMS-TTA.git)
cd MMS-TTA
pip install -r requirements.txt
```

### 2. Data Preparation
Our evaluation strictly follows standard OOD and Cross-Domain TTA settings. Download the corresponding datasets (e.g., ImageNet-A, ImageNet-R, Caltech101) and organize them sequentially in the data/ directory.

### 3. Run Inference
To evaluate MMS-TTA on a specific dataset utilizing the ViT-B/16 backbone, execute the following script:
```bash
python eval.py --dataset imagenet_a --backbone ViT-B/16 --gpu 0
```

## Citation
If you find our work or this code repository useful for your research, please consider citing:
```bash
@inproceedings{jiang2026beyond,
  title={Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation},
  author={Jiang, Guohao and Ma, Zhiheng and Ding, Chenhao and Dong, SongLin and Wang, Qiang and He, Yuhang and Gong, Yihong},
  booktitle={Proceedings of the 34th ACM International Conference on Multimedia},
  year={2026}
}
```
