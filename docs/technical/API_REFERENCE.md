# Internal API Reference & Message Protocol

Because AuraModulator isolates its heavy DSP calculations in an `AudioWorkletProcessor`, the Main Thread (UI) and the Audio Thread (Worklet) must communicate via an asynchronous `MessagePort` API. 

This document outlines the current internal API structure for developers looking to modify the codebase or build external controllers.

## 1. Message Transport
Communication occurs via `liveMathNode.port.postMessage(payload)`. 
The `payload` must be a JSON object containing a `type` string to define the action.

---

## 2. Main Thread -> AudioWorklet (Incoming Commands)

### A. Global Configuration Update
Updates the master routing, gating, and comb-filtering (AuraConv) parameters.
* **Type:** `config`
* **Payload Example:**
  ```json
  {
    "type": "config",
    "inGateEnabled": true,
    "inGateSamples": 4800,
    "acEnabled": false,
    "acBurst": true,
    "acSamples": 100
  }
  ```

### B. Engine Specific Update
Modifies the parameters of a specific frequency bus (Engine) in the array.
* **Type:** `updateEngine`
* **Parameters:**
  * `index` (int): The array index of the engine (0 - 19).
  * `engineData` (object): The specific parameters to patch.
* **Payload Example:**
  ```json
  {
    "type": "updateEngine",
    "index": 4,
    "engineData": {
      "active": true,
      "tracks": 100,
      "trackSpread": 5.0,
      "lfoStart": 20.0,
      "lfoEnd": 500.0,
      "lfoTime": 15.5,
      "lfoActive": true,
      "lfoSamples": 0
    }
  }
  ```

---

## 3. AudioWorklet -> Main Thread (Outgoing Telemetry)

To keep the UI visualizers and text readouts in sync with the DSP math, the Worklet broadcasts its current state every 5 processing frames.

### A. Status Broadcast
Broadcasts the exact current mathematical base frequency of all 20 engines based on their respective LFO progressions.
* **Type:** `status`
* **Payload Example:**
  ```json
  {
    "type": "status",
    "freqs": [
      20.001, 
      520.450, 
      1020.900, 
      "... (up to index 19)"
    ]
  }
  ```
* **Receiver Implementation (Main Thread):**
  ```javascript
  liveMathNode.port.onmessage = (e) => {
      if (e.data.type === 'status') {
          // e.data.freqs array is used to drive the Holographic Oscilloscope speeds
          currentEngineFreqs = e.data.freqs; 
      }
  };
  ```

---

## 4. Future Public API (NPM Module Draft)
In the future, the core Worklet could be exported as a headless NPM package for other Web Audio developers to use in their own web applications.

```javascript
import { AuraModulatorEngine } from 'auramodulator-core';

const audioCtx = new AudioContext();
const auraEngine = new AuraModulatorEngine(audioCtx);

// Example Public Methods:
auraEngine.setGlobalSpread(10.0); // Sets tracks 10Hz apart
auraEngine.sweepArray('split');   // Executes the down/up zero-overlap split
auraEngine.connect(audioCtx.destination);
```
