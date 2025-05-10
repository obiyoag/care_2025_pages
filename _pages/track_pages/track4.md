---
layout: distill
title: CARE-Liver
description: Liver Fibrosis Quantification and Analysis
permalink: /track4/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Tasks
  - name: Data
  - name: Leaderboard
  - name: Rules
  - name: Registration
  - name: Citations
_styles: >
  d-article {
    contain: layout style;
    overflow-x: hidden;
    border-top: 1px solid rgba(0, 0, 0, 0.1);
    padding-top: 2rem;
    color: rgba(0, 0, 0, 0.8);
  }

  d-article > * {
    grid-column: text;
  }
---

## Motivation
{% include figure.liquid loading="eager" path="/assets/img/liqa1.png" class="img-fluid" zoomable=true caption="Figure 1. Track description." %}

Liver fibrosis, arising from chronic viral or metabolic liver conditions, presents a significant global health challenge. Precise liver segmentation (LiSeg) and fibrosis staging (LiFS) are critical for enabling precise disease management, prognostication, and informed clinical decision-making. This challenge focuses on advancing **two interconnected objectives** to bridge clinical needs with AI innovation:  
1. **Automated Liver Segmentation**.  
2. **Multi-Phase Fibrosis Staging**.

Participants will develop robust AI solutions using multi-center, multi-phase MRI data, addressing real-world variability in imaging protocols and scanner systems.  

## Tasks
### **Task 1: Liver Fibrosis Staging (LiFS)**  
Develop models to stage fibrosis into four stages (S1-S4). leveraging **cross-phase complementary information** from dynamic MRI sequences. Two clinically critical binary subtasks are evaluated:  
1. **Cirrhosis Detection**: S1–S3 vs. S4  
2. **Substantial Fibrosis Detection**: S1 vs. S2–S4  

#### Subtasks:  
- **Non-Contrast Subtask**: T1WI, T2WI, and DWI sequences only.  
- **Contrast-Enhanced Subtask**: All modalities allowed, including Gd-EOB-DTPA phases (GED1–GED4).  

### **Task 2: Liver Segmentation (LiSeg)**  
Segment the liver in multi-phase fibrosis, where **limited ground truth of Hepatobiliary phase (GED4) MRI** is available. Non-constrast data (T2WI, DWI) could be segmented via **unsupervised or registration-based approaches** to overcome annotation limitations.  

#### Subtasks:
- **Non-Contrast Subtask**: Segment liver anatomy in **T2WI** and **DWI** sequences. No annotations provided.
- **Contrast-Enhanced Subtask**: Segment **GED4** sequence. Limited annotations provided.

---

## Data

### Training set

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:90%;align:center;">
  <thead>
    <tr>
      <th class="text-center" scope="col">Vendor</th>
      <th class="text-center" scope="col">Center</th>
      <th class="text-center" scope="col">#Cases</th>
      <th class="text-center" scope="col">#Annotation for seg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">130</td>
      <td class="text-center">10</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">170</td>
      <td class="text-center">10</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">60</td>
      <td class="text-center">10</td>
    </tr>
  </tbody>
</table>
</div>


### Validation Set

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:90%;align:center;">
  <thead>
    <tr>
      <th class="text-center" scope="col">Vendor</th>
      <th class="text-center" scope="col">Center</th>
      <th class="text-center" scope="col">#Cases</th>
      <th class="text-center" scope="col">#Annotation for seg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">20</td>
      <td class="text-center">20</td>
    </tr>
  </tbody>
</table>
</div>

### Test Set

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:50%;align:center;">
  <thead>
    <tr>
      <th class="text-center" scope="col">Vendor</th>
      <th class="text-center" scope="col">Center</th>
      <th class="text-center" scope="col">#Cases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="text-center">A</td>
      <td class="text-center">A</td>
      <td class="text-center">40</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B1</td>
      <td class="text-center">40</td>
    </tr>
    <tr>
      <td class="text-center">B</td>
      <td class="text-center">B2</td>
      <td class="text-center">40</td>
    </tr>
    <tr>
      <td class="text-center">C</td>
      <td class="text-center">C</td>
      <td class="text-center">70</td>
    </tr>
  </tbody>
</table>
</div>

- **NOTE: The evaluation on the unseen dataset (C) highlights the generalization capabilities of the models and algorithms, which we particularly emphasize.**

## Leaderboard

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th>Task</th>
      <th>Subtask</th>
      <th>Key Metrics</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2"><strong>LiFS</strong></td>
      <td>Non-Contrast</td>
      <td>AUC, ACC (S4 vs. S1–S3; S1 vs. S2–S4)</td>
    </tr>
    <tr>
      <td>Contrast-Enhanced</td>
      <td>AUC, ACC (S4 vs. S1–S3; S1 vs. S2–S4)</td>
    </tr>
    <tr>
      <td rowspan="2"><strong>LiSeg</strong></td>
      <td>Non-Contrast (T2WI/DWI)</td>
      <td>Dice Score, HD-95</td>
    </tr>
    <tr>
      <td>Contrast-Enhanced (GED4)</td>
      <td>Dice Score, HD-95</td>
    </tr>
  </tbody>
</table>
</div>

- **NOTE: Participants are welcome to participate in a single subtask, and their performance will still be recorded and displayed on the leaderboard.**


## Rules
1. Publicly available data (such as [LLD-MMRI2023](https://github.com/LMMMEng/LLD-MMRI2023)) and pre-trained models are allowed. 
2. Only automatic methods are acceptable. 

## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=care_liver).

## Citations
**Please cite these papers when you use the data for publications:**
```bib
@article{liu2025merit,
  title = {MERIT: Multi-view evidential learning for reliable and interpretable liver fibrosis staging},
  author={Liu, Yuanye and Gao, Zheyao and Shi, Nannan and Wu, Fuping and Shi, Yuxin and Chen, Qingchao and Zhuang, Xiahai},
  journal = {Medical Image Analysis},
  volume = {102},
  pages = {103507},
  year = {2025}
}

@inproceedings{gao2023reliable,
  title={A reliable and interpretable framework of multi-view learning for liver fibrosis staging},
  author={Gao, Zheyao and Liu, Yuanye and Wu, Fuping and Shi, Nannan and Shi, Yuxin and Zhuang, Xiahai},
  booktitle={International Conference on Medical Image Computing and Computer-Assisted Intervention},
  pages={178--188},
  year={2023}
}
```
