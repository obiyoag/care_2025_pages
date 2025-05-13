---
layout: distill
title: CARE-MyoPS
description: Myocardial Pathology Segmentation
permalink: /track2/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Tasks
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
{% include figure.liquid loading="eager" path="/assets/img/myops.png" class="img-fluid" zoomable=true caption="Figure 1. Myocardial pathology segmentation and its challenges. (A) Myocardial Pathology Segmentation: Scar and edema regions are marked in green and yellow, respectively. (B) Challenges of Myocardial Pathology Segmentation: The challenges include multi-center data, missing sequences, and misalignments in multi-sequence CMR images." %}

Myocardial infarction (MI) is a major cause of mortality and disability worldwide. Assessment of myocardial viability is essential in the diagnosis and treatment management of MI patients <d-cite key="myops1"></d-cite>. Multi-sequence cardiac magnetic resonance (MS-CMR) images can provide valuable myocardial pathology information, which is important for the diagnosis and treatment management of patients. As shown in Figure 1 (A), balanced steady-state free precession (bSSFP) cine sequences present clear anatomical boundaries, while late gadolinium enhancement (LGE) and T2-weighted (T2) CMR sequences visualize myocardial scar and edema of MI, respectively.

## Tasks

The target of this track is to segment myocardial pathology regions, specifically scar and edema, from multi-sequence CMR data. This track seeks innovative solutions to address MyoPS using real-world multi-sequence CMR data. We encourage participants to overcome challenges such as the inclusion of multi-center data, missing sequences for some centers <d-cite key="myops2"></d-cite>, and misalignments in multi-sequence CMRs <d-cite key="myops3"></d-cite>, as illustrated in Figure 1 (B).

The specific  substructures, each associated with a unique label value, are:
1. **Scar** - Label value: 2221
2. **Edema** - Label value: 1220
3. **Left ventricle** - Label value: 500
4. **Myocardium** - Label value: 200
5. **Right ventricle** - Label value: 600


We will rank participant methods based on the settings (​Lb1–Lb9) detailed in the following table:

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;"> Leaderboard (Lb) for MyoPS track across targets and evaluation settings.​​ Lb1–Lb9 represent performance from different test centers (e.g., Lb1 = peformance on center B; Lb5 = performance on center D). In-distribution refers to centers included in the training data, while out-of-distribution refers to unseen centers not used during training.</caption>
  <thead>
    <tr>
      <th scope="col">Target</th>
      <th scope="col">In-distribution</th>
      <th scope="col">Out-of-distribution</th>
      <th scope="col">Average (Real-world)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Scar</td>
      <td>Lb1</td>
      <td>Lb2</td>
      <td>Lb3</td>
    </tr>
    <tr>
      <td>Edema</td>
      <td>Lb4</td>
      <td>Lb5</td>
      <td>Lb6</td>
    </tr>
        <tr>
      <td>Scar+Edema</td>
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
      <th scope="col">Sequences</th>
      <th scope="col">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>81</td>
      <td>LGE</td>
      <td>Scar, left ventricle and  myocardium</td>
    </tr>
    <tr>
      <td>B</td>
      <td>50</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
    <tr>
      <td>C</td>
      <td>45</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
    <tr>
      <td>E</td>
      <td>7</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium  and right ventricle</td>
    </tr>
    <tr>
      <td>F</td>
      <td>9</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium and and right ventricle</td>
    </tr>
    <tr>
      <td>G</td>
      <td>8</td>
      <td>LGE and bSSFP</td>
      <td>Scar, left ventricle,  myocardium and and right ventricle</td>
    </tr>
        <tr>
      <td>H</td>
      <td>35</td>
      <td>LGE </td>
      <td>Scar</td>
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
      <th scope="col">Sequences</th>
      <th scope="col">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>D</td>
      <td>25</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium</td>
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
      <th scope="col">Sequences</th>
      <th scope="col">Manual labels</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>D</td>
      <td>25</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
    <tr>
      <td>B</td>
      <td>16</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
  </tbody>
</table>
</div>



## Metrics 


The performance of scar and edema segmentation results will be evaluated by：
- **Dice Similarity Coefficient (DSC)**
- **Precision (PRE)**
- **Sensitivity (SEN)**
- **Hausdorff Distance (HD)**

## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are  allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP, and MedSAM.

## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=care_myops).

## Citations
**Please cite these papers when you use the data for publications:**
```bib
 @article{zhuang2019multivariate,
    title={Multivariate mixture model for myocardial segmentation combining multi-source images},
    author={Zhuang, Xiahai},
    journal={IEEE transactions on pattern analysis and machine intelligence},
    volume={41},
    number={12},
    pages={2933--2946},
    year={2019},
}


@article{qiu2023myops,
  title={MyoPS-Net: Myocardial pathology segmentation with flexible combination of multi-sequence CMR images},
  author={Qiu, Junyi and Li, Lei and Wang, Sihan and Zhang, Ke and Chen, Yinyin and Yang, Shan and Zhuang, Xiahai},
  journal={Medical image analysis},
  volume={84},
  pages={102694},
  year={2023},
}

 @article{ding2023aligning,
  title={Aligning multi-sequence CMR towards fully automated myocardial pathology segmentation},
  author={Ding, Wangbin and Li, Lei and Qiu, Junyi and Wang, Sihan and Huang, Liqin and Chen, Yinyin and Yang, Shan and Zhuang, Xiahai},
  journal={IEEE Transactions on Medical Imaging},
  year={2023},
}
```
