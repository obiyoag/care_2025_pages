---
layout: distill
title: LiQA
description: Liver Fibrosis Quantification and Analysis
permalink: /track3/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Task
  - name: Data
  - name: Metrics & Ranking
  - name: Rules
  - name: Registration
  - name: Submission Guidance
  - name: Timeline
  - name: Citations
  - name: Contact
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

Liver fibrosis, often resulting from chronic viral or metabolic liver diseases, poses a significant global health challenge. Accurate liver segmentation (LiSeg) and fibrosis staging (LiFS) are crucial for assessing disease severity and enabling precise diagnoses<d-cite key="liqa1"></d-cite><d-cite key="liqa2"></d-cite> . This task focuses on developing automated methods for liver segmentation and fibrosis staging using multi-phase, multi-center liver MRI scans. Automatic LiFS presents challenges such as missing modalities for certain patients, misalignments in multi-phase MRI data, and the need for effective integration of multi-phase information to improve the accuracy and generalizability of liver fibrosis diagnoses. Similarly, automatic LiSeg faces difficulties stemming from limited ground truth annotations across different modalities and domain shifts in multi-center datasets.

## Task

To address these challenges, the extensive use of external data and pre-trained models is encouraged to enhance liver segmentation performance. This track aims to foster innovative solutions that overcome these obstacles, leveraging multi-phase MRI data to advance the field of liver segmentation and fibrosis staging. Building on the dataset used in CARE 2024, we have expanded the collection to include 170 newly acquired cases, bringing the total to 610 cases. These cases were obtained from the same vendors and centers, including Philips Ingenia 3.0T, Siemens Skyra 3.0T, and Siemens Aera 1.5T. The dataset features multi-phase imaging modalities such as T2-weighted imaging, diffusion-weighted imaging(DWI), and Gadolinium ethoxybenzyl diethylenetriamine pentaacetic acid (Gd-EOB-DTPA)-enhanced dynamic MRIs. The Gd-EOB-DTPA-enhanced dynamic MRIs include multiple phases: non-contrast, arterial, venous, delayed, and hepatobiliary phases.

**Task 1: The LiSeg Task** focuses on liver segmentation with **limited ground truth**, using Hepatobiliary phase (HBP) MRI, which contains crucial liver information. The challenge is to develop methods capable of accurately segmenting the liver in these images.

**Task 2: The LiFS Task** aims to stage liver fibrosis accurately across four stages (S1-S4). Two binary classification tasks with clinical significance will be evaluated: staging cirrhosis (S1-3 vs. S4) and identifying substantial fibrosis (S1 vs. S2-4).

Both tasks, LiSeg and LiFS, involve **domain shifts** across multi-center data. Participants are encouraged to effectively integrate complementary information from multi-phase MRIs to achieve more **precise and generalizable** results. Additionally, automatic LiFS may encounter challenges such as **random missing sequences** for certain patients and **misalignments** between multi-phase MRIs.

To tackle these challenges, participants are also encouraged to leverage **external datasets**, such as [LLD-MMRI2023](https://github.com/LMMMEng/LLD-MMRI2023), and **pretrained models**.

## Data

### About the data

**1) Scanner:** Philips Ingenia3.0T, Siemens Skyra 3.0T, Siemens Aera 1.5T.

**2) Dataset overview:**  The track cohort comprises **610 patients** diagnosed with liver fibrosis, all of whom underwent multi-phase MRI scans. The dataset includes **multi-phase** and **multi-center** data, with images acquired from clinical centers using three different MRI scanner vendors. The dataset consists of T2-weighted imaging, diffusion-weighted imaging, and Gadolinium ethoxybenzyl diethylenetriamine pentaacetic acid (Gd-EOB-DTPA)-enhanced dynamic MRIs. The Gd-EOB-DTPA-enhanced dynamic MRIs cover the non-contrast phase (T1WI), arterial phase, venous phase, delayed phase, and hepatobiliary phase.

**3) Contrast-enhanced dynamic scans:** Contrast-enhanced scans were performed based on the injection of the GD-EOB-DTPA agent. The arterial phase is captured 25 seconds after the contrast agent is injected. Subsequently, the portal phase is achieved 1 minute later. After another 3 minutes, the delay phase is obtained, and finally, the hepatobiliary phase is reached 20 minutes thereafter.

**4) Data format:** The data are all in Nifty format. Each sample may randomly lack phases (except hepatobiliary phase ), and the sequences have not applied pre-alignment through spatial registration.

### Training set

<div style="display: flex; justify-content: center;">
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
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
<table class="table table-sm table-hover border-bottom" style="table-layout:fixed;width:85%;align:center;">
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

## Metrics & Ranking

### Metrics

* LiSeg: Dice Similarity Coefficient (DSC), Hausdorff Distance
* LiFS: Area under curve (AUC), Accuracy;

### Rank methods

The ranks of classification and segmentation tasks are ranged separately.

* a. For classification, the average of metrics, i.e., Area under curve (AUC) and accuracy, are utilized to evaluate performance.
* b. For segmentation, the average of metrics, i.e., Dice Similarity Coefficient (DSC) and Hausdorff Distance is utilized to  evaluate performance.

Finally, the average of in-distribution results (seen center) and out-of-distribution results (unseen center) are used for the final ranking.

## Rules
1. Publicly available data (such as [LLD-MMRI2023](https://github.com/LMMMEng/LLD-MMRI2023)) and pre-trained models are allowed. 
2. Only automatic methods are acceptable. 

## Registration

To access the dataset, please register in the [LiQA registration platform](http://zmic.org.cn/care_2025/eval/register?track=LiQA).

## Submission Guidance

### Model Submission
After registration, we will assign participants an account to login into our [LiQA evaluation platform](http://zmic.org.cn/care_2025/eval/login?track=LiQA). Participants can directly upload your predictions on the validation data (in nifty format) via the website. Note that evaluation of validation data will be allowed up to 10 times for each task per team. For fair comparison, the test dataset will remain unseen. Participants need to submit their [docker models](http://zmic.org.cn/care_2025/test_submission) for testing.
### Paper Submission
Please refer to our [paper submission guidance](/care_2025/paper_submission).

## Timeline

The schedule for this track is as follows. All deadlines(DDLs) are on 23:59 in Pacific Standard Time.

<table class="table table-sm table-hover border-bottom">
    <tr>
    <td class="text-left"><strong>Training Data Release</strong></td>
    <th scope="row" style="width: 60%" class="text-right">April 30, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Validation Phase start</strong></td>
    <th scope="row" style="width: 60%" class="text-right">May 30, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Test data release</strong></td>
    <th scope="row" style="width: 60%" class="text-right">June 30, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Abstract Submission</strong></td>
    <th scope="row" style="width: 60%" class="text-right">July 15, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Paper Submission</strong></td>
    <th scope="row" style="width: 60%" class="text-right">July 30, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Submission of final results</strong></td>
    <th scope="row" style="width: 60%" class="text-right">July 30, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Release date of the results</strong></td>
    <th scope="row" style="width: 60%" class="text-right">August 10, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Camera Ready</strong></td>
    <th scope="row" style="width: 60%" class="text-right">August 20, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Workshop (Half-Day)</strong></td>
    <th scope="row" style="width: 60%" class="text-right">TBD</th>
    </tr>
</table>

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

## Contact

If you have any questions regarding the LiQA track, please feel free to contact: 

* Yuanye Liu: [yuanyeliu@fudan.edu.cn](mailto:yuanyeliu@fudan.edu.cn)
