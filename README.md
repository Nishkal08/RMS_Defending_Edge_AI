# Defending Edge AI in Healthcare

### A Robust and Secure Approach

**An experimental framework for evaluating adversarial robustness, federated learning security, and privacy-oriented aggregation in Edge AI healthcare systems.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyTorch](https://img.shields.io/badge/Framework-PyTorch-orange)
![Deep Learning](https://img.shields.io/badge/Deep%20Learning-CNN--LSTM-purple)
![Federated Learning](https://img.shields.io/badge/Federated%20Learning-Experimental-green)
![Domain](https://img.shields.io/badge/Domain-Healthcare-red)

---

## Overview

Edge Artificial Intelligence enables healthcare applications to process medical signals locally, reducing reliance on centralised cloud infrastructure. However, deploying AI models in healthcare introduces security challenges, including adversarial input manipulation, malicious federated model updates, and privacy risks during collaborative learning.

**Defending Edge AI in Healthcare** investigates these challenges through an experimental ECG classification framework based on a CNN-LSTM architecture and the MIT-BIH Arrhythmia heartbeat dataset.

The project evaluates white-box adversarial attacks, black-box transfer attacks, and federated model poisoning. It also investigates adversarial training, norm clipping, and simulated additive homomorphic aggregation as potential defensive mechanisms.

The objective is to understand how these attacks affect model reliability and how different defence strategies influence robustness in healthcare-oriented Edge AI systems.

## Research Objectives

* Develop and evaluate a CNN-LSTM model for ECG heartbeat classification.
* Investigate the impact of Fast Gradient Sign Method (FGSM) and Projected Gradient Descent (PGD) attacks.
* Evaluate black-box adversarial transfer using a surrogate CNN1D model.
* Study adversarial training as a defence against manipulated ECG inputs.
* Simulate federated learning across multiple clients.
* Investigate sign-flip model poisoning and norm-clipping defences.
* Explore simulated homomorphic aggregation for privacy-oriented federated learning.

---

## Key Features

* **ECG Classification:** Five-class heartbeat classification using deep learning.
* **CNN-LSTM Architecture:** Combines convolutional feature extraction with recurrent sequence modelling.
* **Adversarial Attack Evaluation:** Implements FGSM and PGD attacks.
* **Black-Box Transfer Testing:** Uses a CNN1D surrogate to investigate transferability against the target CNN-LSTM model.
* **Adversarial Training:** Evaluates training with clean and adversarial examples.
* **Federated Learning Simulation:** Models collaborative training across multiple clients.
* **Model Poisoning Evaluation:** Investigates sign-flip attacks against federated model updates.
* **Norm Clipping:** Studies update clipping as a mitigation strategy.
* **Privacy-Oriented Aggregation:** Explores simulated additive homomorphic aggregation.

---

## System Architecture

The experimental framework consists of the following major components:

| Component                 | Description                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------ |
| Dataset Preparation       | Loads ECG heartbeat samples and prepares training, validation, and test sets.        |
| Deep Learning Models      | Implements CNN1D, CNN-LSTM, and ResNet1D architectures for model evaluation.         |
| Adversarial Attack Module | Generates adversarial examples using FGSM and PGD.                                   |
| Adversarial Training      | Evaluates model training using clean and adversarial samples.                        |
| Federated Learning        | Simulates local model training and global model aggregation across clients.          |
| Poisoning Simulation      | Introduces malicious sign-flipped model updates.                                     |
| Defence Mechanisms        | Evaluates norm clipping and simulated encrypted aggregation.                         |
| Performance Evaluation    | Measures classification performance and robustness under different attack scenarios. |

### Workflow

1. Load and preprocess the ECG heartbeat dataset.
2. Train the baseline deep learning models.
3. Evaluate clean classification performance.
4. Generate white-box and black-box adversarial examples.
5. Investigate adversarial training and evaluate robustness.
6. Simulate federated learning across multiple clients.
7. Introduce model poisoning and evaluate defensive mechanisms.
8. Compare model performance across experimental scenarios.

---

## Dataset

The project uses the **MIT-BIH Arrhythmia heartbeat dataset**, accessed through the `shayanfazeli/heartbeat` dataset on Kaggle.

Each heartbeat sample contains 187 ECG signal values and one categorical class label.

### Dataset Statistics

| Dataset Split | Number of Samples |
| ------------- | ----------------: |
| Training      |            74,420 |
| Validation    |            13,134 |
| Testing       |            21,892 |
| **Total**     |       **109,446** |

### Classification Categories

| Label | Category         |
| ----- | ---------------- |
| N     | Normal           |
| S     | Supraventricular |
| V     | Ventricular      |
| F     | Fusion           |
| Q     | Unknown          |

The dataset exhibits class imbalance, so the implementation also incorporates class-weighted learning to address differences in class frequency.

---

## Deep Learning Models

The experimental implementation includes three neural network architectures.

### 1. CNN-LSTM

The CNN-LSTM model serves as the primary classification backbone.

Its convolutional layers extract local morphological patterns from ECG signals, while the LSTM layers learn sequential representations from the extracted features.

**Architecture:**

* Input: 187 ECG signal values.
* Three convolutional blocks with 32, 64, and 128 channels.
* Batch normalisation and ReLU activation.
* Max-pooling operations for feature reduction.
* Two LSTM layers with 64 hidden units.
* Fully connected classification layers.
* Five-class output layer.

### 2. CNN1D

A one-dimensional convolutional neural network is used as an additional baseline and as a surrogate model for black-box adversarial transfer experiments.

### 3. ResNet1D

A one-dimensional residual network provides an additional baseline for comparing classification performance across architectures.

---

## Threat Model

The framework investigates three principal attack scenarios.

| Attack                    | Description                                                                                  | Defence Investigated                                    |
| ------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| White-Box Evasion         | An attacker generates adversarial ECG inputs using knowledge of the target model.            | Adversarial training                                    |
| Black-Box Transfer        | Adversarial inputs generated using a surrogate model are evaluated against the target model. | Adversarial training and transfer-robustness evaluation |
| Federated Model Poisoning | A compromised client submits sign-flipped model updates during collaborative training.       | Norm clipping and simulated protected aggregation       |

These attacks affect different parts of the learning pipeline. Adversarial training targets input-level evasion, whereas norm clipping targets the magnitude of client updates.

Neither mechanism should be assumed to eliminate all possible attacks.

---

## Experimental Methodology

### 1. Data Preparation

The ECG dataset is loaded, divided into training, validation, and test sets, and prepared for neural network processing.

Class-weighted learning is used to address the imbalanced distribution of heartbeat categories.

### 2. Baseline Training

CNN1D, CNN-LSTM, and ResNet1D models are trained to establish baseline classification performance.

The CNN-LSTM model is used as the primary backbone for subsequent robustness experiments.

### 3. White-Box Adversarial Attacks

FGSM and PGD generate perturbed ECG inputs to evaluate the sensitivity of the target classifier to adversarial manipulation.

Model performance is compared under clean and adversarial conditions.

### 4. Black-Box Transfer Attacks

A CNN1D surrogate model is used to generate adversarial examples that are subsequently evaluated against the CNN-LSTM target model.

This experiment investigates whether adversarial perturbations generated against one architecture can affect another.

### 5. Adversarial Training

Clean and adversarial examples are incorporated into the training process to investigate whether adversarial exposure improves robustness.

### 6. Federated Learning and Model Poisoning

The framework simulates collaborative learning across multiple clients.

A sign-flip poisoning scenario is introduced to examine how malicious client updates affect global model performance.

### 7. Defensive Evaluation

Norm clipping is evaluated as an update-level mitigation technique. Simulated additive homomorphic aggregation is also explored as a privacy-oriented mechanism.

The resulting experiments compare classification performance and robustness across the evaluated configurations.

---

## Evaluation Metrics

The framework uses classification and robustness measurements to assess model behaviour.

| Metric               | Purpose                                                                  |
| -------------------- | ------------------------------------------------------------------------ |
| Accuracy             | Measures the proportion of correctly classified heartbeat samples.       |
| Precision            | Measures the reliability of positive class predictions.                  |
| Recall               | Measures the proportion of actual class instances correctly identified.  |
| Macro F1-Score       | Evaluates class-wise performance while giving each class equal weight.   |
| Confusion Matrix     | Shows correct and incorrect predictions across the heartbeat categories. |
| Adversarial Accuracy | Measures classification performance on adversarially perturbed inputs.   |

Macro F1-score is particularly relevant because the heartbeat dataset contains classes with substantially different sample frequencies.

---

## Experimental Results

The research evaluates model performance across clean inputs, adversarial attacks, adversarial training, and federated poisoning scenarios.

The primary comparisons focus on:

* Classification performance of the baseline neural network architectures.
* Performance degradation under FGSM and PGD attacks.
* Transferability of adversarial examples between model architectures.
* Robustness changes following adversarial training.
* The impact of malicious federated model updates.
* The effectiveness and limitations of norm clipping.

### Results Interpretation

The experiments are intended to identify the trade-offs between clean classification performance and robustness under adversarial conditions.

In particular, the federated poisoning experiments examine whether clipping malicious updates can reduce their impact on the global model.

The effectiveness of each defence must be interpreted using the results from its corresponding experimental configuration. Improvements against one attack do not necessarily imply protection against other attack types.

*Refer to the research notebook for the implemented experiments and recorded outputs. Numerical results should be reported alongside the exact model configuration, attack parameters, and evaluation conditions used to obtain them.*

---

## Repository Structure

```text
RMS_Defending_Edge_AI/
│
├── Defending_Edge_AI_Paper_Aligned (2).ipynb
│
└── README.md
```

The Jupyter notebook contains the current experimental implementation, including dataset preparation, neural network architectures, training procedures, attack evaluation, and federated-learning experiments.

Additional scripts, figures, dependency files, and experiment logs can be organised into separate directories as the repository evolves.

---

## Getting Started

### Prerequisites

The notebook uses Python and the following major libraries:

* NumPy
* Pandas
* Matplotlib
* Seaborn
* PyTorch
* Scikit-learn
* KaggleHub

The notebook may require additional dependencies depending on the execution environment.

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/Nishkal08/RMS_Defending_Edge_AI.git
cd RMS_Defending_Edge_AI
```

**2. Set up a Python environment**

```bash
python -m venv venv
```

Activate the environment on Windows:

```bash
venv\Scripts\activate
```

On Linux or macOS:

```bash
source venv/bin/activate
```

**3. Install the required libraries**

```bash
pip install numpy pandas matplotlib seaborn torch scikit-learn kagglehub jupyter
```

For reproducible experiments, use compatible library versions and a suitable PyTorch installation for your CPU or GPU environment.

**4. Open the notebook**

```bash
jupyter notebook
```

Open `Defending_Edge_AI_Paper_Aligned (2).ipynb` and execute the cells in order.

Alternatively, upload the notebook to Google Colab and execute it in a compatible runtime.

### Dataset Access

The notebook downloads the heartbeat dataset through KaggleHub when the required local CSV files are not available.

Ensure that the runtime has the required internet access and that dataset access complies with the original dataset's terms.

---

## Limitations

* **Experimental Scope:** The implementation evaluates selected attack scenarios and does not establish protection against every adversarial threat.
* **Simulated Cryptography:** Simulated homomorphic aggregation should not be interpreted as a fully validated production cryptographic implementation.
* **Federated Learning:** Simulated client behaviour does not automatically establish performance in a real distributed healthcare network.
* **Clinical Generalisation:** Performance on the selected dataset does not establish clinical validity or generalisation across hospitals, devices, and patient populations.
* **Edge Deployment:** Actual latency, memory consumption, and energy efficiency must be measured on the target hardware before making deployment claims.
* **Reproducibility:** Results depend on the dataset split, training configuration, random seeds, attack parameters, and model checkpoints used in each experiment.

---

## Future Work

Potential extensions include:

* Evaluating the framework on physical edge devices.
* Measuring inference latency, memory usage, and energy consumption.
* Investigating additional adversarial and model-poisoning strategies.
* Evaluating alternative robust aggregation methods.
* Validating privacy mechanisms using a concrete cryptographic implementation.
* Testing across different patient populations and data distributions.
* Adding automated experiment scripts, pinned dependencies, and reproducible configuration files.

---

## Research Reference

The project is based on research into secure Edge AI for healthcare monitoring and federated anomaly detection.

The implementation investigates selected aspects of adversarial robustness and federated model poisoning within an ECG classification pipeline.

The exact bibliographic details of the base paper should be added here from the paper's published record.

---

## Author

**Nishkal Doctor**

Institute of Technology, Nirma University
Ahmedabad, Gujarat, India

**Repository:** [RMS_Defending_Edge_AI](https://github.com/Nishkal08/RMS_Defending_Edge_AI)

---

## Disclaimer

This repository is intended for academic research and experimentation. It is not a clinically validated diagnostic system and should not be used to make medical decisions.

The results demonstrate behaviour under the evaluated experimental conditions and should not be interpreted as a guarantee of security, privacy, or clinical reliability.
