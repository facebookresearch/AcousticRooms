# AcousticRooms Dataset

### From CVPR 2025 Paper: [*Hearing Anywhere in Any Environment*](https://arxiv.org/abs/2504.10746)
**Authors:**  
Xiulong Liu¹, Anurag Kumar², Paul Calamia², Sebastia V. Amengual², Calvin Murdock²,  
Ishwarya Ananthabhotla², Philip Robinson², Eli Shlizerman¹, Vamsi Krishna Ithapu², Ruohan Gao³  
¹University of Washington, ²Meta, ³University of Maryland, College Park

---

## 🏠 Overview

**AcousticRooms** is a large-scale synthetic room impulse response (RIR) dataset designed for cross-room RIR prediction tasks. It includes over **300,000 single-channel RIRs** simulated across **260 rooms** spanning **10 categories**, such as apartment, auditorium, office, and cafe. Each room features high-quality 3D spatial geometry and randomized material properties drawn from a diverse library of **332 acoustic materials** across **11 categories**.
![Simulation Setup](sim_setup.png)

---

## 🎯 Key Features

- 260 professionally designed 3D room geometries from 10 room types
- Over 300K high-quality RIRs simulated using hybrid acoustic simulation (wave + geometric)
- 332 real-world acoustic materials randomly assigned to room surfaces
- Diverse room sizes (20 m³ – 1000 m³) and layouts
- Source-receiver configurations with spatially valid random sampling

---

## 🔬 Simulation Setup

### Acoustic Modeling

Simulations are run using the **[Treble](https://www.treble.tech/)** acoustic simulation platform in hybrid mode:
- **Wave-based simulation** for low frequencies (< 710 Hz)
- **Geometric-based simulation** for high frequencies (> 710 Hz), using:
  - Image-source method up to order 4 with 50k rays
  - Stochastic ray-tracing for higher orders with 5000 rays
- RIRs simulated until 60dB energy decay

### Source & Receiver Placement

- 10–100 omnidirectional sources and 25–100 monaural receivers per room
- Placement constraints:
  - ≥ 0.5m from surfaces
  - ≥ 1.0m between sources
  - ≥ 0.5m between sources and receivers
- Valid locations sampled using spatial point-picking algorithm

### Material Assignment

- Surfaces (walls, floor, ceiling, furniture) are semantically labeled
- Each label mapped to one of 11 material categories
- Randomized selection of specific material with realistic acoustic coefficients from a library of **332 materials**
- Diverse acoustic properties across geometrically similar rooms

---

## 📁 Dataset Contents

This repository includes the following files and folders:

| File/Folder | Description |
|-------------|-------------|
| `single_channel_ir.zip` | 300K normalized, single-channel RIR waveforms (with 22.05kHz sampling rate) across all 10 room categories. Naming: `S{sourceID}_R{receiverID}_hybrid_IR.wav`. |
| `metadata.zip` | JSON metadata for each RIR pair, including `[x, y, z]` positions of source and receiver |
| `depth_map.zip` | Panoramic (equirectangular) depth maps captured at each receiver location, each depth map is named as `{receiverID}.npy` |
| `room_mesh_obj_format/` | 3D mesh geometries of all rooms in `.obj` format |
| `material_library/` | Acoustic material definitions including absorption/reflection coefficients |
| `simulation_info/` | Configuration files and simulation parameters for selected rooms |

---

## Usage for RIR prediction task
**AcousticRooms** is used as a benchmark for cross-room RIR prediction task in the paper. If you are interested in this task, please check out the third-party implementation of the xRIR framework proposed in the CVPR paper at https://github.com/DragonLiu1995/xRIR_code.

---

## 📄 License

**AcousticRooms** is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.  
You are free to share and adapt the dataset, even for commercial use, as long as proper attribution is given.

See the [LICENSE](./LICENSE) file for full terms.

---

## 📖 Citation

If you use this dataset in your research, please cite the following paper:

```bibtex
@inproceedings{liu2025haae,
  title = {Hearing Anywhere in Any Environment},
  author = {Liu, Xiulong and Kumar, Anurag and Calamia, Paul and Garí, Sebastià V. Amengual and Murdock, Calvin and Ananthabhotla, Ishwarya and Robinson, Philip and Shlizerman, Eli and Ithapu, Vamsi Krishna and Gao, Ruohan},
  booktitle = {Conference on Computer Vision and Pattern Recognition (CVPR)},
  year = {2025},
}
