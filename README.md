# HymNet: A Hybrid Multi-Granularity Perception Network for Small Target Detection
**Authors:** Dongjie Zhou, Chang Liu, Jiajun Zhu, Wenrui Li (Member, IEEE), Xiaopeng Fan (Senior Member, IEEE)

[![arXiv](https://img.shields.io/badge/arXiv-2601.00533-b31b1b.svg)](https://arxiv.org/abs/2601.00533)

---

- [2026/02] HymNet training and inference code is released.
- [2026/02] The paper is available on [arXiv](https://arxiv.org/abs/2601.00533).
- [2026/01] The HymDrone dataset is released.

---

## Overview
This repository provides the official implementation of **HymNet** for small target detection. HymNet is a human visual system-inspired framework that emulates retinal resource allocation (via MGFM), contour sharpening (via DMEM), and contextual integration (via GPCM) to achieve robust cross-modal and cross-viewpoint detection.

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div>
    <img src="HVS and HymNet.png" style="height:200px;" alt="Image 1">
  </div>
  <div>
    <img src="The Overall Architecture of HymNet.png" style="height:200px;" alt="Image 2">
  </div>
</div>

**Figure:** Overview of the HymNet.

---

## Environment Setup
```bash
# 1. Clone the repository
git clone https://github.com/tiger413/HymNet.git
cd HymNet

# 2. Create a virtual environment
conda create -n hymnet python=3.9

# 3. Activate the virtual environment
conda activate hymnet

# 4. Install dependencies
pip install -r requirements.txt

# 5. Install the project in editable/development mode
pip install -e .
```

---

## HymDrone Quadrotor UAV Dataset

### Introduction

HymDrone consists of 59,138 images across 55 sequences, covering 9 distinct scene types, 5 diverse weather conditions, and illumination variations ranging from dawn to dusk. All images are captured in high-definition resolution of 1920×1080 pixels, with precise bounding box annotations provided for each UAV target in every image.

Download the `experiment` folder from Google Drive and place it in the repository root directory:

- Google Drive: https://drive.google.com/drive/folders/1b6IpTLh-SJOuDo8oYSREKRpLY5zhxpiq?usp=sharing

After downloading, your directory should look like:

```
ORCANet-SEUD/
  experiment/pretrained_models
  basicsr/
  options/
  scripts/
  ...
```

### 2) Prepare your own dataset (optional)

The synthesis code and the SEUD dataset in paper are under preparation and will be released in a later update. If you use your own training data, generate the meta information file:

```
python scripts/data_preparation/generate_meta_info.py --dataset_path "The root of training sets"
```

The generated file is saved to:

```
basicsr/data/meta_info/<your_dataset>_meta_info.txt
```

---

## SEUD Synthesis Code and Dataset

The synthesis code and the SEUD dataset are under preparation and will be released in a later update.

<p align="center">
  <img src="assets/synthsis_crop.jpg" width="100%">
</p>


**Figure:** Overview of the SEUD weather synthesis pipeline.

---

## Training

Before training, please check the YAML file:

- `dataroot_gt`
- `dataroot_lq`
- `meta_info_file`

Example (single GPU):

```
python basicsr/train.py -opt options/train/train_ORCANet_MOT17t4.yml
```

Multi-GPU training:

```
CUDA_VISIBLE_DEVICES=0,1 LD_LIBRARY_PATH="" torchrun --nproc_per_node=2 --master_port=4321 \
  basicsr/train.py -opt options/train/train_ORCANet_MOT17t4.yml --launcher pytorch
```

------

## Inference (Testing)

Before testing, please check the YAML file:

- `dataroot_gt`
- `dataroot_lq`
- `meta_info_file`

You can enable/disable saving outputs via `save_img` in the test YAML.

Run inference:

```
python basicsr/test.py -opt options/test/test_ORCANet_MOT17t4.yml
```

------

## Acknowledgements

This project builds upon and is inspired by the following open-source projects and resources:

- BasicSR: https://github.com/XPixelGroup/BasicSR
- AverNet: https://github.com/XLearning-SCU/2024-NeurIPS-AverNet/tree/main
- Depth Anything: https://github.com/LiheYoung/Depth-Anything
- IntoTheFog: https://github.com/nadezola/IntoTheFog_MOT17/tree/master

We thank the authors for their excellent work.

------

## Contact

If you have any questions, please contact ht166chen@163.com
