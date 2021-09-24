# Lesson 9 --- Transmit and Receive from a PlutoSDR

In this project you will use a software-defined radio to send and receive a sine wave signal with frequency in the kHz range using a carrier frequency of 2.4 GHz. Besides **QT GUI Range sliders**, **QT GUI Time Sinks**, and **QT GUI Frequency Sinks**, the blocks you'll need are a **Signal Source**, **PlutoSDR Sink**, and **PlutoSDR Source**.

1. Screw in the two antennas to the Pluto's Tx and Rx ports, taking care not to damage the central pin of the SMA connectors. A good technique is to hold the antenna steady with one hand and gently rotate the screw until tight with the other hand.
2. The signal source should put out a complex cosine wave with an adjustable frequency tied to a range slider. Connect it to a time sink to visualize its output and also to the PlutoSDR sink, which will combine that signal with the carrier wave and broadcast it through the TX antenna. Label the traces in the time sink with **TX** or **transmit** so we can distinguish them from the received signal. See the parameter table below for the values to use in the PlutoSDR sink.
3. The PlutoSDR source needs to operate at the same frequency as the sink. Connect the PlutoSDR Source to a time sink and a frequency sink. Label the time sink traces with **RX** or **receive**.


## Equipment

- Analog devices ADALM-PLUTO software-defined radio ![Analog devices ADALM-PLUTO software-defined radio](figs/ADALM-Pluto.jpg)



## Parameters

| Parameter            | Value or Range               |
| ----------------     | --------------:              |
| sample rate          | 2.084MS/s                    |
| tone frequency range | -100 kHz to 100 kHz          |
| RX gain              | 0 to 70 with a default of 64 |
| RX gain mode         | manual                       |
| Pluto LO frequency   | 2.4 GHz                      |
| TX attenuation       | 10 dB                        |





[Lesson 8 flow diagram](figs/lesson08-pluto.png)

## Things to explore

- How does the orientation of the two antennas affect the strength of the received signal?
- If you place your hand near the Pluto, does it change the observed frequency signal?