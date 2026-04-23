# 📡 AM Communication System — ADALM-Pluto & GNU Radio

A complete **Amplitude Modulation (AM) communication system** implemented using **GNU Radio Companion (GRC)** and **ADALM-Pluto SDR**.  
The system supports both **monotone (sine wave)** and **audio signal transmission and reception**, and demonstrates practical SDR-based communication design.

---
### Prepared by  
- [Yasmin Al Shawawrh](https://github.com/YasminAlShawawrh)
- Basmala Abu Hakema
- Layal Hajji
- 
## Table of contents

- [System overview](#system-overview)
- [Signal types](#signal-types)
- [Flowgraph descriptions](#flowgraph-descriptions)
- [Parameter tuning](#parameter-tuning)
- [Results](#results)
- [Limitations](#limitations)
- [How to run](#how-to-run)
- [Future work](#future-work)

---

## System overview

The project implements a full communication chain:

| Stage | Description |
|------|------------|
| Transmitter | Generates and modulates signals using AM |
| Channel | Wireless transmission via ADALM-Pluto |
| Receiver | Demodulates and reconstructs original signal |

The system works with:
- **Monotone signals (sine waves)**
- **Audio signals (WAV input)**

Both are transmitted, received, and analyzed in real time.

---

## Signal types

### Monotone Signal
- Simple sine wave input
- Used to validate AM modulation/demodulation
- Easy to observe in time and frequency domains

### Audio Signal
- Input from WAV file
- Resampled for SDR compatibility
- Played back after reception

---

## Flowgraph descriptions

### `am_transmission1.grc`
Monotone transmission system:
- Generates sine wave (message signal)
- Adds DC offset
- Multiplies with carrier signal (AM modulation)
- Converts to complex signal
- Transmits via PlutoSDR

---

### `am_receiver1.grc`
Monotone receiver system:
- Receives signal using Pluto Source
- Envelope detection (Complex → Magnitude)
- Low-pass filtering
- DC blocking
- Signal visualization (QT GUI)

---

### `audio_transmission.grc`
Audio transmission system:
- Reads WAV file
- Applies rational resampling
- Adds DC offset
- AM modulation using cosine carrier (~300 kHz)
- Converts to complex signal
- Transmits via PlutoSDR

---

### `audio_receiver.grc`
Audio receiver system:
- Receives RF signal
- Band-pass filter (isolates carrier band)
- Envelope detection
- Low-pass filter (~20 kHz cutoff)
- Resampling to 48 kHz
- Audio playback

---

### `audioSystem.grc` / `system.grc`
Complete transmitter + receiver system:
- End-to-end AM communication
- Includes visualization at multiple stages
- Can run with or without SDR hardware

---

## Parameter tuning

Key parameters were optimized experimentally for best performance:

| Parameter | Value | Purpose |
|----------|------|--------|
| Sampling rate | 1 MS/s | SDR compatibility |
| Carrier frequency | ~300 kHz | AM modulation |
| RF frequency | 2.4 GHz | PlutoSDR transmission |
| Low-pass cutoff | ~20 kHz | Audio recovery |
| Band-pass range | 280–320 kHz | Carrier isolation |
| Resampler | 48 / 1000 | Match audio output |

Proper tuning significantly improved:
- Signal clarity
- Noise reduction
- Stability

---

## Results

- Successful transmission and reception of:
  - Monotone signals
  - Audio signals
- Real-time visualization using QT GUI
- Audio successfully recovered and played back
- Parameter tuning improved signal quality

According to the project report :contentReference[oaicite:0]{index=0}, the system effectively demonstrates SDR-based AM communication, despite inherent limitations.

---

## Limitations

- AM efficiency is low (~33%)
- Sensitive to noise and interference
- Wide bandwidth increases susceptibility to distortion
- Some noise remains even after optimization

---

## How to run

### Requirements
- GNU Radio
- ADALM-Pluto SDR (optional for full system)

## Future work
- Implement FM or digital modulation (QAM)
- Improve noise reduction using adaptive filters
- Enhance system efficiency
- Extend to multi-user communication systems
