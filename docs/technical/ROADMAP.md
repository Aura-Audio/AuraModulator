# Development Roadmap

The following outlines the planned feature trajectory for AuraModulator, moving from UI enhancements to massive core DSP expansions and eventually transitioning to native desktop formats.

## Phase 1: Workflow & State Management (v1.3.x)
* **JSON Preset System:** Implement `localStorage` and file export/import capabilities allowing users to save their exact Array sweeps, LFO times, and routing configurations as downloadable `.json` preset files.
* **Wet/Dry Crossfader:** A master visual slider to blend the raw microphone input with the processed mathematical array output.
* **Responsive UI Refinements:** Collapse/Expand toggles for the 20 engine cards to save screen real estate on smaller laptop monitors.

## Phase 2: Hardware Connectivity (v1.4.x)
* **Web MIDI API Integration:** Allow users to map external MIDI hardware (knobs, faders, mod-wheels) directly to AuraModulator parameters.
  * *Example:* Mapping a MIDI mod-wheel to the `Spread Hz` parameter to dynamically expand and collapse the frequency band live.
* **MIDI Pitch Tracking:** Trigger specific "Base Hz" frequencies using a MIDI keyboard rather than the automated LFO sweep.

## Phase 3: Core DSP Expansions (v2.0.0)
* **Single-Sideband (SSB) Mode / Pitch Shifting:** Implement a Hilbert Transform within the `AudioWorklet`. This will allow users to toggle an engine from "Dual-Sideband" (Ring Modulation) to "Single-Sideband" (Pure Pitch Shifting—moving audio *only* up or *only* down).
* **Custom Wavetables:** Expand the Fast Sine Wavetable to include Square, Triangle, and Sawtooth arrays for much harsher, industrial, harmonic textures.
* **ADSR Envelopes per Engine:** Allow engines to trigger their volume based on an Attack/Decay/Sustain/Release envelope rather than constant output.

## Phase 4: Desktop & DAW Integration (v3.0.0)
* **Standalone Electron App:** Wrap the web environment in an Electron container for offline, native desktop use with direct OS-level audio driver access (ASIO/CoreAudio) for lower latency.
* **VST3 / AU Plugin Port:** Translate the JavaScript `AudioWorklet` logic into C++ using the **JUCE** framework. This will allow AuraModulator to be loaded directly onto tracks inside Ableton Live, Logic Pro, and FL Studio.
