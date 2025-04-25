---
layout: distill
title: MyoPS++
description: Myocardial Pathology Segmentation
permalink: /track4/
bibliography: reference.bib
toc:
  - name: Motivation
  - name: Task
  - name: Data 
  - name: Metrics
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
{% include figure.liquid loading="eager" path="/assets/img/myops.png" class="img-fluid" zoomable=true caption="Figure 1. Myocardial pathology segmentation and its challenges. (A) Myocardial Pathology Segmentation: Scar and edema regions are marked in green and yellow, respectively. (B) Challenges of Myocardial Pathology Segmentation: The challenges include multi-center data, missing sequences, and misalignments in multi-sequence CMR images." %}

Myocardial infarction (MI) is a leading cause of mortality and disability worldwide. Accurate assessment of myocardial viability is critical for the diagnosis and management of MI patients <d-cite key="myops1"></d-cite>. This track focuses on myocardial pathology segmentation (MyoPS) using multi-sequence cardiac magnetic resonance (CMR) imaging. The primary objective is to classify myocardial regions into healthy myocardium, scar tissue, and edema based on multi-sequence CMR data from MI patients.

## Task

The challenge emphasizes addressing key real-world issues, including the integration of multi-continent datasets, handling missing sequences from certain centers, and mitigating misalignments in multi-sequence CMRs. This track seeks innovative solutions that tackle these challenges, leveraging diverse and complex multi-sequence CMR datasets to advance the accuracy and reliability of MyoPS <d-cite key="myops2"></d-cite>, <d-cite key="myops3"></d-cite>.


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
    <!-- <tr>
      <td>D</td>
      <td>50</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium  and right ventricle</td>
    </tr> -->
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
      <td>Scar, left ventricle,  myocardium and and right ventricle</td>
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
      <td>I</td>
      <td>16</td>
      <td>LGE, T2 and bSSFP</td>
      <td>Scar, edema, left ventricle,  myocardium and right ventricle</td>
    </tr>
  </tbody>
</table>
</div>

### Pre-Processing

In this track, LGE and T2 images are derived from the end-diastolic phase of the cardiac cycle. Consequently, we have extracted the end-diastolic phase of balanced steady-state free precession (bSSFP, C0) for this track.

It is important to note that the LGE, T2, and C0 images are initially unaligned. The dataset is available in two versions: one version has been pre-aligned using the [MvMM method](https://zmiclab.github.io/zxh/0/zxhproj), while the other remains unaligned. **The test phase will utilize the version that has been aligned using the MvMM method.**

### Data Format
Each CMR sequence and gold standard label of patients will be provided in the NIfTI format as follows:
- [Patient Identifier]_LGE.nii.gz
- [Patient Identifier]_T2.nii.gz
- [Patient Identifier]_C0.nii.gz
- [Patient Identifier]_gd.nii.gz (gold standard label)

## Metrics

The performance of scar and edema segmentation results will be evaluated by：
- **Dice Similarity Coefficient (DSC)**
- **Precision (PRE)**
- **Sensitivity (SEN)**
- **Hausdorff Distance (HD)**
<!-- - **Specificity (SPE)** -->

Note that the track will provide an open platform for research groups to [validate](http://zmic.org.cn/care_2025/eval/scoreboard?track=MyoPS%2B%2B) and [test](http://zmic.org.cn/care_2025/test_submission) their methods. For fair comparison, the test dataset will remain unseen. Participants need to submit their [docker models](http://zmic.org.cn/care_2025/docker_tutorial) to our platform for testing.

<!-- 

### Ranking

The best work, following the precedent of [MyoPS 2020](https://zmiclab.github.io/zxh/0/myops20/), will be recognized with awards. A work is assessed based on several key criteria:**Test Results**, **Ggeneralizability of Methodologies** and **Quality of the Manuscript**.

- **Test Results**: The performance of the methods as demonstrated by the test outcomes.
- **Novelty of Methodologies**: The originality and **generalizability** in the proposed methods.
- **Quality of the Manuscript**: The clarity, organization, and correctness of the written submission. The selected papers will be published in our proceedings [see previous proceedings](https://link.springer.com/book/10.1007/978-3-030-65651-5). 
- **Presentation of Their Paper**: The effectiveness of the oral or poster presentation in conveying the work.

-->

## Rules
- **Only automatic methods are acceptable.** Participants must utilize algorithms that do not require manual intervention or human-assisted processes for the segmentation task.
- **Pre-trained models are  allowed in this track.** The solutions could be developed with pre-trained fundation models, such as SAM, CLIP, and MedSAM.


## Registration
Please [**sign up**](http://zmic.org.cn/care_2025/eval/register?track=MyoPS%2B%2B) to join this track.

## Submission Guidance

### Model Submission
After registration, we will assign participants an account to login into our [MyoPS++ evaluation platform](http://zmic.org.cn/care_2025/eval/login?track=MyoPS%2B%2B). Participants can directly upload your predictions on the validation data (in nifty format) via the website. Note that evaluation of validation data will be allowed up to 10 times for each task per team. For fair comparison, the test dataset will remain unseen. Participants need to submit their [docker models](http://zmic.org.cn/care_2025/test_submission) for testing.
### Paper Submission

Please refer to our [paper submission guidance](/care_2025/paper_submission).



## Timeline
The schedule for this track is as follows. All deadlines(DDLs) are on 23:59 in Pacific Standard Time.

<table class="table table-sm table-hover border-bottom">
    <tr>
    <td class="text-left"><strong>Training Data Release</strong></td>
    <th scope="row" style="width: 60%" class="text-right">April 25, 2025</th>
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

@article{li2023myops,
  title={MyoPS: A benchmark of myocardial pathology segmentation combining three-sequence cardiac magnetic resonance images},
  author={Li, Lei and Wu, Fuping and Wang, Sihan and Luo, Xinzhe and Mart{\'\i}n-Isla, Carlos and Zhai, Shuwei and Zhang, Jianpeng and Liu, Yanfei and Zhang, Zhen and Ankenbrand, Markus J and others},
  journal={Medical Image Analysis},
  volume={87},
  pages={102808},
  year={2023},
  publisher={Elsevier}
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

## Contact

If you have any questions regarding the MyoPS++ track, please feel free to contact:

- Dr. Wangbin Ding: [dingwangbin@fjmu.edu.cn](mailto:dingwangbin@fjmu.edu.cn)
- Sihan Wang: [21110980009@m.fudan.edu.cn](mailto:21110980009@m.fudan.edu.cn)
- Yang Zhang: [zhangyang23@m.fudan.edu.cn](mailto:zhangyang23@m.fudan.edu.cn)

