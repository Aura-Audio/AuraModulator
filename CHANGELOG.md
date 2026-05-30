# Changelog

All notable changes to the **AuraModulator** project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2026-05-30
### 🌟 Major Feature: The Multi-Track Wavetable Update
This update shifts the definition of an "Engine" from a single frequency line to a "Frequency Bus", expanding the app's capability from 20 oscillators to 20,000 simultaneous oscillators without dropping frames.

### Added
- **Multi-Track Engine Buses:** Engines can now hold between 1 and 1,000 individual sine wave tracks.
- **Track Spacing (Spread Hz):** Users can define the exact Hz distance between tracks inside a single engine (e.g., 1Hz, 5Hz, 10Hz).
- **Zero-Overlap Auto-Stack Sweep:** The Array Sweep generator now calculates the physical bandwidth of each engine and stacks them end-to-end, guaranteeing that none of the 20,000 tracks will ever overlap across the human hearing spectrum.

### Under the Hood (Performance Enhancements)
- **Fast Sine Wavetable:** Implemented an 8192-point pre-calculated wavetable in the `AudioWorkletProcessor`. Replacing `Math.sin()` with array lookups saves roughly 1 billion CPU operations per second.
- **Phase Randomization:** Track phases are now randomized upon initialization to prevent instant digital clipping and volume blowouts when 20,000 signals sum together.
- **Deep Math Normalization:** Output is now divided by the square root of *total active tracks* (rather than active engines) to preserve perfectly normalized audio headroom.

---

## [1.1.0] - 2026-05-30
### 🌟 Major Feature: Holographic Array & Sweep Targets
This update overhauled the visualization engine and introduced fast macros for organizing frequency sweeps.

### Added
- **Holographic Oscilloscope:** Completely rewrote the time-domain visualizer. The background now renders all 20 active engines simultaneously as a glowing rainbow spectrum. The visual wave speed dynamically matches the real-time logarithmic mathematical `Hz` of the engine.
- **Array Sweep Targeting:** Added a dropdown to instantly route massive frequency cascades:
  - *Converge to 20Hz:* Spreads starting frequencies from 20-20,000Hz sweeping downwards.
  - *Converge to 20kHz:* Sweeps the array upwards.
  - *Split:* Splits the array perfectly in half (10 engines sweep down, 10 engines sweep up).

### Changed
- **LFO Spread Default:** Engines now initialize with an exponential time spread `[0.001s, 0.01s, 0.1s, 1s, 2s, 5s, 10s, 30s, 60s, 120s]` to generate incredibly complex phasing out-of-the-box.
- Replaced the old "Batch Spacing" module with the new "Array Sweep" UI element.

---

## [1.0.0] - 2026-05-30
### 🎉 Initial Release
*AuraModulator* was officially forked/evolved from the *MicScaler* framework. The core DSP was completely rewritten to focus on frequency shifting rather than amplitude scaling.

### Added
- **20-Engine Frequency Array:** Deployed the custom `AudioWorkletProcessor` to run up to 20 independent mathematical dual-sideband frequency shifters (Ring Modulators) simultaneously.
- **Batch Spacing Generator:** Added arithmetic (+) and geometric (x) spacing modes to cascade frequencies across the array.
- **Linear LFO Sweeps:** Implemented start/end Hz targets and LFO seconds to smoothly sweep pitch modulations over time.
- **Hardware Recording:** Built-in recording to uncompressed WAV, FLAC, and OPUS direct from the browser.
- **Pre-Modulation Bandpass & Comb Filtering:** Preserved the AuraConv and Bandpass processing stages from the legacy MicScaler architecture.
- **Gain-Safe Mix Bus:** Implemented root-mean-square normalization to prevent audio clipping when combining 20 ring modulators.
