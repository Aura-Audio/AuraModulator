# AuraModulator 🌊🎛️ (v1.2.0)
**Mathematical Multi-Track Dual-Sideband Ring Modulator Array**

## 📖 Overview
**AuraModulator** is a powerful, browser-based, real-time audio DSP environment. Transforming live microphone input using extreme mathematical formulas, this engine is capable of calculating **up to 20,000 independent sine wave frequency modifiers per second**.

Powered by a pre-calculated fast sine wavetable embedded in a custom Web Audio `AudioWorkletProcessor`, you can shift, scatter, and stack frequencies (via ring modulation) without suffering audio dropouts.

No installation required. Just open the HTML file and allow microphone access.

---

## ✨ Features

### 🎛️ The Multi-Track Array Engine
* **20 Engine Buses:** Run up to 20 independent mathematical Engine groupings simultaneously.
* **1000 Tracks per Engine:** Each engine acts as a bus that can hold 1 to 1000 independent sine wave tracks.
* **Track Spacing (Spread Hz):** Assign a physical Hz distance between the tracks inside an engine (e.g. 1Hz, 5Hz, 10Hz apart) to create massive bands of frequency shifts. 
* **Zero-Overlap Stack Generator:** Instantly sweep the entire array while mathematically guaranteeing tracks never overlap:
  * **Converge to 20Hz (Down):** The array cascades downwards.
  * **Converge to 20kHz (Up):** The array cascades upwards.
  * **Split Array:** 10 engines sweep down, 10 sweep up.
* **Math Normalization:** Dynamically scales output volume using the square root of active tracks (`Math.sqrt()`) to prevent digital clipping when combining 20,000 phase-shifting signals. Phase tracks are randomized upon initialization to prevent amplitude blowout.

### 🌊 Automation & LFOs
* **Linear Frequency Sweeps:** Each engine features an independent LFO that smoothly sweeps massive track footprints across the human hearing spectrum over designated seconds (or minutes).
* **Master Array Sync:** Trigger all LFOs simultaneously to create massive, shifting walls of sound.

### 📈 Holographic Visualization & Export
* **Holographic Oscilloscope:** A completely custom visualization engine that draws the engines in the background as a rainbow spectrum. The *thickness* of the background waves visually represents the amount of tracks loaded into the engine, while speed matches the real-time logarithmic frequency. 
* **FFT Spectral Distribution:** Monitor frequency spectrums of both the raw microphone input (gray) and the filtered/processed signal (green).
* **Hardware Recording Engine:** Record your massive 20,000-track sessions directly to disk in **WAV (Uncompressed)**, **FLAC (Lossless)**, or **OPUS (WebM)** formats with an auto-stop timer.

### 🎚️ Routing
* **Pre-Modulation Bandpass:** Filter out unwanted low-end rumble or high-end hiss *before* the signal hits the math nodes.
* **AuraConv Comb Filtering:** A custom burst/gap filter that drops sample chunks at the micro-level.
* **HRTF 3D Rotation & Convolution Reverb:** Pan your resulting soundscapes in full 3D space.

---

## 🚀 Usage

1. Clone the repository or download the `AuraModulator.html` file.
2. Open `AuraModulator.html` in any modern web browser (Chrome, Edge, Firefox, or Safari).
3. Click **Start Microphone** and grant browser permissions.
4. From the top panel, ensure Tracks are set to `100` and Spread is set to `5 Hz`, then click **Generate Base Hz**.
5. Click **▶ Start All LFOs**.
6. Speak or play music into your microphone.

---
*Created as a lightweight, purely mathematical approach to extreme audio manipulation.*
