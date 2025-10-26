---
layout: distill
title: CARE-Cardiac
description: Unified Cardiac Image Segmentation
permalink: /track1/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Task
  - name: Data
  - name: Metrics
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

{% include figure.liquid loading="eager" path="/assets/img/care-cardiac.png" class="img-fluid" zoomable=true max-width="70%" %}

Cardiac diagnosis involves multiple interrelated tasks, such as delineating anatomical structures (e.g., atria, ventricles, vessels) and identifying pathological regions (e.g., scar) across diverse imaging modalities and acquisition protocols. Relying on separate models for each task leads to fragmented workflows, limited knowledge transfer, and poor adaptability to missing or heterogeneous data. A **unified cardiac segmentation model** addresses these limitations by enabling unified modeling across tasks. 

## Task

Develop a **unified model** capable of segmenting **single cardiac structure** (left atria), **whole heart structures** and **structure and pathology** (left ventricle, myocardium and scar).

***Note\***: Participants are also encouraged to leverage external data.


## Data

Multi-center and multi-modality datasets are provided for three sub-tasks. Please register [here](http://zmic.org.cn/care_2025/eval/register?track=cardiac) to access the data. 

### Training Dataset

1). Left Atrial Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>130</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>

2). Whole Heart Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modalities</th>
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



3). Myocardial Pathology Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>81</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>B</td>
      <td>50</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>C</td>
      <td>45</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>E</td>
      <td>7</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>F</td>
      <td>9</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>G</td>
      <td>8</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>


### Validation Dataset

 1).  Left Atrial Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Sequences</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
      <td>10</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>C</td>
      <td>10</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>



 2). Whole Heart Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modalities</th>
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
      <td>MRI</td>
    </tr>
  </tbody>
</table>
</div>


 3). Myocardial Pathology Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>D</td>
      <td>25</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>




### Test Dataset

1). Left Atrial Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modality</th>
    </tr>
  </thead>
  <tbody>
     <tr>
      <td>A</td>
      <td>14</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>B</td>
      <td>20</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>C</td>
      <td>10</td>
      <td>LGE MRI</td>
    </tr> 
  </tbody>
</table>
</div>
2). Whole Heart Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modalities</th>
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


3). Myocardial Pathology Segmentation

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. cases</th>
      <th style="text-align:center;">Modality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>D</td>
      <td>25</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>B</td>
      <td>16</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>


## Metrics

- **Dice Similarity Coefficient (Dice)**
- **Hausdorff Distance (HD in mm)**

Both in-distribution (i.e., seen centers) and out-of-distribution (OOD) (i.e., unseen centers) results of the three tasks will be reported in the leaderboard.

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Task</th>
      <th style="text-align:center;">In-distribution</th>
      <th style="text-align:center;">Out-of-distribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Single Cardiac Structure</td>
      <td>Lb1</td>
      <td>Lb2</td>
    </tr>
    <tr>
      <td>Whole Heart Structures</td>
      <td>Lb3</td>
      <td>Lb4</td>
    </tr>
    <tr>
      <td>Structure and Pathology</td>
      <td>Lb5</td>
      <td>Lb6</td>
    </tr>
  </tbody>
</table>
</div>




## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=cardiac).

## Leaderboard

#### Single Cardiac Structure (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Med-AIR</td><td>0.9390</td><td>13.7725</td></tr>
    <tr><td>Space</td><td>0.9392</td><td>15.8789</td></tr>
    <tr><td>Cemrg</td><td>0.9230</td><td>73.7738</td></tr>
    <tr><td>Xcare2025</td><td>0.8708</td><td>68.5828</td></tr>
    <tr><td>Qipeng Su</td><td>0.7777</td><td>112.5363</td></tr>
  </tbody>
</table>
</div>

#### Single Cardiac Structure (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Qipeng Su</td><td>0.7732</td><td>28.2984</td></tr>
    <tr><td>Space</td><td>0.7777</td><td>37.0773</td></tr>
    <tr><td>Med-AIR</td><td>0.7768</td><td>37.4824</td></tr>
    <tr><td>Xcare2025</td><td>0.7059</td><td>49.7781</td></tr>
    <tr><td>Cemrg</td><td>0.4442</td><td>69.7284</td></tr>
  </tbody>
</table>
</div>


#### Whole Heart Structures (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Med-AIR</td><td>0.9088</td><td>13.6256</td></tr>
    <tr><td>Space</td><td>0.8994</td><td>14.6366</td></tr>
    <tr><td>Xcare2025</td><td>0.8486</td><td>28.3754</td></tr>
    <tr><td>Qipeng Su</td><td>0.8454</td><td>31.7669</td></tr>
    <tr><td>Cemrg</td><td>0.8509</td><td>38.2703</td></tr>
  </tbody>
</table>
</div>

#### Whole Heart Structures (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Med-AIR</td><td>0.9261</td><td>10.4423</td></tr>
    <tr><td>Cemrg</td><td>0.9038</td><td>17.0919</td></tr>
    <tr><td>Space</td><td>0.8179</td><td>26.9377</td></tr>
    <tr><td>Qipeng Su</td><td>0.8134</td><td>30.0940</td></tr>
    <tr><td>Xcare2025</td><td>0.6187</td><td>63.3101</td></tr>
  </tbody>
</table>
</div>

#### Structure and Pathology (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Med-AIR</td><td>0.6709</td><td>16.9396</td></tr>
    <tr><td>Space</td><td>0.6705</td><td>17.7413</td></tr>
    <tr><td>Qipeng Su</td><td>0.6096</td><td>21.1745</td></tr>
    <tr><td>Xcare2025</td><td>0.5483</td><td>25.9150</td></tr>
    <tr><td>Cemrg</td><td>0.5394</td><td>83.7736</td></tr>
  </tbody>
</table>
</div>

#### Structure and Pathology (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="dice_hd table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>Dice↑</strong></th>
      <th style="text-align:center;"><strong>HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Med-AIR</td><td>0.7613</td><td>12.6665</td></tr>
    <tr><td>Space</td><td>0.7558</td><td>12.7343</td></tr>
    <tr><td>Cemrg</td><td>0.7236</td><td>14.3194</td></tr>
    <tr><td>Qipeng Su</td><td>0.6474</td><td>18.4937</td></tr>
    <tr><td>Xcare2025</td><td>0.6417</td><td>20.3698</td></tr>
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

@article{zhuang2016multi,
  title={Multi-scale patch and multi-modality atlases for whole heart segmentation of MRI},
  author={Zhuang, Xiahai and Shen, Juan},
  journal={Medical image analysis},
  volume={31},
  pages={77--87},
  year={2016},
  publisher={Elsevier}
}

@article{li2022atrialjsqnet,
  title={AtrialJSQnet: a new framework for joint segmentation and quantification of left atrium and scars incorporating spatial and shape information},
  author={Li, Lei and Zimmer, Veronika A and Schnabel, Julia A and Zhuang, Xiahai},
  journal={Medical image analysis},
  volume={76},
  pages={102303},
  year={2022},
  publisher={Elsevier}
}

@article{GAO2023BayeSeg,
  title = {BayeSeg: Bayesian modeling for medical image segmentation with interpretable generalizability},
  journal = {Medical Image Analysis},
  volume = {89},
  pages = {102889},
  year = {2023},
  author = {Shangqi Gao and Hangqi Zhou and Yibo Gao and Xiahai Zhuang},
}
```


<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
