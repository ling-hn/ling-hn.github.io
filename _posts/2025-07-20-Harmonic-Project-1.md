---
layout: post
title: Harmonic Project (1) - Pitch & Frequency
description: Revisit basic music theory in English
date: 2025-07-20
author: L. H. Huang
tags: ["Study Notes", "Physics", "Music Theory"]
features:
  math:
    enable: true
---

*In this series, I try to (progressively) explore the connections between music theory and physics. Starting from fundamental concepts in music theory, it gradually integrates acoustical and mathematical perspectives, ultimately leading to a visual interpretation of musical structures through Lissajous curves.*

### Pitch & Frequency 音高與頻率

#### Pitch as a perceptual quality (感知)

Is pitch simply the same as frequency? How do we define them? 
(Yes, I start with definition. We all love definition.)

In school physics, we learn about sound waves and their properties, like waveform (波形), frequency (頻率), and amplitude (振福). These are often linked to things like tone quality (音色), pitch (音高), and loudness (音量). Frequency is basically the number of vibrations per second, measured in Hertz (Hz).

Pitch, on the other hand, is more about how high or low a sound seems to a listener. Usually, higher frequencies are thought of as higher pitches, but the relationship isn't perfectly linear. It can be affected by things like context, the sound's texture, and how our ears work. Pitch is more like a perceptual quality

> An interesting recent research—such as a study on mice exposed to repetitive stress—shows that perception (including pitch and loudness) can be altered independently of the physical stimulus, revealing how prolonged stress dampens sound-evoked cortical responses and leads to reduced loudness perception.[^ref1]

#### "high" vs. "low" sounds

We say a pitch is "high" or "low" because our brains map auditory features onto spatial metaphors, particularly vertical ones. It's not that sound waves physically move up or down, but that our perception of pitch is based on space, probably influenced by:

* Embodied cognition - we often think of more as being better (e.g. more light is "brighter", more temperature is "hotter", more pitch is "higher"). Words like "high pitch" (English), 「高い音」 (Japanese), and「高音」(Chinese) all describe high-frequency sounds using vertical metaphors.
* Musical instrument design - many of them put high notes right above low ones (like on a piano or the different strings). People also tend to use right hand to indicate high sound while left hand for low sound.
* Perceptual mapping – Psychophysical studies show that people naturally associate high frequencies with higher spatial locations, even in cross-modal matching tasks (e.g., matching sound to height).[^2] [^3]

So, the idea of pitch as a spatial concept comes about because we perceive it, not measure it directly. It's all down to how our ears work, interpreting different frequencies, and our brain often frames it in a spatial way.


### Octaves, Harmonic Series, and Overtones

But here we still describe musical notes in terms of their physical frequency. ;-)

In music, when one sound has exactly twice the frequency of another, the two are said to be one octave (八度) apart. For example, a tone at 440 Hz (A4, the standard tuning pitch (標準調音音高) in Western music) is perceived as one octave higher than a tone at 220 Hz (A3). These tones are perceived as musically similar because they share a fundamental acoustic relationship: they belong to the same harmonic series (泛音列).

The harmonic series is a natural sequence of frequencies that are whole-number multiples of a fundamental frequency (基頻). If the fundamental frequency is 100 Hz, the harmonics are 200 Hz, 300 Hz, 400 Hz, and so on. Each harmonic is called an overtone (泛音), and while the fundamental determines the pitch we perceive, the combination of overtones shapes the timbre or tone color of the sound (音色).

Musically, the harmonic series explains why certain intervals, like octaves (2:1), fifths (3:2), and fourths (4:3), are perceived as more consonant (協和) — they arise early and clearly in the series. 

![image](https://hackmd.io/_uploads/S1zLAd5Lxx.png)

Let’s use **A4 = 440 Hz** as the reference pitch and compare how key intervals—**octave (P8)**, **perfect fifth (P5)**, and **perfect fourth (P4)**—appear in both **just intonation** (純律) and **equal temperament** (平均律).

| Interval               |  Just Frequency (Hz) | Equal Temperament Frequency (Hz) | Ratio |
| -------------------    |  ------------------- | -------------------------------- | --------------------- |
| Octave (A4-A5)         |  880.00 Hz           | 880.00 Hz                        | 2:1                   |
| Perfect Fifth (A4-E5)  |  660.00 Hz           | 659.26 Hz                        | 3:2                   |
| Perfect Fourth (A4-D5) |  586.67 Hz           | 587.33 Hz                        | 4:3                   |
* In **just intonation**, the fifth and fourth are derived from simple integer ratios (3:2 and 4:3), and they align with the harmonic series.
* In **equal temperament**, the octave remains identical (2:1), but all other intervals are adjusted slightly to allow every semitone to be exactly the 12th root of 2 (≈1.0595) apart. This enables modulation to all keys, but sacrifices perfect harmonic purity.


### Twelve-tone equal temperament and MIDI pitch number

A4 = 440Hz is the standard tuning pitch in Western music. In Just intonation, intervals are defined by small whole-number frequency ratios (like 2:1, 4:3). The twelve-tone equal temperament (12-TET) system divides an octave into 12 equal parts, with each semitone having a frequency ratio of $2^{1/12}$. Twelve-tone equal temperament is the most widespread system in music today. It has been the predominant tuning system of Western music. I will continue this topic in another post.

Before I close, I also want to mention **MIDI pitch number and frequency Conversion**. MIDI (Musical Instrument Digital Interface) assigns each pitch a number (0–127). For example, MIDI 69 corresponds to A4 (440Hz). The frequency of any MIDI note can be calculated with a formula.

$$
f(n) = 440 \cdot 2^{(n - 69)/12}
$$


$$
\text{MIDI 60 = C4 → }f(60) = 440 \cdot 2^{(60 - 69)/12} \approx 261.63\,\text{Hz}
$$

This formula is essential in digital music production and synthesizer programming, where pitch is often specified by MIDI number rather than by frequency.

![image](https://hackmd.io/_uploads/HyZM8YqLxl.png)


#### Digital music production

In modern digital music production, pitch is not just a perceptual or symbolic idea—it needs to be converted into precise numerical values that digital systems can process. Unlike human performers who interpret pitch intuitively, software and hardware instruments require explicit numerical instructions to know exactly what note to play and how to generate it.

This precision enables consistent and seamless pitch control across all digital platforms—including virtual instruments, DAWs (Digital Audio Workstations), and hardware synthesizers. For example, when a MIDI keyboard sends note number 60 (C4), the receiving device can instantly generate the corresponding waveform at approximately 261.63 Hz.

To support musical expression and dynamic control, synthesizers—both analog and digital—offer structured systems for pitch control. Analog synthesizers often use the volt-per-octave standard, where each additional volt doubles the frequency. Digital systems use MIDI pitch mapping, assigning numerical values (0–127) to specific notes. This allows a wide range of pitch-based operations, including:

* Fine tuning (e.g., ± cents for microtonal adjustments)
* Pitch bending (continuous pitch variation)
* Real-time modulation using LFOs, envelopes, or automation

Such control is essential for sound design: a simple sine wave can be turned into a detuned supersaw, or a melody can be shifted by microtones—all because pitch is handled as mathematical data. An example of processing MIDI file by python is shown by International Audio Laboratories Erlangen.[^4]


[^ref1]: Bisharat G, Kaganovski E, Sapir H, Temnogorod A, Levy T, et al. (2025) Repeated stress gradually impairs auditory processing and perception. PLOS Biology 23(2): e3003012.

[^2]: Elena Rusconi et al, Spatial representation of pitch height: the SMARC effect, Cognition, 99(2), 2006, 113-129,

[^3]: Bonetti, L., & Costa, M. (2017). Pitch-verticality and pitch-size cross-modal interactions. Psychology of Music, 46(3), 340-356.

[^4]: https://www.audiolabs-erlangen.de/resources/MIR/FMP/C1/C1S2_MIDI.html