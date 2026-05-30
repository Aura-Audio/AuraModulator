# Architecture & DSP Engine Overview

AuraModulator is built on modern Web Audio API standards, specifically leveraging the `AudioWorklet` interface to perform extreme, real-time mathematical operations without blocking the browser's main UI thread. 

This document explains the core DSP (Digital Signal Processing) engineering that allows the app to process 20,000 simultaneous audio tracks.

## 1. The AudioWorklet Paradigm
Historically, web-based audio manipulation relied on the `ScriptProcessorNode`, which executed on the main thread. This meant that if the UI lagged (e.g., drawing complex visualizers), the audio would stutter and drop out. 

AuraModulator uses the `AudioWorkletProcessor`. The DSP code (`multitrackshifter-processor`) runs in a completely separate, high-priority audio thread. The main thread is only responsible for drawing the Holographic Oscilloscope and capturing user inputs, which it communicates to the Worklet via asynchronous `postMessage` events.

## 2. The Fast Sine Wavetable Optimization
**The Problem:** Running 20 engines, each with 1,000 tracks, requires calculating frequency phases 20,000 times per audio sample. At a standard 48kHz sample rate, calling JavaScript's native `Math.sin()` would require **~1 Billion operations per second**. This would instantly melt standard consumer CPUs and cause audio buffer underruns.

**The Solution:** Pre-calculated Wavetables.
When the Worklet initializes, it generates an 8192-point `Float32Array` containing a perfect sine wave.

```javascript
this.sineTableSize = 8192;
this.sineTable = new Float32Array(this.sineTableSize);
for(let i = 0; i < this.sineTableSize; i++) {
    this.sineTable[i] = Math.sin((i / this.sineTableSize) * Math.PI * 2);
}
```

During the live audio loop, instead of calculating a sine wave, the engine simply looks up the closest value in the array using a highly optimized bitwise floor operation:

```javascript
let phaseIdx = (eng.phases[t] * this.sineTableSize) | 0; 
mixedOutput += val * this.sineTable[phaseIdx];
```

## 3. Mathematical Ring Modulation (Dual-Sideband)
AuraModulator is fundamentally a massive Ring Modulator array. By multiplying the incoming microphone voltage (`val`) against the generated sine table value, it creates a **Dual-Sideband** effect. 

If you input a pure 1,000Hz tone and process it through a 5Hz engine track, AuraModulator simultaneously outputs a 995Hz tone and a 1,005Hz tone, eliminating the original 1,000Hz signal entirely. Multiplied across 20,000 tracks, this creates massive, dense sonic textures.

## 4. Phase Normalization & Clipping Prevention
When summing 20,000 oscillators, if they all start at Phase `0`, the resulting amplitude would instantly cause digital clipping (volume blowouts). 

To solve this:
1. **Phase Randomization:** Every track is assigned a randomized starting phase using `Float32Array.from({length: 1000}, () => Math.random())`.
2. **Square Root Normalization:** The final mixed output is divided by the square root of the total active tracks `(mixedOutput / Math.sqrt(totalActiveTracks))`. This mathematically preserves perceived loudness while providing infinite headroom.
