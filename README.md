# **Convolutional Neural Network for Medical Imaging Analysis - Abnormality detection in mammography** 

This project has the aim to detect abnormality in mammography.

## **Dataset**

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

In light of the procedure described above, particular attention should be paid to the structure of the input tensors:
- odd indices `[2i + 1 for i in range(0,len(tensor)/2)]` will refer to abnormality patches
- previous even indices `[2i for i in range(0,len(tensor)/2)]` will refer to respective baseline patches
You will be able to load the arrays using `numpy load` function.

## **Project structure**
The project is structured with the following files in .ipynb format because performed on Colab notebooks:

1. TASK 1: Perform the classification building a CNN from scratch:
    - [Scratch_CNN_2.1.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/Scratch_CNN_2.1.ipynb): in this notebook we perform the classification between mass and calcification.
    - [Scratch_CNN_2.2.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/Scratch_CNN_2.2.ipynb): in this notebook we perform the classification between benign and mailignant.
2. TASK 2: Perform the classification using a pre-trained network:
    - [PreTrained_CNN_3.1.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/PreTrained_CNN_3.1.ipynb): in this notebook we perform the classification between mass and calcification.
    - [PreTrained_CNN_3.2.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/PreTrained_CNN_3.2.ipynb): in this notebook we perform the classification between benign and mailignant.
3. TASK 3: Perform the classification to distinguish the abnormality considering also the baseline patches:
    - [BaselineCNN.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/BaselineCNN.ipynb): in this notebook we perform the classification between mass and calcification but considering also the baseline patches. For this reason we have used a **Siamese Network**.
4. TASK 4: Perform the classification task using an Ensamble method:
    - [Ensamble1.ipynb](https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/Ensamble1.ipynb): in this notebook we perform the classification between mass and calcification using an **Ensamble method**.
    - [Ensamble2.ipynb]((https://github.com/lorepas/CNN_Medical_Imaging_Analysis/blob/main/Ensamble2.ipynb): in this notebook we perform the classification between benign and malignant using an **Ensamble method**.
