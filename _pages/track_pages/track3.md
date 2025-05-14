---
layout: distill
title: CARE-WHS
description: Whole Heart Segmentation
permalink: /track3/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Task
  - name: Data
  - name: Metrics
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

Cardiovascular diseases (CVDs), as the leading cause of death globally<d-cite key="whs1"></d-cite>, necessitate precise morphological and pathological quantification through segmentation of crucial cardiac structures from medical images<d-cite key="whs2"></d-cite>. However, whole heart segmentation (WHS) faces challenges including heart shape variability during the cardiac cycle, clinical artifacts like motion and poor contrast-to-noise ratio, as well as domain shifts in multi-center data and the distinct modalities of CT and MRI. The WHS track serves to inspire innovative solutions in the realms of biomedical imaging and computer vision, striving to overcome these challenges and advance automated WHS for enhanced understanding and treatment of CVDs.


## Task
{% include figure.liquid loading="eager" path="/assets/img/whs.png" class="img-fluid" zoomable=true caption="Figure 1. Overview of the WHS track" %}


The objective of this track is to achieve precise segmentation of seven substructures of the whole heart, with robustness against domain shifts (see Fig. 1).  
The specific  substructures, each associated with a unique label value, are:

1. **Left Ventricular Blood Cavity (LV)** - Label value: 500
2. **Right Ventricular Blood Cavity (RV)** - Label value: 600
3. **Left Atrial Blood Cavity (LA)** - Label value: 420
4. **Right Atrial Blood Cavity (RA)** - Label value: 550
5. **Myocardium of the Left Ventricle (Myo)** - Label value: 205
6. **Ascending Aorta (AO)** - Label value: 820; defined as the aortic trunk from the aortic valve to the superior level of the atria.
7. **Pulmonary Artery (PA)** - Label value: 850; defined as the initial segment from the pulmonary valve to the bifurcation point.



**Note on Great Vessels:** The great vessels of interest, comprising the ascending aorta and pulmonary artery, are specifically defined due to variations in the fields of view across different scans. This uniform definition is crucial for ensuring consistency across evaluations. During the assessment, segmentation results for these vessels will be truncated to average lengths measured in healthy subjects, although participants are encouraged to extend their segmentation beyond these lengths. Our provided manual segmentations similarly cover more than the defined trunk measurements.

We will rank participant methods based on the settings (​Lb1–Lb9) detailed in the following table:

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;width: 100%;"> Leaderboard (Lb) for WHS track across modalities and evaluation settings.​​ Lb1–Lb9 represent performance from different test centers (e.g., Lb1 = peformance on center A and B (CT) scans; Lb5 = performance on center F (MRI) scans). In-distribution refers to centers included in the training data, while out-of-distribution refers to unseen centers not used during training.</caption>
  <thead>
    <tr>
      <th scope="col">Modality</th>
      <th scope="col">In-distribution</th>
      <th scope="col">Out-of-distribution</th>
      <th scope="col">Average (Real-world)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CT</td>
      <td>Lb1</td>
      <td>Lb2</td>
      <td>Lb3</td>
    </tr>
    <tr>
      <td>MR</td>
      <td>Lb4</td>
      <td>Lb5</td>
      <td>Lb6</td>
    </tr>
        <tr>
      <td>MR+CT</td>
      <td>Lb7</td>
      <td>Lb8</td>
      <td>Lb9</td>
    </tr>
  </tbody>
</table>
</div>

## Data

### Training data

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. patients</th>
      <th scope="col">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>E</td>
      <td>26</td>
      <td>MRI</td>
    </tr>
  </tbody>
</table>
</div>

### Validation data

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. patients</th>
      <th scope="col">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>10</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MR</td>
    </tr>
  </tbody>
</table>
</div>

### Test data

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. patients</th>
      <th scope="col">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>20</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>14</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C & D</td>
      <td>20</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>F</td>
      <td>16</td>
      <td>MRI</td>
    </tr>
    <tr>
      <td>G</td>
      <td>20</td>
      <td>CT</td>
    </tr>
  </tbody>
</table>
</div>


## Metrics
The performance of segmentation results will be assessed through: 
- Dice Similarity Coefficient (DSC), 
- Hausdorff Distance (HD), 
- Average Surface Distance (ASD). 


## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP and MedSAM.


## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=care_whs).

## Citations
**Please cite these papers when you use the data for publications:**

```
@article{Zhuang2016MSMMA,
  Author = {Zhuang, Xiahai and Shen, Juan},
  Title = {Multi-scale patch and multi-modality atlases for whole heart
     segmentation of MRI},
  Journal = {Medical Image Analysis},
  Year = {2016},
  Volume = {31},
  Pages = {77-87},
}

@article{Zhuang2019MvMM,
  Author = {Zhuang, Xiahai},
  Title = {Multivariate Mixture Model for Myocardial Segmentation Combining
     Multi-Source Images},
  Journal = {IEEE Transactions on Pattern Analysis and Machine Intelligence},
  Year = {2019},
  Volume = {41},
  Number = {12},
  Pages = {2933-2946},
}

@article{GAO2023BayeSeg,
  Author = {Gao, Shangqi and Zhou, Hangqi and Gao, Yibo and Zhuang, Xiahai},
  Title = {BayeSeg: Bayesian modeling for medical image segmentation with
     interpretable generalizability},
  Journal = {Medical Image Analysis},
  Year = {2023},
  Volume = {89},
  Pages = {102889},
}
```
