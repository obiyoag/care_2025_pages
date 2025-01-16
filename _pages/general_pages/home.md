---
layout: home
title: Home
permalink: /
---

## Motivation
Many foundation models for medical image analysis, such as Segment Anything Model (SAM), have been released and proved to be useful in multiple tasks. However, their effectiveness on real world medical imaging data has not been explored. For example, specific images targeted on organs with large deformation, i.e., heart and liver, exhibit greater challenges for analysis.

## Challenges
First, the misalignment caused by the respiratory motion and cardiac pulsation increases the complexity of performing joint analysis on these data. Second, the inhomogeneity of real-world medical images poses a challenge, including the diversity of modality and the distribution shift caused by collection from various centers. Third, it could be more challenging for those foundation model to work on irregular ROIs, such as lesions or scars, whose size can be very small and shape irregular. Hence, developing effective and efficient transfer learning approaches to fully utilize those foundation models for real world medical image segmentation is of great values.

## Our Contribution
In this challenge, we set up a fair and public stage for developing and validating algorithms and applications of transferring foundation models to diverse real-world medical images to address specific practical medical image analysis problems, as well as using conventional methods without pre-trained models.

## Datasets
Four specific datasets will be released grouped by clinical requirements, targeted on organs with grand large deformation, i.e., heart and liver, and consisting of over 1250 patients from three continents. The diversity of datasets manifests in the following aspects, i.e., multi-continents: collected from over 18 centers across three continents, multi-modality: various modalities are encompassed, misalignment: inherent misalignment exists caused by the respiratory motion and cardiac pulsation, and missing data: refers to the modality missing occurred in practice.

## Tracks
Five tracks will be held in this challenge, including one comprehensive issue and four specific tracks with corresponding images and clinical problems:
1. Transferring Foundation Models for Multi-center Real-World Medical Image Analysis ([TFM4MedIA](/care_2025/track1))
2. Left Atrial and Scar Quantification & Segmentation ([LAScarQS++](/care_2025/track2))
3. Liver Fibrosis Quantification and Analysis ([LiQA](/care_2025/track3))
4. Myocardial Pathology Segmentation ([MyoPS++](/care_2025/track4))
5. Whole Heart Segmentation ([WHS++](/care_2025/track5))

Specifically, the first track aims at a uniform Transferring Foundation model for the generality across the other four tracks, namely to address all or partial tasks. The uniform model will undergo comprehensive evaluation, with various metrics being integrated for ranking purposes.

