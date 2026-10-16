# 🫁 Chest X-Ray Pneumonia Detection

Binary classification of chest X-ray images (**NORMAL** vs **PNEUMONIA**) using CNNs and transfer learning.

> This repository is my fork of the class competition repo by [Tasneem Selim](https://github.com/tasneem-mselim/CXR). The competition infrastructure (evaluation scripts, leaderboard, submission encryption) belongs to the organizer. The model, experiments, and analysis described below are my own work.

---

## 📊 Results

Final result on the competition's hidden test set (one submission allowed):

| Metric | Score |
| :--- | :---: |
| Accuracy | **78.37%** |
| Macro F1-score | **72.86** |

Live leaderboard: [CXR Leaderboard](https://tasneem-mselim.github.io/CXR/)

---

## 🎯 Task

- **Input:** a chest X-ray image
- **Output:** `0` = NORMAL, `1` = PNEUMONIA 
- **Primary metric:** Macro F1 (accounts for class imbalance), plus accuracy

## 📂 Dataset

[Chest X-Ray Images (Pneumonia)](https://www.kaggle.com/datasets/paultimothymooney/chest-xray-pneumonia) (Kermany et al., 2018), organized as `train/` and `test/`.

- Training images used: 5,232 (4,187 training / 1,045 validation)
- Class distribution: NORMAL 0 / PNEUMONIA 1
- Validation strategy: random 80/20 image-level split
- Rules: CNNs and transfer learning allowed; no external medical datasets.

## 🧠 My Approach

- **Model:** custom CNN trained from scratch (no pretrained weights): 3 × [Conv2D (32/64/128 filters, 3×3, ReLU) + MaxPool], Flatten, Dense(128) + Dropout(0.5), softmax over 2 classes.
- **Input / preprocessing:** images resized to 128×128 and rescaled to [0, 1]. No data augmentation and no class weighting.
- **Training:** Adam (lr = 0.001), batch size 16, up to 10 epochs, early stopping on validation loss (patience 3, best weights restored), seed 25. About 12 minutes on a Kaggle notebook.
- **Validation:** random 80/20 split of the training images (4,187 train / 1,045 validation).
- **Framework:** Python, TensorFlow/Keras, NumPy, pandas, Matplotlib.

## 🔬 Analysis

Validation accuracy peaked at about **96%** (96.17% at the epoch with the best validation loss), while the hidden test results were **78.37% accuracy and 72.86 Macro F1**. Possible causes, not yet verified:

- A random image-level split can place several X-rays of the same patient in both training and validation, which inflates validation accuracy. 
- The test set may differ in distribution from the training set (different acquisition conditions or class balance). 
- Accuracy above Macro F1 suggests the minority class is handled worse than the majority class; no per-class metrics were computed in this version.

Planned improvements:

- Report a confusion matrix and per-class precision/recall (recall on PNEUMONIA matters most clinically).
- Use class weights or a weighted sampler for the imbalance.
- Add augmentation and compare against a pretrained backbone (e.g. ResNet / DenseNet) with fine-tuning.
- Use a stricter validation split that keeps each patient's images together.

## ⚠️ Limitations

- Validation accuracy (~96%) is not a reliable estimate of real performance. The hidden-test result is the honest number.
- No augmentation, class weighting, or transfer learning was used in this version.
- This is a competition baseline, not a clinically validated tool.

## 🚀 Reproducing

```bash
git clone https://github.com/Yousif2005/CXR.git
cd CXR
# open and run your notebook (CXR.ipynb)
```

## 🗂 Repository Contents

| Path | Description |
| :--- | :--- |
| `CXR.ipynb` | Jupyter notebook  |
| `evaluate.py`, `generate_leaderboard_html.py`, `final_leaderboard.csv`, `index.html` | Competition evaluation and leaderboard (organizer) |
| `submission/`, `encryption/` | Encrypted submission workflow (organizer) |

## 📝 Original Competition Format

Participants submit `submission.csv` with columns `id` (test image name, exactly as provided) and `label` (integer), encrypted with the provided script and submitted through a pull request. One submission per participant. Full instructions are in the [upstream repository](https://github.com/tasneem-mselim/CXR).

## 📚 References

- Kermany et al., 2018. *Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning.* Cell.

## 👩‍🏫 Credits

Competition organizer: Tasneem Selim
