# Lesson 19 --- Carrier Phase Synchronization with a Costas Loop


<iframe width="560" height="315" src="https://www.youtube.com/embed/iUA4dRZww90" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Let's remind ourselves what a software-defined radio does to a real sinusoidal signal $$r(t)$$ at frequency $$f$$, with some arbitrary phase $$\phi$$,
\begin{equation}\label{eq:real-source}
  r(t) = A \cos(2\pi f t + \phi) 
\end{equation}
The SDR beats this signal against a local oscillator at frequency $$f_0$$ and produces a complex output signal
\begin{equation}\label{eq:shifted}
  z(t) = A e^{i(2\pi(f-f_0)t + \phi)}
\end{equation}
that preserves the original phase offset $$\phi$$ present in the real signal.

We have discussed how the clocks in the transmitter and receiver will not be synchronized, so that we must expect at least a modest frequency offset between the what was sent and what was (apparently) received; and we have seen how to use a [frequency-locked loop](lesson17.md) to remove most of the frequency offset.

a bit more here (including 18)

## Theory of the Costas loop

We will analyze for the case of quadrature phase-shift keying (QPSK), where the constellation of points we transmit lie on the unit circle in the complex plane along the diagonals, at phase angles of 45°, 135°, 225°, and 315°. As the receiver clock drifts gradually with respect to the transmitter clock, the phase of the received symbols will rotate slowly around the unit circle. The job of the Costas loop is to monitor and correct for this gradual rotation.

To manage this correction, the Costas loop needs to know the constellation of values that it is *supposed* to receive. For QPSK, they are the points with equal real and imaginary parts along the unit circle. When we measure something that doesn't have equal real and imaginary magnitudes, we know that we have rotated from the proper orientation. Assuming a perfect automatic gain control loop, the signal has unit magnitude and so only differs from the correct value by a pure rotation of $$e^{i\theta}$$ on the complex plane, where $$\theta$$ is the difference between the phase of the observed signal and the phase of the (nearest) constellation value.