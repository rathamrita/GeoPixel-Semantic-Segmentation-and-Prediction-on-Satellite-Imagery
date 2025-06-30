# PROJECT : Pixel wise segmentation of Satellite images
# METHODS

# 1. Dataset
-> Source : https://www.kaggle.com/datasets/humansintheloop/semantic-segmentation-of-aerial-imagery
-> The dataset consists of aerial imagery of Dubai obtained by MBRSC satellites and annotated with pixel-wise semantic segmentation in 6 classes. The total volume of the dataset is 72 images grouped into 6 larger tiles. The classes are:
Building: #3C1098
Land (unpaved area): #8429F6
Road: #6EC1E4
Vegetation: #FEDD3A
Water: #E2A929
Unlabeled: #9B9B9B

# 2. Preprocessing Pipeline Overview
This preprocessing pipeline prepares satellite imagery and corresponding mask data for training a deep learning model on semantic segmentation tasks. It involves several key steps:

Image Normalization and Patching:
Raw satellite images are cropped to ensure dimensions are divisible by a defined patch size (256×256), then split into smaller patches. Normalization is applied to each patch using Min-Max scaling, ensuring the input data is numerically stable and standardized for model training.

Mask Preparation and Patching:
RGB segmentation masks are similarly patched. Each patch corresponds spatially to its paired image patch, maintaining alignment between data and labels.

Color-to-Class Conversion:
The RGB color-coded masks are converted into single-channel class label maps. Each unique color represents a specific land cover class (e.g., building, water, road), which is mapped to a corresponding integer label (0–5). This is essential for converting human-annotated visual data into machine-readable targets.

Data Pairing and Visualization:
The code validates and visualizes a random image-mask patch pair to ensure integrity. This serves as a sanity check before feeding the data into a model.

# 3. Model Training
Model Training: Multi-Class U-Net for Satellite Image Segmentation

Data Splitting: The preprocessed dataset is split into training and test sets to enable performance evaluation on unseen data.

Model Architecture: A custom multi-class U-Net is implemented to effectively capture spatial features and reconstruct class maps at pixel level.

Custom Loss Function: A composite loss combining Dice Loss and Categorical Focal Loss is used to balance class imbalance and penalize hard-to-classify regions.

Evaluation Metrics: Accuracy and Jaccard Coefficient are tracked to monitor both per-pixel accuracy and overlap quality between predictions and ground truth.

# 4. Training Monitoring
To monitor model learning progress and evaluate performance in real-time, a custom Keras callback is implemented. 

What It Tracks:
Training and Validation Loss: Helps understand how well the model fits the data and whether it's overfitting.

Jaccard Coefficient (IoU): A crucial metric for segmentation tasks, indicating the overlap between predicted and true class regions.

Custom Callback Features:
Real-time plotting of training curves during model fitting.

Dual-panel graphs display:

Left: Loss curves (training vs. validation) on a log scale.

Right: Jaccard Coefficient curves (training vs. validation) on a log scale.

Enables early visual detection of underfitting, overfitting, or training instability.


![image](https://github.com/user-attachments/assets/e89bffaf-d6c6-4733-aaf7-a14d8b461cd9)
