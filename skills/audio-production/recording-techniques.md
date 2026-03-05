# Recording Techniques

This note is a practical, repeatable workflow for clean dialog and voice recording.

## Basic Mic Placement

1. Pick a quiet spot before touching the mic.
2. Put the mic slightly off-axis (not aimed directly at the mouth).
3. Start at 6-8 in / 15-20 cm from the mouth.
4. Aim the capsule at the corner of the mouth or the chin, not straight at the lips.
5. If you hear boomy low end, increase distance or move further off-axis.
6. If you hear too much room, decrease distance and add absorption.

### Quick Placement Targets

- Spoken word / podcast: 4-8 in / 10-20 cm, slightly off-axis.
- Very dynamic speaker: 8-12 in / 20-30 cm plus more room treatment.
- Laptop/phone mic (fallback): 8-12 in / 20-30 cm, keep device stable, treat the room.

## Gain Staging Targets (Digital)

Goal: record cleanly with headroom; do not chase "hot" levels.

1. Disable any auto-gain / "enhancements" in the OS/app.
2. Set input gain while speaking at the loudest expected level.
3. Use these targets:

- Average (speech): around -18 dBFS RMS (or -20 to -16 dBFS is fine).
- Peaks (normal speech): around -10 to -6 dBFS.
- Hard limit: never hit 0 dBFS (clipping).

If you have an analog preamp meter, keep it comfortably below the red and let the interface convert with headroom.

## Room Noise Checklist

Run this list before every session.

1. Turn off common noise sources:
   - HVAC / fans / air purifiers
   - refrigerators (if close), dehumidifiers
   - printers, monitors with coil whine
2. Silence handling noise:
   - place mic on a stable stand; avoid desk-mounted vibrations
   - route cables so they cannot rub the stand
3. Reduce reflections:
   - put soft material behind and to the sides of the mic (blanket, duvet, absorber)
   - avoid facing a bare wall or window
4. Check the noise floor:
   - record 10 seconds of "silence" at the same gain
   - listen on headphones for hum, hiss, traffic, birds, neighbors
5. Check electrical/ground issues:
   - if you hear 50/60 Hz hum, try a different outlet or remove unneeded USB devices
   - keep audio cables away from power bricks

## Plosives And Sibilance Mitigation

### Plosives (P/B blasts)

1. Use a pop filter 2-3 in / 5-8 cm in front of the mic.
2. Speak slightly across the mic (off-axis) to avoid direct air hits.
3. Increase distance (move from 4 in to 6-8 in) if plosives persist.
4. Raise the mic slightly above mouth level and aim down toward the chin.
5. Avoid breathy "over-articulation" right on the capsule.

### Sibilance (S/SH harshness)

1. Go more off-axis (rotate mic 20-45 degrees away from the mouth).
2. Increase distance slightly and add absorption to keep the room quiet.
3. Use a smoother mic if available; bright condensers often emphasize sibilance.
4. If the sound is already recorded, use a de-esser gently:
   - target 5-9 kHz as a starting band
   - reduce only the "S" moments, not the whole vocal

## Remote Recording Considerations

Use this workflow to keep quality consistent across locations.

1. Prefer local recording on each side:
   - each person records their own mic to WAV locally
   - the call app is only for monitoring and sync
2. Standardize the basics:
   - sample rate: 48 kHz (common for video) or 44.1 kHz (music/podcast); do not mix if you can avoid it
   - bit depth: 24-bit if available
   - file format: WAV (or AIFF)
3. Sync strategy:
   - clap once at the start (visible spike)
   - do a short spoken slate: date, episode, take number
4. Monitoring:
   - wear closed-back headphones to prevent echo/bleed
   - mute speakers; never monitor through laptop speakers
5. Network safety:
   - record even if the call sounds fine; network audio can glitch
   - if you must rely on call audio, use the highest-quality setting and disable noise suppression if it harms tone
6. Consistency notes:
   - keep mic distance and angle constant; mark the stand height
   - match gain staging targets; do not normalize during recording

## Short Pre-Record Checklist

Run this in order; stop and fix any failed item.

1. Room is quiet; HVAC/fans off.
2. Mic is stable; pop filter installed; cable strain relieved.
3. Mic placement: 6-8 in, slightly off-axis, aimed at mouth corner/chin.
4. Input chain set: correct mic selected; no auto-gain; no "enhancements".
5. Levels set at loudest voice:
   - average around -18 dBFS
   - peaks around -10 to -6 dBFS
   - never clip
6. Record 10 seconds of room tone.
7. Record a 15-30 second test read; listen for plosives, hiss, hum, room echo.
8. Start take; clap/slate if needed for sync.

## Troubleshooting Fast Fixes

- Too quiet: raise preamp gain slightly; do not move the mic far away.
- Too loud/clipping: lower gain first; then increase distance.
- Too much room: move closer; add absorption behind the mic and behind the speaker.
- Pops: add pop filter; go more off-axis; increase distance.
- Harsh S: rotate off-axis; soften delivery; apply light de-essing in post.
