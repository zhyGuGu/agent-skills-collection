# Processing Guides (Spoken Voice)

This guide is a practical, repeatable checklist for cleaning and shaping spoken voice.
Use your ears, work in small moves, and level-match when comparing before/after.

## Quick Start: Recommended Order (Typical Voice Chain)

1. Clip gain / trim (get consistent input level)
2. High-pass filter (remove rumble)
3. Noise reduction (if needed; do it early and lightly)
4. Subtractive EQ (cut problems before boosting)
5. De-esser (tame harsh S/T sounds)
6. Compression (control dynamics)
7. Additive EQ (optional tone shaping)
8. Limiter / output trim (final level safety)

Notes:
- If noise reduction is heavy, consider: NR -> EQ -> de-ess -> comp -> light NR cleanup.
- If breaths are distracting, reduce them manually (clip gain) before dynamics processing.

## EQ Basics (Common Problem Areas)

Goal: remove problems first, then shape tone.

### Step-by-step

1. Start with a high-pass filter (HPF):
   - Set by ear so the voice stays full but the low-end rumble is gone.
   - Typical spoken voice HPF ranges are often in the ~60-120 Hz area, but do not use a number blindly.
2. Sweep to find problems, then cut narrowly:
   - Use a narrow-ish bell, boost temporarily to locate the issue, then switch to a cut.
   - Prefer small cuts (often 1-4 dB) and re-check in context.
3. Add gentle tone (optional):
   - Use broad shelves/bells for small, musical boosts.
   - If you boost, re-check sibilance and compression behavior.

### Common problem areas (what they sound like)

- 20-80 Hz: rumble, handling noise, HVAC thumps; usually remove with HPF.
- 80-200 Hz: boom, proximity effect, muddy low-end.
- 200-500 Hz: boxy, wooly, "cardboard" tone.
- 500 Hz-1.2 kHz: nasal, honky, "telephone" midrange.
- 2-5 kHz: presence/clarity; too much becomes harsh or fatiguing.
- 5-8 kHz: sibilance edge; can turn "S" into "shh" or piercing.
- 8-12 kHz: brightness/air; too much emphasizes hiss and mouth noise.

### Safety checks

- Avoid stacking many narrow cuts; if you need lots of notches, suspect room/mic issues.
- Level-match EQ moves before deciding they are "better".

## Compression Basics (Threshold / Ratio / Attack / Release)

Goal: reduce level swings so words stay intelligible without sounding squashed.

### What the controls do

- Threshold: level where compression starts. Lower threshold = more compression.
- Ratio: strength of compression once above threshold (e.g., 2:1 gentler, 4:1 firmer).
- Attack: how fast compression engages after crossing threshold.
  - Faster attack catches peaks but can dull consonants.
  - Slower attack can keep transients/presence but may let peaks through.
- Release: how fast compression returns to normal after the signal drops.
  - Too fast = pumping / distortion.
  - Too slow = sustained dulling / "held down" feel.
- Makeup gain / output: restores level after gain reduction (GR).

### Setup procedure (spoken voice)

1. Set ratio to a moderate starting point (often 2:1 to 4:1).
2. Choose an attack that preserves articulation:
   - If consonants get dull, slow the attack slightly.
   - If peaks jump out, speed the attack slightly.
3. Set release so GR returns smoothly between phrases:
   - Listen for pumping on pauses and breath noise.
   - Aim for a natural return without obvious level "breathing".
4. Lower threshold until you see consistent GR on loud words.
5. Level-match with makeup gain, then A/B.

### Practical targets (use as guidance, not rules)

- Light control: ~2-4 dB GR on louder phrases.
- Firm control: ~4-8 dB GR if the performance is very dynamic.

### Common compression issues and fixes

- Dull voice: attack too fast, or too much GR; ease attack or raise threshold.
- Pumping / breathing: release too fast, or threshold too low; slow release or reduce GR.
- Too spitty / sibilant: compression can bring up "S"; de-ess before/after comp as needed.

## Noise Reduction Guidance (Order of Operations)

Goal: reduce constant background noise (hiss, fan, room tone) without damaging speech.

### Principles

- Less is more: heavy NR creates artifacts (chirps, warble, dullness).
- Treat the source first: mic placement, room, and gain staging beat processing.
- Prefer manual fixes for non-constant noise (clicks, bumps, plosives).

### Order of operations

1. First, clean obvious issues manually:
   - Remove or reduce bumps, lip smacks, clicks, and loud breaths with editing.
2. Apply HPF before NR if low rumble is triggering the NR.
3. Apply noise reduction early in the chain:
   - NR before compression prevents the compressor from raising the noise floor.
4. Follow with subtractive EQ and de-essing.
5. Compress.
6. If needed, do a second very light NR pass after compression.

### When not to use NR

- If the noise is already masked by the program or is not noticeable in context.
- If NR artifacts are more distracting than the original noise.

## De-essing Basics

Goal: reduce excessive sibilance ("S", "SH", "T", "CH") while keeping clarity.

### Setup procedure

1. Identify the sibilant range by listening and sweeping the detector frequency.
2. Set threshold so only sibilant moments trigger reduction.
3. Use the smallest reduction that solves the problem.
4. Check that the voice does not lisp or lose presence.

### Placement guidance

- Before compression: prevents the compressor from exaggerating sibilance.
- After compression: catches sibilance brought up by compression.
- If needed, use two light stages rather than one heavy stage.

## Checklist: Spoken Voice Processing

- Input level: peaks are controlled, no clipping, consistent loudness.
- HPF: rumble removed, voice still sounds full.
- Noise: reduced with minimal artifacts (or left alone if acceptable).
- EQ: boxiness/harshness tamed; clarity improved without hiss.
- De-ess: sibilance controlled without lisp.
- Compression: intelligible and steady; no pumping.
- Output: final level set with headroom; no limiter distortion.
