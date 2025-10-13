# Landsat-TIR-SISR  
**Experimental Single-Image Super-Resolution (SISR) for Landsat Thermal Infrared Data**

---

## Overview

This repository contains a minimal research implementation for **single-image super-resolution (SISR)** of **Landsat thermal infrared (TIR)** imagery using a **SwinIR-based network**.  
It is designed for participants of the **Landsat SISR Experimental Competition**, aiming to find a practical and effective way to apply super-resolution to public thermal products that have already been upsampled or projected.

Only the essential components are included for transparency and reproducibility:

sisr_auto_landsat_tir_single_band.py # Complete end-to-end pipeline for Landsat TIR (1-band UInt16/Float32)
inference.py # Model inference using SwinIR-based network
network_architecture.py # Network architecture (adapted from SwinIR)

---

## Pre-trained Models

Pre-trained models for this experiment (denoted **m-2 family**) are available here:

🔗 [Google Drive – m-2 Weights](https://drive.google.com/drive/folders/1xeECUR_DYOrPYHPki4vLWt-IaUY3NB89?usp=sharing)

These models are trained specifically for **native resolution TIR imagery** (e.g., Landsat Band 10/11) and do not work for upsampled TIR imagery.

---

## Usage

### 1. Dependencies
Install Python 3.8+ and required packages:
```bash
pip install numpy opencv-python torch torchvision
For GeoTIFF I/O:
sudo apt-get install gdal-bin python3-gdal
2. Run the Landsat TIR SISR Pipeline
python sisr_auto_landsat_tir_single_band.py <input.tif> <output_dir> <weights.pth> [-COG] [-CLEAN]
Arguments:
<input.tif>: Input Landsat TIR GeoTIFF (UInt16 or Float32)

<output_dir>: Output directory for intermediate and final products

<weights.pth>: Path to m-2 pre-trained model weights

-COG (optional): Generate a Cloud-Optimized GeoTIFF

-CLEAN (optional): Delete intermediate PNGs and temporary tiles after completion

Example:
python sisr_auto_landsat_tir_single_band.py L8_TIR_20230614.tif out_dir pre-trained-models/m-2_psnr.pth -COG
The script will:

Automatically preprocess the input (GeoTIFF → PNG + metadata header)

Run SwinIR inference using inference.py

Restore geospatial metadata and generate the final super-resolved GeoTIFF

Output Description
Final Output: <basename>.srr.tif
Super-resolved GeoTIFF at 4× resolution, with original projection and nodata preserved.

Intermediate Files: PNG and .x4header.tif files (removed automatically if -CLEAN flag used).

Optional: Cloud-Optimized GeoTIFF (-COG) for large datasets.

Acknowledgements and Intellectual Property Rights (IPR)
This implementation and its model architecture are based on the open-source SwinIR project:

Liang, J., Cao, J., Sun, G., Zhang, K., Van Gool, L., & Timofte, R. (2021).
SwinIR: Image Restoration Using Swin Transformer
GitHub: https://github.com/JingyunLiang/SwinIR

The network_architecture.py and inference.py scripts in this repository adapt and extend the original SwinIR implementation for the specific case of geospatial single-band (TIR) Landsat imagery.

All intellectual property rights of the SwinIR architecture remain with the original authors and contributors.
This repository only provides derived, research-oriented code for experimentation under fair academic use.

Research-Only Disclaimer
This repository and its contents are provided strictly for research and educational purposes.
Commercial use, redistribution, or modification for proprietary applications is not permitted without explicit written consent from the respective right holders.

All materials are provided “as is,” without warranty of any kind.

Citation
If you use this repository in your research or competition submission, please cite both:

Tao, Y. (Surrey AI Imaging Limited), Landsat-TIR-SISR Experimental Toolbox, GitHub repository, 2025.
https://github.com/[YOUR_ORG]/Landsat-TIR-SISR

and

Liang, J. et al. (2021). SwinIR: Image Restoration Using Swin Transformer, GitHub repository.
https://github.com/JingyunLiang/SwinIR

Contact
For academic or research collaboration enquiries, please contact:
Dr. Yu Tao
Surrey AI Imaging Limited
✉️ yu.tao@saiil.co.uk
