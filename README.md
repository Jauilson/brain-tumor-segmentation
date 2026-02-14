# 🧠 Brain Tumor Segmentation using U-Net

<div align="center">

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)

*Automated brain tumor segmentation in MRI images using deep learning*

[View Demo](#results) · [Report Bug](https://github.com/jauilson/brain-tumor-segmentation/issues) · [Request Feature](https://github.com/jauilson/brain-tumor-segmentation/issues)

</div>

---

## 📋 Table of Contents

- [About](#about)
- [Key Features](#key-features)
- [Dataset](#dataset)
- [Model Architecture](#model-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Project Context](#project-context)
- [Technical Skills](#technical-skills)
- [Future Work](#future-work)
- [Author](#author)
- [References](#references)

---

## 🎯 About

This project implements an automated brain tumor segmentation system using the **U-Net** deep learning architecture. The model is trained on the **BraTS 2019** (Brain Tumor Segmentation Challenge) dataset, which contains 484 multi-modal MRI scans.

The primary goal is to accurately segment brain tumors in MRI images, providing quantitative information about tumor size, shape, and location to assist in clinical diagnosis and treatment planning.

### Why This Matters

- **Clinical Impact:** Automated segmentation reduces manual annotation time and inter-observer variability
- **Treatment Planning:** Precise tumor boundaries are critical for radiation therapy and surgical planning
- **Research Value:** Enables large-scale quantitative analysis of brain tumors
- **Educational Purpose:** Demonstrates practical application of deep learning in medical imaging

---

## ✨ Key Features

- **U-Net Architecture** - State-of-the-art encoder-decoder network for medical image segmentation
- **BraTS 2019 Dataset** - Trained on standardized, multi-institutional brain tumor MRI data
- **Comprehensive Metrics** - Evaluation using Dice coefficient, IoU, and pixel accuracy
- **Visualization Tools** - Built-in functions to visualize segmentation results
- **Model Checkpointing** - Automatic saving of best-performing models
- **Easy to Use** - Well-documented Jupyter notebook with step-by-step execution

---

## 📊 Dataset

### BraTS 2019 (Brain Tumor Segmentation Challenge)

- **Source:** [Medical Image Computing and Computer Assisted Intervention (MICCAI)](https://www.med.upenn.edu/sbia/brats2019/data.html)
- **Size:** 484 training cases, 66 validation cases
- **Modalities:** T1, T1-contrast, T2, FLAIR MRI sequences
- **Format:** NIfTI (.nii.gz)
- **Resolution:** Variable (240x240x155 typical)
- **Labels:** Background, Necrotic/Non-enhancing tumor, Edema, Enhancing tumor

### Data Preprocessing

1. **Normalization:** Min-max normalization to [0, 1] range
2. **Slice Extraction:** Middle axial slice extraction from 3D volumes
3. **Resizing:** Standardization to 128x128 pixels
4. **Binarization:** Tumor vs. background classification

---

## 🏗️ Model Architecture

### U-Net Architecture

The U-Net architecture consists of:

**Encoder (Contracting Path):**
- 4 encoder blocks with increasing filters (64 → 128 → 256 → 512)
- Each block: 2 Conv2D layers + BatchNorm + MaxPooling

**Bottleneck:**
- Deepest layer with 1024 filters
- Captures high-level semantic features

**Decoder (Expanding Path):**
- 4 decoder blocks with decreasing filters (512 → 256 → 128 → 64)
- Each block: Upsampling + Skip connections + Conv2D layers

**Output:**
- Single Conv2D layer with sigmoid activation
- Binary segmentation (tumor vs. background)

```
Input (128x128x1) → [Encoder] → Bottleneck (8x8x1024) → [Decoder] → Output (128x128x1)
                          ↓ Skip Connections ↓
```

### Model Statistics

- **Total Parameters:** ~31M
- **Trainable Parameters:** ~31M
- **Input Shape:** (128, 128, 1)
- **Output Shape:** (128, 128, 1)

---

## 🚀 Installation

### Prerequisites

- Python 3.8+
- CUDA-compatible GPU (recommended)
- 8GB+ RAM
- Google Colab (optional, for cloud execution)

### Setup

1. **Clone the repository**

```bash
git clone https://github.com/jauilson/brain-tumor-segmentation.git
cd brain-tumor-segmentation
```

2. **Create virtual environment**

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**

```bash
pip install -r requirements.txt
```

4. **Download BraTS 2019 dataset**

- Register at [BraTS Challenge](https://www.med.upenn.edu/sbia/brats2019/registration.html)
- Download training data
- Extract to `data/` directory

### Google Colab Setup

1. Upload notebook to Google Drive
2. Open with Google Colab
3. Mount Google Drive
4. Upload dataset to Drive

---

## 💻 Usage

### Quick Start (Jupyter Notebook)

1. **Open the notebook**

```bash
jupyter notebook brain_tumor_segmentation.ipynb
```

2. **Run cells sequentially**
   - Configure paths in the Config class
   - Load and preprocess data
   - Train model
   - Visualize results

### Training Configuration

Modify the `Config` class to adjust hyperparameters:

```python
class Config:
    IMG_HEIGHT = 128
    IMG_WIDTH = 128
    BATCH_SIZE = 8
    EPOCHS = 50
    LEARNING_RATE = 1e-4
    VALIDATION_SPLIT = 0.2
```

### Running Training

```python
# Load dataset
X, y = load_dataset(config, max_samples=50)  # Use None for full dataset

# Split data
X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2)

# Train model
history = model.fit(
    X_train, y_train,
    validation_data=(X_val, y_val),
    batch_size=8,
    epochs=50,
    callbacks=callbacks
)
```

### Making Predictions

```python
# Load trained model
model = keras.models.load_model('results/best_unet_model.h5')

# Predict on new images
predictions = model.predict(X_test)

# Visualize results
visualize_predictions(model, X_test, y_test, num_samples=5)
```

---

## 📈 Results

### Quantitative Results

| Metric | Training | Validation |
|--------|----------|------------|
| **Loss** | 0.XXX | 0.XXX |
| **Accuracy** | XX.X% | XX.X% |
| **Dice Coefficient** | 0.XXX | 0.XXX |
| **IoU** | 0.XXX | 0.XXX |

*Note: Results will vary based on training duration and dataset size*

### Qualitative Results

Sample segmentation outputs will be generated in the `results/` directory:

- `training_history.png` - Training and validation curves
- `segmentation_results.png` - Side-by-side comparison of predictions
- `sample_data.png` - Dataset visualization

---

## 📚 Project Context

### Academic Background

This project was developed in **May 2023** as part of a research proposal for master's program application at the **Universidade Federal de Sergipe (UFS)**. The proposal was submitted to:

- **Advisor:** Prof. Dr. Daniel Oliveira Dantas
- **Department:** Departamento de Ciências da Computação
- **Institution:** Universidade Federal de Sergipe (UFS)

### Learning Journey

Following the initial proposal, I enhanced my knowledge by attending classes as a **guest student** with:

- **Professor:** Prof. Dr. Jugurta Rosa Montalvão Filho
- **Department:** Departamento de Engenharia Elétrica
- **Courses:** Pattern Recognition and Medical Image Processing

This hands-on project allowed me to:
- Apply theoretical knowledge in a practical setting
- Gain experience with medical image analysis
- Develop skills in deep learning and computer vision
- Contribute to the field of automated medical diagnosis

---

## 🛠️ Technical Skills

### Technologies Used

**Deep Learning:**
- TensorFlow 2.x
- Keras API
- U-Net architecture
- Convolutional Neural Networks

**Medical Image Processing:**
- NiBabel (NIfTI format)
- 3D volume processing
- Image normalization
- Data augmentation

**Data Science:**
- NumPy
- scikit-learn
- scikit-image
- Train-test splitting

**Visualization:**
- Matplotlib
- Training curve plotting
- Segmentation result visualization

**Development Tools:**
- Jupyter Notebook
- Google Colab
- Git/GitHub
- Virtual environments

---

## 🔮 Future Work

### Planned Improvements

1. **3D U-Net Implementation**
   - Process entire 3D volumes instead of 2D slices
   - Capture volumetric context for better segmentation

2. **Multi-class Segmentation**
   - Segment different tumor regions (necrotic, edema, enhancing)
   - Provide more detailed clinical information

3. **Data Augmentation**
   - Rotation, flipping, elastic deformation
   - Increase model robustness

4. **Attention Mechanisms**
   - Attention U-Net
   - Focus on relevant features

5. **Model Deployment**
   - Web application for clinical use
   - REST API for integration
   - Docker containerization

6. **Transfer Learning**
   - Pre-trained weights from similar tasks
   - Fine-tuning on smaller datasets

7. **Ensemble Methods**
   - Combine multiple models
   - Improve prediction reliability

---

## 👤 Author

**Jauilson Crisostomo da Silva**

Mechatronics Engineer | Data Science Enthusiast | Medical AI Researcher

- 🎓 **Education:** 
  - B.Sc. in Mechatronics Engineering - Universidade Tiradentes (2022)
  - M.Sc. in Electrical Engineering (interrupted) - UFS (2024-2025)

- 🔬 **Research Interests:** 
  - Medical Image Analysis
  - Deep Learning
  - Computer Vision
  - Pattern Recognition

- 📧 **Email:** jauilson@gmail.com
- 💼 **LinkedIn:** [linkedin.com/in/jauilson](https://linkedin.com/in/jauilson)
- 📄 **Lattes CV:** [lattes.cnpq.br/4402347929712204](http://lattes.cnpq.br/4402347929712204)
- 🐙 **GitHub:** [github.com/jauilson](https://github.com/jauilson)

---

## 📖 References

### Dataset

1. **BraTS 2019 Challenge**
   - Menze et al. "The Multimodal Brain Tumor Image Segmentation Benchmark (BRATS)", *IEEE Transactions on Medical Imaging*, 2015.
   - Website: https://www.med.upenn.edu/sbia/brats2019/data.html

### U-Net Architecture

2. **Original U-Net Paper**
   - Ronneberger, O., Fischer, P., & Brox, T. (2015). "U-Net: Convolutional Networks for Biomedical Image Segmentation". *MICCAI 2015*.
   - [arXiv:1505.04597](https://arxiv.org/abs/1505.04597)

### Related Work

3. **Brazilian Neuroscience Institute (BRAINN)**
   - "Estudo de Tendências em Neurotecnologia do BRAINN" (2021)
   - https://www.brainn.org.br/

4. **Medical Image Segmentation**
   - Mascarenhas LR, Ribeiro Júnior AS, Ramos RP. "Segmentação automática de tumores cerebrais em imagens de ressonância magnética". *Einstein (São Paulo)*, 2020.
   - DOI: 10.31744/einstein_journal/2020AO4948

5. **Deep Learning for Medical Imaging**
   - Zhou, S. K., Greenspan, H., & Shen, D. (Eds.). (2017). *Deep Learning for Medical Image Analysis*. Academic Press.

6. **Computational Analysis**
   - Tyagi, A. K. (Ed.). (2021). *Computational Analysis and Deep Learning for Medical Care: Principles, Methods, and Applications*. Wiley.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Prof. Dr. Daniel Oliveira Dantas** - For the initial research guidance
- **Prof. Dr. Jugurta Rosa Montalvão Filho** - For the pattern recognition knowledge
- **BraTS Challenge Organizers** - For providing the dataset
- **Medical Image Computing Community** - For advancing the field

---

## 📞 Contact

For questions, suggestions, or collaborations, please feel free to reach out:

- **Email:** jauilson@gmail.com
- **LinkedIn:** [linkedin.com/in/jauilson](https://linkedin.com/in/jauilson)
- **GitHub Issues:** [Open an issue](https://github.com/jauilson/brain-tumor-segmentation/issues)

---

<div align="center">

Made with ❤️ by [Jauilson Crisostomo da Silva](https://github.com/jauilson)

⭐️ If you find this project useful, please consider giving it a star!

</div>
