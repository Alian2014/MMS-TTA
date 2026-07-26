# Beyond Unimodal Reliance: Multimodal Synergy for Training-Free Test-Time Adaptation

### [[Paper](https://arxiv.org/abs/XXXXXXX)] 




Guohao Jiang, Chenhao Ding, SongLin Dong, Zhiheng Ma, Qiang Wang, Yuhang He, and Yihong Gong

> **Abstract:**  Test-Time Adaptation (TTA), particularly the training-free paradigm, has garnered widespread attention due to its significant advantages in addressing test-time distribution shifts in Vision-Language Models. However, existing training-free approaches are often constrained by the inherent limitations caused by an over-reliance on a single textual or visual modality, resulting in suboptimal performance and robustness. To address this issue, we propose a novel \textbf{training-free dynamic multimodal synergy strategy}. First, to extract textual modality features with enhanced robustness, we construct a cache-based, hierarchical retrieval-augmented TTA paradigm. Building upon this, we introduce a negative-entropy-driven dynamic synergy mechanism that adaptively fuses the optimized textual modality, the visual modality, and the original CLIP modality. This integration ultimately yields a predictive distribution characterized by both high robustness and high confidence. Our approach significantly enhances class discriminability while maintaining exceptional robustness during testing. Extensive experiments across multiple benchmarks demonstrate that the proposed method consistently outperforms state-of-the-art approaches in both performance and efficiency.

<p align="center">
    <img src="assets/framework.png" style="border-radius: 15px">
</p>

## <a name="installation"></a> Installation

This codebase was tested with the following environment configurations. It may work with other versions.

- Python 3.9
- CUDA 11.8
- PyTorch 2.2.0 + cu118

## Datasets
Please follow [Datasets](docs/DATASETS.md) to download the OOD and Cross-Domain benchmarks. 


## <a name="training"></a>  Running

Run the following script to run MMS-TTA:
```
Coming soon
```

For example, you can run the a demo with the following command:  
```
Coming soon
```


## <a name="cite"></a> Citation

Please cite us if our work is useful for your research.

```
Coming soon
```

## License

This project is released under the [MIT license](LICENSE).

## Acknowledgement

This code is based on [RATTA](https://github.com/kaist-dmlab/RA-TTA) and [BoostAdapter](https://github.com/taolinzhang/BoostAdapter). Thanks for their awesome work.
