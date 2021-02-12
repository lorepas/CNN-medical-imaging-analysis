# Convolutional Neural Network for Medical Imaging Analysis - Abnormality detection in mammography 

This project has the aim to detect abnormality in mammography.

## Dataset

The dataset we will focus on is CBIS DDSM: Curated Breast Imaging Subset of Digital Database for Screening Mammography. In the images are present two types of abnormality: mass or calcification. Then we can distinguish between benign or malignant. For this reason we have the following classes:
- Mass, Benign (with or without callback)
- Mass, Malignant
- Calcification, Benign
- Calcification, Malignant

Original images have a high resolution, e.g. 3000x4000 and they are grayscale images with a depth of 16bit.
We use a **numpy arrays** containing images and labels from training and test sets.
The steps performed on each original image are described below:
- the abnormality patch has been extracted from the original image according to the binary mask;
- a patch of healthy tissue (baseline patch) adjacent to the abnormality patch has been extracted from the original image (left, right, top or bottom - no overlap). Both abnormality patch and baseline patch have been added to the images tensor; in other words, an abnormality patch has been ignored if a related baseline patch could not be extracted.
- both abnormality patch and baseline patch have been resized to shape (150x150) using OpenCV resize function: `cv2.resize(img, dsize=(shape, shape), interpolation=cv2.INTER_NEAREST)`
- class labels have been assigned to the patches according to the following mapping:
  - 0: Baseline patch
  - 1: Mass, benign
  - 2: Mass, malignant
  - 3: Calcification, benign
  - 4: Calcification, malignant
 - images of baseline patch and abnormality patch, and their related labels, have been added to distinct numpy arrays for images and labels.
  - train_tensor.npy: images tensor for training
  - train_labels.npy: labels tensor for training
  - public_test_tensor.npy: images tensor for test
  - public_test_labels.npy: images tensor for test
