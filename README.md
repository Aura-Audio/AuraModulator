<div align="center">
  
  # 🌊 AuraModulator
  **High-Performance, Browser-Based Multi-Track Ring Modulation Array**

  [![Version](https://img.shields.io/badge/version-1.3.0-blue.svg?style=flat-square)](#)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](#)
  [![Environment](https://img.shields.io/badge/env-Browser%20(Web%20Audio%20API)-00e5ff.svg?style=flat-square)](#)
  [![CPU Optimization](https://img.shields.io/badge/DSP-Zero--Branch%20Optimized-76ff03.svg?style=flat-square)](#)

  <p align="center">
    AuraModulator is a zero-installation Digital Signal Processing (DSP) environment capable of calculating <strong>20,000+ simultaneous sine-wave frequency modifiers</strong> in real-time natively within a web browser.
  </p>

  [Getting Started](#-getting-started) •
  [Architecture](#-architecture--performance) •
  [Features](#-key-features) •
  [Roadmap](#-roadmap)

</div>

---

## 📖 Overview

AuraModulator pushes the boundaries of the Web Audio API. Designed for experimental electronic musicians, sound designers, and DSP engineers, it transforms live microphone input using a massive array of mathematical dual-sideband frequency shifters (Ring Modulators).

By leveraging a custom `AudioWorkletProcessor`, a pre-calculated fast sine wavetable, and branchless DSP inner loops, AuraModulator achieves native-level performance without the need for external VSTs, DAWs, or C++ compilation.

## 🚀 Getting Started

AuraModulator requires **zero installation** and has **zero dependencies**.

1. Clone the repository or download the source:
   ```sh
   git clone https://github.com/yourusername/AuraModulator.git
   ```
2. Open `index.html` (or `AuraModulator.html`) in any modern, Web Audio-compliant browser (Chrome, Edge, Firefox, Safari).
3. Grant microphone permissions when prompted.
4. Set **Tracks** to `100`, click **Generate Base Hz**, and click **▶ Start All LFOs**.

> **⚠️ Warning:** AuraModulator generates extreme frequencies. Please lower your volume and use headphones to prevent feedback loops before starting the microphone.

## 🧠 Architecture & Performance

As of `v1.3.0`, the core engine has been heavily optimized to prevent CPU bottlenecking, Main Thread blocking, and Garbage Collection (GC) stutters.

### 1. Zero-Branch DSP Inner Loop
The audio processing loop executes millions of times per second. Traditional float-based phase tracking requires `if (phase >= 1.0)` branch checks, which destroy CPU branch prediction. 
AuraModulator v1.3.0 utilizes **32-bit Unsigned Integer Accumulators**. Phases automatically wrap at `4,294,967,295`, allowing for completely branchless, uninterrupted mathematical execution.

### 2. Fast Sine Wavetable
Instead of calling JavaScript's native `Math.sin()` 960+ million times per second, the engine pre-allocates an `8192-point` Float32Array sine wavetable. Values are fetched using highly optimized bitwise floor operations (`phase >>> 19`).

### 3. Canvas Decimation & Low-GC Telemetry
UI thread CPU usage has been reduced by 80% via canvas decimation (rendering every 4th sample without visual degradation). Telemetry between the Audio Thread and Main Thread now utilizes pre-allocated Float32 buffers, eliminating JSON serialization and preventing browser Garbage Collection spikes.

## ✨ Key Features

| Category | Feature | Description |
| :--- | :--- | :--- |
| **Routing** | **20 Frequency Buses** | Route audio through up to 20 independent mathematical Engine groupings. |
| **Scale** | **1,000 Tracks per Bus** | Each engine can house up to 1,000 independent sine wave tracks, allowing for 20,000 active oscillators. |
| **Math** | **Zero-Overlap Stack Generator** | Automatically calculates bandwidth footprints to stack frequency bands sequentially, ensuring 0% track overlap across the 20Hz-20kHz spectrum. |
| **Visuals** | **Holographic Oscilloscope** | Real-time, multi-layered visualizer displaying the active mathematical state of all 20 engines simultaneously. |
| **I/O** | **Direct-to-Disk Export** | Native recording of processed audio output to `WAV` (Uncompressed), `FLAC` (Lossless), or `OPUS` formats. |

## 📂 Project Structure

```text
AuraModulator/
├── docs/                        # Project documentation
│   ├── business/                # GTM, Market Sizing, Monetization plans
│   └── technical/               # DSP Architecture, API Reference
├── assets/                      # Audio samples and UI screenshots
├── CHANGELOG.md                 # Semantic version history
├── index.html                   # 🚀 Main Application Entry Point
└── README.md                    # Project overview
```

## 🛣 Roadmap

AuraModulator is under active development. Current engineering priorities include:

- [ ] **State Management:** Implement JSON import/export for saving LFO configurations and Array sweeps.
- [ ] **Hardware Connectivity:** Web MIDI API integration to map hardware mod-wheels/faders to Engine `Spread Hz` parameters.
- [ ] **DSP Expansion:** Hilbert Transform implementations for Single-Sideband (SSB) Pitch Shifting modes.
- [ ] **Native Wrappers:** Porting the isolated JS Worklet logic to C++ (JUCE) for VST3/AU distribution.

## 🤝 Contributing

We welcome contributions from the audio engineering and web development communities. 

1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

---
<div align="center">
  <i>Built for the love of digital signal processing.</i>
</div>
