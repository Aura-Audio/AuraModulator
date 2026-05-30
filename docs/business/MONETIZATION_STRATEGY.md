# Monetization Strategy: AuraModulator

AuraModulator will utilize a multi-phased monetization approach, beginning with a freemium Web App (SaaS) model to capture maximum market share, followed by a traditional Desktop/VST software release.

## Phase 1: Freemium Web App (SaaS MRR)
The goal is to eliminate barriers to entry. Anyone can visit the URL and immediately play with the engine, but power-user features are gated.

### Tier 1: Free (Basic Access)
*   **Features:** Up to 5 Engines, maximum 100 tracks per engine (500 total tracks). 
*   **Exporting:** Low-quality OPUS (WebM) recording only. Maximum 1-minute auto-stop timer.
*   **UI:** Subtle watermark on the Holographic Oscilloscope.
*   **Purpose:** Lead generation, viral sharing, and user onboarding.

### Tier 2: AuraModulator PRO ($4.99/month or $39/year)
*   **Features:** Unlocks all 20 Engines and up to 1,000 tracks per engine (20,000 total tracks).
*   **Exporting:** High-resolution Lossless FLAC and uncompressed WAV recording. Up to 120-minute auto-stop timer.
*   **Workflow:** Unlock Preset Management (Save/Load `.json` states) and MIDI Controller mapping.
*   **Revenue Projection:** Converting 2,000 users to the $39/year tier generates **~$78,000 in ARR**. Because all heavy DSP processing is executed *client-side* (in the user's browser via Web Audio API), server/hosting costs remain virtually zero.

## Phase 2: The Studio Plugin (VST3 / AU / AAX)
Many professional sound designers refuse to leave their DAW (Digital Audio Workstation). To capture this high-value market, the `AudioWorklet` C++/JS logic will be ported to a traditional plugin wrapper (using frameworks like JUCE or RNBO).

*   **Pricing:** $49 - $79 One-Time Purchase.
*   **Distribution:** PluginBoutique, Splice, and direct website sales.
*   **Value Add for DAW Users:** Full parameter automation within Ableton/Logic, exact tempo-syncing to DAW grids, and offline bounce capabilities.
*   **Revenue Projection:** 5,000 units sold at an average of $49 generates **$245,000**.

## Phase 3: B2B Educational Licensing
Targeting university music technology and DSP programs.
*   **Pricing:** $499/year for a site-wide campus license.
*   **Value Add:** Gives educators a stunning visual tool to teach phase, frequency modulation, and sidebands without requiring IT departments to install heavy software on lab computers.
