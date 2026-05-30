# AuraModulator 🌊🎛️
**Mathematical Dual-Sideband Frequency Transposition Array**

## 📖 Overview
**AuraModulator** is a powerful, browser-based, real-time audio DSP environment that transforms live microphone input using a massive 20-engine frequency shifter array. Born as an evolution of the *MicScaler/AuraScaler* framework, AuraModulator pivots from amplitude scaling to **Frequency Math**. 

By utilizing highly optimized `AudioWorkletProcessor` nodes, it applies Dual-Sideband Signal Multiplication (Ring Modulation) to shift incoming frequencies up and down simultaneously. Whether you are generating complex inharmonic metallic textures, deep sub-hertz phasing (0.1Hz / 0.01Hz), or cascading harmonic harmonic/octave scales, AuraModulator handles the math in real time directly in your browser.

No installation required. Just open the HTML file and allow microphone access.

---

## ✨ Features

### 🎛️ Core DSP & Array Engines
* **20-Engine Frequency Array:** Run up to 20 independent mathematical dual-sideband frequency shifters simultaneously.
* **Dual-Sideband Shift (Ring Mod):** Multiplies live audio against internally generated sine waves to symmetrically push frequencies up and down.
* **Batch Spacing Calculator:** Instantly assign mathematical relationships across all active engines:
  * **Arithmetic Spacing (+):** Step frequencies by exact Hz amounts (e.g., 5Hz, 10Hz, 15Hz, 20Hz...).
  * **Geometric Spacing (x):** Multiply frequencies for octave or harmonic stacking (e.g., 5Hz, 10Hz, 20Hz, 40Hz...).
* **Gain-Safe Normalization:** Dynamically scales output volume using the square root of active engines (`Math.sqrt()`) to prevent digital clipping when combining multiple phase-shifting signals.

### 🌊 Automation & LFOs
* **Linear Frequency Sweeps:** Each engine features an independent LFO that sweeps from a designated Start Hz to an End Hz over a configurable duration (up to 600 seconds).
* **Master Array Sync:** Trigger all LFOs simultaneously to create massive, shifting walls of sound.

### 🎚️ Pre-Processing & Routing
* **Pre-Modulation Bandpass:** Filter out unwanted low-end rumble or high-end hiss *before* the signal hits the math nodes.
* **Math Gating & Output Gating:** Hard-chop the mathematical input or the physical speaker output down to the millisecond to create rhythmic stutters.
* **AuraConv Comb Filtering:** A custom burst/gap filter that drops sample chunks at the micro-level.
* **HRTF 3D Rotation & Convolution Reverb:** Pan your resulting soundscapes in full 3D space.

### 📊 Visualization & Export
* **Real-time Oscilloscope:** High-framerate time-domain output visualizer.
* **FFT Spectral Distribution:** Monitor frequency spectrums of both the raw microphone input (gray) and the filtered/processed signal (green).
* **Hardware Recording Engine:** Record your sessions directly to disk in **WAV (Uncompressed)**, **FLAC (Lossless)**, or **OPUS (WebM)** formats with an auto-stop timer.

---

## 🚀 Usage

1. Clone the repository or download the `AuraModulator.html` file.
2. Open `AuraModulator.html` in any modern web browser (Chrome, Edge, Firefox, or Safari).
3. Click **Start Microphone** and grant browser permissions.
4. Adjust your **Batch Spacing** (e.g., 5Hz Base, `x` mode, 2 Step) and click **Apply to Array**.
5. Enable **Speaker Out** to hear the results (use headphones to avoid feedback).

---

## 🛣️ Roadmap

Here is what is currently planned for future updates to the AuraModulator engine:

* [ ] **Single-Sideband (SSB) Mode:** Implement Hilbert Transforms within the AudioWorklet to allow *pitch shifting* (moving frequencies *only* up or *only* down, rather than dual-sideband ring modulation).
* [ ] **Custom Modulator Waveforms:** Allow engines to multiply using Triangle, Square, or Sawtooth waves instead of purely Sine waves for harsher, noisier harmonics.
* [ ] **Preset Manager:** Save and load array configurations (Hz bases, LFO speeds, and routing settings) to local storage or downloadable JSON files.
* [ ] **MIDI Integration:** Use the Web MIDI API to control the "Base Hz" or LFO triggers via external MIDI keyboards/controllers.
* [ ] **Wet/Dry Mix Node:** Add a master crossfader to blend the raw microphone input with the fully processed array output.
* [ ] **Node-Based UI View:** A secondary view mode to visually map the signal chain with draggable cables.

---
*Created as a lightweight, purely mathematical approach to extreme audio manipulation.*
