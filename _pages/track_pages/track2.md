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
  - name: Leaderboards
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
{% include figure.liquid loading="eager" path="/assets/img/myops.png" class="img-fluid" max-width="70%" zoomable=true caption="Figure 1. Myocardial pathology segmentation and its challenges. (A) Myocardial Pathology Segmentation: Scar and edema regions are marked in green and yellow, respectively. (B) Challenges of Myocardial Pathology Segmentation: The challenges include multi-center data, missing sequences, and misalignments in multi-sequence CMR images." %}

Myocardial infarction (MI) is a major cause of mortality and disability worldwide. Assessment of myocardial viability is essential in the diagnosis and treatment management of MI patients <d-cite key="myops1"></d-cite>. Multi-sequence cardiac magnetic resonance (MS-CMR) images can provide valuable myocardial pathology information, which is important for the diagnosis and treatment management of patients. As shown in Figure 1 (A), balanced steady-state free precession (bSSFP) cine sequences present clear anatomical boundaries, while late gadolinium enhancement (LGE) and T2-weighted (T2) CMR sequences visualize myocardial scar and edema of MI, respectively.

## Tasks

The target of this track is to segment myocardial pathology regions, specifically scar and edema, from multi-sequence CMR data. This track seeks innovative solutions to address MyoPS using real-world multi-sequence CMR data. We encourage participants to overcome challenges such as the inclusion of multi-center data, missing sequences for some centers <d-cite key="myops2"></d-cite>, and misalignments in multi-sequence CMRs <d-cite key="myops3"></d-cite>, as illustrated in Figure 1 (B).

The specific  substructures, each associated with a unique label value, are:
1. **Scar** - Label value: 2221
2. **Edema** - Label value: 1220
3. **Left ventricle** - Label value: 500
4. **Myocardium** - Label value: 200
5. **Right ventricle** - Label value: 600


We will rank participant methods based on the settings (​Lb1–Lb4) detailed in the following table:

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;"> Leaderboard (Lb) for MyoPS track across targets and evaluation settings.​​ Lb1–Lb4 represent performance from different test centers and targets (e.g., Lb1 = scar segmentation peformance on center B). In-distribution refers to centers included in the training data, while out-of-distribution refers to unseen centers not used during training.</caption>
  <thead>
    <tr>
      <th style="text-align:center;">Target</th>
      <th style="text-align:center;">In-distribution</th>
      <th style="text-align:center;">Out-of-distribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Scar</td>
      <td>Lb1</td>
      <td>Lb2</td>
    </tr>
    <tr>
      <td>Edema</td>
      <td>Lb3</td>
      <td>Lb4</td>
    </tr>
  </tbody>
</table>
</div>





## Data

### Training data

<div style="display: flex; ">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
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

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
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

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
      <th style="text-align:center;">Sequences</th>
      <th style="text-align:center;">Manual labels</th>
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
      <td>15</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
  </tbody>
</table>
</div>



## Metrics 


The performance of scar and edema segmentation results will be evaluated by：
- **Dice Similarity Coefficient (Dice)**
- **Precision (Pre)**
- **Sensitivity (Sen)**
- **Hausdorff Distance (HD in mm)**

## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are  allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP, and MedSAM.

## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=myops).


## Leaderboard

#### MyoPS Scar (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="scar table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Scar_Dice↑</strong></th>
      <th style="text-align:center;"><strong>Scar_Sen↑</strong></th>
      <th style="text-align:center;"><strong>Scar_Pre↑</strong></th>
      <th style="text-align:center;"><strong>Scar_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>JMT</td><td>0.4864</td><td>0.6580</td><td>0.4117</td><td>31.9086</td></tr>
    <tr><td>ZXN</td><td>0.4329</td><td>0.5863</td><td>0.3833</td><td>37.4517</td></tr>
    <tr><td>FireMan</td><td>0.4694</td><td>0.6572</td><td>0.3935</td><td>30.2447</td></tr>
    <tr><td>king</td><td>0.4245</td><td>0.5416</td><td>0.3744</td><td>46.7791</td></tr>
    <tr><td>marisabe</td><td>0.4841</td><td>0.6177</td><td>0.4221</td><td>29.2022</td></tr>
    <tr><td>fpt</td><td>0.4933</td><td>0.6075</td><td>0.4390</td><td>28.7960</td></tr>
    <tr><td>David</td><td>0.4248</td><td>0.5469</td><td>0.3772</td><td>46.8064</td></tr>
    <tr><td>Space</td><td>0.4642</td><td>0.6750</td><td>0.3875</td><td>35.8338</td></tr>
  </tbody>
</table>
</div>

#### MyoPS Scar (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="scar table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Scar_Dice↑</strong></th>
      <th style="text-align:center;"><strong>Scar_Sen↑</strong></th>
      <th style="text-align:center;"><strong>Scar_Pre↑</strong></th>
      <th style="text-align:center;"><strong>Scar_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>JMT</td><td>0.6780</td><td>0.6126</td><td>0.7747</td><td>15.6920</td></tr>
    <tr><td>ZXN</td><td>0.6667</td><td>0.6140</td><td>0.7549</td><td>16.1454</td></tr>
    <tr><td>FireMan</td><td>0.6826</td><td>0.6394</td><td>0.7436</td><td>20.8305</td></tr>
    <tr><td>king</td><td>0.7387</td><td>0.6888</td><td>0.8160</td><td>13.5691</td></tr>
    <tr><td>marisabe</td><td>0.6573</td><td>0.5812</td><td>0.7775</td><td>17.2670</td></tr>
    <tr><td>fpt</td><td>0.6459</td><td>0.5769</td><td>0.7550</td><td>24.1498</td></tr>
    <tr><td>David</td><td>0.6654</td><td>0.6168</td><td>0.7747</td><td>16.4942</td></tr>
    <tr><td>Space</td><td>0.5616</td><td>0.5991</td><td>0.5833</td><td>18.9891</td></tr>
  </tbody>
</table>
</div>


#### MyoPS Edema (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="edema table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Edema_Dice↑</strong></th>
      <th style="text-align:center;"><strong>Edema_Sen↑</strong></th>
      <th style="text-align:center;"><strong>Edema_Pre↑</strong></th>
      <th style="text-align:center;"><strong>Edema_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>JMT</td><td>0.6061</td><td>0.6775</td><td>0.5873</td><td>32.1836</td></tr>
    <tr><td>ZXN</td><td>0.6499</td><td>0.6430</td><td>0.6992</td><td>31.8488</td></tr>
    <tr><td>FireMan</td><td>0.5935</td><td>0.7099</td><td>0.5361</td><td>31.1575</td></tr>
    <tr><td>king</td><td>0.5187</td><td>0.6030</td><td>0.4826</td><td>46.2529</td></tr>
    <tr><td>marisabe</td><td>0.5633</td><td>0.6430</td><td>0.5390</td><td>32.0530</td></tr>
    <tr><td>fpt</td><td>0.6180</td><td>0.6247</td><td>0.6597</td><td>32.7830</td></tr>
    <tr><td>David</td><td>0.5753</td><td>0.6227</td><td>0.5757</td><td>39.8774</td></tr>
    <tr><td>Space</td><td>0.5953</td><td>0.6128</td><td>0.6310</td><td>33.8135</td></tr>
  </tbody>
</table>
</div>

#### MyoPS Edema (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="edema table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Edema_Dice↑</strong></th>
      <th style="text-align:center;"><strong>Edema_Sen↑</strong></th>
      <th style="text-align:center;"><strong>Edema_Pre↑</strong></th>
      <th style="text-align:center;"><strong>Edema_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>JMT</td><td>0.6655</td><td>0.5980</td><td>0.8039</td><td>21.8737</td></tr>
    <tr><td>ZXN</td><td>0.6857</td><td>0.6339</td><td>0.7866</td><td>19.3169</td></tr>
    <tr><td>FireMan</td><td>0.6819</td><td>0.6840</td><td>0.7211</td><td>22.2706</td></tr>
    <tr><td>king</td><td>0.7585</td><td>0.7677</td><td>0.7715</td><td>14.7051</td></tr>
    <tr><td>marisabe</td><td>0.6554</td><td>0.6371</td><td>0.7158</td><td>22.7204</td></tr>
    <tr><td>fpt</td><td>0.6404</td><td>0.5548</td><td>0.7932</td><td>27.0451</td></tr>
    <tr><td>David</td><td>0.6878</td><td>0.6208</td><td>0.8070</td><td>19.7881</td></tr>
    <tr><td>Space</td><td>0.6392</td><td>0.5741</td><td>0.7551</td><td>22.4153</td></tr>
  </tbody>
</table>
</div>


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


<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
