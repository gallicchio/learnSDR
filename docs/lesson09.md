# Lesson 9 --- Pluto Doppler RADAR

When a radio wave bounces off a moving target, its frequency shifts. This shift is called the *Doppler effect*. Our goal in this project is to build a flow diagram in GNU Radio that will transmit a pure tone in the audible range, and then receive the shifted waves that have bounced from a hand or other object that is moved towards or away from the antenna.

For speeds that are small compared to the speed of light $$c$$, the frequency of a wave that reflects from a surface moving at speed $$v$$ toward the transmitter is
\begin{equation}
  f_{\rm Rx} = f_{\rm Tx} \times \left(1+\frac{2 v}{c} \right)
\end{equation}
The frequency shift for a 3.5 GHz carrier wave for a speed of 3 m/s would be
\begin{equation}
  \Delta f = 2\frac{3~\mathrm{m/s}}{3 \times 10^8~\mathrm{m/s}} (3.5 \times 10^9~\mathrm{Hz}) = 70~\mathrm{Hz}
\end{equation}
so we ought to be able to hear this shift, provided that we can block out the much stronger unshifted signal that goes straight from the transmit antenna to the receive antenna. We'll use a narrow band reject filter to do that. Finally, we will convert the complex output to a real signal and send it to an audio sink, which will allow us to hear the shifted tone.


## Equipment

- Analog devices ADALM-PLUTO software-defined radio ![Analog devices ADALM-PLUTO software-defined radio](figs/ADALM-Pluto.jpg)

## Directions

1. Audio cards typically have a maximum sampling rate of 48 kHz. We will design the SDR to sample at a multiple of this frequency, so that we can down-sample the output of the radio to produce an output at 48 kHz. Set the `samp_rate` to 2.4 MS/s so that when you decimate by a factor of 50, you get 48 kHz.

2. Set up four **QT GUI Range**s: `tone_freq`, `tx_gain`, `rx_gain`, and `audio_gain`. Defaults and ranges are shown in the tables below.

3. Set up a **Signal Source** to generate a cosine at `tone_freq`. Remember that when the source is set to generate a complex output, the cosine really means $$e^{i \, 2\pi f t}$$. Connect it to a **PlutoSDR Sink** and also display the output with a **QT GUI Time Sink**. You'll need to configure the PlutoSDR to use the right local oscillator frequency and link to the `tx_gain` slider. Make sure to label the traces in the time sink, since you will have many plots.

4. Add a **PlutoSDR Source** to receive the signal, display the output in the usual way, and also send the output to a **Low Pass Filter** (LPF), which will roll off frequencies above 1 kHz and reduce the sample rate to the desired 48 kHz.

5. Before sending the output of the LPF to an **Audio Sink**, we need to strip out the strong peak at `tone_freq`. Set up a **Band Reject Filter** (BRF), and then use a **Multiply Constant** block tied to `audio_gain` to boost the signal before sending it into the **Audio Sink**.


## Parameters

| Parameter            | Value or Range               |
| ----------------     | --------------:              |
| sample rate          | 2.4 MS/s                     |
| tone frequency range | -1 kHz to 1 kHz, default 500 |
| Rx gain              | 0 to 70, default 64          |
| Rx gain mode         | manual                       |
| Pluto LO frequency   | 3.5 GHz                      |
| Tx gain              | 0 to 100, default 40         |
| Tx attenuation       | 10 dB                        |
| audio gain           | 0 to 100, default 50         |


## Filter properties

| Parameter                 | Value or Range          |
| -----------------         | ----------------------: |
| LPF decimation            | 50                      |
| LPF cutoff frequency      | 1 kHz                   |
| LPF transition width      | 250 Hz                  |
| LPF window                | Hamming                 |
| BRF low cutoff frequency  | tone - 5 Hz             |
| BRF high cutoff frequency | tone + 5 Hz             |
| BRF window                | Hamming                 |





[Lesson 9 flow diagram](figs/lesson09-flowdiagram.png)

## Things to explore

- How does the orientation of the two antennas affect the strength of the received signal?
- If you place your hand near the Pluto, does it change the observed frequency signal?