# Lesson 11 --- Amplitude-Shift Keying (ASK) from Pluto to SDR

- modulate the amplitude of the complex wave
- 


`tx_attenuation` 0--89, 10
`samp_rate` 1 MS/s
`center_freq` 915 MHz
`rx_gain` 0--70, 10

transmit a bunch of constants and let the 
vector: (0.0, 1.0/3.0, 2.0/3.0, 1.0) and repeat
repeat: 100 times, `sps`

What is a symbol? a more general version of a bit. Now, we have 4 symbols, instead of the two we have when we think of data as binary digits (bits). With four levels, we can transmit two bits per sample. Multiplies the cosine at 915 MHz times the amplitude coming from the repeated vector source.
Look at the received signal strength in a constellation plot.
Nice view of saturation.

Just decode by taking complex-to-magnitude.

Keeping only one in 100 is not the best way to extract the information. We want to maximize the information we can transmit per bandwidth.
Square pulses are pretty inefficient.

Homework:
For high transmitter attenuation and low signal gain, how can....
