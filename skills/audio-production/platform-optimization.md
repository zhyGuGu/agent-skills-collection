# Platform Optimization

Use this checklist to export and package audio so it behaves predictably on each platform.

## Workflow

1. Mix to a clean, unclipped master (leave headroom).
2. Render a lossless "archive/master" file.
3. Create platform-specific deliverables (podcast, YouTube, social) from the master.
4. Confirm loudness and true peak before publishing.
5. Add metadata and consistent file naming.

## Export Formats And Bitrate Guidance

Always keep a lossless master, then make compressed versions for delivery.

### Master (Archive)

- Format: WAV (PCM)
- Sample rate: 48 kHz (preferred) or 44.1 kHz
- Bit depth: 24-bit (preferred) or 16-bit
- Channels: match the project (mono or stereo)
- Notes: no normalization unless it is part of your loudness workflow

### Podcast (Audio-First Platforms)

- Delivery format: MP3 (most compatible)
- Bitrate:
  - Spoken word mono: 96-128 kbps CBR
  - Spoken word stereo: 128-160 kbps CBR
  - Music-heavy: 160-192 kbps CBR
- Sample rate: 44.1 kHz or 48 kHz (match hosting guidance)
- Channels: mono if your content is effectively mono; otherwise stereo
- Notes: avoid very low bitrates with strong noise reduction (can create swirls/warble)

### YouTube (Online Video)

- Delivery format: AAC audio inside MP4/MOV (typical video export)
- Bitrate:
  - Stereo: 256-320 kbps AAC
  - Mono: 128-192 kbps AAC
- Sample rate: 48 kHz (recommended for video)
- Notes: export audio at the same sample rate as the video timeline (usually 48 kHz)

### Social (Short-Form Video: Reels/TikTok/Shorts)

- Delivery format: AAC inside MP4 (common)
- Bitrate: 192-256 kbps AAC (higher is fine; platforms often re-encode anyway)
- Sample rate: 48 kHz (safe default)
- Notes: expect aggressive re-encoding; keep speech bright and steady, avoid extreme stereo width

## Loudness Targets (Conceptual)

Platforms normalize loudness differently. The goal is consistency without clipping.

### Key Terms

- Integrated loudness (LUFS-I): overall program loudness.
- True peak (dBTP): peak level after reconstruction; important for avoiding codec clipping.

### Practical Targets

- Podcasts:
  - Target loudness: about -16 LUFS-I (stereo) or -19 LUFS-I (mono)
  - True peak ceiling: about -1.0 to -1.5 dBTP
- Online video (YouTube and most streaming video):
  - Target loudness: around -14 LUFS-I is a common reference
  - True peak ceiling: about -1.0 dBTP
- Social short-form:
  - Target loudness: typically similar to online video; aim for clarity over maximum loudness
  - True peak ceiling: about -1.0 dBTP

Notes:
- If you publish quieter than a platform target, the platform may turn you up (and reveal noise).
- If you publish louder, the platform may turn you down (and your dynamics may feel flat).

## Metadata And File Naming Checklist

### Metadata

- Title: episode/video title (consistent capitalization)
- Artist/Author: show name or channel name
- Album/Series: podcast name / season name
- Track number: episode number (if used)
- Year/Date: release year or ISO date
- Genre: optional, keep consistent
- Artwork:
  - Use square cover for podcast audio files (if embedding)
  - Keep file size reasonable; follow your host/platform limits

### File Naming

Use stable, sortable names so files are easy to find and re-export.

- Pattern:
  - `ShowName_Ep###_YYYY-MM-DD_ShortTitle_Platform_V#_SRkHz.ext`
- Examples:
  - `MyShow_Ep042_2026-03-04_RoomTone_Podcast_V1_44k1.mp3`
  - `MyShow_Ep042_2026-03-04_RoomTone_YouTube_V1_48k.mp4`

Checklist:
- No spaces if your pipeline is sensitive (use underscores)
- Avoid special characters: `: * ? " < > |` and trailing periods
- Include platform tag (Podcast, YouTube, Social)
- Increment version number on every re-export

## Quick Troubleshooting

### Clipping (Distortion)

Symptoms:
- Crunchy peaks on loud words/music, especially after upload.

Fix:
- Lower limiter ceiling to about -1.0 dBTP (or -1.5 dBTP if codecs are harsh).
- Reduce input gain into the limiter; do not rely on limiter alone.
- Re-check true peak after exporting to the delivery codec.

### Pumping (Over-Compression)

Symptoms:
- Background rises and falls audibly; voice sounds squashed.

Fix:
- Lower compressor ratio and/or threshold; increase attack/release times.
- Use less aggressive noise reduction (it can exaggerate pumping).
- Consider splitting processing: gentle compression, then gentle limiting.

### Noise (Hiss/Hum/Rumble)

Symptoms:
- Constant hiss, electrical hum, or low-frequency rumble.

Fix:
- High-pass filter for voice (start around 60-100 Hz, adjust by ear).
- For hum: notch at 50/60 Hz and harmonics (100/120 Hz, etc.).
- Use noise reduction lightly; prefer better mic technique and room treatment.
