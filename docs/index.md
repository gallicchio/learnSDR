# Learn SDR : Tutorials with Videos

We use the [GNURadio](https://www.gnuradio.org/) software along with [RTL-SDR](https://www.rtl-sdr.com/buy-rtl-sdr-dvb-t-dongles/) and [ADALM-PLUTO](https://wiki.analog.com/university/tools/pluto) hardware to explore the world of digital communication. We build up to a simple QPSK modem and rudimentary GPS reception.

- [Installation --- Instructions for installing GNURadio](installation.md)
- [Lesson 1 --- FM broadcast receiver with RTL-SDR](lesson01.md)
- [Lesson 2 --- Signal Generator as sine-wave transmitter and RTL-SDR receiver](lesson02.md)
- [Lesson 3a --- Complex Numbers in SDR](lesson03a.md)
- [Lesson 3b --- Negative Frequencies](lesson03b.md)
- [Lesson 4 --- What's Inside a Software-Defined Radio?](lesson04.md)
- [Lesson 5 --- On-Off Keying with Adafruit Keyfob 4-Button RF Remote Control](lesson05.md)
- [Lesson 6 --- Sampling](lesson06.md)
- [Lesson 7 --- Frequency Spectrum, Fourier Transform, and FFT](lesson07.md)
- [Lesson 8a --- Transmit and Receive from a PlutoSDR](lesson08a.md)
- [Lesson 8b --- Pluto Doppler RADAR](lesson08b.md)
- [Lesson 9 --- Tx from Pluto, Rx on RTL-SDR](lesson09.md)
- [Lesson 10 --- On-Off Keying (OOK) from Pluto to RTL SDR](lesson10.md)
- [Lesson 11 --- Amplitude-Shift Keying (ASK) from Pluto to SDR](lesson11.md)
- [Lesson 12 --- PSK (BPSK) Phase-Shift Keying](lesson12.md)
- [Lesson 13 --- QPSK Naive with no Pulse Shaping](lesson13.md)
- [Lesson 14 --- Pulse Shaping and Nyquist Criteria](lesson14.md)
- [Lesson 15 --- Pulse Shaping Matched Filter](lesson15.md)
- [Lesson 16 --- Constellation Modulator](lesson16.md)
- [Lesson 17 --- Frequency Locked Loop (FLL)](lesson17.md)
- [Lesson 18 --- Symbol Timing Recovery and Synchronization](lesson18.md)
- [Lesson 19 --- Carrier Phase Synchronization with a Costas Loop](lesson19.md)
- [Lesson 20 --- Resolving the Phase Ambiguity and Differential Encoding](lesson20.md)
- [Lesson 21 --- Linear Feedback Shift Registers (LFSR)](lesson21.md)
- [Lesson 22 --- GPS Gold Codes; Spread Spectrum; Code-division multiple access (CDMA)](lesson22.md)
- [Lesson 23 --- GPS Reception](lesson23.md)

References:

- Software Defined Radio (SDR) and Digital Communications Books:
 - [Chaudhari; Wireless Communications from the Ground Up: An SDR Perspective](https://www.addall.com/New/NewCompare.cgi?isbn=9781729732236) -- The book I first used to understand tricky things like timing synchronization. Lots of pictures and intuition. Explains GNUradio blocks. I wish he wouldn’t avoid complex numbers, because it makes many things messy and opaque with lots of trig identities.
 - [Rice; Digital Communications: A Discrete-Time Approach](https://www.amazon.com/Digital-Communications-Discrete-Time-Michael-Rice/dp/B08GVGCKCC) -- The second good book I read on this topic. A bit more mathy than Chaudhari, but good explanations. Introduces and uses complex notation. Many of my lessons are inspired by this book, including Symbol Timing Recovery and Carrier Phase Synchronization.
 - [Collins et al; Software-Defined Radio for Engineers](https://www.analog.com/en/education/education-library/software-defined-radio-for-engineers.html) A free PDF from Analog Devices. Uses Pluto as an example, which is good, but isn’t as well written as the above.
 - [Proakis; Digital Communications 5th Edition](https://www.addall.com/New/NewCompare.cgi?isbn=0072957166) Advanced and very mathy; proves optimality under certain conditions; only book here to really talk about FSK, MSK, GMSK and code-division multiple access (CDMA) with pseudo-random streams.
 - PySDR: A Guide to SDR and DSP using Python (online book) <https://pysdr.org/>
- Digital Signal Processing DSP Books (sampling, noise, FIR filters, correlation and convolution, quadrature (complex) signals, and all Fourier techniques DFT, FFT)
 - [Smith; Scientist & Engineer's Guide](https://www.analog.com/en/education/education-library/scientist_engineers_guide.html#) -- online and in print. A very concrete start. My only criticism is that I wish he’d introduce complex numbers earlier.
 - Lyons; Understanding DSP -- another good self-study book with lots of figures.
 - Oppenheim and Schafer Discrete-Time Signal Processing -- the standard textbook. Assumes more background and introduces mathy things like z-transforms too early, at least for our applications.
 - Learning DSP Illustrated: <https://dspillustrations.com/> (lots of little python examples)
- Global Satellite Navigation Systems (GNSS) and GPS Books:
 - Borre et al A Software-Defined GPS and Galileo Receiver -- where I started. Talks about acquisition through Fourier correlation and feedback-loop tracking.
 - Tsui Fundamentals of GPS Receivers A Software Approach -- I think this is the second thing I read

All GNURadio flowgraphs are at <https://github.com/gallicchio/learnSDR>

Back to top: <https://gallicchio.github.io/learnSDR>

<!---
- Lesson 20 --- Full PSK or QPSK modem with carrier and timing recovery
- Lesson 24 --- Equalization (skip for GNUradio 3.8 because everything changes in 3.9)
- Lesson 25 --- Orthogonal Frequency-Division Multiplexing (OFDM) (Too advanced?)
- Lesson 26 --- Frequency Shift Keying (FSK) Pluto to RTL-SDR
- Lesson 27 --- Minimum-Shift Keying (MSK) and Gaussian-MSK (GMSK)
- Lesson 28 --- Noise (meant to talk about this earlier but it broke the flow)
- Lesson 29 --- Filtering (meant to talk about this earlier but it broke the flow)
- Lesson 30 --- Correlation
- Lesson 31 --- Chirps in radar and LoRa
- Lesson 32 --- Linear Feedback Shift Registers (LFSRs) and Gold Codes
- Lesson 33 --- Spread spectrum and Code-Division Multiple Access (CDMA)
- Lesson 34 --- GPS outside (slide Doppler by hand and see code correlation)
- Lesson 35 --- MIMO Phased array of 2 antennas into a B210
- Lesson 36 --- Direction Finding
-->
