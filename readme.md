README.md

Project Title & Description
 Multimodal EO-SAR Binary Change Detection using U-Net
This project presents an end-to-end deep learning framework for binary change detection using multimodal Earth Observation (EO) optical imagery and Synthetic Aperture Radar (SAR) imagery for post-disaster building damage assessment. The primary objective is to identify structurally damaged regions from temporally aligned EO-SAR image pairs through semantic segmentation techniques.
The implemented pipeline includes TIFF image preprocessing, binary label remapping, multimodal EO-SAR feature fusion, semantic segmentation, quantitative evaluation, and qualitative visualization. EO RGB channels and SAR imagery were fused into a unified four-channel representation to improve multimodal feature learning under challenging remote sensing conditions.
A U-Net architecture with a ResNet34 encoder backbone was implemented as the baseline segmentation model due to its strong spatial feature preservation capability and computational efficiency. During experimentation, severe class imbalance and SAR speckle noise were identified as major challenges affecting segmentation performance. To address this issue, Weighted Binary Cross Entropy combined with Dice Loss was implemented to improve sensitivity toward sparse damaged regions and stabilize optimization.
The final system was evaluated using IoU, Precision, Recall, F1 Score, and confusion matrix analysis on validation and test datasets. The project establishes a complete EO-SAR multimodal segmentation workflow and provides a strong baseline for future research involving transformer-based fusion architectures, advanced imbalance-aware loss functions, and SAR-specific preprocessing techniques.
Requirements
numpy==2.2.6
pandas==2.3.3
matplotlib==3.10.7
opencv-python==4.x
torch==2.x
torchvision==0.x
albumentations==1.x
segmentation-models-pytorch==0.x
scikit-learn==1.x
seaborn==0.13.2
tqdm==4.x
Pillow==12.0.0

Environment Setup
Create a dedicated Python environment and install all required dependencies before running the project.
Conda Environment Setup
bash id=l9q2zm
conda create -n galaxeye python=3.10
conda activate galaxeye
pip install -r requirements.txt
Verify Installation
python --version
pip list
Dataset Structure
The dataset consists of paired Earth Observation (EO) optical imagery and Synthetic Aperture Radar (SAR) imagery organized into training, validation, and test splits. The expected directory structure after placing the dataset is shown below.



data/
├── train/
│   ├── pre-event/
│   ├── post-event/
│   ├── target/
│   ├── remapped_labels/
│   └── binary_masks/
│
├── val/
│   ├── pre-event/
│   ├── post-event/
│   ├── target/
│   ├── remapped_labels/
│   └── binary_masks/
│
└── test/
    ├── pre-event/
    ├── post-event/
    ├── target/
    ├── remapped_labels/
    └── binary_masks/
Training
The model was trained using a U-Net segmentation architecture with a ResNet34 encoder backbone on multimodal EO-SAR imagery. Weighted Binary Cross Entropy combined with Dice Loss was implemented to address severe class imbalance and improve damaged region sensitivity.
Training Configuration
- Architecture: U-Net
- Encoder: ResNet34
- Input Channels: 4 (EO RGB + SAR)
- Optimizer: AdamW
- Learning Rate: 1e-4
- Batch Size: 4
- Epochs: 15
- Loss Function: Weighted BCE + Dice Loss
Training Command
Run training from scratch using:
python train.py --config config.yaml
Configuration File
Example configuration:
learning_rate: 0.0001
batch_size: 4
epochs: 15
optimizer: AdamW
loss: Weighted BCE + Dice
image_size: 256
threshold: 0.3
encoder: resnet34
seed: 42

Training Notes
Severe class imbalance required weighted loss functions to prevent prediction collapse toward the background class.
Threshold tuning was performed to improve recall performance on sparse damaged regions.
Training was executed locally using the PyTorch MPS backend on Apple Silicon hardware.
Evaluation
python eval.py --data_path /path/to/test --weights /path/to/checkpoint.pth
Model Weights
Upload final_model.pth to Google Drive or HuggingFace and place public link here.
Results
The trained model was evaluated on both validation and test datasets using standard semantic segmentation metrics including IoU, Precision, Recall, F1 Score, and confusion matrix analysis.
Evaluation Command
Run evaluation using:
Evaluation Metrics
The following metrics were used for performance analysis:
Intersection over Union (IoU)
Precision
Recall
F1 Score
Confusion Matrix


Confusion Matrix
[[4921800   86351]
 [  21450   16671]]]
Evaluation Metrics
The following metrics were used for performance analysis:
Intersection over Union (IoU)
Precision
Recall
F1 Score
Confusion Matrix
Citation / References
- U-Net: Convolutional Networks for Biomedical Image Segmentation - ChangeFormer - PyTorch Documentation - segmentation-models-pytorch - EO-SAR change detection research papers
Author
P Deepak B.E. – Artificial Intelligence and Data Science
