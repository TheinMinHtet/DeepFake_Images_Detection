# DeepFake_Images_Detection
Deepfake_Images_Detection is a Deepfake Detection website where you can check if a video or photo is real or if it has been tampered with. It’s built for anyone who wants to make sure what they are seeing online is the truth.

## 🐍 Option 1: Run Locally with Python

1. Clone the repository:

```bash
git clone https://github.com/TheinMinHtet/DeepFake_Images_Detection
cd DeepFake_Images_Detection
```

2 Create a virtual environment:
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Mac/Linux
source venv/bin/activate
```

3.Install dependencies:
```bash
pip install -r requirements.txt
```

4.Run the FastAPI server:
```bash
python -m app/main.py
```

5.Open the API docs in your browser:
```bash
http://localhost:8000/docs
```
------------------------------------
## 🐳 Option 2: Run with Docker

1.Clone the repository:
```bash
git clone https://github.com/TheinMinHtet/DeepFake_Images_Detection
cd DeepFake_Images_Detection
```

2.Build the Docker image:
```bash
docker build -t DeepFake_Images_Detection .
```

3.Run the Docker container:
```bash
docker run -p 8000:8000 -v "C:/Users/Asus/Desktop/weights:/app/weights" DeepFake_Images_Detection
```
4.Access API docs:
```bash
http://localhost:8000/docs
```
## 🧠 Model Weights
The deepfake detection model weights (`best_fusion_srm_model.pth`) are too large for GitHub. You must download them separately from Hugging Face.

1. Visit the [DeepFake_Images_Detection](https://huggingface.co/Thein777/DeepFake_Images_Detection/tree/main).
2. Download the `best_fusion_srm_model.pth` file.
3. Create a folder in the project root: `app/weights/`.
4. Place the downloaded file inside that folder.

## How to call from frontend
1.Do the steps that i provided and then check http://127.0.0.1:8000 it shows {Deepfake API is running}.

2.then use http://127.0.0.1:8000/predict as a endpoint.

## Training Code 
If you want to know how to train this model more details you can check in this (https://huggingface.co/Thein777/DeepFake_Images_Detection/tree/main) in this you can also see the weights of the model

## Training Dataset
If you want to check the training dataset you can check in this (https://huggingface.co/datasets/Thein777/real_fake_low_high_quality_images/tree/main)

---------------------------------------------------------------------------------------------------------------

## Model Description
DeepFake_Images_Detection is a deep learning project where I trained a fusion PyTorch model for detecting deepfake images. The model uses SigLIP (prithivMLmods/deepfake-detector-model-v1) as a backbone and a custom ArtifactCNN with SRM layers to analyze subtle artifacts in both low- and high-quality images. It outputs whether an image is real or manipulated along with a confidence score.

## Limitation/Warning
Trained on specific datasets; results may vary on new data distributions.

## About Training Dataset
Training and validation datasets included real and fake images at both low (LQ) and high quality (HQ).LQ:HQ - 2:1 Because i used Siglip as a backbone so it is already trained and seen too many high quality images.

training data - HQ (real - 145 / fake - 145) | LQ (real - 290 / fake -290) Total = 870

validation data - HQ (real - 29 / fake - 29) | LQ (real - 58 / fake -58) Total = 174

TOTAL = 1044 images

Augmentation techniques such as face cutouts were applied to improve robustness.

# Classification Evaluation
The model achieved 97.9% training accuracy and 97.7% validation accuracy on training dataset and validation dataset, demonstrating strong performance and robustness for real-world detection.
=Training accuracy: 97.9%
=Validation accuracy: 97.7%

## Model Architecture
The proposed architecture is a fusion-based deepfake detection model that combines a pretrained Hugging Face Transformers implementation of SigLIP (loaded from prithivMLmods/deepfake-detector-model-v1) with a custom SRM-enhanced CNN branch. SigLIP acts as the semantic backbone, where most of its parameters are frozen to preserve pretrained visual representations, and only the final classifier layer and the last transformer block (layers.11) are unfrozen for fine-tuning on the deepfake dataset. In parallel, a custom ArtifactCNN branch processes SRM-filtered noise maps to capture low-level manipulation artifacts. The embeddings from both branches are concatenated and passed through a fusion classifier (Linear → BatchNorm → ReLU → Dropout → Linear) to produce binary predictions (real vs fake). Training is performed using AdamW with different learning rates for each component (lower LR for SigLIP, higher LR for newly initialized layers), cross-entropy loss, early stopping with patience of 10 epochs, and the best model is saved based on validation loss.

## Future Enhancement
Larger & More Diverse Dataset: Train on a broader range of deepfake sources, ethnicities, lighting conditions, and compression levels to improve generalization.
