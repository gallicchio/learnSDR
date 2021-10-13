# Lesson 15 --- Pulse Shaping Matched Filter


<iframe width="560" height="315" src="https://www.youtube.com/embed/JeW1HfTGnEE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br />

Last time we saw that if we use a **raised cosine spectrum** in the frequency domain, the signal in time has the very nice property that the zero crossings of all the adjacent pulses occur at the peak of the "current" pulse you are transmitting. It would seem natural, therefore, that we should use the pulse shape that arises from a raised cosine. However, it turns out that we can achieve a much higher signal-to-noise ratio---when we have to factor in real-world noise---by splitting up the raised cosine filter, applying half on the transmission side and half on the reception side.

## Matched filters

If you pass a noisy signal, whose shape in the absence of noise we know, through a filter that has the same noise-free shape, we will get maximum amplitude for a signal (noisy or otherwise) that passes through the filter with appropriate delay. This is the basic idea of a **matched filter**. So, if we transmit a **raised root cosine** pulse through a matched filter, the output has the wonderful Nyquist ISI property of no interference between pulses.
