# Learn SDR : Tutorials with Videos

All GNURadio flowgraphs are at <https://github.com/gallicchio/learnSDR>

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
- [Extra: Spectrum Analyzer Demo with USRP B210 or X310](SpectrumDemo.md)
- Absolute link to this index: <https://gallicchio.github.io/learnSDR>

<!---
These lessons were planned, but have not yet been made:
- Lesson 21 --- Full PSK or QPSK modem with carrier and timing recovery
- Lesson 22 --- Example of decoding some widely-available PSK or QPSK signal from a satellite or something.
- Lesson 23 --- Pluto transmit QPSK DVB-S2
- Lesson 24 --- Multipath and Equalization (skip for GNUradio 3.8 because everything changes in 3.9)
- Lesson 25 --- Orthogonal Frequency-Division Multiplexing (OFDM) and cyclic prefix
- Lesson 26 --- Frequency Shift Keying (FSK) Pluto to RTL-SDR. Pagers: POCSAG as 2FSK and FLEX as 4FSK
- Lesson 27 --- Minimum-Shift Keying (MSK) and Gaussian-MSK (GMSK). ACARS, AIS, GSM 2G
- Lesson 28 --- Noise: source of physics RF nosise; mathematically-generated white gaussian; spectral density
- Lesson 29 --- Filtering LPF, HPF, BPF. Transition sharpness vs processing power. Multirate.
- Lesson 30 --- Correlation; sliding, multiplying, and summing; noise correlation is delta; efficient FFT; Barker codes
- Lesson 31 --- Chirps in radar and LoRa
- Lesson 35 --- MIMO Phased array of 2 antennas into a B210
- Lesson 36 --- Direction Finding; concepts and relative phase
- Lesson 37 --- MUSIC as a subspace method for direction finding
- Lesson 38 --- Error correction; Scrambler and interleaver; simple parity, CRC, FEC, Reed–Solomon, Viterbi decoder, Turbo codes, LDPC
- Lesson 39 --- Encryption
- Lesson 40 --- Whole system design
- Lesson 41 --- Sniffing to determine modulation and coding--autocorrelation and higher correlations
- Lesson 42 --- Radio astronomy: 21cm, solar, other easy things
- Lesson 43 --- Radio interferometer and the relationship between interferometry and beam forming
-->

# References

### Software Defined Radio (SDR) and Digital Communications Books:

- [Chaudhari; Wireless Communications from the Ground Up: An SDR Perspective](https://www.addall.com/New/NewCompare.cgi?isbn=9781729732236) -- The book I first used to understand tricky things like timing synchronization. Lots of pictures and intuition. Explains GNUradio blocks. I wish he wouldn’t avoid complex numbers, because it makes many things messy and opaque with lots of trig identities.
- [Rice; Digital Communications: A Discrete-Time Approach](https://www.amazon.com/Digital-Communications-Discrete-Time-Michael-Rice/dp/B08GVGCKCC) -- The second good book I read on this topic. A bit more mathy than Chaudhari, but great explanations. Introduces and uses complex notation. Many of my lessons are inspired by this book, including Symbol Timing Recovery and Carrier Phase Synchronization.
- [Collins et al; Software-Defined Radio for Engineers](https://www.analog.com/en/education/education-library/software-defined-radio-for-engineers.html) A free PDF from Analog Devices. Uses Pluto as an example, which is good, but isn’t always as well written as the above.
- [Proakis; Digital Communications 5th Edition](https://www.addall.com/New/NewCompare.cgi?isbn=0072957166) Advanced and very mathy; proves optimality under certain conditions; only book here to really talk about FSK, MSK, GMSK and code-division multiple access (CDMA) with pseudo-random streams.
- PySDR: A Guide to SDR and DSP using Python (online book) <https://pysdr.org/> Very good if you want to go to python directly without the live visual GNURadio flowgraphs.

### Digital Signal Processing DSP Books

This topic includes sampling, noise, FIR filters, correlation and convolution, quadrature (complex) signals, and all Fourier techniques DFT, FFT.

- [Smith; Scientist & Engineer's Guide to Digital Signal Processing](https://www.analog.com/en/education/education-library/scientist_engineers_guide.html#) -- online and in print. A very concrete start. My only criticism is that I wish he’d introduce complex numbers earlier.
- [Lyons; Understanding DSP](https://www.addall.com/New/NewCompare.cgi?isbn=0137027419) -- another good self-study book with lots of figures.
- [Oppenheim and Schafer; Discrete-Time Signal Processing](https://www.addall.com/New/NewCompare.cgi?isbn=0131988425) -- the standard textbook. Assumes more background and introduces mathy things like z-transforms too early, at least for our applications.
- Learning DSP Illustrated: <https://dspillustrations.com/> Lots of little python examples with plots. Confusing organization, popups, and ads.

### Global Satellite Navigation Systems (GNSS) and GPS Books:

- [Borre et al; A Software-Defined GPS and Galileo Receiver](https://www.ocf.berkeley.edu/~marsy/resources/gnss/A%20Software-Defined%20GPS%20and%20Galileo%20Receiver.pdf) -- where I started. Talks about acquisition through Fourier correlation and feedback-loop tracking.
- [Tsui; Fundamentals of GPS Receivers A Software Approach](https://www.addall.com/New/NewCompare.cgi?isbn=9780471706472) -- I think this is the second thing I read.


