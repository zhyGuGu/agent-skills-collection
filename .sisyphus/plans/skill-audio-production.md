# Skill Implementation Plan: audio-production

## Overview
Comprehensive audio production guidance for podcasters, content creators, musicians, and voiceover artists, covering recording, editing, processing, and publishing workflows.

## Problem Statement
- Content creation is exploding (podcasts, YouTube, TikTok)
- Audio quality is crucial but creators lack:
  - Recording technique knowledge
  - Editing workflow optimization
  - Audio processing fundamentals
  - Platform-specific requirements
- No AI-assisted audio production guidance exists
- Professional audio editing is complex and time-consuming

## Target Market
- **Primary**: Podcasters, content creators, YouTubers
- **Secondary**: Musicians, voiceover artists
- **Tertiary**: Video creators needing audio enhancement

## Success Metrics
- Clear recording setup guides
- Editing workflow optimization
- Audio processing fundamentals (EQ, compression, noise reduction)
- Platform-specific export settings
- Tool-agnostic guidance (works with any DAW)

---

## Implementation Checklist

### Phase 1: Recording Fundamentals (Week 1)

#### 1.1 Create SKILL.md
```yaml
---
name: audio-production
description: Comprehensive audio production guidance for recording, editing, processing, and publishing high-quality audio for podcasts, music, voiceover, and content creation
version: 1.0.0
author: yourusername
tags: [audio, podcast, music, voiceover, recording, editing, content-creation]
---
```

**Required Sections**:
- `# When to Use` - Trigger conditions
- `# Recording` - Setup, techniques, best practices
- `# Editing` - Workflow, cutting, transitions
- `# Processing` - EQ, compression, effects
- `# Publishing` - Export settings, platforms
- `# Troubleshooting` - Common issues and fixes

#### 1.2 Recording Setup Guide
Create `recording/`:
- Microphone selection guide (USB, XLR, dynamic, condenser)
- Room acoustics basics
- Gain staging fundamentals
- Recording environment setup
- Remote recording solutions

#### 1.3 Recording Techniques
Create `recording/techniques.md`:
- Microphone placement
- Proximity effect management
- Pop filter usage
- Voice warm-up techniques
- Interview recording (single mic, dual mic, remote)

### Phase 2: Editing Workflows (Week 2)

#### 2.1 DAW Workflows
Create `editing/daw-workflows.md`:
- Universal editing principles
- Non-destructive editing
- Session organization
- Keyboard shortcuts (universal + DAW-specific)
- Backup strategies

#### 2.2 Editing Techniques
Create `editing/techniques.md`:
- Removing mistakes and filler words
- Crossfades and transitions
- Breathing room management
- Pacing and timing
- Multi-track editing

#### 2.3 Content-Specific Editing
Create `editing/content-types/`:
- `podcast-editing.md` - Interview flow, intro/outro, show notes
- `music-editing.md` - Arrangement, comping, quantization
- `voiceover-editing.md` - Breath control, pacing, pickup lines
- `audiobook-editing.md` - Chapter breaks, consistency, mouth clicks

### Phase 3: Audio Processing (Week 3)

#### 3.1 EQ Fundamentals
Create `processing/eq-guide.md`:
- Frequency spectrum basics
- High-pass filtering
- Problem frequency identification
- Vocal EQ curves
- Instrument EQ guidance

#### 3.2 Compression Guide
Create `processing/compression-guide.md`:
- Threshold, ratio, attack, release
- Vocal compression settings
- Parallel compression
- Multiband compression
- Limiting and loudness

#### 3.3 Noise Reduction
Create `processing/noise-reduction.md`:
- Room noise removal
- Mouth click reduction
- Plosive management
- De-essing
- Hum and buzz removal

#### 3.4 Effects and Enhancement
Create `processing/effects.md`:
- Reverb types and usage
- Delay effects
- Stereo widening
- Saturation and warmth
- Pitch correction basics

### Phase 4: Publishing & Tools (Week 4)

#### 4.1 Export Settings
Create `publishing/export-settings.md`:
- Format selection (MP3, WAV, AAC, OGG)
- Bitrate recommendations
- Sample rate guidelines
- Loudness standards (LUFS)
- True peak limiting

#### 4.2 Platform Requirements
Create `publishing/platforms/`:
- `podcast-platforms.md` - Apple Podcasts, Spotify, Google Podcasts
- `youtube-audio.md` - YouTube audio optimization
- `social-media.md` - TikTok, Instagram, Twitter
- `music-platforms.md` - Spotify, Apple Music, Bandcamp
- `audiobook-platforms.md` - Audible, ACX

#### 4.3 DAW-Specific Guides
Create `tools/`:
- `audacity-guide.md` - Free, cross-platform
- `garageband-guide.md` - macOS/iOS, beginner-friendly
- `adobe-audition-guide.md` - Professional, subscription
- `logic-pro-guide.md` - macOS, music-focused
- `pro-tools-guide.md` - Industry standard
- `reaper-guide.md` - Affordable, powerful
- `studio-one-guide.md` - Modern, intuitive

---

## File Structure

```
audio-production/
├── README.md
├── SKILL.md
├── CHANGELOG.md
│
├── recording/
│   ├── microphone-selection.md
│   ├── room-acoustics.md
│   ├── gain-staging.md
│   ├── recording-environment.md
│   ├── remote-recording.md
│   └── techniques.md
│
├── editing/
│   ├── daw-workflows.md
│   ├── techniques.md
│   ├── keyboard-shortcuts.md
│   └── content-types/
│       ├── podcast-editing.md
│       ├── music-editing.md
│       ├── voiceover-editing.md
│       └── audiobook-editing.md
│
├── processing/
│   ├── signal-flow.md
│   ├── eq-guide.md
│   ├── compression-guide.md
│   ├── noise-reduction.md
│   ├── effects.md
│   └── mastering-basics.md
│
├── publishing/
│   ├── export-settings.md
│   ├── loudness-standards.md
│   └── platforms/
│       ├── podcast-platforms.md
│       ├── youtube-audio.md
│       ├── social-media.md
│       ├── music-platforms.md
│       └── audiobook-platforms.md
│
├── tools/
│   ├── audacity-guide.md
│   ├── garageband-guide.md
│   ├── adobe-audition-guide.md
│   ├── logic-pro-guide.md
│   ├── pro-tools-guide.md
│   ├── reaper-guide.md
│   └── studio-one-guide.md
│
├── troubleshooting/
│   ├── common-issues.md
│   ├── audio-quality-problems.md
│   ├── sync-issues.md
│   └── file-format-issues.md
│
├── resources/
│   ├── glossary.md
│   ├── equipment-recommendations.md
│   ├── plugin-recommendations.md
│   └── further-learning.md
│
└── examples/
    ├── podcast-template/
    ├── music-mixing-template/
    └── voiceover-template/
```

---

## Content Requirements

### SKILL.md Content Outline

```markdown
# Audio Production

## When to Use
- Starting a podcast
- Recording voiceover
- Editing audio content
- Processing recorded audio
- Exporting for different platforms
- Troubleshooting audio issues
- Optimizing audio quality

## Capabilities
1. Recording setup and technique guidance
2. Editing workflow optimization
3. Audio processing (EQ, compression, effects)
4. Noise reduction and cleanup
5. Platform-specific export settings
6. Equipment recommendations
7. Troubleshooting common issues
8. DAW-agnostic workflows

## Quick Start
1. Set up your recording environment
2. Configure your microphone
3. Record with proper gain staging
4. Edit your audio
5. Apply processing (EQ, compression)
6. Export with platform-appropriate settings

## Recording
[Microphone selection, room setup, techniques]

## Editing
[DAW workflows, cutting techniques, organization]

## Processing
[EQ, compression, noise reduction, effects]

## Publishing
[Export settings, loudness standards, platform requirements]

## Tools
[DAW-specific guides and recommendations]

## Troubleshooting
[Common problems and solutions]
```

### Microphone Selection Guide

| Use Case | Budget Option | Mid-Range | Professional |
|----------|--------------|-----------|--------------|
| Podcast | Audio-Technica ATR2100 | Shure SM7B | Neumann TLM 103 |
| Voiceover | Blue Yeti | Rode NT1 | Sennheiser MKH 416 |
| Music | Audio-Technica AT2020 | AKG C414 | Neumann U87 |
| Interview | Zoom H1n | Zoom H6 | Sound Devices MixPre |

### Export Settings Matrix

| Platform | Format | Bitrate | Sample Rate | LUFS |
|----------|--------|---------|-------------|------|
| Podcast | MP3 | 128-192 kbps | 44.1 kHz | -16 |
| YouTube | AAC | 256 kbps | 48 kHz | -14 |
| Music | WAV/FLAC | Lossless | 44.1/48 kHz | -14 |
| Social Media | AAC | 128 kbps | 44.1 kHz | -14 |
| Audiobook | MP3 | 64-128 kbps | 44.1 kHz | -20 |

---

## Quality Standards

### Recording Quality
- Proper gain staging (-12dB to -6dB peak)
- Room noise below -60dB
- No clipping or distortion
- Consistent levels

### Editing Quality
- Clean cuts without clicks
- Proper crossfades
- Consistent pacing
- Breathing room maintained

### Processing Quality
- Natural-sounding EQ
- Transparent compression
- Controlled dynamics
- Appropriate loudness (LUFS)

### Export Quality
- Correct format for platform
- Proper loudness standard
- No clipping
- Metadata included

---

## Testing Strategy

### Content Validation
- Test with different DAWs
- Verify across multiple platforms
- Check on different devices
- Validate export settings

### User Testing
- Test with beginner creators
- Test with professional producers
- Test with different content types
- Validate troubleshooting guides

### Accuracy Testing
- Verify technical specifications
- Test equipment recommendations
- Validate processing settings
- Check platform requirements

---

## DAW Coverage Strategy

### Free/Low-Cost
- **Audacity** - Cross-platform, beginner-friendly
- **GarageBand** - macOS/iOS, musician-focused
- **Cakewalk** - Windows, professional features

### Professional
- **Adobe Audition** - Subscription, podcast-focused
- **Logic Pro** - macOS, music production
- **Pro Tools** - Industry standard, subscription
- **Reaper** - Affordable, highly customizable
- **Studio One** - Modern workflow, intuitive

### Coverage Approach
- Provide DAW-agnostic principles first
- Include DAW-specific shortcuts and workflows
- Focus on universal concepts
- Link to official documentation

---

## Platform-Specific Guidance

### Podcast Platforms
- Apple Podcasts requirements
- Spotify for Podcasters
- Google Podcasts
- RSS feed requirements
- Cover art specifications

### Video Platforms
- YouTube audio optimization
- TikTok audio requirements
- Instagram audio specs
- Sync with video

### Music Platforms
- Streaming service loudness
- Distribution service requirements
- Mastering for streaming
- Format requirements

### Audiobook Platforms
- ACX/Audible requirements
- Chapter specifications
- Metadata requirements
- Quality standards

---

## GitHub Repository Setup

### Repository Structure
```
yourusername/audio-production/
├── .github/
│   ├── workflows/
│   │   └── validate.yml
│   └── CODEOWNERS
├── skills/
│   └── audio-production/
├── examples/
│   ├── podcast-session-template/
│   ├── music-mixing-template/
│   └── voiceover-template/
├── resources/
│   └── equipment-database.md
├── CONTRIBUTING.md
├── LICENSE (MIT or Apache 2.0)
└── README.md
```

### README.md Sections
1. Overview & Value Proposition
2. Installation (`npx skills add yourusername/audio-production`)
3. Quick Start Guide
4. Recording Setup
5. Editing Workflows
6. Processing Guide
7. Platform Publishing
8. Contributing Guidelines

### GitHub Topics
`audio`, `podcast`, `music`, `voiceover`, `recording`, `editing`, `content-creation`, `daw`, `agent-skill`

---

## Implementation Timeline

| Week | Deliverable | Owner |
|------|-------------|-------|
| 1 | SKILL.md + Recording guides | Audio Engineer |
| 1 | Microphone selection guide | Audio Engineer |
| 2 | Editing workflows | Audio Engineer |
| 2 | Content-type guides | Content Creator |
| 3 | Processing guides (EQ, compression) | Audio Engineer |
| 3 | Noise reduction guide | Audio Engineer |
| 4 | Export settings | Audio Engineer |
| 4 | Platform requirements | Content Creator |
| 5 | DAW guides (Audacity, GarageBand) | Technical Writer |
| 5 | DAW guides (Pro tools, Logic) | Technical Writer |
| 6 | Examples + validation | Audio Engineer |

---

## Success Criteria Checklist

- [ ] Repository created and public
- [ ] SKILL.md complete with all sections
- [ ] Recording setup guide
- [ ] Editing workflow documentation
- [ ] Processing guides (EQ, compression, noise reduction)
- [ ] Platform export settings
- [ ] Minimum 5 DAW guides
- [ ] Troubleshooting guide
- [ ] Equipment recommendations
- [ ] Validated with Claude Code
- [ ] Validated with OpenCode
- [ ] Published to skills.sh
