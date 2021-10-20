# Lesson 18 --- Symbol Timing Recovery and Synchronization


<iframe width="560" height="315" src="https://www.youtube.com/embed/jag3btxSsig" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Even if the clocks in the transmitter and receiver happened to have exactly the same frequency, they will inevitably have an arbitrary phase offset, which means that sampling at the receiver won't line up with the symbol times on the transmitter. So, after using the **automatic gain controller** to get the signal level right and the frequency-locked loop to perform the gross frequency correction, we now have to correct for the slowly drifting phase offset, interpolate between samples to sample effectively at the moment when the no ISI property of the raised-cosine pulses allows us to measure the current pulse without contamination from the other pulses, and then correct for an absolute phase offset.

## Strategy

The primary problem we will address in this lesson is determining the proper timing of the symbol. Imagine that we use four samples per symbol, so we sample at four equally spaced times during the symbol pulse. Because clocks drift, the odds that we will have one of these samples at the proper time are vanishingly small. We need to interpolate between samples to "read" the symbol at the optimum time. How can we do this?

The strategy we will employ takes full advantage of the **Nyquist-Shannon sampling theorem**. Recall the gist of this important insight: provided that we sample _a bandwidth-limited signal_ at or above its Nyquist frequency---meaning that we take at least two samples per cycle of the maximum frequency that is present in the signal---**the discrete samples have all the information needed to perfectly reconstruct the continuous signal.** Amazing but true!

So, how do we use this theorem to our advantage here? We will use a strategy that allows us to precompute a number of filters that will interpolate at many places in the symbol and use an error signal to select the best filter to use.

To produce an error signal, multiply the slope times the value. When we are early, we get a positive value for the error signal. When too late, we get a negative value. $$e = x \dot{x} $$. Another would be $$e = \text{sign}(x) \dot{x}$$

Note, we need data that has transitions.

Not clear exactly why $$<e>$$ should be linear if we use the sign version.

Plot of the error is called the S curve.

- How do you compute the derivative with sparse samples?
- How do you interpolate?
- 

$$ x = r * p_{\rm RRC} $$

To get the derivative, we could use a derivative filter

$$ \dot{x} = x * d = (r * p) * d = r * (p * d) $$

To interpolate, you can upsample the signal, installing 31 zeros between each data point and then pass the output through a low-pass filter.

Precomputing can generate a bank of 32 filters, each of which acts like a shifted version of the output. Polyphase filter bank.

[Flow diagram](figs/flow/polyphase.png){: target='flow'}
