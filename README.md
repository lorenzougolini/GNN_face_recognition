# Exploring Efficacy of GNNs for Face Recognition

## 📖 About the Project
This repository contains the code and implementation details for a study that explores Geometric Deep Learning for face recognition. The project investigates how much a graph representation of a face—where nodes represent anatomical landmarks and edges represent spatial connectivity—can provide a robust signature when used alone or alongside image texture-based analysis. 

The primary objective is to design, implement, and evaluate a biometric pipeline that performs face verification and identification using Graph Neural Networks (GNNs).

## 🧠 Architectures Investigated
This project investigates two main architectural strategies:

* **Single-Channel GNN (SC-GNN):** This geometric approach utilizes Graph Attention Networks (specifically GATv2) to learn embeddings from the spatial geometry of 478 facial landmarks extracted via the MediaPipe Face Mesh. Each node is enriched with local visual features extracted from a small patch using a MobileNet backbone. The model is trained using Triplet Margin Loss.
* **Dual-Channel GNN (DC-GNN):** This is a hybrid multi-modal approach that fuses geometric features with texture features. It processes data via two parallel streams: a visual stream using a pre-trained ResNet-18 backbone to extract a global visual embedding, and a graph stream using the GATv2 network. To enforce strong inter-class separation, this model is trained using a metric learning approach inspired by ArcFace.

## 📊 Dataset and Evaluation
The system is developed and evaluated using the standard Labeled Faces in the Wild (LFW) dataset. We used a subset of the LFW composed of identities that have at least 3 image samples. 

To thoroughly test generalization capabilities, the models were evaluated under two distinct protocols:
* **Closed-Set:** The dataset is split randomly by images, meaning the model sees images of the same identity in both training and testing.
* **Open-Set:** The dataset is split by identity, meaning the training and test sets are disjoint, and the model must verify unknown subjects. 

## 🏆 Key Results
Our findings demonstrate that integrating graph-based spatial relationships with global visual context significantly improves biometric verification and identification. The DC-GNN consistently outperforms the geometric-only SC-GNN approach. 

Here is a summary of the biometric performance across both scenarios:

| Metric | Closed-Set (SC-GNN) | Closed-Set (DC-GNN) | Open-Set (SC-GNN) | Open-Set (DC-GNN) |
| :--- | :--- | :--- | :--- | :--- |
| **EER (↓)** | 20.50% | 6.36% | 16.80% | 11.41% |
| **Accuracy** | 75.60% | 93.48% | 79.58% | 88.68% |
| **AUC** | 85.03% | 97.86% | 87.81% | 95.25% |
| **CMS@1** | 6.86% | 42.62% | 18.39% | 72.73% |
| **CMS@5** | 22.86% | 50.66% | 48.23% | 89.24% |

## 👥 Authors
* **Antonio Cordeiro** - Sapienza University of Rome
* **Lorenzo Ugolini** - Sapienza University of Rome
* **Christian Bianchi** - Sapienza University of Rome
