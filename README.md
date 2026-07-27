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

To evaluate the temporal stability and visual authenticity of **SG-VVTON**, we present unified side-by-side video demonstrations. Each clip displays the **Input Frames**, the **Target Garment**, and the synthesized **Output Frames** together, highlighting performance under rapid locomotion, severe topological occlusions, and complex lighting conditions.

### 1. Fine-Grained Detail Preservation & Complex Locomotion
Our framework regularizes the latent trajectory using negative textual constraints and CLIP-derived visual embeddings, faithfully retaining intricate fabric patterns, embroidery, and weaves without blurring occluded boundaries over time.

<div align="center">
  <video src="https://github.com/MahdiKhSh/SG-VVTON/raw/main/1.mp4" width="85%" autoplay loop muted playsinline></video>
  <p><i>Demo 1: High-frequency pattern preservation under dynamic human motion.</i></p>
  <br>
  <video src="https://github.com/MahdiKhSh/SG-VVTON/raw/main/2.mp4" width="85%" autoplay loop muted playsinline></video>
  <p><i>Demo 2: Robust spatiotemporal coherence during severe anatomical occlusions.</i></p>
</div>

### 2. Multi-Garment Generalization & Photometric Adaptation
By incorporating embedded LoRA layers, the network dynamically adapts garment shading, wrinkles, and ambient shadows to complex scene illumination across diverse apparel categories—**all without requiring auxiliary 3D physical simulators.**

<div align="center">
  <video src="https://github.com/MahdiKhSh/SG-VVTON/raw/main/3.mp4" width="85%" autoplay loop muted playsinline></video>
  <p><i>Demo 3: Photometric adaptation and realistic ambient shading.</i></p>
  <br>
  <video src="https://github.com/MahdiKhSh/SG-VVTON/raw/main/4.mp4" width="85%" autoplay loop muted playsinline></video>
  <p><i>Demo 4: Generalization across complex apparel categories and unconstrained backgrounds.</i></p>
  <br>
  <video src="https://github.com/MahdiKhSh/SG-VVTON/raw/main/5.mp4" width="85%" autoplay loop muted playsinline></video>
  <p><i>Demo 5: Seamless identity preservation and fabric mechanics.</i></p>
</div>

---

## 📖 Abstract

While recent Video Virtual Try-On (VVTON) methods incorporate temporal attention modules, they frequently struggle to maintain visual fidelity and motion consistency simultaneously, often suffering from temporal instability and detail degradation under complex locomotion. 

In this work, we propose **SG-VVTON**, an end-to-end generative framework that integrates discriminative vision backbones into a large-scale video diffusion architecture. Rather than relying on global feature diffusion or auxiliary 3D physical simulators, our pipeline:
1. Extracts deterministic skeletal priors via **ViTPose** whole-body estimation.
2. Isolates semantic garment boundaries using **SAM3** video segmentation.
3. Directly conditions the denoising trajectory of a **14B-parameter diffusion backbone (WAN 2.2)**, enforcing strict anatomical alignment and spatiotemporal coherence.

---

## 🚀 Key Features

- **🔥 Multimodal Latent Video Diffusion**: Synthesizes fluid fabric mechanics and complex deformations directly within the compressed latent space of a 14B-parameter DiT backbone.
- **🦴 Dynamic Pose & Kinematic Guidance**: Eliminates inter-frame instability and anatomical hallucinations by injecting continuous whole-body skeletal graphs into the conditioning tensor.
- **🎯 Precise Semantic Isolation**: Utilizes SAM3 tracking to isolate garment masks ($m_{\text{garment}}$), facial identity ($m_{\text{face}}$), and background context ($m_{\text{bg}}$), preventing artificial boundary transitions.
- **💡 Dual Visual-Lexical Conditioning**: Employs CLIP-Vision texture embeddings ($c_v$) combined with structured positive/negative lexical prompts ($c_{\text{txt}}^+, c_{\text{txt}}^-$) via a Multi-Modal CFG formulation to eliminate color shift and transparency artifacts.

---

## 🏗️ Architecture Overview

The denoising trajectory is modulated at each timestep $\tau$ using our multi-modal Classifier-Free Guidance (CFG) formulation:

$$\tilde{\epsilon}_\theta(z_\tau, \tau) = \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_{\text{txt}}^-) + \omega \cdot \Big[ \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_v, c_{\text{txt}}^+) - \epsilon_\theta(z_\tau, \tau, Z_{\text{cond}}, c_{\text{txt}}^-) \Big]$$

where $\omega \ge 1.0$ controls the guidance intensity toward the target garment distribution while strictly bound by the kinematic motion signal $Z_{\text{cond}}$.

---

## 🛠️ Installation & Setup

### 1. Clone the Repository
```bash
git clone [https://github.com/MahdiKhSh/SG-VVTON.git](https://github.com/MahdiKhSh/SG-VVTON.git)
cd SG-VVTON
