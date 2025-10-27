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
{% include figure.liquid loading="eager" path="/assets/img/liqa1.png" class="img-fluid" zoomable=true caption="Figure 1. Track description." max-width="70%" %}

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
Segment the liver in multi-phase fibrosis, where **limited ground truth of Hepatobiliary phase (GED4) MRI** is available. Non-constrast data (T2WI, T1, DWI) could be segmented via **unsupervised or registration-based approaches** to overcome annotation limitations.  

#### Subtasks:
- **Non-Contrast Subtask**: Segment liver anatomy in **T2WI**, **T1**, and **DWI** sequences. No annotations provided.
- **Contrast-Enhanced Subtask**: Segment **GED4** sequence. Limited annotations provided.

---

## Data

### About the data

**1) Scanner:** Philips Ingenia3.0T, Siemens Skyra 3.0T, Siemens Aera 1.5T.

**2) Dataset overview:**  The track cohort comprises **610 patients** (170 newly cases compared to CARE2024) diagnosed with liver fibrosis, all of whom underwent multi-phase MRI scans. The dataset includes **multi-phase** and **multi-center** data, with images acquired from clinical centers using three different MRI scanner vendors. The dataset consists of T2-weighted imaging, diffusion-weighted imaging, and Gadolinium ethoxybenzyl diethylenetriamine pentaacetic acid (**Gd-EOB-DTPA**)-enhanced dynamic MRIs. The Gd-EOB-DTPA-enhanced dynamic MRIs cover the non-contrast phase (T1WI), arterial phase, venous phase, delayed phase, and hepatobiliary phase.

**3) Contrast-enhanced dynamic scans:** Contrast-enhanced scans were performed based on the injection of the GD-EOB-DTPA agent. The arterial phase is captured 25 seconds after the contrast agent is injected. Subsequently, the portal phase is achieved 1 minute later. After another 3 minutes, the delay phase is obtained, and finally, the hepatobiliary phase is reached 20 minutes thereafter.

**4) Data format:** The data are all in Nifty format. Each sample may randomly lack phases (except hepatobiliary phase), and the sequences have not applied pre-alignment through spatial registration.

### Training set

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
      <th class="text-center" style="text-align:center;">#Annotation for seg</th>
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

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
      <th class="text-center" style="text-align:center;">#Annotation for seg</th>
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

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:50%;align:center;">
  <thead>
    <tr>
      <th class="text-center" style="text-align:center;">Vendor</th>
      <th class="text-center" style="text-align:center;">Center</th>
      <th class="text-center" style="text-align:center;">#Cases</th>
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

## Rules
1. Publicly available data (such as [LLD-MMRI2023](https://github.com/LMMMEng/LLD-MMRI2023)) and pre-trained models are allowed. 
2. Only automatic methods are acceptable. 

## Registration
To access the dataset, please register [here](http://zmic.org.cn/care_2025/eval/register?track=liver).

## Leaderboards

<div style="display: flex;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;">
  <thead>
    <tr>
      <th style="text-align:center;">Task</th>
      <th style="text-align:center;">Subtask</th>
      <th style="text-align:center;">Key Metrics</th>
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
      <td>Dice Similarity Score (Dice), Hausdorff Distance (HD in mm)</td>
    </tr>
    <tr>
      <td>Contrast-Enhanced (GED4)</td>
      <td>Dice Similarity Score (Dice), Hausdorff Distance (HD in mm)</td>
    </tr>
  </tbody>
</table>
</div>

- **NOTE: Participants are welcome to participate in a single subtask, and their performance will still be recorded and displayed on the leaderboard.**

#### LiFS Contrast-Enhanced (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="lifs table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S1 vs. S2–S4)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S1 vs. S2–S4)</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BioDreamer</td>
        <td>68.33</td>
        <td>77.19</td>
        <td>74.58</td>
        <td>78.11</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>70.83</td>
        <td>75.10</td>
        <td>75.00</td>
        <td>78.45</td>
      </tr>
      <tr>
        <td>NW-Radio</td>
        <td>47.50</td>
        <td>78.03</td>
        <td>65.83</td>
        <td>78.20</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>75.83</td>
        <td>83.92</td>
        <td>77.50</td>
        <td>83.42</td>
      </tr>
      <tr>
        <td>Team space</td>
        <td>71.67</td>
        <td>79.39</td>
        <td>79.17</td>
        <td>80.24</td>
      </tr>
      <tr>
        <td>WSQ</td>
        <td>72.50</td>
        <td>78.31</td>
        <td>80.83</td>
        <td>84.50</td>
      </tr>
  </tbody>
</table>
</div>

#### LiFS Contrast-Enhanced (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="lifs table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S1 vs. S2–S4)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S1 vs. S2–S4)</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BioDreamer</td>
        <td>63.71</td>
        <td>67.40</td>
        <td>92.86</td>
        <td>47.68</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>41.43</td>
        <td>46.81</td>
        <td>64.29</td>
        <td>52.62</td>
      </tr>
      <tr>
        <td>NW-Radio</td>
        <td>32.86</td>
        <td>64.11</td>
        <td>92.86</td>
        <td>52.62</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>58.57</td>
        <td>54.12</td>
        <td>92.86</td>
        <td>75.38</td>
      </tr>
      <tr>
        <td>Team space</td>
        <td>52.86</td>
        <td>60.22</td>
        <td>64.29</td>
        <td>64.62</td>
      </tr>
      <tr>
        <td>WSQ</td>
        <td>41.43</td>
        <td>66.05</td>
        <td>82.86</td>
        <td>37.23</td>
      </tr>
  </tbody>
</table>
</div>

#### LiFS Non-Contrast (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="lifs table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S1 vs. S2–S4)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S1 vs. S2–S4)</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BioDreamer</td>
        <td>70.83</td>
        <td>77.89</td>
        <td>70.00</td>
        <td>77.11</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>71.67</td>
        <td>78.61</td>
        <td>70.00</td>
        <td>73.70</td>
      </tr>
      <tr>
        <td>NW-Radio</td>
        <td>47.50</td>
        <td>79.78</td>
        <td>65.83</td>
        <td>67.27</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>70.00</td>
        <td>77.22</td>
        <td>65.00</td>
        <td>74.28</td>
      </tr>
      <tr>
        <td>Team space</td>
        <td>74.17</td>
        <td>81.33</td>
        <td>76.67</td>
        <td>83.93</td>
      </tr>
      <tr>
        <td>TeamZhang</td>
        <td>66.67</td>
        <td>71.73</td>
        <td>74.17</td>
        <td>68.48</td>
      </tr>
      <tr>
        <td>potato</td>
        <td>72.50</td>
        <td>77.22</td>
        <td>71.67</td>
        <td>78.51</td>
      </tr>
  </tbody>
</table>
</div>

#### LiFS Non-Contrast (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="lifs table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S4 vs. S1–S3)</strong></th>
      <th style="text-align:center;"><strong>ACC↑(S1 vs. S2–S4)</strong></th>
      <th style="text-align:center;"><strong>AUC↑(S1 vs. S2–S4)</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BioDreamer</td>
        <td>32.86</td>
        <td>56.65</td>
        <td>88.29</td>
        <td>59.40</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>42.86</td>
        <td>49.31</td>
        <td>70.00</td>
        <td>31.08</td>
      </tr>
      <tr>
        <td>NW-Radio</td>
        <td>32.86</td>
        <td>46.25</td>
        <td>92.86</td>
        <td>40.31</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>71.43</td>
        <td>69.47</td>
        <td>92.86</td>
        <td>86.31</td>
      </tr>
      <tr>
        <td>Team space</td>
        <td>64.29</td>
        <td>52.73</td>
        <td>88.57</td>
        <td>61.23</td>
      </tr>
      <tr>
        <td>TeamZhang</td>
        <td>64.29</td>
        <td>68.83</td>
        <td>91.43</td>
        <td>71.38</td>
      </tr>
      <tr>
        <td>potato</td>
        <td>70.00</td>
        <td>71.51</td>
        <td>67.14</td>
        <td>33.23</td>
      </tr>
  </tbody>
</table>
</div>

#### LiSeg Contrast-Enhanced (ID)

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
      <tr>
        <td>Team space</td>
        <td>0.9641</td>
        <td>24.32</td>
      </tr>
      <tr>
        <td>BI</td>
        <td>0.9644</td>
        <td>22.63</td>
      </tr>
      <tr>
        <td>MIHL</td>
        <td>0.9456</td>
        <td>56.59</td>
      </tr>
      <tr>
        <td>UON_IMA</td>
        <td>0.9684</td>
        <td>22.97</td>
      </tr>
      <tr>
        <td>Wenting Yue</td>
        <td>0.9631</td>
        <td>24.12</td>
      </tr>
      <tr>
        <td>xcj</td>
        <td>0.9647</td>
        <td>25.03</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>0.8302</td>
        <td>66.78</td>
      </tr>
      <tr>
        <td>SuperIdols</td>
        <td>0.9610</td>
        <td>23.30</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>0.9488</td>
        <td>42.12</td>
      </tr>
      <tr>
        <td>SUSTVI</td>
        <td>0.9612</td>
        <td>26.84</td>
      </tr>
      <tr>
        <td>BIGS2</td>
        <td>0.9619</td>
        <td>24.50</td>
      </tr>
      <tr>
        <td>Monster</td>
        <td>0.9703</td>
        <td>21.40</td>
      </tr>
      <tr>
        <td>IntelliLiver</td>
        <td>0.9630</td>
        <td>25.75</td>
      </tr>
      <tr>
        <td>BioDreamer</td>
        <td>0.9516</td>
        <td>29.07</td>
      </tr>
  </tbody>
</table>
</div>

#### LiSeg Contrast-Enhanced (OOD)

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
      <tr>
        <td>Team space</td>
        <td>0.9753</td>
        <td>15.72</td>
      </tr>
      <tr>
        <td>BI</td>
        <td>0.9754</td>
        <td>14.37</td>
      </tr>
      <tr>
        <td>MIHL</td>
        <td>0.9726</td>
        <td>21.52</td>
      </tr>
      <tr>
        <td>UON_IMA</td>
        <td>0.9754</td>
        <td>15.11</td>
      </tr>
      <tr>
        <td>Wenting Yue</td>
        <td>0.9741</td>
        <td>15.58</td>
      </tr>
      <tr>
        <td>xcj</td>
        <td>0.9745</td>
        <td>15.84</td>
      </tr>
      <tr>
        <td>SuperIdols</td>
        <td>0.9770</td>
        <td>14.65</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>0.9586</td>
        <td>20.65</td>
      </tr>
      <tr>
        <td>SUSTVI</td>
        <td>0.9652</td>
        <td>29.02</td>
      </tr>
      <tr>
        <td>BIGS2</td>
        <td>0.9688</td>
        <td>15.56</td>
      </tr>
      <tr>
        <td>IntelliLiver</td>
        <td>0.9716</td>
        <td>16.41</td>
      </tr>
      <tr>
        <td>Monster</td>
        <td>0.9765</td>
        <td>15.17</td>
      </tr>
      <tr>
        <td>BioDreamer</td>
        <td>0.9656</td>
        <td>19.51</td>
      </tr>
  </tbody>
</table>
</div>

#### LiSeg Non-Contrast (ID)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="liseg_noncontrast table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>T1_Dice↑</strong></th>
      <th style="text-align:center;"><strong>T1_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>T2_Dice↑</strong></th>
      <th style="text-align:center;"><strong>T2_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>DWI_Dice↑</strong></th>
      <th style="text-align:center;"><strong>DWI_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BIGS2</td>
        <td>0.9434</td>
        <td>38.06</td>
        <td>0.8722</td>
        <td>35.24</td>
        <td>0.8029</td>
        <td>31.04</td>
      </tr>
      <tr>
        <td>BioDreamer</td>
        <td>0.9196</td>
        <td>31.83</td>
        <td>0.8201</td>
        <td>37.16</td>
        <td>0.7210</td>
        <td>31.33</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>0.9262</td>
        <td>27.80</td>
        <td>0.8890</td>
        <td>34.60</td>
        <td>0.8374</td>
        <td>26.96</td>
      </tr>
      <tr>
        <td>MIHL</td>
        <td>0.8642</td>
        <td>163.91</td>
        <td>0.2024</td>
        <td>121.48</td>
        <td>0.2612</td>
        <td>99.25</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>0.9318</td>
        <td>58.99</td>
        <td>0.7568</td>
        <td>75.44</td>
        <td>0.8234</td>
        <td>34.19</td>
      </tr>
  </tbody>
</table>
</div>

#### LiSeg Non-Contrast (OOD)

<div style="display:flex; flex-direction:column; gap:8px;">
<table class="liseg_noncontrast table table-sm table-hover border-bottom" style="table-layout:fixed;width:80%;align:center;color:black;">
  <thead>
    <tr>
      <th style="text-align:center;"><strong>Team</strong></th>
      <th style="text-align:center;"><strong>T1_Dice↑</strong></th>
      <th style="text-align:center;"><strong>T1_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>T2_Dice↑</strong></th>
      <th style="text-align:center;"><strong>T2_HD(mm)↓</strong></th>
      <th style="text-align:center;"><strong>DWI_Dice↑</strong></th>
      <th style="text-align:center;"><strong>DWI_HD(mm)↓</strong></th>
    </tr>
  </thead>
  <tbody>
      <tr>
        <td>BIGS2</td>
        <td>0.9548</td>
        <td>22.11</td>
        <td>0.9015</td>
        <td>35.17</td>
        <td>0.8481</td>
        <td>22.58</td>
      </tr>
      <tr>
        <td>BioDreamer</td>
        <td>0.9418</td>
        <td>28.24</td>
        <td>0.8457</td>
        <td>25.84</td>
        <td>0.7812</td>
        <td>15.96</td>
      </tr>
      <tr>
        <td>CitySJTU</td>
        <td>0.9444</td>
        <td>25.54</td>
        <td>0.8894</td>
        <td>24.52</td>
        <td>0.8857</td>
        <td>11.21</td>
      </tr>
      <tr>
        <td>MIHL</td>
        <td>0.7351</td>
        <td>102.79</td>
        <td>0.0714</td>
        <td>118.06</td>
        <td>0.4567</td>
        <td>51.76</td>
      </tr>
      <tr>
        <td>Sigma</td>
        <td>0.9503</td>
        <td>29.04</td>
        <td>0.6208</td>
        <td>72.29</td>
        <td>0.9041</td>
        <td>19.72</td>
      </tr>
  </tbody>
</table>
</div>


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

@article{wu2022meru,
  title = {Minimizing Estimated Risks on Unlabeled Data: A New Formulation for Semi-Supervised Medical Image Segmentation},
  author={Wu, Fuping and Zhuang, Xiahai},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
  title={Minimizing Estimated Risks on Unlabeled Data: A New Formulation for Semi-Supervised Medical Image Segmentation}, 
  year={2023},
  volume={45},
  number={5},
  pages={6021-6036},
}
```

<script defer src="{{ '/assets/js/leaderboard_sort.js' | relative_url }}"></script>
