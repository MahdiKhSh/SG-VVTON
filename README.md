# 🎭 SG-VVTON: Skeletal-Guided Diffusion for High-Fidelity and Temporally Coherent Video Virtual Try-On

<div align="center">

[![Paper](https://img.shields.io/badge/Paper-ACM%20%2F%20ArXiv-b31b1b.svg)](https://arxiv.org/abs/xxxx.xxxxx)
[![Project Page](https://img.shields.io/badge/Project-Website-blue)](https://your-project-page.github.io)
[![Hugging Face Demo](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Spaces-yellow)](https://huggingface.co/spaces/your-username/SG-VVTON)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/release/python-3100/)
[![PyTorch 2.0+](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

*An end-to-end generative framework integrating ViTPose kinematic priors and SAM3 semantic segmentation into a 14B-parameter Video Diffusion Transformer (DiT) for realistic, temporally coherent virtual try-on in unconstrained videos.*

</div>

---

## 🌟 Visual Showcase & Demonstrations

To evaluate the temporal stability and visual authenticity of **SG-VVTON**, we present unified side-by-side video demonstrations. Each clip displays the **Input Frames**, the **Target Garment**, and the synthesized **Output Frames** together, highlighting our model's performance across preprocessing extraction, dynamic human motion, severe anatomical occlusions, and complex lighting conditions.

---

### 1. Multimodal Preprocessing & Spatiotemporal Conditioning Signals
Unlike static virtual try-on models, our pipeline explicitly extracts structured representations from unconstrained video frames before generative denoising. This module isolates exact clothing boundaries, preserves facial identity, and tracks kinematic motion trajectories without relying on optical flow estimation or auxiliary 3D simulators.

#### Demo 1: Extraction of SAM3 semantic garment masks, face bounding boxes, and ViTPose skeletal graphs
*This demonstration visualizes our automated preprocessing pipeline: generating precise binary garment masks ($m_{\text{garment}}$), facial bounding boxes ($B_{\text{face}}$), and continuous whole-body kinematic motion signals ($C_{\text{pos}}$) across diverse video scenes.*
<div align="center">
  <video src="https://github.com/user-attachments/assets/f50800b5-83c0-46f3-84b7-9d9d39e57c97" controls="controls" autoplay="autoplay" loop="loop" muted="muted" style="max-width: 100%; border-radius: 8px;"></video>
</div>

---

### 2. Fine-Grained Detail Preservation & Complex Locomotion
Our framework regularizes the latent trajectory using structured negative textual constraints and CLIP-derived visual embeddings ($c_v$). This ensures that intricate garment structures—such as high-frequency fabric weaves, embroidery, ribbons, and logos—are faithfully rendered without inter-frame blurring or warping degradation.

#### Demo 2: High-frequency pattern and texture preservation under dynamic human motion
*As shown below, complex garment patterns (e.g., ribbon motifs and sharp prints) remain visually authentic and spatially stable as the subject moves freely within an office environment.*
<div align="center">
  <video src="https://github.com/user-attachments/assets/511a42c7-58bf-42f6-8cbc-549e85d706b0" controls="controls" autoplay="autoplay" loop="loop" muted="muted" style="max-width: 100%; border-radius: 8px;"></video>
</div>

---

### 3. Photometric Adaptation & Multi-Garment Generalization
By incorporating embedded LoRA layers into the large-scale diffusion backbone, **SG-VVTON** generalizes robustly across diverse apparel categories and challenging, unconstrained video footage (including broadcast clips and complex cinematic scenes). The network dynamically adapts garment shading, surface wrinkles, and ambient shadows to complex environmental lighting—**all without requiring auxiliary 3D physical simulators.**

#### Demos 3 & 4: Generalization across complex apparel categories, cinematic footage, and realistic ambient shading
*The synthesized garments seamlessly interact with varying room illumination and dynamic backgrounds across multiple body types, generating natural fabric folds, shading, and shadows that perfectly match the ambient environmental context.*
<div align="center">
  <video src="https://github.com/user-attachments/assets/4ae5a8f6-2f11-43c0-a772-3ad0e2a8e578" controls="controls" autoplay="autoplay" loop="loop" muted="muted" style="max-width: 100%; border-radius: 8px;"></video>
</div>
<br>
<div align="center">
  <video src="https://github.com/user-attachments/assets/0001c202-8a95-4033-abc2-2ff27dfd8825" controls="controls" autoplay="autoplay" loop="loop" muted="muted" style="max-width: 100%; border-radius: 8px;"></video>
</div>

---

### 4. Robustness to Severe Anatomical Occlusions
A primary failure mode of existing video try-on methods is boundary hallucination when body parts or external objects obstruct the torso. By conditioning the diffusion trajectory on continuous skeletal graphs, our architecture maintains structural boundary integrity.

#### Demo 5: Robust spatiotemporal coherence and identity preservation during severe topological occlusions
*Even during complex human-object interactions—such as walking while holding coffee cups or crossing arms over the chest—the garment boundaries remain temporally stable without artifact accumulation.*
<div align="center">
  <video src="https://github.com/user-attachments/assets/de3eb158-6354-4a03-8253-907fa762a134" controls="controls" autoplay="autoplay" loop="loop" muted="muted" style="max-width: 100%; border-radius: 8px;"></video>
</div>

---

## 📖 Abstract

While recent Video Virtual Try-On (VVTON) methods incorporate temporal attention modules, they frequently struggle to maintain visual fidelity and motion consistency simultaneously, often suffering from temporal instability and detail degradation under complex locomotion. 

In this work, we propose **SG-VVTON**, an end-to-end generative framework that integrates discriminative vision backbones into a large-scale video diffusion architecture. Rather than relying on global feature diffusion or auxiliary 3D physical simulators, our pipeline:
1. **Extracts deterministic skeletal priors** via **ViTPose** whole-body estimation to parameterize bodily dynamics.
2. **Isolates semantic garment boundaries** using **SAM3** video segmentation to prevent boundary drift.
3. **Directly conditions the denoising trajectory** of a **14B-parameter diffusion backbone (WAN 2.2)**, enforcing strict anatomical alignment and spatiotemporal coherence.

Qualitative evaluations across unconstrained broadcast and real-world sequences demonstrate that our approach realistically synthesizes fluid fabric mechanics and ambient photometric shading, significantly mitigating prevalent artifacts such as inter-frame inconsistency, color shift, and the loss of fine-grained details over time.

---

## 🚀 Key Features

- **🔥 Scalable Latent Video Diffusion**: Synthesizes fluid fabric mechanics and complex non-linear deformations directly within the compressed latent space of a **14B-parameter Video DiT (WAN 2.2)** backbone.
- **🦴 Dynamic Kinematic Guidance**: Eliminates inter-frame jitter and anatomical hallucinations by injecting continuous whole-body skeletal graphs ($C_{\text{pos}}$) from **ViTPose** directly into the conditioning tensor.
- **🎯 Precise Semantic Mask Propagation**: Utilizes **SAM3** tracking to isolate the reference garment mask ($m_{\text{garment}}$), facial identity ($m_{\text{face}}$), and background context ($m_{\text{bg}}$), ensuring temporal boundary stability without spatial misalignment.
- **💡 Multimodal Visual-Lexical Conditioning**: Employs **CLIP-Vision** texture embeddings ($c_v$) combined with structured positive/negative lexical prompts ($c_{\text{txt}}^+, c_{\text{txt}}^-$) via a Multi-Modal CFG formulation to eliminate color shift, anatomical distortion, and undesired transparency.
- **⚡ Zero 3D Simulation Overhead**: Achieves realistic garment draping, wrinkle dynamics, and ambient photometric shading purely through generative diffusion, completely bypassing computationally expensive 3D mesh simulators or optical flow tracking modules.

---

## 🏗️ Methodology & Architecture Overview

We formulate the VVTON task as a latent-space spatiotemporal conditional generation problem. Given an input video sequence $V \in \mathbb{R}^{T \times 3 \times H \times W}$, a target garment image $I_g \in \mathbb{R}^{3 \times H_g \times W_g}$, and an auxiliary textual prompt $P$, our framework approximates the conditional distribution:

$$p_\theta(V \mid V_{\text{mask}}, C_{\text{kin}}, B_{\text{face}}, c_v, c_{\text{txt}})$$

### 1. Preprocessing & Feature Extraction Graph
As illustrated in our pipeline architecture, the input modalities are processed through parallel discriminative branches:
* **Spatiotemporal Masking ($V_{\text{mask}}$):** Binary masks from SAM3 are dilated, smoothed via a Gaussian filter, and inverted to isolate the garment region while preserving background and facial identity: $V_{\text{mask}, t} = V_t \odot M_{\text{cond}, t}$.
* **Skeletal Rendering ($C_{\text{spatiotemporal}}$):** Skeletal landmarks from ViTPose are rendered as continuous skeleton graphs and concatenated with facial bounding box coordinates and masked video frames: $C_{\text{spatiotemporal}} = [V_{\text{mask}}, C_{\text{pos}}, B_{\text{face}}]$.
* **Visual Texture Embedding ($c_v$):** A pre-trained CLIP-Vision encoder extracts high-frequency structural features and surface patterns directly from the reference garment: $c_v = E_{\text{CLIP-Vision}}(I_g)$.

### 2. Latent Diffusion & Multi-Modal CFG
The latent conditioning tensor $Z_{\text{cond}}$ (derived from encoding $C_{\text{spatiotemporal}}$ via a VAE) is concatenated with the noisy latent state $z_\tau$ along the channel dimension before entering the **14B-parameter DiT backbone (WAN 2.2)**. 

Denoising is executed via a discrete Euler sampler using a uniform noise schedule. At each timestep $\tau$, the predicted noise $\epsilon_\theta$ is modulated using our novel multi-modal Classifier-Free Guidance (CFG) formulation:

$$\tilde{\epsilon}_\theta(z_\tau, \tau) = \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_{\text{txt}}^-) + \omega \cdot \Big[ \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_v, c_{\text{txt}}^+) - \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_{\text{txt}}^-) \Big]$$

where $\omega \ge 1.0$ is the scaling factor controlling guidance intensity toward the target garment distribution ($c_v$), while strictly bound by the physical movement defined by $Z_{\text{cond}}$.

---

## 🛠️ Code Release & Setup

> **📢 Announcement:** The full source code, pre-trained checkpoints, and detailed inference instructions are currently undergoing clean-up and internal peer-review. **The repository code will be made publicly available immediately after the paper is accepted.**

Stay tuned! Once published, this repository will include:
- Complete PyTorch training and evaluation pipelines.
- Automated preprocessing scripts for ViTPose skeletal rendering and SAM3 mask generation.
- One-click inference scripts for custom video virtual try-on.
- Pre-trained checkpoints and LoRA adaptation layers for WAN 2.2.

---

## 📚 Citation

If you find **SG-VVTON** useful for your research or applications, please consider citing our work:

```bibtex
@article{sgvvton2026,
  title={SG-VVTON: Skeletal-Guided Diffusion for High-Fidelity and Temporally Coherent Video Virtual Try-On},
  author={Your Name and Co-Authors},
  journal={arXiv preprint arXiv:xxxx.xxxxx},
  year={2026}
}
