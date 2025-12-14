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

*In this series, I try to (progressively) understand the connections between music theory and physics. Starting from revisting fundamental concepts in music theory, gradually integrating mathematical perspectives, ultimately leading to a visual interpretation of musical structures through Lissajous curves.*

#### Pitch as a perceptual quality (感知)

Is pitch simply the same as frequency? How do we define them? 

In school physics, we learn about sound waves and their properties, like waveform (波形), frequency (頻率), and amplitude (振福). These are often linked to things like tone quality (音色), pitch (音高/音準), and loudness (音量). Frequency is basically the number of vibrations per second, measured in Hertz (Hz).

Pitch, on the other hand, is more about how high or low a sound seems to a listener. Usually, higher frequencies are thought of as higher pitches, but the relationship isn't perfectly linear. It can be affected by things like context, the sound's texture, and how our ears work. Pitch is more like a perceptual quality

> An interesting recent research on mice exposed to repetitive stress shows that how we perceive things like pitch and loudness can actually be changed even if the physical stimulus isn't there, revealing how prolonged stress dampens sound-evoked responses and leads to reduced loudness perception.[^[ref1]] 

#### "high" vs. "low" sounds

We say a pitch is "high" or "low" because our brains map auditory features onto spatial metaphors, particularly vertical ones. It's not that sound waves physically move up or down, but that our perception of pitch is based on space. This could be probably influenced by:

* Embodied cognition - we often think of more as being better (e.g. more light is "brighter", more temperature is "hotter", more pitch is "higher"). Words like "high pitch" (English), 「高い音」 (Japanese), and「高音」(Chinese) all describe high-frequency sounds using vertical metaphors.

* Musical instrument design - many of them put high notes right above low ones (like on a piano or the different strings). People also tend to use right hand to indicate high sound while left hand for low sound.

* Perceptual mapping – Psychophysical studies show that people naturally associate high frequencies with higher spatial locations, even in cross-modal matching tasks (e.g., matching sound to height).[^[2]] [^[3]]

The idea of pitch as a spatial concept comes about because we perceive it, not measure it directly. It all comes down to how our ears work, picking up different frequencies, and our brain often frames it in a spatial way.


#### Octaves, Harmonic Series, and Overtones

But here we still describe musical notes in terms of their physical frequency. ;-)

In music, when one sound has exactly twice the frequency of another, the two are said to be one octave (八度) apart. For example, a tone at 440 Hz (A4, the standard tuning pitch (標準調音音高) in Western music) is perceived as one octave higher than a tone at 220 Hz (A3). These tones are perceived as musically similar because they share a fundamental acoustic relationship: they belong to the same harmonic series (泛音列).

The harmonic series is a natural sequence of frequencies that are whole-number multiples of a fundamental frequency (基頻). If the fundamental frequency is 100 Hz, the harmonics are 200 Hz, 300 Hz, 400 Hz, and so on. Each harmonic is called an overtone (泛音), and while the fundamental determines the pitch we perceive, the combination of overtones shapes the timbre or tone color of the sound (音色).

Musically, the harmonic series explains why certain intervals, like octaves (2:1), fifths (3:2), and fourths (4:3), are perceived as more consonant (協和). They arise early and clearly in the series. 

![image](https://hackmd.io/_uploads/S1zLAd5Lxx.png)

Let’s use **A4 = 440 Hz** as the reference pitch and compare how key intervals—**octave (P8)**, **perfect fifth (P5)**, and **perfect fourth (P4)**—appear in both **just intonation** (純律) and **equal temperament** (平均律). Just intonation and equal temperament are tuning systems.

In **just intonation**, intervals are defined by small whole-number frequency ratios (like 2:1, 4:3), aligning with the harmonic series. The **twelve-tone equal temperament (12-TET)** system divides an octave into 12 equal parts, with each semitone having a frequency ratio of $$2^{1/12}$$. Twelve-tone equal temperament is the most widespread tuning system in music today. I will continue this topic in another post.

An octave from A4 (440 Hz) to A5 is the same in both systems: 880 Hz, because both define the octave as a 2:1 frequency ratio. A perfect fifth (A4 to E5) in just intonation is 660 Hz, while in equal temperament it is slightly lower at 659.26 Hz. A perfect fourth (A4 to D5) is 586.67 Hz in just intonation and slightly higher at 587.33 Hz in equal temperament.


#### Twelve-tone equal temperament and MIDI pitch number

In modern digital music production, pitch is not just a perceptual or symbolic idea—it needs to be converted into precise numerical values that digital systems can process. Unlike human performers who interpret pitch intuitively, software and hardware instruments require explicit numerical instructions to know exactly what note to play and how to generate it.

The **twelve-tone equal temperament (12-TET)** system divides an octave into 12 equal parts, with each semitone having a frequency ratio of $$2^{1/12}$$. This is implemented in the MIDI (Musical Instrument Digital Interface) system. MIDI (Musical Instrument Digital Interface) assigns each pitch a number (0–127). For example, MIDI 69 corresponds to A4 (440Hz). The frequency of any MIDI note can be calculated with a formula.

$$
f(n) = 440 \cdot 2^{(n - 69)/12}
$$


$$
\text{MIDI 60 = C4 → }f(60) = 440 \cdot 2^{(60 - 69)/12} \approx 261.63\,\text{Hz}
$$


![image](https://hackmd.io/_uploads/HyZM8YqLxl.png)


This precision enables consistent and seamless pitch control across all digital platforms, including virtual instruments and hardware synthesizers. For example, when a MIDI keyboard sends note number 60 (C4), the receiving device can instantly generate the corresponding waveform at approximately 261.63 Hz.

For exmaple, synthesizers offer structured systems for pitch control. Analog synthesizers often use the volt-per-octave standard, where each additional volt doubles the frequency. Digital systems use MIDI pitch mapping, assigning numerical values (0–127) to specific notes. This allows a wide range of pitch-based operations, such as fine tuning, pitch variation, and automation — all because pitch is handled as mathematical data. An example of processing MIDI file by python is shown by International Audio Laboratories Erlangen.[^4]


$$
\quad
$$

---

$$
\quad
$$

#### References

[^ref1]: Bisharat G, Kaganovski E, Sapir H, Temnogorod A, Levy T, et al. (2025) Repeated stress gradually impairs auditory processing and perception. PLOS Biology 23(2): e3003012.

[^2]: Elena Rusconi et al, Spatial representation of pitch height: the SMARC effect, Cognition, 99(2), 2006, 113-129,

[^3]: Bonetti, L., & Costa, M. (2017). Pitch-verticality and pitch-size cross-modal interactions. Psychology of Music, 46(3), 340-356.

[^4]: https://www.audiolabs-erlangen.de/resources/MIR/FMP/C1/C1S2_MIDI.html