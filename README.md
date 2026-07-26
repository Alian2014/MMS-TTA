# Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation (ACM MM 2026)

 official PyTorch implementation of the ACM MM 2026 paper: **"Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation"**[cite: 1].

> **Authors:** Guohao Jiang, Zhiheng Ma, Chenhao Ding, SongLin Dong, Yuhang He, Qiang Wang, Yihong Gong[cite: 1]  
> **Institutions:** Xi'an Jiaotong University, Shenzhen University of Advanced Technology, The University of Tokyo[cite: 1]  
> 📜 [Paper](https://arxiv.org/abs/xxx) | 🌐 [Project Page](https://your-project-page.github.io)

---

## 💡 Overview

Existing training-free Test-Time Adaptation (TTA) methods for Vision-Language Models (VLMs) often suffer from unimodal reliance[cite: 1]:
1. **Vision-reliant methods** produce overly dispersed predictions with **low confidence**[cite: 1].
2. **Text-reliant methods** yield pathologically concentrated predictions leading to **blind overconfidence**[cite: 1].

To overcome these unimodal bottlenecks, we propose **MMS-TTA**, a training-free dynamic Multimodal Synergy framework that achieves a synergy of **high robustness and high confidence**[cite: 1]:
* **Hierarchical Retrieval-Augmented (H-RA) Module:** A coarse-to-fine mechanism using Optimal Transport (OT) to reshape textual representations and suppress semantic noise, mitigating blind overconfidence[cite: 1].
* **Dynamic Multimodal Synergy (MMS):** An instance-level cross-modal consensus anchor (grounded in Jensen-Shannon & KL divergence) that dynamically fuses zero-shot CLIP, cache-based visual, and H-RA textual modalities without backpropagation[cite: 1].

![MMS-TTA Overview](assets/framework.png) <!-- Ensure you upload your Figure 2 here -->

---

## 🚀 Main Results

### Cross-Dataset Benchmark (ViT-B/16 & ResNet50)
MMS-TTA outperforms state-of-the-art training-free and optimization-based TTA methods across 9 benchmark datasets[cite: 1]:

| Backbone | Method | Type | Avg Acc (%) | Aircraft | Caltech | Flowers | Pets | SUN397 | UCF101 | Cars | DTD | Food101 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **ViT-B/16** | CLIP (Zero-Shot) | - | 66.16 | 23.22 | 93.55 | 66.99 | 86.92 | 65.63 | 65.16 | 66.11 | 45.04 | 82.86 |
| | TPT (NeurIPS'22) | Grad | 67.62 | 24.78 | 94.16 | 68.98 | 87.79 | 65.50 | 68.04 | 66.87 | 47.75 | 84.67 |
| | BoostAdapter (NeurIPS'24) | Training-Free | 69.51 | 27.45 | 94.77 | 71.66 | 89.51 | 68.09 | 71.93 | 69.30 | 45.69 | **87.17** |
| | **MMS-TTA (Ours)** | **Training-Free** | **73.00** | **30.81** | **95.13** | **78.36** | **92.45** | **70.44** | **73.59** | **70.08** | **58.92** | 87.24 |
| **ResNet-50**| BoostAdapter (NeurIPS'24) | Training-Free | 63.44 | 18.93 | 88.48 | 68.25 | 85.75 | 62.83 | 64.42 | 59.67 | 43.85 | **78.78** |
| | **MMS-TTA (Ours)** | **Training-Free** | **65.88** | **21.90** | **89.53** | **71.46** | **87.84** | **64.94** | **66.22** | **60.83** | **52.42** | 77.75 |

### Efficiency vs. Performance
MMS-TTA achieves state-of-the-art accuracy while maintaining a lightweight computational footprint (~10.77 FPS on an NVIDIA RTX 3090, requiring only 1.2 GB VRAM)[cite: 1].

---

## 🛠️ Installation

```bash
# Clone repository
git clone [https://github.com/Alian2014/MMS-TTA.git](https://github.com/Alian2014/MMS-TTA.git)
cd MMS-TTA

# Create conda environment
conda create -n mmstta python=3.9 -y
conda activate mmstta

# Install PyTorch and dependencies
pip install torch torchvision
pip install -r requirements.txt
```

---

## 📦 Data Preparation

Please download the standard TTA benchmark datasets following [TPT](https://github.com/azsh251/TPT) and place them under the `./data` directory:

```text
data/
├── caltech101/
├── dtd/
├── fgvc_aircraft/
├── flowers102/
├── food101/
├── imagenet/
├── oxford_pets/
├── stanford_cars/
├── sun397/
└── ucf101/
```

We also provide the pre-generated LLM descriptions in `./descriptors/`[cite: 1].

---

## 🏃 Quick Start

To run **MMS-TTA** on the Cross-Dataset benchmark using ViT-B/16[cite: 1]:

```bash
# Run on DTD dataset with ViT-B/16
python main.py \
    --config configs/cross_dataset.yaml \
    --dataset dtd \
    --arch ViT-B/16 \
    --data_dir ./data \
    --K_D 17 \
    --tau_gate 0.5
```

To run across all 9 cross-dataset benchmarks[cite: 1]:
```bash
bash scripts/run_cross_dataset.sh
```

To run on Out-of-Distribution (OOD) ImageNet benchmarks[cite: 1]:
```bash
bash scripts/run_ood.sh
```

---

## 🖼️ Visual Comparison

Predictive negative entropy distributions on **OxfordPets**[cite: 1]:

| BoostAdapter (Dispersed) | CuPL (Overconfident) | MMS-TTA (Calibrated & Confident) |
| :---: | :---: | :---: |
| Low confidence ceiling[cite: 1] | Pathological alignment[cite: 1] | **Optimal Multimodal Synergy**[cite: 1] |

---

## 📝 Citation

If you find our work useful in your research, please consider citing:

```bibtex
@inproceedings{jiang2026beyond,
  title={Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation},
  author={Jiang, Guohao and Ma, Zhiheng and Ding, Chenhao and Dong, Songlin and He, Yuhang and Wang, Qiang and Gong, Yihong},
  booktitle={Proceedings of the ACM International Conference on Multimedia (ACM MM)},
  year={2026}
}
```

---

## 🙏 Acknowledgements
This project is built upon [CLIP](https://github.com/openai/CLIP), [TDA](https://github.com/AdilbekKarmanov/TDA), and [BoostAdapter](https://github.com/ZhangTaolin/BoostAdapter)[cite: 1]. We thank the authors for their open-source contributions.
