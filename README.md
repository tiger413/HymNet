# HymNet: A Hybrid Multi-Granularity Perception Network for Small Target Detection
**Authors:** Dongjie Zhou, Chang Liu, Jiajun Zhu, Wenrui Li (Member, IEEE), Xiaopeng Fan (Senior Member, IEEE)

[![arXiv](https://img.shields.io/badge/arXiv-2601.00533-b31b1b.svg)](https://arxiv.org/abs/2601.00533)

---

- [2026/02] HymNet training and inference code is released.
- [2026/02] The paper is available on [arXiv](https://arxiv.org/abs/2601.00533).
- [2026/01] The HymDrone dataset is released.

---

## Overview
This repository provides the official implementation of **HymNet** for small target detection. HymNet is a human visual system (HVS) inspired framework that emulates retinal resource allocation (via MGFM), contour sharpening (via DMEM), and contextual integration (via GPCM) to achieve robust cross-modal and cross-viewpoint detection.

<p align="center">
  <img src="assets/HymNet.png" height="470">
  &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;
  <img src="assets/HVS_HymNet.png" height="380">
</p>   

**Figure**: Overview of HymNet and its dual-stream functional mapping with the human visual system (HVS).

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

**HymDrone** consists of 59,138 images across 55 sequences, covering 9 distinct scene types (park, nighttime, hilly areas with trees, terrain with trees, beach, jungle, mountains, highways, and sunset), 5 diverse weather conditions (sunny (a), fog (b), haze (c), falling leaves (d), and heavy snow/rain (e)), and illumination variations ranging from dawn to dusk. All images are captured in high-definition resolution of 1920×1080 pixels, with precise bounding box annotations provided for each UAV target in every image.

<p align="center">
  <img src="assets/scenes.png" width="300">
  &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;
  <img src="assets/weather.png" width="300">
</p>  

**Figure**: Nine different scene types and five different weather conditions of HymDrone.

Regarding target scale, statistical analysis reveals that over 52\% of UAV targets occupy less than 0.5\% of the image area, and most bounding boxes are small in both width and height.

<p align="center">
  <img src="assets/histogram.png" width="300">
  &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;
  <img src="assets/scatter.png" width="300">
</p>  

**Figure**: Histogram of bounding box area ratios relative to image area in HymDrone. catter plot of bounding box width versus height, with
color indicating area ratio relative to the image.

### Download
Download HymDrone dataset from Baidu Drive and place it in the repository root directory:

- Baidu Drive: https://drive.google.com/drive/folders/1b6IpTLh-SJOuDo8oYSREKRpLY5zhxpiq?usp=sharing

After downloading, your directory should look like:

```
HymNet/
  Datasets/HymDrone
  basicsr/
  options/
  scripts/
  ...
```
## Training

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
