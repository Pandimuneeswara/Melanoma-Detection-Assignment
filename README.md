# Melanoma Detection Using CNN
> Evaluvate the images and detect the presence of Melanoma using the Convolution Neural Network model


## Problem Statement
>To build a CNN based model which can accurately detect melanoma. Melanoma is a type of cancer that can be deadly if not detected early. It accounts for 75% of skin cancer deaths. A solution which can evaluate images and alert the dermatologists about the presence of melanoma has the potential to reduce a lot of manual effort needed in diagnosis.


### Dataset 
The dataset consists of 2357 images of 9 diseases, which were formed from the International Skin Imaging Collaboration (ISIC). All images were sorted according to the classification taken with ISIC.
The data set contains the following diseases:
- Actinic keratosis
- Basal cell carcinoma
- Dermatofibroma
- Melanoma
- Nevus
- Pigmented benign keratosis
- Seborrheic keratosis
- Squamous cell carcinoma
- Vascular lesion

### Project Pipeline

1. Data Reading/Data Understanding → Defining the path for train and test images 
2. Dataset Creation→ Create train & validation dataset from the train directory with a batch size of 32. Also, make sure you resize your images to 180*180.
3. Dataset visualisation → Create a code to visualize one instance of all the nine classes present in the dataset classes 
4. Model Building & training:
    - Create a CNN model, which can accurately detect 9 classes present in the dataset. Use ```layers.experimental.preprocessing.Rescaling``` to normalize pixel values between (0,1). The RGB channel values are in the `[0, 255]` range. This is not ideal for a neural network. Here, it is good to standardize values to be in the `[0, 1]`.
    - Use adam optimiser for model training
    - Train the model for ~20 epochs
	- The output of this model is overfitting.
5. Choose an appropriate data augmentation strategy to resolve overfitting
6. Model Building & training on the augmented data :
    - Use the model -1
	- Add Augmentation layer with the model -1
	- Add a dropout layer to handle the overfitting
	- Train the model for ~20 epochs
    - This resolve the overfitting. However, model -2 resulted underfitting
7. Class distribution: 
    - Validate the class distribution. It is imbalanced.
    - Add a class balance to handle the class imbalance to over come with the underfitting.	
8. Handling class imbalances: Rectify class imbalances present in the training dataset with [Augmentor](https://augmentor.readthedocs.io/en/master/) library.
9. Model Building & training on the rectified class imbalance data :
    - Use the model -2 using the new test data which is created using the Augmentor
    - Train the model for 50 epochs
    - Now the model underfitting is also resolved and the accuracy is 85% on Training data and 82% on Validation data.

### Python Packages:
- Numpy
- Tensorflow
- Pandas
- Seaborn
- Matplotlib

## Conclusions

- Model -1: Basic Model
  - Model Training is not having good accuracy - Training accuracy 81% and Validation Accuracy 53%  
  - Model was **Overfitting**

- Model -2: Model 1 + Dropout Layers + Data Augmentation
  - Dropout Layers Added
  - Data Augmentation layer was added
  - Accuracy of the model is reduced compare to model -1 - Training Accuracy 56% and Validation Accuracy 51%
  - Model was **Underfitting** due to the class imbalance

- Model -3: Model 2 + Class balanced Dataset
  - To fix the class imbalance issue, Dataset Added using Augmentor (500 images added per class)
  - Same Model 2 was used.
  - The accuracy of the model is improved. So, handling the class imbalance give better result and this model is reliable model.