# PGFormer: A Prototype-Graph Transformer for Incomplete Multiview Clustering

**Yiming Du, Yao Wang, Ziyu Wang, Rui Ning, and Lusi Li***

Department of Computer Science, Old Dominion University, Norfolk, VA, USA  

📄 **Published in IEEE Transactions on Neural Networks and Learning Systems (TNNLS), Vol. 37, No. 3, pp. 1163–1175, March 2026**  
🔗 **[Paper (DOI)](https://doi.org/10.1109/TNNLS.2025.3617888)**  

---

## 📖 Overview

**PGFormer** is a prototype-guided graph transformer framework for **incomplete multiview clustering (IMVC)**. Incomplete views and discrepancies among views can distort neighborhood structures and degrade clustering when models force view-specific representations to become identical.

Instead of directly enforcing identical representations across views, PGFormer learns **view-specific semantic prototypes** and aligns their **cluster assignments**. It combines graph convolution, prototype-level self-attention, prototype-to-node cross-attention, and cross-prototype imputation to capture multilevel topological relationships and recover missing information in the embedding space.

## ✨ Key Contributions

1. **Prototype-graph representation learning:** Uses view-specific prototypes as semantic bottlenecks to capture graph structure and long-range dependencies without discarding view diversity.
2. **Dual attention mechanisms:** Prototype-to-prototype (**P2P**) self-attention models prototype relationships, while prototype-to-node (**P2N**) cross-attention refines node embeddings using prototype information.
3. **Cross-prototype imputation (CPI):** Reconstructs missing embeddings using prototype assignments from available views and refined prototypes of the missing view.
4. **Cross-view alignment:** Encourages consistent cluster assignments using cluster-level contrastive learning and a KL-divergence-based alignment objective.

## 🏗️ Framework

The overall pipeline has four stages:

1. **View feature learning:** Pretrain view-specific autoencoders using available samples.
2. **Prototype-graph representation learning:** Apply view-specific GCNs to model node-to-node topology, initialize prototypes with K-means, and refine prototypes and node embeddings with P2P and P2N attention.
3. **Cross-prototype imputation:** Estimate missing-view embeddings from cross-view prototype assignments and intraview prototypes.
4. **Cross-view alignment and clustering:** Align completed prototype assignments across views and derive cluster labels by aggregating the assignments.

> **Architecture figure:** Add an image of Fig. 1 from the paper (with appropriate permission) to the repository and embed it here, for example using `![PGFormer framework](figures/PGFormer.png)`.

### Training objective

PGFormer jointly optimizes:

$$
\mathcal{L}=\mathcal{L}_{\mathrm{re}}+\lambda\mathcal{L}_{\mathrm{ca}}+\gamma\mathcal{L}_{\mathrm{kl}},
$$

where $\mathcal{L}_{\mathrm{re}}$ is the reconstruction loss on available samples, $\mathcal{L}_{\mathrm{ca}}$ is the cross-view cluster-level contrastive loss, and $\mathcal{L}_{\mathrm{kl}}$ promotes assignment alignment and regularization.

## 📊 Experiments

PGFormer is evaluated on six benchmark datasets: **BDGP, MNIST-USPS, Scene15, Fashion-MNIST, Handwritten, and Prokaryotic**. Incomplete views are simulated using missing ratios from **10% to 60%**. The paper compares against COMPLETER, DCP, ProImp, MCAC, ICMVC, and DVIMVC using **clustering accuracy (ACC), normalized mutual information (NMI), and purity**.

### Reported ACC results

The following values are the ACC results reported for PGFormer in Table II of the paper (mean ± standard deviation, in percent, aggregated across the evaluated missing ratios):

| Dataset | ACC (%) |
|---|---:|
| BDGP | 90.36 ± 7.83 |
| MNIST-USPS | 90.96 ± 5.75 |
| Scene15 | 38.68 ± 3.97 |
| Fashion-MNIST | 92.26 ± 2.78 |
| Handwritten | 91.17 ± 4.29 |
| Prokaryotic | 88.57 ± 6.95 |

The paper also reports ablation studies, t-SNE visualizations, convergence analyses, and hyperparameter sensitivity experiments.

## ⚙️ Implementation Details

The paper reports the following settings:

| Setting | Value |
|---|---|
| Framework | PyTorch |
| Shared feature dimension | 200 |
| Prototype dimension | 200 |
| Learning rate | 0.0005 |
| Autoencoder pretraining | 200 epochs |
| Fine-tuning | 100 epochs |
| $\lambda$ | 0.04 |
| $\gamma$ | 0.01 |
| Evaluation | 10 experimental runs |
| Reported hardware | NVIDIA RTX 3080 GPU, 32 GB RAM |

Encoder architectures and batch sizes vary by dataset; see Section IV-A of the paper for details. The paper does not specify a public repository layout, dependency versions, or command-line interface, so installation and execution instructions should be added once the implementation is published.

## 📚 Citation

If you find this work useful, please cite:

```bibtex
@article{du2026pgformer,
  title={PGFormer: A Prototype-Graph Transformer for Incomplete Multiview Clustering},
  author={Du, Yiming and Wang, Yao and Wang, Ziyu and Ning, Rui and Li, Lusi},
  journal={IEEE Transactions on Neural Networks and Learning Systems},
  volume={37},
  number={3},
  pages={1163--1175},
  year={2026},
  doi={10.1109/TNNLS.2025.3617888}
}
```

## 📬 Contact

For questions about the research, don't hesitate to get in touch with the authors.

---

*Please refer to the published paper for the full methodological details, experimental settings, and results.*
