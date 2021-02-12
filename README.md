# Convolutional Neural Network for Medical Imaging Analysis - Abnormality detection in mammography 

This project has the aim to detect abnormality in mammography.

## Dataset

The dataset we will focus on is CBIS DDSM: Curated Breast Imaging Subset of Digital Database for Screening Mammography. In the images are present two types of abnormality: mass or calcification. Then we can distinguish between benign or malignant. For this reason we have the following classes:
- [Mass, Benign (with or without callback)]
- [Mass, Malignant]
- [Calcification, Benign]
- [Calcification, Malignant]

Original images have a high resolution, e.g. 3000x4000 and they are grayscale images with a depth of 16bit.
We use a *numpy arrays* containing images and labels from training and test sets.
