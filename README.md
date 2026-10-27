# CNN Pruning Using Genetic Algorithms and Knowledge Distillation

A Soft Computing case study that investigates **Genetic Algorithm (GA)-based structured CNN pruning combined with Knowledge Distillation (KD)** to reduce model complexity while maintaining image classification performance on the CIFAR-10 dataset.

## 📌 Project Overview

Convolutional Neural Networks (CNNs) are widely used for image classification, but larger models can require considerable computational resources. This project explores a compression approach that combines Genetic Algorithms and Knowledge Distillation.

- **Structured Pruning:** Removes selected convolutional channels to reduce model complexity.
- **Genetic Algorithm:** Searches for suitable channel-pruning configurations.
- **Knowledge Distillation:** Transfers useful knowledge from a larger teacher model to a smaller student model.
- **Performance Evaluation:** Compares classification metrics, parameter count, multiply–accumulate operations (MACs), and inference latency.

The goal is to achieve a smaller CNN while preserving accuracy close to the original model.

## 🎯 Objectives

- Reduce the number of trainable model parameters.
- Reduce computational operations measured in MACs.
- Maintain classification accuracy after pruning.
- Apply Knowledge Distillation to train the pruned student model.
- Compare the original CNN and the GA-pruned student model using consistent evaluation metrics.
- Examine whether lower model complexity improves measured inference latency.

## 📂 Dataset

**Dataset:** CIFAR-10

CIFAR-10 contains colour images from 10 classes, each with dimensions of \(32 \times 32\) pixels.

| Dataset split | Number of images |
|---|---:|
| Training | 45,000 |
| Validation | 5,000 |
| Testing | 10,000 |
| **Total** | **60,000** |

**Classes:** Airplane, Automobile, Bird, Cat, Deer, Dog, Frog, Horse, Ship, and Truck.

## 🧠 Methodology

The project follows these stages:

1. **Teacher CNN Training:** Train the original CNN on CIFAR-10.
2. **GA-Based Search:** Search for suitable channel-pruning ratios using a Genetic Algorithm.
3. **Structured Pruning:** Construct a smaller CNN using the selected channel configuration.
4. **Knowledge Distillation:** Train the student model using knowledge from the teacher.
5. **Evaluation:** Compare classification performance and model efficiency.

### Workflow

```text
             CIFAR-10 Dataset
                    |
                    v
              Original CNN
              (Teacher Model)
                    |
                    v
          Genetic Algorithm Search
                    |
                    v
           Structured Channel Pruning
                    |
                    v
             Student CNN
                    |
                    v
          Knowledge Distillation
                    |
                    v
          Performance Evaluation
                    |
                    v
       Accuracy | Parameters | MACs
                | Latency
```

## 🏗️ CNN Architecture

### Original CNN — M1

| Layer | Channels / Units |
|---|---:|
| Convolutional Layer 1 | 32 |
| Convolutional Layer 2 | 64 |
| Convolutional Layer 3 | 128 |
| Fully Connected Layer | 256 |
| Output Classes | 10 |

### GA-Pruned Student CNN — M5

| Layer | Channels / Units |
|---|---:|
| Convolutional Layer 1 | 28 |
| Convolutional Layer 2 | 64 |
| Convolutional Layer 3 | 94 |
| Fully Connected Layer | 256 |
| Output Classes | 10 |

The Genetic Algorithm selected a configuration that reduced channels in the first and third convolutional layers while retaining the second layer's channel count.

## ⚙️ Technologies Used

- **Programming Language:** Python
- **Deep Learning Framework:** PyTorch
- **Dataset:** CIFAR-10
- **Optimization Technique:** Genetic Algorithm
- **Model Compression:** Structured CNN Pruning
- **Training Technique:** Knowledge Distillation
- **Evaluation:** Accuracy, macro precision, macro recall, macro F1-score, parameter count, MACs, and inference latency

*Note: Add exact library versions and hardware details only if they are recorded in the implementation.*

## 📊 Experimental Results

The following table presents the measured results from the original CNN (M1) and the GA-pruned model trained with Knowledge Distillation (M5).

| Metric | Original CNN (M1) | GA Pruning + KD (M5) |
|---|---:|---:|
| Test Accuracy | 79.33% | 79.00% |
| Macro Precision | 0.7924 | 0.7905 |
| Macro Recall | 0.7933 | 0.7900 |
| Macro F1-score | 0.7927 | 0.7899 |
| Parameters | 620,810 | 459,436 |
| MACs | 10.8488 million | 8.7557 million |
| Latency per Image | 1.3488 ms | 1.6645 ms |

### Key Findings

| Measurement | Result |
|---|---:|
| Parameter reduction | 25.99% |
| MAC reduction | 19.29% |
| Accuracy decrease | 0.33 percentage points |
| Latency change | Increased |

### Results Interpretation

- The student model reduced the parameter count by **25.99%**.
- Computational operations decreased by **19.29%**.
- Test accuracy remained close to the original model, decreasing from 79.33% to 79.00%.
- Measured inference latency increased from 1.3488 ms to 1.6645 ms per image.

These results indicate that reducing parameters and MACs does not necessarily guarantee faster inference on the evaluated setup.

## 📈 Results Visualizations

If available in the project files, include graphs comparing:

- Test accuracy of M1 and M5.
- Parameter count before and after pruning.
- MACs before and after pruning.
- Inference latency before and after pruning.

Suggested directory:

```text
results/
├── accuracy_comparison.png
├── parameter_comparison.png
├── macs_comparison.png
└── latency_comparison.png
```

Update these filenames to match the actual generated plots. Do not add placeholder graphs as if they were experimental outputs.

## 📁 Suggested Repository Structure

```text
GA-CNN-Pruning-Knowledge-Distillation/
│
├── README.md
├── notebooks/
│   └── cnn_pruning_knowledge_distillation.ipynb
│
├── src/
│   ├── model.py
│   ├── genetic_algorithm.py
│   ├── pruning.py
│   ├── knowledge_distillation.py
│   └── evaluation.py
│
├── results/
│   ├── accuracy_comparison.png
│   ├── parameter_comparison.png
│   ├── macs_comparison.png
│   └── latency_comparison.png
│
├── report/
│   └── soft_computing_case_study.pdf
│
├── presentation/
│   └── soft_computing_presentation.pptx
│
└── requirements.txt
```

*This is a suggested structure. Keep only files and folders that actually exist in your repository.*

## 🚀 How to Run

The exact execution commands depend on the implementation files included in the repository.

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd GA-CNN-Pruning-Knowledge-Distillation
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

### 3. Install dependencies

If `requirements.txt` is available:

```bash
pip install -r requirements.txt
```

Otherwise, install the dependencies listed in your actual implementation.

### 4. Run the implementation

Run the notebook or Python entry-point file included in the repository. Replace this instruction with the exact command used by your project.

## 🔬 Limitations

- The pruned student model achieved slightly lower accuracy than the original CNN.
- Inference latency increased despite the reductions in parameters and MACs.
- The results are based on the reported CIFAR-10 experiment.
- Additional experiments are required to assess performance across different architectures, datasets, and hardware platforms.

## 🔮 Future Scope

- Explore different pruning ratios and Genetic Algorithm fitness functions.
- Compare with uniform pruning, Taylor-based pruning, and Knowledge-Distillation-only baselines.
- Repeat experiments with multiple random seeds.
- Evaluate additional CNN architectures and image datasets.
- Measure latency on CPU, GPU, and edge devices.
- Investigate hardware-aware pruning to improve real-world inference speed.

These are proposed extensions and are not claimed as completed experiments.

## 📚 References

Add the complete, verified bibliographic details of the research papers cited in the case study report. Ensure that author names, paper titles, publication venues, years, page numbers, and DOI links are accurate.

## 👨‍💻 Author

**Bheeshma Shankar A**

- Department: CSE (Artificial Intelligence and Machine Learning)
- Institution: Chaitanya Bharathi Institute of Technology (CBIT), Hyderabad
- Roll Number: 160124748093

## 📄 Project Information

- **Subject:** Soft Computing
- **Project Type:** Academic Case Study
- **Topic:** GA-Based Structured CNN Pruning with Knowledge Distillation
- **Dataset:** CIFAR-10

---

*This project evaluates the trade-off between CNN model complexity and classification performance using Genetic Algorithm-based structured pruning and Knowledge Distillation.*
