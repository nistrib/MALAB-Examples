MATLAB-Examples include: 

# ELEC 324 Lab 3: Fourier Series, Fourier Transform and Signal Spectra

A comprehensive MATLAB implementation exploring discrete-time Fourier transforms, signal analysis, and spectrogram visualization techniques.

## Overview

This lab demonstrates fundamental signal processing concepts including:
- Discrete-Time Fourier Series (DTFS) and Discrete Fourier Transform (DFT)
- Periodic and aperiodic signal analysis
- Frequency-domain representation of signals
- Time-frequency analysis using spectrograms
- Audio signal processing and visualization

## Lab Structure

### Section 2: Periodic Signals
- Analysis of discrete-time periodic signals
- Creation of DTPS from continuous-time signals
- Period identification and signal classification

### Section 3: Discrete-Time Fourier Transform
**3.2 DFT of Sinusoidal Signals**
- Basic DFT computation and visualization
- Effects of transform size on frequency resolution
- Windowing effects and spectral leakage
- Zero-padding and frequency interpolation

**3.3 DFT of Aperiodic Signals**
- Linear frequency modulation (chirp signals)
- Effects of signal length and DFT size
- Aliasing and Nyquist limit violations

### Section 4: Spectrum Analysis
**4.0 Time and Frequency Analysis**
- FM signal generation and audio playback
- Time-reversal properties in frequency domain
- Phase and magnitude spectrum comparison

**4.1 Waterfall Spectrogram**
- 3D time-frequency representation
- Chunk-based DFT computation

**4.2 Two-Dimensional Spectrogram**
- Color-coded frequency visualization
- Overlapping window implementation
- Comparison with MATLAB's built-in `specgram`
- Real-world audio file analysis

## Key Concepts Demonstrated

### Signal Properties
- **Periodicity**: Identification of periodic vs. aperiodic signals
- **Spectral Leakage**: Effects of non-integer period windows
- **Time-Frequency Trade-off**: Chunk size vs. resolution

### DFT Properties
- **Frequency Resolution**: Δf = Fs/N
- **Time Reversal**: Magnitude preservation, phase conjugation
- **Windowing**: Rectangular window effects (sinc convolution)

### Spectrogram Parameters
- **Chunk Size**: Frequency resolution (smaller = better time resolution)
- **Overlap**: Temporal smoothness (typically 50%)
- **Colormap**: Dynamic range visualization

## Prerequisites

- MATLAB R2016a or later
- Signal Processing Toolbox (optional, for comparison functions)
- Audio files: `newvoice.wav` (provided or user-supplied)

## Usage

### Running Individual Sections

Each section can be run independently. Example:
```matlab
% Section 3.2.1: Basic DFT
clear; close all; clc;
L = 100;
period = 20;
n = 0:L-1;
x = sin(2*pi*n/period);

X = fft(x, L);
x_reconstructed = ifft(X, L);

figure;
subplot(3,1,1);
stem(n, x, 'filled');
title('Original Signal');
% ... (see full code in lab report)
```

### Complete Spectrogram Implementation
```matlab
% Generate spectrogram with overlapping chunks
Fs = 2000;
[x, ~] = audioread('newvoice.wav');
chunk_size = 256;
overlap = 0.5;

% ... (see Section 4.2.3 for complete implementation)
```

## Important Parameters

| Parameter | Typical Value | Purpose |
|-----------|--------------|---------|
| `Fs` | 2000-8000 Hz | Sampling frequency |
| `chunk_size` | 66-256 samples | DFT window size |
| `overlap` | 0.5 (50%) | Window overlap factor |
| `colormap` | jet(256) | Visualization colors |

## Key Findings

1. **DFT accurately reconstructs periodic signals** when N = L and the signal completes integer periods within the window

2. **Spectral leakage occurs** when the analysis window contains non-integer periods, spreading energy across adjacent frequency bins

3. **Overlapping chunks improve temporal resolution** in spectrograms at the cost of increased computation

4. **Multiplying signals by large constants** (e.g., 1000×) expands the color range in spectrograms, revealing low-magnitude components

5. **The DFT shows average frequency content** but doesn't reveal when frequencies occur—spectrograms solve this limitation

## Files Description

- Lab report with theoretical background and all answers
- MATLAB code snippets for each section
- Generated plots and spectrograms
- Audio analysis results

## Learning Outcomes

After completing this lab, you will understand:
- How to compute and interpret DFT coefficients
- The relationship between DTFS, DFT, and DTFT
- Time-frequency analysis trade-offs
- Practical spectrogram implementation
- Real-world audio signal analysis

## Common Issues and Solutions

**Issue**: IDFT produces small imaginary parts  
**Solution**: This is normal due to floating-point precision. Use `real(ifft(X))` for real signals

**Issue**: Spectrogram appears too dark  
**Solution**: Multiply signal by 1000 or normalize DFT magnitudes before display

**Issue**: Frequency axis doesn't match expectations  
**Solution**: Ensure proper axis scaling: `freq_axis = linspace(0, Fs/2, half_spectrum)`

## Extensions and Improvements

Consider implementing:
- Hamming or Hann windows to reduce spectral leakage
- Logarithmic magnitude scaling (dB) for better dynamic range
- Variable overlap percentages (75%, 87.5%)
- Comparison with Short-Time Fourier Transform (STFT)
- Real-time spectrogram for live audio input

## References

- Lab manual: "ELEC 324 Lab 3 – Fourier Series, Fourier Transform and Signal Spectra" © G. Chan, S. Blostein
- Course textbook (consult posted syllabus)
- MATLAB Documentation: Signal Processing Toolbox

## Author

Daniil Nistribenko  
Queen's University  
ELEC 324  
Date: November 13, 2025

## License

This lab is for educational purposes as part of ELEC 324 at Queen's University. For licensing questions regarding distribution of this code, please see the repository license file.

---

**Note**: This README accompanies the full lab report which contains detailed explanations, prelab answers, and comprehensive code listings for all sections.
