## ADHD Brain Connectivity Saliency with Deep Learning
**Project Summary**

This script analyzes functional brain connectivity to identify salient brain regions associated with 
Attention Deficit Hyperactivity Disorder (ADHD), using resting-state fMRI data from the 
WiDS Datathon 2025 competition:
(https://www.kaggle.com/competitions/widsdatathon2025/overview).

It applies a deep learning approach to model and interpret ADHD-related neural patterns, with the 
goal of visualizing differences in brain saliency between ADHD and control subjects.


🔧 Model

- **Architecture:** A deep attention-based graph neural network adapted from the 
  "Diffusion Kernel Attention Network" by Zhang et al. (TMI 2022) [DOI: 10.1109/TMI.2022.3170701]
- **Modules** include spatial and temporal attention blocks for learning from 200×200 functional connectome matrices
- **Input format:** Each subject's brain connectivity is represented as a 200×200 matrix (full or upper-triangular)
- **Output:** Binary classification logits (ADHD vs. control)


📊 Training and Evaluation

- **Dataset:** Connectome matrices reshaped from upper-triangular vectors or full matrices
  - Each connectome matrix is wrapped into a PyTorch `Dataset` object and accessed via a `DataLoader`
  - Allows for efficient batch processing, optional data augmentation during training, and parallel loading
- **Loss Function:** Cross-entropy loss based on predicted class probabilities
- **Evaluation Metric:** F1 score, to balance precision and recall in binary ADHD classification


🧠 Saliency and Visualization

- Node-level importance is calculated by averaging saliency maps across samples
- Top-30 most salient brain regions are selected for each group
- Visualization:
    - **NetworkX graph:** 2D topological brain graphs with left/right hemisphere coloring and edge classification
    - **Nilearn plot:** Top regions visualized on actual brain using Schaefer 200 MNI coordinates
