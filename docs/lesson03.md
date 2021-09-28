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

## Polar Form

The polar form of a complex number uses the "length" of the number and its orientation angle with respect to the real axis to specify the number, rather than its real and imaginary components. To express the complex number $$4 + 3i$$ in polar form, examine the figure below.

![Polar form of complex numbers](figs/complex-polar.png){: width="400px" height="400px"}

Using the Pythagorean theorem, we can compute the length of the hypotenuse, which is the magnitude $$r$$ of the number:
\begin{equation}
  r = \sqrt{4^2 + 3^2} = \sqrt{25} = 5
\end{equation}
We could also express the phase angle $$\phi$$ using the definition of tangent, which is opposite over adjacent:
\begin{equation}
  \tan\phi = \frac{3}{4} \qquad \phi = \arctan(3/4)
\end{equation}

## Euler's Identity

## Complex Sinusoids

## Illustrations in GNU Radio

- time sinks
- frequency sinks
- constellation plots

## Negative Frequencies
