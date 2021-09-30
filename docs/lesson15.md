# Lesson 15 --- Pulse Shapes - Root Raised Cosine

Scratch notes from live lecture:

Key Idea: How can we recover digital data from an input stream?

## Conceptual
Rectangular pulse with T_s period.

Boxcar pulse

A raised cosine pulse in the frequency spectrum. (1 + \alpha)/T_s

has impulse response with trace sin(x)/x

where \alpha is excess bandwidth

\alpha is our design parameter. The smaller the \alpha, the closer to the minimum bandwidth. But it also looks closer to a bit of data.

Decrease alpha, lower bandwidth. Increase alpha, humps look nice, transitions look better. It makes timing recovery easier.

NO ISI

No intersymbol intereference, property holds for any alpha.

Nyquist ISI criteria

To create a raised cosine pulse in the time spectrum, send a discrete time impulse (use Vector Source block) and send it into a Root Raised Cosine Filter.

Compare 

## GNURadio Practical

Challenge: where to sample my input stream to recover the 1's and 0's in digital data.


