---
layout: distill
title: WHS++
description: Whole Heart Segmentation
permalink: /track5/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Task
  - name: Data
  - name: Guidance for Training Strategies
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
Cardiovascular diseases (CVDs), recognized by the WHO as the leading cause of death globally<d-cite key="whs1"></d-cite>, necessitate precise morphological and pathological quantification through segmentation of crucial cardiac structures from medical images<d-cite key="whs2"></d-cite>. demand precise morphological and pathological assessments through the segmentation of key cardiac structures from medical images. This task aims to achieve whole heart segmentation (WHS), including the extraction of individual substructures such as the left ventricle (LV), right ventricle (RV), left atrium (LA), right atrium (RA), left ventricular myocardium (Myo), ascending aorta (AO), entire aorta, and pulmonary artery (PA). Automated WHS faces several challenges, including variability in heart shape throughout the cardiac cycle, clinical artifacts such as motion blur and poor contrast-to-noise ratios, as well as domain shifts across multi-center datasets and differing imaging modalities like CT and MRI.

## Task
{% include figure.liquid loading="eager" path="/assets/img/whs.png" class="img-fluid" zoomable=true caption="Figure 1. Overview of the WHS++ track" %}

This task seeks to inspire innovative solutions in biomedical imaging and computer vision, addressing these challenges to advance automated WHS. The ultimate goal is to enhance the understanding and treatment of CVDs through accurate and robust segmentation methods. In addition to the data from CARE 2024, we have added 200 newly collected CT cases from patients with atrial fibrillation. These images were obtained using a Siemens SOMATOM Force scanner, providing an in-plane resolution of 1 × 1 × 1 mm. The inclusion of these new cases enhances the diversity and clinical relevance of the dataset, offering a broader spectrum of anatomical and pathological variations.  The specific  substructures, each associated with a unique label value, are:

1. **Left Ventricular Blood Cavity (LV)** - Label value: 500
2. **Right Ventricular Blood Cavity (RV)** - Label value: 600
3. **Left Atrial Blood Cavity (LA)** - Label value: 420
4. **Right Atrial Blood Cavity (RA)** - Label value: 550
5. **Myocardium of the Left Ventricle (Myo)** - Label value: 205
6. **Ascending Aorta (AO)** - Label value: 820; defined as the aortic trunk from the aortic valve to the superior level of the atria.
7. **Pulmonary Artery (PA)** - Label value: 850; defined as the initial segment from the pulmonary valve to the bifurcation point.

**Note on Great Vessels:** The great vessels of interest, specifically the ascending aorta and pulmonary artery, are clearly defined due to variations in the fields of view across different scans. This consistent definition is essential for ensuring uniformity across evaluations. During the assessment, segmentation results for these vessels will be truncated to the average lengths measured in healthy subjects. However, participants are encouraged to extend their segmentation beyond these predefined lengths. Our provided manual segmentations also cover areas extending beyond the defined trunk measurements.

The selected papers will be published as part of the MICCAI Satellite Events joint LNCS proceedings.([see previous proceedings](https://link.springer.com/book/10.1007/978-3-319-75541-0)).

Topics may cover (not exclusively):

- Cardiac anatomy segmentation
- Cardiac image registration
- Cardiac modeling
- Domain adaptation
- Model generalization

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
      <td>100</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C and D</td>
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
      <td>40</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>B</td>
      <td>100</td>
      <td>CT</td>
    </tr>
    <tr>
      <td>C/D</td>
      <td>40</td>
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
      <td>CTA</td>
    </tr>
  </tbody>
</table>
</div>

### Data Acquisition

The cardiac CT/CTA data were acquired using standard coronary CT angiography protocols. At Center A, imaging was conducted with 64-slice Philips CT scanners. Center B used a dual-source SIEMENS CT scanner or a high-end, single-source GE CT scanner. The cardiac MRI data were obtained using various steady-state free precession (SSFP) sequences, adaptable for both free-breathing and breath-held imaging. Centers C and D employed either a 1.5T Philips scanner or a Siemens Avanto 1.5T scanner for scanning. Center E utilized Philips Achieva 1.5T scanners. Center F conducted its imaging with a Siemens Avanto 1.5T scanner. This diversity in the data acquisition process across centers underscores the extensive scope and scale of the dataset.

### Guidance for Training Strategies

To support an informed training process, details about the imaging centers will be provided alongside the cases, as indicated by the case naming (see Fig. 2). Participants are strongly encouraged to utilize this information when designing their training strategies, with a focus on achieving high generalization capability. This approach aims to foster the development of algorithms that perform robustly not only under controlled conditions but also across a variety of real-world clinical environments.

## Metrics & Ranking

### Metrics

The performance of segmentation results will be assessed through: 

- Dice Similarity Coefficient (DSC), 
- Hausdorff Distance (HD), and 
- Average Surface Distance (ASD). 

### Aim

Accuracy and robustness are crucial for the success of automatic WHS algorithms in clinical settings. Therefore, the final evaluation during the test phase will include images from both centers that have been involved in previous phases and a new, unseen center (detailed in the Data Information section). 

### Rank

Outstanding contributions will be recognized with awards, similar to [MM-WHS 2017](https://zmiclab.github.io/zxh/0/mmwhs/)<d-cite key="whs3"></d-cite> . Submissions will be evaluated based on
- the test results,
- the novelty of their methodologies, 
- the quality of their manuscript, and
- the clarity of their presentation.

For test results, both in-sample performance from seen centers and generalization capabilities at the unseen center will be considered. The empirical results will be ranked by averaging the performance scores from both scenarios.


## Rules

- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **External data sets and pre-trained models are not allowed in this track.** The solutions must be developed using only the data provided within the scope of this track and cannot leverage any external datasets or models for assistance.

## Registration

Please register [here](http://zmic.org.cn/care_2025/eval/register?track=WHS%2B%2B) to participate in the challenge and get access to the dataset!!


## Submission Guidance

### Model Submission
After registration, we will assign participants an account to login into our [WHS++ evaluation platform](http://zmic.org.cn/care_2025/eval/login?track=WHS%2B%2B). Participants can directly upload your predictions on the validation data (in nifty format) via the website. Note that evaluation of validation data will be allowed up to 10 times for each task per team. For fair comparison, the test dataset will remain unseen. Participants need to submit their [docker models](http://zmic.org.cn/care_2025/test_submission) for testing.
### Paper Submission
Please refer to our [paper submission guidance](/care_2025/paper_submission).

## Timeline
The schedule for this track is as follows. All deadlines(DDLs) are on 23:59 in Pacific Standard Time.

<table class="table table-sm table-hover border-bottom">
    <tr>
    <td class="text-left"><strong>Training Data Release</strong></td>
    <th scope="row" style="width: 60%" class="text-right">April 10, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Validation Phase start</strong></td>
    <th scope="row" style="width: 60%" class="text-right">May 1, 2025</th>
    </tr>
    <tr>
    <td class="text-left"><strong>Test data release</strong></td>
    <th scope="row" style="width: 60%" class="text-right">June 20, 2025</th>
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

@article{Zhuang2019evaluation,
  Author={Zhuang, Xiahai and Li, Lei and Payer, Christian and Stern, Darko and Urschler, Martin and Heinrich, Mattias P and Oster, Julien and Wang, Chunliang and Smedby, {\"O}rjan and Bian, Cheng and others},
  Title={Evaluation of algorithms for multi-modality whole heart segmentation: an open-access grand challenge},
  Journal={Medical image analysis},
  Year={2019},
  Volume={58},
  Pages={101537}，
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

## Contact

If you have any problems about the WHS++ track, please contact [Dr. Wangbin Ding](mailto:dingwangbin@fjmu.edu.cn) or [Xicheng Sheng](mailto:xcsheng22@m.fudan.edu.cn).
