# Lesson 2 --- Signal Generator as sine-wave transmitter and RTL-SDR receiver


<iframe width="560" height="315" src="https://www.youtube.com/embed/bV4oJTPlAeQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Notes on the Video

The simplest radio signal to work with is a pure sinusoidal wave with no modulation (changes) in frequency or amplitude. I generate such a signal around 100 MHz with a signal generator, show it on an oscilloscope, and look at the data coming from the SDR tuned to 100 MHz. I make a few observations whose significance will be fully explained in the next few lessons.

1. The data that comes out of the SDR is a sequence of complex numbers. We'll spend a lot of time explaining why this is and what it means.
2. A plot of the real part of the complex numbers looks like a consine and a plot of the imaginary part of the numbers looks like a sine.
3. The frequency of the real and imaginary sinusoids isn't at the absolute frequency of transmission of 100.010 MHz --- we don't sample fast enough to see that. Instead, it's at the difference between the frequency that the transmitter sends and the frequency that the receiver is tuned to. (100.010 MHz - 100.000 MHz = +10 kHz).
4. A plot of the spectrum shows a peak not at the absolute frequency 100.010 MHz, but at the difference in frequencies of +10 kHz.
5. If the transmitter then sends 99.990 MHz, a frequency 10 kHz lower than what the tranmistter is tuned to, it will show up as a negative frequency, -10 kHz, on the frequency spectrum. In the time-series plots, the imaginary part's sine wave has switched signs. Negative frequencies and the details of these complex numbers will be further explained in the next few lessons.

Sines and cosines are both **sinusoids**; they differ only by a **phase**. The combination of both a sine wave and a cosine wave at a given frequency can always be represented either as two signals—the cosine part, which we identify as the _real_ part (or the _in-phase_ part) of the signal, and the sine part (or the _quadrature_ part) of the signal, which represents the imaginary part of the signal. In GNU Radio, the real part is represented by default with a <span style='color:blue;'>blue</span> curve and the imaginary part is represented with a <span style='color:red;'>red</span> curve.


## Dictionary of GNU Radio Companion Terms

<i>RTL-SDR Source</i>: Uses a signal received from a RTL-SDR USB source, which should be connected to some antenna to receive a signal.

<i>QT GUI Time Sink</i>: Plots a sequence of complex numbers coming out of the source

<i>QT GUI Frequency Sink</i>: Plots the frequency of complex numbers coming out of the source

<i>Variable</i>: Creates a variable with a name and a value, similar to instantiating a variable in Python. (<i>In the video, we instantiated samp_rate with value 1e6. 1e6, in this case, is meant for a signal of 1 Mega Hertz (1 MHz); since the RTL-SDR source uses the variable samp_rate, it will be checking for some signal at a frequency of 1 MHz.</i>)


<b> When Writing a GNU Program with the RTL-SDR Source </b>
1. Title your program in the 'Options' box at the top left of the screen
2. Set your variable samp_rate to the frequency you are expecting to receive (a value of 1 means 1 Hertz)
3. Place your RTL-SDR Source, a QT Time Sink, and a QT Frequency Sink


## When real life intrudes...

You would think that if the function generator is tuned precisely to 100.000 MHz and the SDR is set to receive the exact same frequency, that the resulting output (at the difference frequency) should be a constant (0 Hz). While entirely logical, that's not what happens, because the precision of the clocks in the function generator and in the SDR aren't **perfect**. They will have small but noticeable frequency offsets that may fluctuate in time with variations in local temperature. Even if they were in perfect agreement at one moment, we cannot count on their remaining synchronized as time passes. As we look at the output on the **QT GUI Time Sink**, we indeed see real and imaginary signals oscillating _very slowly_ in time; they are not steady and constant. 

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

3. If we are looking to receive 100 MHz on our RTL-SDR Source, but the generator's clock is slightly different than the source's (which is often the case), what happens to the functions in our Time Sink when the generator is at exactly 100 MHz?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The plots will very slowly oscillate.
</details>

4. When the frequency of the signal generated is greater than the tunning of the receiver, what do the Time and Frequency Sinks look like?

<details markdown='block'>
<summary markdown='span'> Click to expand </summary>

The real signal reaches its maximum before the imaginary signal in the Time Sink, and the peak on the Frequency sink lies above the value we're looking for.
</details>

All GNURadio flowgraphs are at [https://github.com/gallicchio/learnSDR](https://github.com/gallicchio/learnSDR)

<!--
Transmit a 100 MHz sine wave from a signal generator simultaneously into a real oscilloscope and a BNC with hooks.

Tune the RTL-SDR to 100 MHz. You get a complex exponential out. Why not a real sinusoidal signal? What does this complex number mean? Understanding this is half the SDR battle.

Tune the generator up and down. Tune the SDR up and down. See the signal go up and down in time and frequency and maybe constellation plots.

See it go below zero frequency and explain what's going on. "Negative frequencies!?" Observe that the real and imaginary parts either lead or lag each other depending on sign of frequency.

See that it's basically a constant (or at least very slow moving) when you're tuned spot on, but the phase is arbitrary.

You need to deal with these small oscillator mismatches when you use different hardware to transmit and receive -- oscillators drift in time and frequency and when you move around.

HW Check time signal at 25.000 MHz WWV North of Denver Colorado. Hmm. Need to use 1 MHz sample_rate because otherwise the bottom of the band is below the RTL-SDR limit.

Carry the antenna around the room or close to signals. Try finding places that have the most activity, and what type of waves or what amplitude they give off.

Zoe's additions:
1. Transmit a signal from a signal generator through an oscilloscope and through your RTL-SDR radio to see the difference like we did in the video. Try approaching the MHz frequency that your GNU Radio Companion is set to using the signal generator, and make sure that you see the sinosoidal functions become flat planes.
2. Tune the generator up and down. In the QT folder (where you found QT GUI Frequency Sink), find the `QT GUI Constellation Sink` and attach that to to the RTL-SDR block. What do you see as you change the frequency? What doesn't change?
3. If you move the signal generator below 0 MHz, what does that negative frequency mean? What happens to the sinosoidal functions when you make the frequency negative? Explain why.
4. Carry your antenna and computer around the room. Try to find the places in your room with the most frequency or radio activity, and what types of waves and what level of amplitude they give off. If you are around a larger structure that carries, receives, or produces signals, like a radio tower, try walking nearby and seeing what happens.

--> 
