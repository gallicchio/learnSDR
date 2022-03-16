# Lesson 2 --- Signal Generator as sine-wave transmitter and RTL-SDR receiver


<iframe width="560" height="315" src="https://www.youtube.com/embed/bV4oJTPlAeQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Notes on the Video

<b> Dictionary of GNU Radio Companion Terms </b>

<i>RTL-SDR Source</i>: Uses a signal received from a RTL-SDR USB source, which should be connected to some antenna to receive a signal.

<i>QT GUI Time Sink</i>: Plots a sequence of complex numbers coming out of the source

<i>QT GUI Frequency Sink</i>: Plots the frequency of complex numbers coming out of the source

<i>Variable</i>: Creates a variable with a name and a value, similar to instantiating a variable in Python. (<i>In the video, we instantiated samp_rate with value 1e6. 1e6, in this case, is meant for a signal of 1 mega Hertz (1 mHz); since the RTL-SDR source uses the variable samp_rate, it will be checking for some signal at a frequency of 1 mHZ.</i>)


<b> When Writing a GNU Program with the RTL-SDR Source </b>
1. Title your program in the 'Options' box at the top left of the screen
2. Set your variable samp_rate to the frequency you are expecting to receive (a value of 1 means 1 Hertz)
3. Place your RTL-SDR Source, a QT Time Sink, and a QT Frequency Sink

<b> About the Video </b> 
Rather than providing a radio-frequency signal by propagating radio waves through the air to a receiver, we will start our exploration by feeding a "pure" electronic signal from a function generator operating at 100.001 MHz into an RTL-SDR and plotting its output in both time and frequency.

We will tell the RTL-SDR that the function generator is transmitting at 100 MHz and we will find that the signal that the RTL-SDR output has the difference frequency between the function generator (100.001 MHz) and the SDR's local oscillator frequency (100 MHz), which is a sinusoidal wave at 1 kHz.

Sines and cosines are both **sinusoids**; they differ only by a **phase**. The combination of both a sine wave and a cosine wave at a given frequency can always be represented either as two signals—the cosine part, which we identify as the _real_ part (or the _in-phase_ part) of the signal, and the sine part (or the _quadrature_ part) of the signal, which represents the imaginary part of the signal. In GNU Radio, the real part is represented by default with a <span style='color:blue;'>blue</span> curve and the imaginary part is represented with a <span style='color:red;'>red</span> curve.

## When real life intrudes...

You would think that if the function generator is tuned precisely to 100.000 MHz and the SDR is set to receive the exact same frequency, that the resulting output (at the difference frequency) should be a constant. While entirely logical, that's not what happens, because the precision of the clocks in the function generator and in the SDR aren't **perfect**. They will have small but noticeable frequency offsets that may fluctuate in time with variations in local temperature. Even if they were in perfect agreement at one moment, we cannot count on their remaining synchronized as time passes. As we look at the output on the **QT GUI Time Sink**, we indeed see real and imaginary signals oscillating _very slowly_ in time; they are not steady and constant. 

Dealing with the small and gradually changing difference between clock rates in different components of a radio system will occupy a significant portion of this course; we will need to develop methods to monitor and correct for slow drifts in both frequency and phase, so that we can extract meaningful information from signals transmitted "on the back" of radio-frequency carriers.

## Homework
1. When frequency goes up, do the peaks of waves in the Time Sink get closer or farther apart?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The peaks should get **closer** together.
</details>

2. Which signal is real in the Time Sink: the blue or the red? Which sample are real numbers associated with in the Time Sink key? What sinusoidal function does represents it? What about the complex signal?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The blue wave is the real wave. It is indicated by sample 1 - additionally, it is considered as a cosine wave. Inversely, the red wave represents the complex part of the signal. This is sample 2, and it's sinusoidal function is a sine function.
</details>

3. If we are looking to receive 100 mHz on our RTL-SDR Source, but the generator's clock is slightly different than the source's (which is often the case), what happens to the functions in our Time Sink when the generator is at exactly 100 mHz?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The functions will very slowly oscillate.
</details>

4. When the signal generated is greater than the signal you are trying to receive, what do the Time and Frequency Sinks look like?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The real signal oscillates before the complex signal in the Time Sink, and the peak on the Frequency sink lies above the value we're looking for.
</details>

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
