# Lesson 10 --- Tx from Pluto, Rx on RTL-SDR

Things to watch for: difference in clock rates and sample rates between devices

Pay attention to the colored background of parameters. If the background is green, the value has to be an integer. If you run into problems, just surround the expression you have with `int()`.

Variables: center_freq

The RTL-SDR can go lower. See [allocations of the ultrahigh frequency band](https://en.wikipedia.org/wiki/Ultra_high_frequency). 902 to 928 MHz is the ISM band (industrial, scientific, and medical).


## Equipment

- Analog devices ADALM-PLUTO software-defined radio ![Analog devices ADALM-PLUTO software-defined radio](figs/ADALM-Pluto.jpg)
- RTL-SDR, ![blah](figs/RTL-SDR.png)

## Directions




## Parameters

| Parameter            | Value or Range               |
| ----------------     | --------------:              |
| sample rate          | 1 MS/s                       |
| tone frequency range | -1 kHz to 1 kHz, default 500 |
| Rx gain              | 0 to 70, default 64          |
| Rx gain mode         | manual                       |
| Pluto LO frequency   | 915 MHz                      |
| Tx attenuation       | 0 to 100, default TBD        |
| audio gain           | 0 to 100, default 50         |


## Filter properties

| Parameter                 | Value or Range          |
| -----------------         | ----------------------: |
| LPF decimation            | 50                      |
| LPF cutoff frequency      | 2 * tone                |
| LPF transition width      | 250 Hz                  |
| LPF window                | Hamming                 |
| BRF low cutoff frequency  | tone - 5 Hz             |
| BRF high cutoff frequency | tone + 5 Hz             |
| BRF transition width      | 5 Hz                    |
| BRF window                | Hamming                 |


[Lesson 10 flow diagram](figs/lesson10-flowdiagram.png)

## Things to explore

Note: *Depending on your hardware, you may find that displaying all the plots causes errors. You may find that disabling ones that arise earlier in the chain that you are not observing frees up enough computing power to avoid the errors.*

1. Can you hear the chirped sound from your computer's sound card when you move your hand rapidly towards or away from the PlutoSDR? What you hear probably lags behind the motion of your hand, since the PlutoSDR needs to send a lot of data over the USB to the computer for processing and filtering before it can be sent to the audio card.

2. In principle, you should be able to hear the shift over a range of tone frequencies. Play around a bit and figure out what frequency produces the best audio signal.

3. How does the LPF cutoff frequency affect the performance of your radio? Do you get a clearer signal with a smaller transition width on the BRF?

4. Is it easier to hear the Doppler shifted frequencies, or see them in the frequency output of the BRF?

