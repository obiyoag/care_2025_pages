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
  - name: Metrics and Leaderboards
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

{% include figure.liquid loading="eager" path="/assets/img/care-cardiac.png" class="img-fluid" zoomable=true %}

Cardiac diagnosis involves multiple interrelated tasks, such as delineating anatomical structures (e.g., atria, ventricles, vessels) and identifying pathological regions (e.g., scar) across diverse imaging modalities and acquisition protocols. Relying on separate models for each task leads to fragmented workflows, limited knowledge transfer, and poor adaptability to missing or heterogeneous data. A **unified cardiac segmentation model** addresses these limitations by enabling unified modeling across tasks. 

## Task

Develop a **unified model** capable of segmenting **single cardiac structure** (left atria), **whole heart structures** and **structure and pathology** (left ventricle, myocardium and scar).

***Note\***: Participants are also encouraged to leverage external data.


## Data

Multi-center and multi-modality datasets are provided for three sub-tasks. Please register [here](http://zmic.org.cn/care_2025/eval/register?track=care_cardiac) to access the data. 

### Training Dataset

1). Left Atrial Segmentation

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modality</th>
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

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
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



3). Myocardial Pathology Segmentation

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modality</th>
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

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Sequences</th>
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



 2). Whole Heart Segmentation

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modalities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>B</td>
      <td>44</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>E</td>
      <td>6</td>
      <td>MRI</td>
    </tr>
  </tbody>
</table>
</div>


 3). Myocardial Pathology Segmentation

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modality</th>
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

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modality</th>
    </tr>
  </thead>
  <tbody>
     <tr>
      <td>A</td>
      <td>24</td>
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

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
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
      <td>C/D</td>
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

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th scope="col">Center</th>
      <th scope="col">Num. cases</th>
      <th scope="col">Modality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>D</td>
      <td>25</td>
      <td>LGE MRI</td>
    </tr>
    <tr>
      <td>I</td>
      <td>16</td>
      <td>LGE MRI</td>
    </tr>
  </tbody>
</table>
</div>






## Metrics and Leaderboards

### Metrics

Dice Similarity Coefficient (DSC), Hausdorff Distance (HD).

### Leaderboards

The leadboards will be organized as follows: 
1. Rankings for both **in-distribution** (i.e., seen centers) and **out-of-distribution (OOD)** (i.e., unseen centers) will be based on the **average performance across three sub-tasks**.

2. The **weighted average** of in-distribution and OOD scores will be computed and used to determine real-world leaderboard.

   <div style="display: flex; justify-content: center;">
   <table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
     <thead>
       <tr>
         <th scope="col">In-distribution</th>
         <th scope="col">Out-of-distribution</th>
         <th scope="col">Average(Real-world)</th>
       </tr>
     </thead>
     <tbody>
       <tr>
         <td>Lb1</td>
         <td>Lb2</td>
         <td>Lb3</td>
       </tr>
     </tbody>
   </table>
   </div>


## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=care_cardiac).


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
