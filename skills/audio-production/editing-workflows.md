# Editing Workflows

This guide describes a practical, repeatable editing workflow for spoken-word audio (podcasts, interviews, narration). It is DAW-agnostic and focuses on process and listening decisions rather than specific tools.

## Non-destructive editing principles

1. Preserve originals.
   - Import or copy raw recordings into a session/project folder.
   - Do not overwrite source files; keep them read-only if your setup supports it.

2. Edit with reversibility.
   - Prefer edits that can be changed later (clips/regions, automation, metadata).
   - Avoid printing processing into the source unless you have a clear reason and a backup.

3. Separate decisions by stage.
   - Do content decisions first (what stays/what goes).
   - Do noise cleanup second (what is distracting).
   - Do mix/loudness last (how it feels and translates).

4. Keep a safety lane.
   - Duplicate tracks before major restructuring.
   - Keep an unused copy of the raw track(s) in the session for reference.

5. Make changes obvious.
   - Use consistent naming (e.g., Host A RAW, Host A EDIT, Host A MIX).
   - Use markers/notes for open questions (breathe edits, facts to verify, etc.).

## Podcast editing workflow (rough cut -> cleanup -> mix -> export)

### Stage 1: Rough cut (structure and story)

Goal: deliver a listenable edit that has the right content, order, and pacing.

1. Assemble
   - Align tracks, confirm sample rate, and verify no drift.
   - Choose a reference anchor (usually the primary host track).

2. First pass: remove obvious issues
   - Delete false starts, repeated takes, and long dead air.
   - Trim accidental noises that interrupt words.

3. Second pass: tighten pacing
   - Shorten long pauses while keeping natural breath and emphasis.
   - Remove tangents and redundancies.

4. Third pass: conversation continuity
   - Ensure questions and answers still make sense after cuts.
   - Check for interrupted thoughts, missing context, and abrupt topic jumps.

Output of this stage: a complete episode timeline with content locked as much as practical.

### Stage 2: Cleanup (noise and intelligibility)

Goal: reduce distractions without making speech sound processed or unnatural.

1. Listen for recurring problems
   - Room tone changes, hum, intermittent clicks, mouth noise, plosives.
   - Sibilance, harshness, and low-end rumble.

2. Handle noise in order of impact
   - Fix the loudest/most distracting issues first.
   - Prefer minimal moves: small trims, short fades, and targeted attenuation.

3. Maintain consistent ambience
   - When removing sections, avoid creating "vacuum" silence.
   - Use consistent room tone under edits when appropriate.

4. De-ess and de-plosive as needed
   - Reduce only what distracts; preserve articulation.
   - Re-check intelligibility on small speakers/headphones.

Output of this stage: clean dialogue that still sounds human and continuous.

### Stage 3: Mix (balance, tone, and loudness shape)

Goal: consistent level and tone across speakers, with comfortable dynamics.

1. Set balance
   - Match perceived loudness between speakers.
   - Bring the quiet speaker up; avoid pushing the loud speaker down so far that noise dominates.

2. Tone shaping (conceptual)
   - Reduce distracting low rumble; avoid thinning voices.
   - Tame harshness gently; preserve consonants.
   - Keep tonal changes consistent across segments.

3. Dynamics control (conceptual)
   - Use light control to reduce big peaks and keep speech forward.
   - Avoid over-compression artifacts (pumping, lisping, exaggerated breaths).

4. Music/bed/sfx (if used)
   - Keep voice clearly dominant.
   - Duck music under speech and transitions; avoid masking consonants.

Output of this stage: a cohesive-sounding episode that is comfortable to listen to end-to-end.

### Stage 4: Export (deliverables and QC)

Goal: produce a distribution-ready file and confirm it survives conversion.

1. Choose export settings appropriate for your platform.
2. Export a master file (and any alternate versions if required).
3. Re-import the export and spot-check starts, ends, and transitions.
4. If you will encode to a lossy format, verify the encoded version for artifacts.

## Crossfades and click/pop avoidance

Clicks/pops usually come from abrupt waveform discontinuities at edit points.

1. Always fade edits
   - Add a short fade-out on the outgoing clip and fade-in on the incoming clip.
   - Use the shortest fades that eliminate the click; longer fades can blur consonants.

2. Prefer crossfades for dialogue edits
   - When cutting within continuous ambience, overlap clips slightly and crossfade.
   - Keep the crossfade centered on a low-energy portion (between words, not on a consonant).

3. Cut at natural boundaries
   - Edit at breaths, between phrases, or during low-level room tone.
   - Avoid cutting directly on plosives (p/b), sharp t's, or sibilants.

4. Match room tone across the cut
   - If the background changes, a crossfade can reveal the change.
   - Use consistent underlying ambience so the ear does not "snap" to a new space.

5. Zoom and confirm
   - If you hear a tick, zoom in and adjust the cut location and fade length.
   - Verify both channels if working with stereo sources.

## Loudness leveling strategy (conceptual)

Goal: consistent perceived loudness without flattening expression.

1. Pick a loudness target
   - Choose a target that matches your distribution norms and genre expectations.
   - Define a true-peak safety margin to avoid clipping after encoding.

2. Level in layers
   - First: clip gain (or equivalent) to get each speaker into a similar range.
   - Second: gentle dynamics control to tame peaks and keep speech steady.
   - Third: final loudness adjustment on the full mix to hit the target.

3. Use short-term listening as well as numbers
   - Ensure quiet sections remain intelligible without making loud sections fatiguing.
   - Check transitions between segments and speakers for perceived jumps.

4. Protect transients and consonants
   - Do not chase loudness by crushing dynamics; preserve clarity.
   - Keep breaths natural; reduce only what distracts.

5. Validate after export
   - If you encode to a lossy format, re-check peaks and overall loudness.
   - Confirm the episode does not distort on common playback devices.

## Final listen pass checklist

Do this pass in real time, with no editing unless you stop and take notes.

- Start/end hygiene: clean start, no accidental pre-roll, no cut-off ending
- Transitions: no abrupt topic jumps, no missing words, no confusing edits
- Clicks/pops: scan edits; ensure fades/crossfades remove ticks
- Noise consistency: no sudden room tone changes, hum, or intermittent artifacts
- Balance: speakers match in perceived loudness; music never masks speech
- Harshness/sibilance: no painful s's; consonants remain clear
- Plosives/rumble: no low-end thumps; voice still sounds full
- Loudness: overall level feels consistent; no clipping/distortion on peaks
- Metadata: title/artist/episode info correct if you embed it
- Deliverable: file plays on phone, laptop, and headphones without surprises
