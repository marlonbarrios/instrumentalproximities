# Interactive Audio-Visual Hand & Face Tracking

An interactive art piece that creates visual connections between hands and face, generating ambient sounds based on movement. Built with p5.js, MediaPipe, and Tone.js.

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