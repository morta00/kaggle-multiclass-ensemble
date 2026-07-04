
# Multiclass Image Classification — Kaggle 1st Place

CNN ensemble trained **from scratch** on low-resolution RGB images (no pretrained weights).

| Metric | Value |
|--------|-------|
| Rank | **1st place** |
| Test accuracy | **93.4%** |
| Input | 16×16 RGB → upscaled to 32×32 |
| Models | WideResNet-28-10, WideResNet-40-4, ResNet-110 |

## Method

1. **Upscale** 16×16 images to 32×32 (Lanczos)
2. **Train 3 CNNs** with different architectures for diversity
3. **Augment** with CutMix, Mixup, random crop/flip, brightness/contrast
4. **Optimize** with SGD + Nesterov, cosine LR decay, label smoothing
5. **Pseudo-label** high-confidence test samples (2 rounds: thresholds 0.95 → 0.98)
6. **TTA** — 15 augmented passes per model at inference
7. **Ensemble** — weights chosen by grid search on the validation set

## Requirements

- Python 3.10+
- GPU recommended (trained on Colab A100)
- Competition data as pickle files (not included)

## How to run (Google Colab)

1. Upload `notebooks/Kaggle_Competition.ipynb` to Colab
2. Runtime → Change runtime type → **GPU**
3. Put data on Drive:

```
MyDrive/kaggle-Competition/
  train_X_y.pkl
  test_X.pkl
```

4. Run all cells in order

Locally (if you have the data and a GPU):

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Kaggle_Competition.ipynb
```

Update `BASE_PATH` in the notebook if your data folder is different.

## Notes

- Models and submission CSV are written to Drive (`*.keras`, `submission_FINAL.csv`)
- Weights and competition data are **not** in this repo
- Re-running training may vary slightly due to GPU non-determinism

## Author

**Mortadha Ghnimi**  
MS Artificial Intelligence @ Grand Valley State University  

- LinkedIn: https://www.linkedin.com/in/mortadha-ghnimi-021183252/
=======
