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

Cardiovascular diseases (CVDs), as the leading cause of death globally<d-cite key="whs1"></d-cite>, necessitate precise morphological and pathological quantification through segmentation of crucial cardiac structures from medical images<d-cite key="whs2"></d-cite>. However, whole heart segmentation (WHS) faces challenges including heart shape variability during the cardiac cycle, clinical artifacts like motion and poor contrast-to-noise ratio, as well as domain shifts in multi-center data and the distinct modalities of CT and MRI. The WHS track serves to inspire innovative solutions in the realms of biomedical imaging and computer vision, striving to overcome these challenges and advance automated WHS for enhanced understanding and treatment of CVDs.


## Task
{% include figure.liquid loading="eager" path="/assets/img/whs.png" class="img-fluid" zoomable=true max-width="70%" caption="Figure 1. Overview of the WHS track" %}


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

We will rank participant methods based on the settings (​Lb1–Lb4) detailed in the following table:

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
<caption style="caption-side: top; text-align: left; font-weight: bold; padding-bottom: 10px;width: 100%;"> Leaderboard (Lb) for WHS track across modalities and evaluation settings.​​ Lb1–Lb4 represent performance from different test centers and modalities (e.g., Lb1 = CT segmentation peformance on center A and B). In-distribution refers to centers included in the training data, while out-of-distribution refers to unseen centers not used during training.</caption>
  <thead>
    <tr>
      <th style="text-align:center;">Modality</th>
      <th style="text-align:center;">In-distribution</th>
      <th style="text-align:center;">Out-of-distribution</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CT</td>
      <td>Lb1</td>
      <td>Lb2</td>
    </tr>
    <tr>
      <td>MR</td>
      <td>Lb3</td>
      <td>Lb4</td>
    </tr>
  </tbody>
</table>
</div>

## Data

### Training data

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
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

### Validation data

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Center</th>
      <th style="text-align:center;">Num. patients</th>
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
      <td>MR</td>
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


## Metrics
The performance of segmentation results will be assessed through: 
- **Dice Similarity Coefficient (Dice)**
- **Hausdorff Distance (HD in mm)**
- **Average Surface Distance (ASD in mm)**


## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP and MedSAM.


## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=whs).


## Leaderboard
#### WHS CT (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="whs table table-sm table-hover border-bottom" style="table-layout:fixed;width:100%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>LV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>Myo_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>LA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>AO_Dice↑</strong></th>
    <th style="text-align:center;"><strong>PA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>WHS_Dice↑</strong></th>
      <th style="text-align:center;"><strong>WHS_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>WHS_ASD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
  <tr><td>wei_yuan</td><td>0.9426</td><td>0.9300</td><td>0.9284</td><td>0.9653</td><td>0.9240</td><td>0.9604</td><td>0.8783</td><td>0.9410</td><td>12.5151</td><td>0.7237</td></tr>
    <tr><td>dzr</td><td>0.9440</td><td>0.9294</td><td>0.9271</td><td>0.9625</td><td>0.9208</td><td>0.9595</td><td>0.8749</td><td>0.9400</td><td>12.9502</td><td>0.7416</td></tr>
    <tr><td>huangzh</td><td>0.9398</td><td>0.9298</td><td>0.9239</td><td>0.9631</td><td>0.9189</td><td>0.9601</td><td>0.8661</td><td>0.9381</td><td>12.8066</td><td>0.7535</td></tr>
    <tr><td>Cardiac<br>Endeavours</td><td>0.9421</td><td>0.9289</td><td>0.9224</td><td>0.9646</td><td>0.9203</td><td>0.9600</td><td>0.8630</td><td>0.9381</td><td>13.1335</td><td>0.7525</td></tr>
    <tr><td>Nacho</td><td>0.9430</td><td>0.9272</td><td>0.9228</td><td>0.9616</td><td>0.9184</td><td>0.9580</td><td>0.8694</td><td>0.9378</td><td>12.8374</td><td>0.7629</td></tr>
    <tr><td>spz312</td><td>0.9421</td><td>0.9270</td><td>0.9237</td><td>0.9607</td><td>0.9167</td><td>0.9591</td><td>0.8687</td><td>0.9374</td><td>13.7740</td><td>0.7772</td></tr>
    <tr><td>Zhiyou Lin</td><td>0.9426</td><td>0.9242</td><td>0.9207</td><td>0.9604</td><td>0.9193</td><td>0.9568</td><td>0.8652</td><td>0.9361</td><td>15.9188</td><td>0.7788</td></tr>
    <tr><td>Space</td><td>0.9344</td><td>0.9114</td><td>0.9078</td><td>0.9617</td><td>0.8829</td><td>0.9502</td><td>0.8490</td><td>0.9230</td><td>14.8967</td><td>0.9549</td></tr>
    <tr><td>ImFusion</td><td>0.9209</td><td>0.8932</td><td>0.9041</td><td>0.9398</td><td>0.9076</td><td>0.9206</td><td>0.8492</td><td>0.9150</td><td>17.3939</td><td>1.1766</td></tr>
    <tr><td>kwh</td><td>0.8859</td><td>0.7872</td><td>0.7052</td><td>0.8637</td><td>0.6865</td><td>0.8949</td><td>0.6599</td><td>0.8057</td><td>36.1450</td><td>2.9919</td></tr>
  </tbody>
</table>
</div>

#### WHS CT (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="whs table table-sm table-hover border-bottom" style="table-layout:fixed;width:100%;align:center;color:black;font-size:0.8rem;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>LV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>Myo_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>LA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>AO_Dice↑</strong></th>
    <th style="text-align:center;"><strong>PA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>WHS_Dice↑</strong></th>
      <th style="text-align:center;"><strong>WHS_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>WHS_ASD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>wei_yuan</td><td>0.9754</td><td>0.9742</td><td>0.9617</td><td>0.9839</td><td>0.9695</td><td>0.9805</td><td>0.9561</td><td>0.9740</td><td>11.6691</td><td>0.3616</td></tr>
    <tr><td>dzr</td><td>0.9772</td><td>0.9755</td><td>0.9621</td><td>0.9830</td><td>0.9670</td><td>0.9825</td><td>0.9527</td><td>0.9739</td><td>11.9296</td><td>0.3668</td></tr>
    <tr><td>huangzh</td><td>0.9738</td><td>0.9719</td><td>0.9561</td><td>0.9838</td><td>0.9653</td><td>0.9791</td><td>0.9503</td><td>0.9713</td><td>11.8991</td><td>0.3935</td></tr>
    <tr><td>Cardiac<br>Endeavours</td><td>0.9738</td><td>0.9712</td><td>0.9553</td><td>0.9791</td><td>0.9610</td><td>0.9757</td><td>0.9522</td><td>0.9692</td><td>16.3845</td><td>0.4333</td></tr>
    <tr><td>Nacho</td><td>0.9749</td><td>0.9725</td><td>0.9572</td><td>0.9802</td><td>0.9638</td><td>0.9798</td><td>0.9527</td><td>0.9708</td><td>12.1136</td><td>0.4074</td></tr>
    <tr><td>spz312</td><td>0.9763</td><td>0.9746</td><td>0.9552</td><td>0.9841</td><td>0.9639</td><td>0.9829</td><td>0.9482</td><td>0.9721</td><td>12.3174</td><td>0.3887</td></tr>
    <tr><td>Zhiyou Lin</td><td>0.9721</td><td>0.9675</td><td>0.9557</td><td>0.9806</td><td>0.9658</td><td>0.9823</td><td>0.9526</td><td>0.9697</td><td>13.8909</td><td>0.4089</td></tr>
    <tr><td>Space</td><td>0.8507</td><td>0.9456</td><td>0.5362</td><td>0.7182</td><td>0.8674</td><td>0.7533</td><td>0.7401</td><td>0.8099</td><td>48.5065</td><td>2.5080</td></tr>
    <tr><td>ImFusion</td><td>0.9112</td><td>0.8980</td><td>0.8953</td><td>0.9328</td><td>0.9235</td><td>0.9195</td><td>0.8888</td><td>0.9135</td><td>19.9910</td><td>1.2760</td></tr>
    <tr><td>kwh</td><td>0.9210</td><td>0.8349</td><td>0.6574</td><td>0.9479</td><td>0.6643</td><td>0.9078</td><td>0.7401</td><td>0.8257</td><td>39.0210</td><td>2.7931</td></tr>
  </tbody>
</table>
</div>

* The annotation methodology for the gold standards differed across the centers. Datasets from Centers A, B, C, D, and E underwent a fully manual annotation process, while a semi-automatically assisted approach was employed for Center F (OOD).

#### WHS MR (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="whs table table-sm table-hover border-bottom" style="table-layout:fixed;width:100%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>LV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>Myo_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>LA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>AO_Dice↑</strong></th>
    <th style="text-align:center;"><strong>PA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>WHS_Dice↑</strong></th>
      <th style="text-align:center;"><strong>WHS_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>WHS_ASD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>wei_yuan</td><td>0.9354</td><td>0.8496</td><td>0.9148</td><td>0.8959</td><td>0.8892</td><td>0.8966</td><td>0.8148</td><td>0.8992</td><td>24.7081</td><td>1.1629</td></tr>
    <tr><td>dzr</td><td>0.9329</td><td>0.8467</td><td>0.9187</td><td>0.8937</td><td>0.8890</td><td>0.8948</td><td>0.7973</td><td>0.8979</td><td>29.6365</td><td>1.2133</td></tr>
    <tr><td>huangzh</td><td>0.9343</td><td>0.8503</td><td>0.9056</td><td>0.8825</td><td>0.8725</td><td>0.8887</td><td>0.8001</td><td>0.8913</td><td>35.8354</td><td>1.6442</td></tr>
    <tr><td>Cardiac<br>Endeavours</td><td>0.9331</td><td>0.8473</td><td>0.9115</td><td>0.8839</td><td>0.8837</td><td>0.8957</td><td>0.8079</td><td>0.8948</td><td>27.7563</td><td>1.3423</td></tr>
    <tr><td>Nacho</td><td>0.9323</td><td>0.8439</td><td>0.9143</td><td>0.8862</td><td>0.8875</td><td>0.8932</td><td>0.8068</td><td>0.8951</td><td>24.0996</td><td>1.2457</td></tr>
    <tr><td>spz312</td><td>0.9164</td><td>0.8321</td><td>0.9169</td><td>0.8927</td><td>0.8768</td><td>0.8929</td><td>0.8099</td><td>0.8888</td><td>42.4716</td><td>2.1076</td></tr>
    <tr><td>Zhiyou Lin</td><td>0.9357</td><td>0.8394</td><td>0.9100</td><td>0.8817</td><td>0.8876</td><td>0.8864</td><td>0.7815</td><td>0.8937</td><td>36.7519</td><td>1.4858</td></tr>
    <tr><td>Space</td><td>0.9323</td><td>0.8414</td><td>0.9008</td><td>0.8839</td><td>0.8855</td><td>0.8891</td><td>0.8091</td><td>0.8899</td><td>29.6204</td><td>1.7214</td></tr>
    <tr><td>ImFusion</td><td>0.4201</td><td>0.1910</td><td>0.0924</td><td>0.3747</td><td>0.1258</td><td>0.0010</td><td>0.0000</td><td>0.2183</td><td>86.5388</td><td>20.5581</td></tr>
    <tr><td>kwh</td><td>0.9303</td><td>0.8404</td><td>0.9063</td><td>0.8672</td><td>0.8612</td><td>0.8851</td><td>0.7992</td><td>0.8852</td><td>48.5327</td><td>1.9555</td></tr>
  </tbody>
</table>
</div>

#### WHS MR (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="whs table table-sm table-hover border-bottom" style="table-layout:fixed;width:100%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>LV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>Myo_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RV_Dice↑</strong></th>
    <th style="text-align:center;"><strong>LA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>RA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>AO_Dice↑</strong></th>
    <th style="text-align:center;"><strong>PA_Dice↑</strong></th>
    <th style="text-align:center;"><strong>WHS_Dice↑</strong></th>
      <th style="text-align:center;"><strong>WHS_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>WHS_ASD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr><td>wei_yuan</td><td>0.9426</td><td>0.8235</td><td>0.8735</td><td>0.9116</td><td>0.8897</td><td>0.9106</td><td>0.8848</td><td>0.8959</td><td>20.6044</td><td>1.5678</td></tr>
    <tr><td>dzr</td><td>0.9348</td><td>0.8232</td><td>0.8742</td><td>0.9080</td><td>0.8880</td><td>0.9112</td><td>0.8818</td><td>0.8934</td><td>21.2980</td><td>1.5955</td></tr>
    <tr><td>huangzh</td><td>0.9462</td><td>0.8358</td><td>0.8907</td><td>0.9056</td><td>0.8881</td><td>0.9044</td><td>0.8766</td><td>0.8969</td><td>20.7411</td><td>1.5648</td></tr>
    <tr><td>Cardiac<br>Endeavours</td><td>0.9449</td><td>0.8329</td><td>0.8798</td><td>0.9065</td><td>0.8903</td><td>0.9126</td><td>0.8850</td><td>0.8965</td><td>21.6923</td><td>1.5574</td></tr>
    <tr><td>Nacho</td><td>0.9310</td><td>0.8234</td><td>0.8772</td><td>0.9042</td><td>0.8903</td><td>0.9077</td><td>0.8816</td><td>0.8923</td><td>21.4862</td><td>1.6170</td></tr>
    <tr><td>spz312</td><td>0.9364</td><td>0.8129</td><td>0.8644</td><td>0.9103</td><td>0.8812</td><td>0.9058</td><td>0.8753</td><td>0.8895</td><td>22.2377</td><td>1.6504</td></tr>
    <tr><td>Zhiyou Lin</td><td>0.9069</td><td>0.7664</td><td>0.8718</td><td>0.9053</td><td>0.8852</td><td>0.9018</td><td>0.8591</td><td>0.8764</td><td>28.9588</td><td>1.9135</td></tr>
    <tr><td>Space</td><td>0.9411</td><td>0.8355</td><td>0.8815</td><td>0.9081</td><td>0.8862</td><td>0.9032</td><td>0.8666</td><td>0.8947</td><td>21.9386</td><td>1.5576</td></tr>
    <tr><td>ImFusion</td><td>0.2172</td><td>0.1051</td><td>0.0296</td><td>0.2463</td><td>0.0000</td><td>0.0004</td><td>0.0000</td><td>0.1225</td><td>88.9726</td><td>26.1159</td></tr>
    <tr><td>kwh</td><td>0.9017</td><td>0.7860</td><td>0.8264</td><td>0.8997</td><td>0.8714</td><td>0.8850</td><td>0.8484</td><td>0.8711</td><td>41.6986</td><td>2.1071</td></tr>
  </tbody>
</table>
</div>


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

<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
