# AuraModulator 🌊🎛️ (v1.1.0)
**Mathematical Dual-Sideband Frequency Transposition Array**

## 📖 Overview
**AuraModulator** is a powerful, browser-based, real-time audio DSP environment that transforms live microphone input using a massive 20-engine frequency shifter array. 

By utilizing highly optimized `AudioWorkletProcessor` nodes, it applies Dual-Sideband Signal Multiplication (Ring Modulation) to shift incoming frequencies up and down simultaneously. Whether you are generating complex inharmonic metallic textures, deep sub-hertz phasing (0.001Hz), or cascading scale sweeps spanning 20Hz to 20,000Hz, AuraModulator handles the math in real time directly in your browser.

No installation required. Just open the HTML file and allow microphone access.

---

## ✨ Features

### 🎛️ Core DSP & Array Engines
* **20-Engine Frequency Array:** Run up to 20 independent mathematical dual-sideband frequency shifters simultaneously.
* **Dual-Sideband Shift (Ring Mod):** Multiplies live audio against internally generated sine waves to symmetrically push frequencies up and down.
* **Array Sweep Targeting:** Instantly assign mathematical relationships and directionality across all active engines:
  * **Converge to 20Hz (Down):** Spread all engines from 20kHz down to 20Hz. 
  * **Converge to 20kHz (Up):** Spread all engines from 20Hz ascending to 20kHz.
  * **Split Array:** The first 10 engines sweep downwards to 20Hz; the last 10 engines sweep upwards to 20kHz.
* **Gain-Safe Normalization:** Dynamically scales output volume using the square root of active engines (`Math.sqrt()`) to prevent digital clipping when combining multiple phase-shifting signals.

### 🌊 Automation & LFOs
* **Exponential LFO Spread:** LFO times are arrayed by default via an exponential curve (`[0.001s, 0.01s, 0.1s, 1s, 2s, 5s, 10s, 30s, 60s, 120s]`) to generate intensely complex phasing overlaps.
* **Linear Frequency Sweeps:** Each engine features an independent LFO that sweeps smoothly between target frequencies.
* **Master Array Sync:** Trigger all LFOs simultaneously to create massive, shifting walls of sound.

### 📈 Holographic Visualization & Export
* **Holographic Oscilloscope:** A completely custom visualization engine that draws *all 20 individual processing channels* in the background as a rainbow spectrum. The speed of the background waves visually represents the real-time math happening in the engines, while the main audio mix is drawn over the top as a glowing cyan waveform.
* **FFT Spectral Distribution:** Monitor frequency spectrums of both the raw microphone input (gray) and the filtered/processed signal (green).
* **Hardware Recording Engine:** Record your sessions directly to disk in **WAV (Uncompressed)**, **FLAC (Lossless)**, or **OPUS (WebM)** formats with an auto-stop timer.

### 🎚️ Routing
* **Pre-Modulation Bandpass:** Filter out unwanted low-end rumble or high-end hiss *before* the signal hits the math nodes.
* **AuraConv Comb Filtering:** A custom burst/gap filter that drops sample chunks at the micro-level.
* **HRTF 3D Rotation & Convolution Reverb:** Pan your resulting soundscapes in full 3D space.

---

## 🚀 Usage

1. Clone the repository or download the `AuraModulator.html` file.
2. Open `AuraModulator.html` in any modern web browser (Chrome, Edge, Firefox, or Safari).
3. Click **Start Microphone** and grant browser permissions.
4. Try clicking **▶ Start All LFOs** with the default spread to hear the immediate effect.
5. Enable **Speaker Out** to hear the results (use headphones to avoid feedback).

---
*Created as a lightweight, purely mathematical approach to extreme audio manipulation.*
