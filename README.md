# Performance Collapse Threshold of ResNet-18 under Label Noise on CIFAR-10

DSAI5207 Final Project  
Team: Yang Yuxin, Song Zhaohui, Zhang Siyao, Chen Xinyi  
The Hong Kong Polytechnic University

## Overview

This repository contains the code, experimental data, and figures for our empirical study of the performance collapse threshold of ResNet-18 under symmetric and asymmetric label noise on CIFAR-10. We sweep noise rates from 0% to 50% in 10% increments across two random seeds, covering 24 experimental conditions in total.


## Repository Structure

- `main.ipynb` — Complete end-to-end experiment notebook reproducing all results.
- `results/` — Saved experimental data (`all_results.json`) and five figures used in the report.
- `requirements.txt` — Python dependencies required to run the project.

## Setup

### Environment

This project was developed and tested on:
- Python 3.11
- PyTorch 2.10 with CUDA 12.8
- NVIDIA A100-SXM4-40GB GPU
### Install Dependencies

```bash
pip install -r requirements.txt
```

## Dataset

CIFAR-10 is downloaded automatically by `torchvision.datasets.CIFAR10` on first run. No manual preparation is required. The standard split of 50,000 training images and 10,000 test images is used. Label noise is injected only into the training set.

## Reproducing Results

### Option 1: Run the full notebook

Open `main.ipynb` in Jupyter or Google Colab and run all cells in order. Total runtime on a single A100 GPU is approximately 4 hours for all 24 conditions.



## Experimental Configuration

- Model: ResNet-18 (random initialization)
- Optimizer: SGD, momentum 0.9, weight decay 5e-4
- Learning rate: 0.1 with cosine annealing over 60 epochs
- Batch size: 256
- Mixed precision: FP16 via PyTorch AMP
- Noise rates: {0.0, 0.1, 0.2, 0.3, 0.4, 0.5}
- Seeds: {42, 123}

## Results Summary

No performance collapse is observed under either noise type within the tested range. Symmetric noise proves consistently more damaging than asymmetric noise at equivalent nominal rates, due to the lower effective flip rate inherent in the asymmetric transition structure. See the final report for detailed analysis.

## References

Key references are listed in the report. The noise injection protocol follows Patrini et al. (2017); the backbone architecture is ResNet-18 (He et al., 2016); the dataset is CIFAR-10 (Krizhevsky, 2009).