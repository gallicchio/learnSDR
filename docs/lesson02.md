# Lesson 2 --- Signal Generator as sine-wave transmitter and RTL-SDR receiver


<iframe width="560" height="315" src="https://www.youtube.com/embed/bV4oJTPlAeQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<!--
Transmit a 100 MHz sine wave from a signal generator simultaneously into a real oscilloscope and a BNC with hooks.

Tune the RTL-SDR to 100 MHz. You get a complex exponential out. Why not a real sinusoidal signal? What does this complex number mean? Understanding this is half the SDR battle.

Tune the generator up and down. Tune the SDR up and down. See the signal go up and down in time and frequency and maybe constellation plots.

See it go below zero frequency and explain what's going on. "Negative frequencies!?" Observe that the real and imaginary parts either lead or lag each other depending on sign of frequency.

See that it's basically a constant (or at least very slow moving) when you're tuned spot on, but the phase is arbitrary.

You need to deal with these small oscillator mismatches when you use different hardware to transmit and receive -- oscillators drift in time and frequency and when you move around.

HW Check time signal at 25.000 MHz WWV North of Denver Colorado. Hmm. Need to use 1 MHz sample_rate because otherwise the bottom of the band is below the RTL-SDR limit.

--> 