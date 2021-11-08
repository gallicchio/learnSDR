# Key Concepts and Where They are Introduced

## Mathematics

+ The relationship between sines & cosines and complex exponentials [(Euler's identity)](lesson03a.md){:target="_link"}
+ Representing complex numbers in polar form greatly simplifies [complex multiplication](lesson03a#multiplying-complex-numbers-in-polar-form){:target="_link"}
+ The product of two sinusoidal functions with frequencies $$f$$ and $$f_0$$ is [the sum of sinusoids at frequencies $$f+f_0$$ and $$f-f_0$$](lesson03b.md){:target="_link"}
+ Periodic signals with period $$T$$ may be expressed as a **Fourier series**:
\begin{equation}\label{eq:Fourier-series}
  f(t) = a_0 + \sum_{n=1}^{\infty} \bigg[ a_n \cos\bigg(\frac{2\pi n t}{T}\bigg) + b_n \sin\bigg(\frac{2\pi n t}{T}\bigg) \bigg]
\end{equation}
where the amplitude coefficients $$a_n$$ and $$b_n$$ can be determined by integration:
\begin{align}
  a_0 &= \frac{1}{T} \int_0^T f(t) \; dt \\\\  a_n &= \frac{2}{T} \int_0^T f(t) 
  \cos\bigg(\frac{2\pi n t}{T}\bigg)\;dt \\\\ b_n &= \frac{2}{T} \int_0^T f(t)
  \sin\bigg(\frac{2\pi n t}{T}\bigg)\;dt
\end{align}

## Digital Signal Processing

+ Any signal in time may be represented as a superposition (sum) of sinusoidal functions of various frequencies; the Fourier transform maps the representation in time to the representation in frequency, and vice versa.
+ The power in a sinusoidal signal is proportional to the **square** of its **amplitude** (in volts, for example).
+ Signals as a function of frequency are typically displayed using a logarithmic scale in **decibels**. Suppose signal 1 has amplitude $$A_1 = 1$$ and signal 2 has amplitude $$A_2 = 10^{-2}$$. We may express the strength of $$A_2$$ with respect to $$A_1$$ as $$A_2/A_1 = 0.01$$. In decibels, the amplitude ratio would be expressed
\begin{equation}
    \frac{A_2}{A_1} = -10 \log_{10} (0.01) = 20\text{ dB}
\end{equation}
That is, the decibel expression for the *amplitude ratio* is ten times the negative base-10 logarithm of the amplitude ratio. Because the power in a signal is proportional to the *square of its amplitude*, the decibel expression for the power in signal 1 compared to signal 2 is
\begin{equation}
  P_2 / P_1 = 20 \log_{10} (A_2/A_1)
\end{equation}
amplitudes that differ by a factor of 10 In a GNU Radio flow diagram, a **QT Frequency Sink** shows the power in the signal it displays as a function of frequency using decibels. For 
+ [A low-pass filter](lesson03b#low-pass){:target="_link"} transmits frequencies below a corner frequency without attenuation (nearly), but attenuates frequencies above the corner frequency more strongly the farther they are above the corner frequency. If you know something about resistors and capacitors, the

<p class='center' markdown='0'>
  <img src='figs/low-pass-circuit.png' alt='low-pass circuit' style='width: 200px;'>
</p>

<p class='mycap' markdown='1' style="margin-left: 48px;">
**Figure n** --- Since a capacitor is a "short-circuit" at high frequency, high-frequency signals will be strongly attenuated. On the other hand, at low frequencies a capacitor is like an open circuit (it charges up to the applied voltage), so $$V_{\rm out} \approx V_{\rm in}$$ (meaning that the low-frequency signal passes through unattenuated).
</p>


## GNU Radio Blocks

+ blah 
