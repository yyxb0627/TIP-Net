# TIP-Net

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)](https://pytorch.org/)

This is the official PyTorch implementation for the paper: 
**Partially Manipulated DeepFake Video Detection and Localization via Weakly Supervised Learning**

TIP-Net is a weakly supervised framework designed to detect and localize partially manipulated DeepFake videos using only video-level labels.

## ⚙️ Prerequisites

- Python 3.8+
- PyTorch 1.10+
- CUDA 11.3+

Clone the repository and install the required packages:
```bash
git clone [https://github.com/yyxb0627/TIP-Net.git](https://github.com/yyxb0627/TIP-Net.git)
cd TIP-Net
pip install -r requirements.txt
(Optional) Install facenet-pytorch if you need face cropping during preprocessing.

📁 Data Preparation
Please organize your raw videos (e.g., ForgeryNet, FF++, Celeb-DF) into real and fake folders as follows:

Plaintext
raw_dataset/
├── real/
│   ├── id00001.mp4
│   └── id00002.mp4
└── fake/
    ├── id00003.mp4
    └── id00004.mp4
Extract frames from the raw videos using the provided preprocessing script:

Bash
python scripts/preprocess.py \
    --data_root  ./raw_dataset \
    --frames_dir ./frames \
    --face_crop
🚀 Quick Start
Training
To train TIP-Net from scratch, run the following command. The model will automatically build the memory bank and update prototypes during training.

Bash
python train.py \
    --frames_dir ./frames \
    --save_dir   ./checkpoints \
    --log_dir    ./logs
Note: If you encounter Out-Of-Memory (OOM) issues, consider decreasing the batch size or utilizing gradient accumulation.

Testing & Evaluation
To evaluate the trained model and get video-level/snippet-level metrics:

Bash
python test.py \
    --frames_dir ./frames \
    --checkpoint ./checkpoints/best_model.pth \
    --save_dir   ./results
