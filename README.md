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

pip install numpy opencv-python torch torchvision

For GeoTIFF I/O:
sudo apt-get install gdal-bin python3-gdal

### 2. Run the Landsat TIR SISR Pipeline

python sisr_auto_landsat_tir_single_band.py <input.tif> <output_dir> <weights.pth> [-COG] [-CLEAN]

#### Arguments:

<input.tif>: Input Landsat TIR GeoTIFF (UInt16 or Float32)

<output_dir>: Output directory for intermediate and final products

<weights.pth>: Path to m-2 pre-trained model weights

-COG (optional): Generate a Cloud-Optimized GeoTIFF

-CLEAN (optional): Delete intermediate PNGs and temporary tiles after completion

#### Example:

python sisr_auto_landsat_tir_single_band.py L8_TIR_20230614.tif out_dir pre-trained-models/m-2_psnr.pth -COG

#### The script will:

1. Automatically preprocess the input (GeoTIFF → PNG + metadata header)

2. Run SwinIR inference using inference.py

3. Restore geospatial metadata and generate the final super-resolved GeoTIFF

#### Output Description

Final Output: <basename>.srr.tif

Super-resolved GeoTIFF at 4× resolution, with original projection and nodata preserved.

Intermediate Files: PNG and .x4header.tif files (removed automatically if -CLEAN flag used).

Optional: Cloud-Optimized GeoTIFF (-COG) for large datasets.

---

## License and Acknowledgements

This project is released under the Apache 2.0 license. This implementation's model architecture is based on the open-source SwinIR project:

Liang, J., Cao, J., Sun, G., Zhang, K., Van Gool, L., & Timofte, R. (2021).
SwinIR: Image Restoration Using Swin Transformer
GitHub: https://github.com/JingyunLiang/SwinIR

Please also follow their licenses.
All materials are provided “as is,” without warranty of any kind.

Contact
For academic or research collaboration enquiries, please contact:
Dr. Yu Tao
Surrey AI Imaging Limited
✉️ yu.tao@saiil.co.uk
