# Lesson 3 --- Complex Numbers in Software-Defined Radio

Although a radio signal is inherently a real thing---the electric field has a real magnitude and direction at a given point in space and time---the frequency shifting inherent in radio inherently introduces complex numbers, as we will see. So, to prepare, let's review some basic properties of complex numbers.

In general, a complex number has a real part and an imaginary part: $$z = x + iy$$, where $$x$$ and $$y$$ are real numbers and $$i = \sqrt{-1}$$. To add two complex numbers, just add the real parts and add the imaginary parts. For example, to add $$2+1i$$ and $$1 + 3i$$, add the real parts ($$2+1=3$$) and add the imaginary parts ($$1i + 3i = 4i$$). The result is $$3 + 4i$$.

A very useful way to visualize this process is to represent complex numbers with their real part along the $$x$$ axis and their imaginary part along the $$y$$ axis. This same addition problem is illustrated in the following figure.

![Addition of complex numbers](figs/complex-addition.png){: width="400px" height="400px"}

## Multiplying Complex Numbers

You can multiply two complex numbers just the way you would algebraic expressions (using FOIL, but I will change the order to FLOI for "firsts-lasts-outside-inside"):
\begin{equation}
  (a+b)\times(c+d) = ac + bd + ad + bc 
\end{equation}
Similarly,
\begin{equation}
  (2+1i) \times (3+4i) = (2\times3) + (1i\times 4i) + (2\times4 i) + (1i\times 3)
\end{equation}
\begin{equation}
  = (6-4) + (8+3)i = 2 + 11 i
\end{equation}
where we have used that $$i^2=-1$$. This is just the approach the computer uses, but we will see that multiplication gets simpler when we use polar form for complex numbers.

Do you see why I changed the order in "FOIL"?
<details>
<summary markdown='span'> Click to expand </summary>

The product of the *lasts* yields a real number, since $$i^2=-1$$, so it helps to put it next to the product of the *firsts*, which is also real. The *outsides* and the *insides* yield imaginary terms.
</details>

## Polar Form

The polar form of a complex number uses the "length" of the number and its orientation angle with respect to the real axis to specify the number, rather than its real and imaginary components. To express the complex number $$4 + 3i$$ in polar form, examine the figure below.

![Polar form of complex numbers](figs/complex-polar.png){: width="400px" height="400px"}

Using the Pythagorean theorem, we can compute the length of the hypotenuse, which is the magnitude $$r$$ of the number:
\begin{equation}
  r = \sqrt{4^2 + 3^2} = \sqrt{25} = 5
\end{equation}
We could also express the phase angle $$\phi$$ using the definition of tangent, which is opposite over adjacent:
\begin{equation}
  \tan\phi = \frac{3}{4} \qquad\text{or}\qquad \phi = \arctan(3/4) \approx 36.9°
\end{equation}

## Euler's Identity

There is a most beautiful mathematical relationship known as **Euler's identity** that makes expressing complex numbers in polar form incredibly useful. It is
\begin{equation}
  e^{i\phi} = \cos\phi + i \sin\phi
\end{equation}
If you have learned about Taylor series, you can probably show that this is true, but if you haven't, don't worry. We will just use Euler's identity to express the complex number $$z = 4 + 3i$$ as
\begin{equation}
  z = r e^{i\phi}
\end{equation}

Why is this so great? Well, because when you multiply exponentials, you just add the exponents. So, if we have numbers $$z_1 = r_1 e^{i \phi_1}$$ and $$z_2 = r_2 e^{i \phi_2}$$, their product is
\begin{equation}
  z_1 \times z_2 = r_1 e^{i \phi_1} \times r_2 e^{i \phi_2} = r_1 r_2 e^{i(\phi_1+\phi_2)}
\end{equation}

- The magnitude of the product of the two complex numbers is the product of their magnitudes
- The phase of the product of two complex numbers is the sum of their phases

Put another way, complex multiplication rotates and stretches complex numbers.

**Exercise:** If $$z_1 = 3 e^{i 30°}$$ and $$z_2 = 4 e^{i 60°}$$, what is $$z_1 z_2$$? Work it out first in polar form, then try it in rectangular $$(x + iy)$$ form. You'll see why we love the polar version!
<details>
<summary markdown='span'> Click to expand </summary>

$$z_1 z_2 = 12 e^{i 90°} = 12 i$$
</details>

## Complex Sinusoids

What does a signal of the form $$A e^{i\;2\pi f t}$$ look like? According to Euler's identity, it is
\begin{equation}
  A e^{i\;2\pi f t} = A \cos(2\pi f t) + i A \sin(2\pi f t)
\end{equation}
In other words, the real part is a cosine wave with amplitude $$A$$ and frequency $$f$$. The imaginary part is a sine wave with the same amplitude and frequency. By default, GNU Radio shows the real part in blue and the imaginary part in red. So, a plot of a pure "cosine" wave, when passed to a **QT GUI Time Sink** appears as in the figure below.

![Complex cosine wave in GNU Radio](figs/complex-cosine.png)

Note that the blue (real) part starts at 1 and is a cosine wave, whereas the red (imag) part starts at 0 and rises with increasing time. What is the frequency of this source?
<details>
<summary markdown='span'> Click to expand </summary>

The period of the wave is 1 ms, so the frequency is 1 kHz.
</details>

## Negative Frequencies

*Yes, but why do we care? Real electrical signals are **real**, aren't they?* Well, yes, they are. As you can verify from Euler's identity,
\begin{equation}
  \cos \phi = \frac{1}{2} (e^{i\phi} + e^{-i\phi})
\end{equation}
for any phase $$\phi$$, including $$\phi = 2\pi f t$$. That is, a real cosine wave is composed of equal parts of positive and negative frequencies:
\begin{equation}
  \cos(2\pi f t) = \frac{1}{2} ( e^{i\,2\pi f t} + e^{-i \,2\pi f t})
\end{equation}

When a software-defined radio *mixes* such a wave with a high-frequency carrier, it multiplies the cosine wave by a signal of the form $$2 e^{-i 2\pi f_0 t}$$. That produces
\begin{equation}
  2\cos(2\pi f t) e^{-i 2\pi f_0 t} = [ e^{i\,2\pi (f-f_0) t} + e^{-i \,2\pi (f+f_0) t}]
\end{equation}
The first term oscillates at the difference frequency $$f - f_0$$. For frequencies $$f$$ close to the carrier frequency, the difference frequency will be *much* lower in frequency. The second term oscillates at almost twice the carrier frequency. Passing the result through a **low-pass filter**, which strongly attenuates high frequencies, effectively removes the second term, leaving just $$ e^{i\,2\pi (f-f_0) t} $$, which is clearly a **complex sinusoidal signal**. Thus, the frequency shifting done by a software-defined radio necessarily generates complex signals.

## Illustrations in GNU Radio

- time sinks
- frequency sinks
- constellation plots



## Homework

1. The Taylor series for the exponential function is
\begin{equation}
  e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots
\end{equation}
where $$n! = n (n-1) (n-2) \cdots (2) (1)$$ is the factorial of $$n$$.