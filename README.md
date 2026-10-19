# Signals-And-System--Deep-learning-
A hybrid speech enhancement system built in MATLAB combining GRU deep learning, db4 Wavelet Transforms, and DSP filtering to isolate and amplify human voice from chaotic background noise
# Speech Enhancement System: Hybrid AI & DSP Pipeline

**Authors:** Shivam Pagar, Yash Kharat, Dhruv Patil  
**Institution:** Vidyalankar Institute of Technology, Mumbai  

## Project Overview
This project presents a robust, automated speech enhancement engine built entirely in MATLAB. It utilizes a hybrid architecture to isolate human speech from heavy background noise. Instead of relying solely on artificial intelligence, this system combines a deep learning model with a traditional Digital Signal Processing (DSP) mastering chain to produce crisp, broadcast-ready audio. 

## System Architecture

The pipeline processes multi-minute audio files by slicing them into 5-second chunks and running them through a two-stage cleaning process:

**1. The AI Engine (Signal Teardown & Denoising)**
*   **Wavelet Decomposition:** Utilizes 'db4' Discrete Wavelet Transforms (`dwt`/`idwt`) to separate the core speech structure from high-frequency noise textures.
*   **GRU Network:** A trained Gated Recurrent Unit (GRU) analyzes the time-series flow of the audio, retaining human vocal patterns while discarding chaotic noise.
*   **Detail Coefficient Suppression:** High-frequency noise artifacts are mathematically choked to 1% during signal reconstruction.

**2. The Virtual Sound Engineer (DSP Post-Processing)**
*   **Envelope-Based Noise Gate:** Calculates volume trends over 50ms windows. If the volume drops below an 8% threshold, the audio is forcefully flatlined and the silence is truncated to physically stitch spoken words together.
*   **Butterworth Bandpass Filter:** A 4th-order brick-wall filter (300 Hz - 3400 Hz) that strips sub-bass traffic rumble and high-end static.
*   **Pre-Emphasis Filter:** Mathematically boosts presence frequencies to make the voice crisp and upfront.
*   **Peak Normalization:** Scans for the loudest syllable and proportionally scales the final stitched track to 95% maximum volume without clipping.

## Prerequisites
*   **MATLAB R2023a or newer** (Compatible with MATLAB Online).
*   *Note: This script is heavily optimized using core mathematics and does **not** require the specialized MATLAB Audio Toolbox, preventing licensing errors during academic evaluation.*

## How to Run the Pipeline
Click Run.

Outputs
Upon completion, the script automatically generates:

FINAL_Production_Cleaned.wav: The fully processed, stitched, and amplified audio track.

Visual Proof Dashboard: A 2x2 grid UI displaying side-by-side Waveforms (proving silence truncation) and Spectrograms (proving broadband noise elimination).

1. Clone this repository and open the project folder in MATLAB.
2. Ensure your noisy audio file (e.g., `.wav` or `.mp3`) and the trained AI model (`Final_Speech_Model.mat`) are in the current working directory.
3. Open `Production_Enhancer.m`.
4. Navigate to **Line 6** and update the `fileName` variable to match your specific audio file:
   ```matlab
   fileName = 'your_audio_file.wav';
