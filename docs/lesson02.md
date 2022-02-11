# Lesson 2 --- Signal Generator as sine-wave transmitter and RTL-SDR receiver


<iframe width="560" height="315" src="https://www.youtube.com/embed/bV4oJTPlAeQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Rather than using providing a radio-frequency signal by propagating radio waves through the air to a receiver, we will start our exploration by feeding a "pure" electronic signal from a function generator operating at 100.001 MHz into an RTL-SDR and plotting its output in both time and frequency.

We will tell the RTL-SDR that the function generator is transmitting at 100 MHz and we will find that the signal that the RTL-SDR output has the difference frequency between the function generator (100.001 MHz) and the SDR's local oscillator frequency (100 MHz), which is a sinusoidal wave at 1 kHz.

Sines and cosines are both **sinusoids**; they differ only by a **phase**. The combination of both a sine wave and a cosine wave at a given frequency can always be represented either as two signals—the cosine part, which we identify as the _real_ part (or the _in-phase_ part) of the signal, and the sine part (or the _quadrature_ part) of the signal, which represents the imaginary part of the signal. In GNU Radio, the real part is represented by default with a <span style='color:blue;'>blue</span> curve and the imaginary part is represented with a <span style='color:red;'>red</span> curve.

## When real life intrudes...

You would think that if the function generator is tuned precisely to 100.000 MHz and the SDR is set to receive the exact same frequency, that the resulting output (at the difference frequency) should be a constant. While entirely logical, that's not what happens, because the precision of the clocks in the function generator and in the SDR aren't **perfect**. They will have small but noticeable frequency offsets that may fluctuate in time with variations in local temperature. Even if they were in perfect agreement at one moment, we cannot count on their remaining synchronized as time passes. As we look at the output on the **QT GUI Time Sink**, we indeed see real and imaginary signals oscillating _very slowly_ in time; they are not steady and constant. 

Dealing with the small and gradually changing difference between clock rates in different components of a radio system will occupy a significant portion of this course; we will need to develop methods to monitor and correct for slow drifts in both frequency and phase, so that we can extract meaningful information from signals transmitted "on the back" of radio-frequency carriers.

## Homework

?


<!--
Transmit a 100 MHz sine wave from a signal generator simultaneously into a real oscilloscope and a BNC with hooks.

Tune the RTL-SDR to 100 MHz. You get a complex exponential out. Why not a real sinusoidal signal? What does this complex number mean? Understanding this is half the SDR battle.

Tune the generator up and down. Tune the SDR up and down. See the signal go up and down in time and frequency and maybe constellation plots.

See it go below zero frequency and explain what's going on. "Negative frequencies!?" Observe that the real and imaginary parts either lead or lag each other depending on sign of frequency.

See that it's basically a constant (or at least very slow moving) when you're tuned spot on, but the phase is arbitrary.

You need to deal with these small oscillator mismatches when you use different hardware to transmit and receive -- oscillators drift in time and frequency and when you move around.

HW Check time signal at 25.000 MHz WWV North of Denver Colorado. Hmm. Need to use 1 MHz sample_rate because otherwise the bottom of the band is below the RTL-SDR limit.

Carry the antenna around the room or close to signals. Try finding places that have the most activity, and what type of waves or what amplitude they give off.
--> 
