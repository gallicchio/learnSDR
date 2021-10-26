# Lesson 4 --- What's Inside the Software-Defined Radio?
(Designing one from first principles)


<iframe width="560" height="315" src="https://www.youtube.com/embed/O09DTlp_UAw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

As we saw last time, using Euler's identity, $$e^{i\phi} = \cos\phi + i \sin\phi$$, we can write the manifestly real function $$\cos\phi$$ as the sum of two complex exponentials:
\begin{equation}
  \cos\phi = \frac{1}{2}(e^{i\phi} + e^{-i\phi})
\end{equation}

Now consider what happens if we multiply a cosine at one frequency, $$f$$, by another at $$f_0$$:
\begin{align}
  \cos(2\pi f t)\;& 2\cos(2 \pi f_0 t) = \frac{1}{2} \bigg( e^{i 2\pi f t} + e^{-i 2 \pi f t} \bigg)\bigg(e^{i 2\pi f_0 t} + e^{-i 2 \pi f_0 t} \bigg) \\\\  &= \frac{1}{2}\bigg[ \textcolor{blue}{e^{i 2\pi (f+f_0)t}} + \textcolor{red}{e^{i 2\pi (f-f_0)t} + e^{-i 2\pi (f-f_0)t}} + \textcolor{blue}{e^{-i 2\pi (f+f_0)t}}\bigg] \\\\ &= \textcolor{blue}{\cos[2\pi(f+f_0)t]} + \textcolor{red}{\cos[2\pi(f-f_0)t]}
\end{align}
We get a cosine at the sum of the two frequencies and another at the difference frequency. If $$f$$ and $$f_0$$ are not too dissimilar, the difference frequency will oscillate **much** more slowly than $$f_0$$, so that if we were to pass this product of cosines through a low-pass filter, only the difference frequency would emerge with appreciable amplitude. You can confirm that a similar separation into sine functions would take place on the lower branch of Fig. 1.

<p class='center' markdown='0'>
  <img src='figs/how-it-works.png' alt='How a software-defined radio works' style="width: 100%;">
</p>

<p class='mycap' markdown='1'>
**Figure 1** --- Consider a real sinusoidal signal, $$r(t) = A \cos(2 \pi f t + \phi_{0})$$ entering the diagram from the left. A local oscillator (LO) at frequency $$f_0$$ generates $$2\cos(2\pi f_0 t)$$ which multiplies $$r(t)$$ on the upper branch, and a shifted version multiplies $$r(t)$$ by $$-2 \sin(2 \pi f_0 t)$$ on the lower branch. Each product passes through a low-pass filter and is then digitized.
</p>

As illustrated in Fig. 1, the software-defined radio has to manage two of these operations using a local oscillator at frequency $$f_0$$ and a copy shifted by exactly 90° to yield the real part of the difference-frequency signal, $$x(t)$$ and the imaginary part $$y(t)$$ that together represent the signal at the difference frequency,
\begin{equation}
  z(t) = x(t) + i y(t) = e^{i 2\pi (f-f_0) t}
\end{equation}
