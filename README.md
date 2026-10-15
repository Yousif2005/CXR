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

- Training images used: [5,863 ]
- Class distribution: [ NORMAL 0 / PNEUMONIA 1]
- Validation strategy: [3 folders (train, test, val)]
- Rules: CNNs and transfer learning allowed; no external medical datasets.

## 🧠 My Approach

- **Model:** [TODO: exact architecture, e.g. ResNet50 pretrained on ImageNet]
- **Preprocessing:** [TODO: resize, grayscale-to-3-channel, normalization]
- **Augmentation:** [TODO: flips, rotation, brightness, etc.]
- **Class imbalance handling:** [TODO: class weights / weighted sampler / none]
- **Training setup:** [TODO: optimizer, learning rate, epochs, batch size, frozen vs fine-tuned layers]
- **Frameworks:** Python, PyTorch / TensorFlow, OpenCV, scikit-learn [TODO: keep only what you used]

## 🔬 Analysis

[TODO: add these once you have them]

- Confusion matrix and per-class precision/recall (recall on PNEUMONIA matters most clinically)
- Comparison with the simple CNN baseline
- Ablations (e.g. with/without augmentation, frozen vs fine-tuned backbone)
- Error analysis: what kinds of images are misclassified, and why

## ⚠️ Limitations

- The gap between accuracy (78.37%) and Macro F1 (72.86) shows the minority class is not handled perfectly.
- The test set may differ in distribution from the training set, so performance on unseen data can be lower than validation performance. [TODO: confirm with your own validation vs test comparison]
- This is a competition project, not a clinically validated tool.

## 🚀 Reproducing

```bash
git clone https://github.com/Yousif2005/CXR.git
cd CXR
pip install -r requirements.txt   # [TODO: add requirements.txt]
jupyter notebook starter-code.ipynb   # [TODO: or name of your own notebook]
```

## 🗂 Repository Contents

| Path | Description |
| :--- | :--- |
| `starter-code.ipynb` | Starter notebook from the organizer [TODO: link or rename your own notebook] |
| `evaluate.py`, `generate_leaderboard_html.py`, `final_leaderboard.csv`, `index.html` | Competition evaluation and leaderboard (organizer) |
| `submission/`, `encryption/` | Encrypted submission workflow (organizer) |

## 📝 Original Competition Format

Participants submit `submission.csv` with columns `id` (test image name, exactly as provided) and `label` (integer), encrypted with the provided script and submitted through a pull request. One submission per participant. Full instructions are in the [upstream repository](https://github.com/tasneem-mselim/CXR).

## 📚 References

- Kermany et al., 2018. *Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning.* Cell.

## 👩‍🏫 Credits

Competition organizer: Tasneem Selim
