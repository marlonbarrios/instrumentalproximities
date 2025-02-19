# Instrumental Proximities
# Gestural Augmentation of Subjective Intimacy

An interactive art piece that creates visual connections between hands and face, generating ambient sounds based on movement. Built with p5.js, MediaPipe, and Tone.js.

🎮 [Try the Live App](https://marlonbarrios.github.io/instrumentalproximities/)

## Overview

This project creates a real-time interactive experience where:
- Facial features and hand movements are tracked
- Visual connections are drawn between different points
- Movement generates ambient sounds and music
- Everything responds fluidly to user interaction

## Visual Elements

### Face Network
- Subtle connections between key facial points
- Points include: eyes, mouth corners, nose, cheeks, and forehead
- Delicate animated lines with wave patterns
- Intensity changes based on distance between points
- Soft particle effects at intersections

### Hand Connections
- Glowing points at finger tips
- Complex wave patterns between finger tips
- Lines become more intense when fingers are closer
- Interweaving paths with animated waves
- Particle effects along the connections

### Hand-to-Face Connections
- Dynamic lines connect facial points to finger tips
- Connection intensity based on proximity
- Complex wave patterns that respond to movement
- Subtle particle systems along connections

## Sound Generation

### Drone Synth
- Base drone chord changes based on left hand height
- Creates ambient foundation
- Changes every 4 seconds
- Uses sine waves for smooth texture

### Main Synth (Left Hand)
- Triggered by left hand movement
- Pitch determined by vertical position
- Higher notes when hand is up
- Lower notes when hand is down
- Uses triangle waves for clarity

### Bass Synth (Mouth)
- Triggered by mouth opening
- Pitch based on mouth openness
- Wider opening = lower notes
- Uses filtered triangle waves
- More resonant at lower frequencies

### Hi-hat (Overall Movement)
- Rhythmic element based on hand movement
- Velocity controlled by movement speed
- Uses pink noise for softer texture
- Plays at regular intervals

## Sound Generation Technical Details

### Audio Engine Architecture

#### Synthesis Chain
1. **Main Signal Path**
   - Synths → Delay → Reverb → Output
   - Individual volume control per synth
   - Parallel processing for multiple voices

2. **Effects Configuration**
   ```javascript
   reverb = new Tone.Reverb({
     decay: 4,
     wet: 0.4
   })
   
   delay = new Tone.FeedbackDelay({
     delayTime: "8n",
     feedback: 0.3,
     wet: 0.2
   })
   ```

### Synthesizer Specifications

1. **Drone Synth (Background Texture)**
   ```javascript
   droneSynth = new Tone.PolySynth(Tone.Synth, {
     oscillator: {
       type: "sine4"  // 4 detuned sine waves
     },
     envelope: {
       attack: 2,     // Slow fade in
       decay: 1,
       sustain: 1,    // Hold at full volume
       release: 4     // Long release tail
     }
   })
   ```
   - Uses 4-voice polyphony for chord generation
   - Chord structure: root, perfect 5th, octave, major 3rd
   - Updates every 4 seconds based on hand position

2. **Main Synth (Hand Movement)**
   ```javascript
   synth = new Tone.Synth({
     oscillator: {
       type: "triangle4"  // 4 detuned triangle waves
     },
     envelope: {
       attack: 0.1,
       decay: 0.3,
       sustain: 0.4,
       release: 1
     }
   })
   ```
   - Triggered by velocity threshold (>15)
   - Note duration: "2n" (half note)
   - Velocity scaling: 0.3 maximum

3. **Bass Synth (Mouth Control)**
   ```javascript
   bassline = new Tone.MonoSynth({
     oscillator: {
       type: "triangle"
     },
     envelope: {
       attack: 0.1,
       decay: 0.3,
       sustain: 0.6,
       release: 0.8
     },
     filterEnvelope: {
       baseFrequency: 100,
       octaves: 3,
       attack: 0.1,
       decay: 0.2,
       sustain: 0.4,
       release: 0.8
     }
   })
   ```
   - Monophonic for clean bass lines
   - Filter envelope for dynamic timbre
   - Note duration: "1n" (whole note)

4. **Hi-hat (Rhythmic Element)**
   ```javascript
   hihat = new Tone.NoiseSynth({
     noise: {
       type: "pink"  // Softer noise type
     },
     envelope: {
       attack: 0.02,
       decay: 0.2,
       sustain: 0,
       release: 0.2
     }
   })
   ```
   - Triggered every 16 frames
   - Velocity range: 0.05 - 0.2
   - Note duration: "16n" (sixteenth note)

### Rate Limiting System

## Interaction Mappings

### Left Hand
- Vertical position → Synth pitch (48-72 MIDI)
- Movement speed → Sound triggering
- Position → Drone root note

### Right Hand
- Movement speed → Sound intensity
- Position → Visual connection density

### Mouth
- Opening width → Bass note (36-48 MIDI)
- Opening threshold → Bass triggering

### Overall Movement
- Hand velocity → Hi-hat velocity
- Movement amount → Reverb wet mix
- Distance between points → Visual intensity

## Technical Details

### Dependencies
- p5.js for graphics
- MediaPipe for tracking
- Tone.js for audio synthesis

### Sound Design
- Reverb with 4s decay
- Delay feedback for ambience
- Rate limiting for stability
- Error handling for audio triggers

### Visual Design
- Additive blending for glow
- Alpha-based layering
- Dynamic intensity scaling
- Particle systems for detail

## Getting Started

1. Click anywhere to initialize audio
2. Allow webcam access
3. Move hands and face to interact
4. Experiment with different movements and gestures

## Performance Notes

- Smooth movements create more musical results
- Try combining hand movements with facial expressions
- Explore the space between hands and face
- Find sweet spots for different sound combinations 
