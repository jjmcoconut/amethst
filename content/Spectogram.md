### Definition

A visual representation of the spectrum frequencies in a signals as it varies with time. 
- X axis: Time
- Y axis: Frequency
- Color: Intensity or amplitude of each frequency component at each time

### Methodology

1. Preprocess the signal(resampling, noise reduction,...)
2. Divide signal using window function(Hamming window, Hann window, ...)
3. Apply Fourier transform(usually [[Short-Time Fourier Transform(STFT)]])
4. Plot the graph using color to express intensity.

