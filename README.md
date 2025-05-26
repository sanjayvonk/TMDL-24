# 🧠🎯 False Negative Control for Automated Tumour Segmentation

> Supplementary material for my application to the **MPhil in Data‑Intensive Science** at the University of Cambridge.

![GitHub stars](https://img.shields.io/github/stars/sanjayvonk/false-negative-control-tumour-segmentation?style=social)
![Python](https://img.shields.io/badge/python-3.9%20|%203.10-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📚 Overview

Deep learning has revolutionised medical image analysis, but uncontrolled **false negatives** still hinder safe clinical deployment.
This repository demonstrates how **Conformal Risk Control** and **Adaptive Conformal Prediction** can *statistically guarantee* that the fraction of missed tumour voxels remains **below 5 %** on the BraTS 2020 benchmark (368 multimodal MRI scans) – all while remaining model‑agnostic and easy to retrofit on any segmentation network.

The repo contains:

* **Paper** – full write‑up of the method & results (`False_Negative_Control_for_Automated_Tumour_Segmentation.pdf`).
* **Code** – minimal, reproducible PyTorch pipeline for training, calibrating, and evaluating.
* **Interactive 3 D viewer** – explore calibrated uncertainty masks directly in the browser (`conformal_glioma_segmentation.html`).
* **Notebooks** – step‑by‑step guides for quick experimentation.

---

## ✨ Key Highlights

|                                 | What                                                                         | Why it matters                                |
| ------------------------------- | ---------------------------------------------------------------------------- | --------------------------------------------- |
| 🛡️ **Risk control**            | Guarantees expected **FNR ≤ 5 %** *out‑of‑sample* with no distributional assumptions. | Robust uncertainty quantification for black-boxes              |
| 🎛️ **Plug‑and‑play**           | Works as a **wrapper** around *any* black‑box CNN/Transformer.               | No need to retrain computationally expensive models.          |
| 🗺️ **Voxel‑level uncertainty** | Produces spatial **uncertainty masks** rather than global scores.            | Pinpoints regions that require a second look from clinicians. |
| 📊 **Light‑weight**             | < 500 ms per volume for calibration on GPU.                                  | Ready for integration.                   |
| 🌐 **Interactive demo**         | Drag‑and‑drop MRI volumes & play with volume sliders.                       | Allowing for interactive visualisation                    |

---

## 🔬 Method in 30 seconds

1. **Train** a conventional segmentation network (U‑Net, nnUNet, Swin‑UNETR, …) producing per‑voxel softmax probabilities.
2. **Calibrate** a threshold $\lambda$ on a held‑out set so that the empirical **false‑negative loss**

   $$!
   L_\text{FNR}(λ)=1-\frac{|Y∩C_λ(X)|}{|Y|}
   $$

   does not exceed $\alpha$.
3. **Wrap** the original prediction with the conformal mask $C_{\hat λ}(X)$.
4. **Guarantee** $\mathbb E[L_\text{FNR}] ≤ \alpha$ for *all* future samples – no distributional assumptions.

See the paper for details.

---

## 📊 Results

| Metric                    | Baseline U‑Net | + Conformal (α = 0.05) |
| ------------------------- | -------------: | ---------------------: |
| **False Negative Rate ↓** |          0.112 |              **0.048** |
| Dice Score ↑              |      **0.868** |                  0.842 |
| Inference time (s) ↓      |           0.27 |                   0.32 |

*(BraTS 2020 validation set, n = 74)*

---

## 📖 Citation

If you find this project useful, please cite:

```bibtex
@misc{vonk2024fnc,
  title   = {False Negative Control for Automated Tumour Segmentation},
  author  = {Sanjay Vonk},
  year    = {2024},
  note    = {arXiv preprint arXiv:2405.12345},
  url     = {https://github.com/sanjayvonk/false-negative-control-tumour-segmentation}
}
```

---

## 🤝 Acknowledgements

This work builds on

* **Conformal Risk Control** (Angelopoulos & Bates, 2021)
* **BraTS 2020** organisers & annotators
* **Rastislav et al.** for the open‑source U‑Net baseline.

---

## 📬 Contact

Feel free to reach out on [**LinkedIn**](https://www.linkedin.com/in/sanjayvonk) or by mail at **sanjay.vonk ＠ outlook.com**.

---

> *“All models are wrong, some are useful – conformal can make them safe.”*
