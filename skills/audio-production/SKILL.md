---
name: audio-production
description: Assist with audio production tasks such as recording setup guidance, dialog cleanup plans, noise reduction strategy, EQ/dynamics suggestions, loudness targeting, editing workflows, and export/delivery settings for common platforms.
---

# Audio Production

## When to Use

Use this skill when you need help with:

- Planning a recording session (mic choice/placement, gain staging, room treatment basics)
- Cleaning spoken-word audio (noise, hum, plosives, sibilance, clicks, breaths)
- Building a repeatable processing chain for dialog/podcasts/voiceover
- Meeting delivery specs (sample rate/bit depth, codecs, loudness targets, true peak)
- Troubleshooting audio issues (clipping, distortion, phase problems, inconsistent levels)

## Capabilities

- Recommend an editing and cleanup order of operations
- Suggest parameter starting points for common tools (HPF, EQ, de-esser, compressor, limiter)
- Provide loudness and peak targets by destination (podcast, YouTube, streaming, broadcast)
- Explain tradeoffs (noise reduction vs artifacts, compression vs intelligibility, mono vs stereo)
- Produce checklists for QC before export (head/tail, fades, clicks, metadata)

## Core Workflow

1. Gather constraints: source type (spoken word/music), environment, issues heard, destination specs.
2. Establish a baseline: confirm sample rate/bit depth; ensure no clipping; set a reference level.
3. Edit first: remove obvious problems (cuts, fades, timing, mouth clicks) before heavy processing.
4. Reduce noise: address constant noise (hum/hiss) with conservative settings; avoid artifacts.
5. Shape tone: apply HPF and corrective EQ; re-check intelligibility against reference.
6. Control dynamics: de-ess, compress in stages if needed, then limit to a true-peak ceiling.
7. Loudness match: measure integrated loudness; adjust with gain/limiting to target.
8. Export and QC: render to required format; listen for artifacts; verify loudness/peaks.

## Example Outputs

```text
Podcast cleanup chain (starting point)

Track prep:
- Trim starts/ends, remove mistakes, add short fades on edits
- Clip gain: bring average speech near a consistent level before plugins

Processing order:
1) High-pass filter: 70-90 Hz (12-24 dB/oct), adjust for voice
2) De-click / mouth noise: light setting; avoid over-processing
3) Noise reduction: learn noise profile from room tone; 3-6 dB reduction; smooth release
4) EQ (subtractive): -2 to -4 dB at muddy area (150-300 Hz) if needed
5) De-esser: target 5-8 kHz; reduce 2-6 dB on peaks
6) Compressor: ratio 2:1 to 4:1; attack 10-30 ms; release 60-150 ms; 2-6 dB GR
7) Limiter (true-peak): ceiling -1.0 dBTP; only catch peaks (1-3 dB GR)
8) Loudness: adjust gain to target -16 LUFS (stereo) or -19 LUFS (mono)

QC:
- Check for pumping, lisping from de-esser, metallic noise-reduction artifacts
- Ensure breaths are natural and not distracting
```

```text
Export settings recommendation (podcast distribution)

Delivery goals:
- Integrated loudness: -16 LUFS (stereo) or -19 LUFS (mono)
- True peak: <= -1.0 dBTP

Master export (archive):
- Format: WAV
- Sample rate: 48 kHz (or match session)
- Bit depth: 24-bit
- Dither: only if rendering to 16-bit

Distribution export (typical):
- Format: MP3
- Mode: CBR 128-192 kbps (spoken word) or VBR high
- Sample rate: 44.1 kHz (common) or 48 kHz if platform supports; avoid resampling twice
- Channels: stereo for music beds; mono acceptable for voice-only if required

Notes:
- Normalize to loudness target (LUFS), not peak-only normalization
- Leave a small head/tail (0.25-0.5 s) and ensure fades prevent clicks
```
