<h2 align="center"> <a href="https://arxiv.org/abs/2510.22119">CogStereo: Neural Stereo Matching with Implicit Spatial Cognition Embedding</a></h2>

<h5 align="center">

*Accepted by IEEE International Conference on Robotics and Automation （ICRA 2026, CCF B）*

</h5>
<h5 align="center">

[![arXiv](https://img.shields.io/badge/arXiv-2510.22119-b31b1b.svg?logo=arXiv)](https://arxiv.org/abs/2510.22119)
</h5>

**Authors:** [Lihuang Fang](https://scholar.google.com/citations?hl=en&user=pFazUOQAAAAJ)<sup>1,2</sup>, Xiao Hu, [Yuchen Zou](https://scholar.google.com/citations?user=m9AfyE8AAAAJ&hl=en), [Hong Zhang](https://www.sustech.edu.cn/zh/faculties/zhanghong.html)<sup>*1,2</sup>  
**(Corresponding Author: Hong Zhang.)**


---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Installation](#installation)
- [Quick Start](#quick-start)
  - [Data Preparation](#data-preparation)
  - [Train](#train)
  - [Test](#test)
  - [Visualize](#visualize)
- [Evaluation](#evaluation)
- [Acknowledgements](#acknowledgements)
- [Citation](#citation)

## Overview

CogStereo is a neural stereo matching framework that embeds **implicit spatial cognition** into the matching pipeline. It estimates dense disparity/depth from left-right image pairs for robotics, autonomous driving, and 3D reconstruction, improving robustness and generalization across scenes while maintaining accuracy.

## Key Features

- **Implicit Spatial Cognition**: Enhances geometric and occlusion awareness in stereo matching
- **Standard Benchmarks**: Supports SceneFlow, KITTI 2012/2015, Middlebury, ETH3D


## Installation

### 1. Clone and Environment

```bash
git clone https://github.com/lhfang228/CogStereo.git
cd CogStereo

conda create -n cogstereo python=3.10
conda activate cogstereo
```

### 2. Dependencies

```bash
# Install PyTorch (choose according to your CUDA version: https://pytorch.org)
# pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118

pip install -r requirements.txt
```

## Quick Start

### Data Preparation

Place datasets under `data/` or set paths in config. Common benchmarks:

| Dataset | Use | Link |
|---------|-----|------|
| SceneFlow | Training | [SceneFlow](https://lmb.informatik.uni-freiburg.de/resources/datasets/SceneFlowDatasets.en.html) |
| KITTI 2012/2015 | Train / Test | [KITTI](http://www.cvlibs.net/datasets/kitti/eval_stereo.php) |
| Middlebury 2014 | Test | [Middlebury](https://vision.middlebury.edu/stereo/data/) |
| ETH3D | Test | [ETH3D](https://www.eth3d.net/) |

### Train

```bash
# Single GPU
python train.py --config configs/cogstereo_sceneflow.yaml

# Multi-GPU (e.g., 4 GPUs)
torchrun --nproc_per_node=4 train.py --config configs/cogstereo_sceneflow.yaml
```

Logs and checkpoints are saved to `output/` or the path specified in the config.

### Test

```bash
python test.py --checkpoint path/to/checkpoint.pth --data_path data/KITTI --split test
```

### Visualize

```bash
python visualize.py --checkpoint path/to/checkpoint.pth --input left.png right.png --output disp.png
```

## Evaluation

Standard metrics:

- **EPE**: End-Point-Error (mean disparity error)
- **D1**: Percentage of bad pixels (e.g., threshold 3px)

Use the official evaluation scripts from each benchmark (KITTI, Middlebury, etc.) for submission and comparison.

## Acknowledgements

CogStereo builds upon the following works and resources. We thank the authors and the community.

**Stereo matching & backbones:**
- [IGEV](https://github.com/princeton-vl/IGEV) — iterative geometry encoding volume, used as stereo feature backbone
- [RAFT-Stereo](https://github.com/princeton-vl/RAFT-Stereo) — recurrent refinement for stereo matching

**Spatial cognition (monocular depth):**
- [Depth Anything v2 (DAv2)](https://github.com/DepthAnything/Depth-Anything-V2) — provides implicit spatial cognition features used in our refinement module

**Related stereo methods (compared in the paper):**
- [DEFOMStereo](https://github.com/ToughMeow/DeFoMStereo), [FoundationStereo](https://github.com/facebookresearch/foundation-stereo), [NMRF-Stereo](https://github.com/Master-chen/NMRF-Stereo), [Selective-IGEV](https://github.com/XiandaGuo/Selective-IGEV), [CREStereo](https://github.com/megvii-research/CREStereo)

**Datasets:** Scene Flow, KITTI 2012/2015, Middlebury 2014, ETH3D, EuRoC.

## Citation

If you find this work useful, please consider citing:

```bibtex
@inproceedings{fang2026cogstereo,
  title     = {CogStereo: Neural Stereo Matching with Implicit Spatial Cognition Embedding},
  author    = {Fang, Lihuang and Hu, Xiao and Zou, Yuchen and Zhang, Hong},
  booktitle = {IEEE International Conference on Robotics and Automation (ICRA)},
  year      = {2026}
}
```

arXiv: [2510.22119](https://arxiv.org/abs/2510.22119)
