# Lesson 12 --- Phase-Shift Keying (PSK)

Last time, we used a vector of values to modulate the amplitude of the carrier wave, which allowed us to send symbols which could contain more information than a single bit. In **binary phase-shift keying** (BPSK) we multiply the carrier wave either by 1 or -1. It is common to associate the amplitude of 1 with the binary value 0 and the amplitude of -1 to the binary value 1, which has a simple mapping to the binary XOR operator.

<!-- [ ![video](figs/video/PSK-video.jpg)](https://youtu.be/EHQcuFuQA5w){:target="_blank"}  -->

<iframe width="560" height="315" src="https://www.youtube.com/embed/EHQcuFuQA5w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Start with your flow graph from the previous lesson, save a copy with the name BPSK, and then work on the following modifications.

As before, we will use a **Vector Source** to supply a string of values, only this time our input will be a string of binary digits in a pattern that we will repeat over and over. You can pick whatever pattern you like, but it is helpful to pick something that you can readily recognize in the output [e.g., (0,1,0,1,0,0,1,1,1,1)].

To convert this list of symbols into the values 1 and --1 that we will use to encode, use the **Chunks to Symbols** block and provide the values `(1,-1)` as the symbol table.


Because the Pluto and RTL-SDR clocks differ, the received constellation spins. In this lesson we cancel the frequency difference by hand with the `offset` slider (keep its range small, a few kHz, so the slider has enough resolution). Even so the two points slowly rotate, and we cannot tell which is "1" and which is "--1". The next lessons fix this properly with a frequency-locked loop (Lesson 17), a timing-recovery loop (Lesson 18), and a Costas loop (Lesson 19).



## Homework

1. Square the incoming signal to adjust the slider and zero out the frequency difference. 






<!-- flowgraphs:begin -->
## Flowgraphs

[`lesson12_PSK_Pluto_to_RTL_SDR.grc`](https://github.com/gallicchio/learnSDR/blob/main/lesson12_PSK_Pluto_to_RTL_SDR.grc)

[![lesson12_PSK_Pluto_to_RTL_SDR flowgraph](figs/flow/lesson12_PSK_Pluto_to_RTL_SDR.png)](figs/flow/lesson12_PSK_Pluto_to_RTL_SDR.png){:target="_blank"}

Running:

[![lesson12_PSK_Pluto_to_RTL_SDR running](figs/run/lesson12_PSK_Pluto_to_RTL_SDR.png)](figs/run/lesson12_PSK_Pluto_to_RTL_SDR.png){:target="_blank"}
<!-- flowgraphs:end -->

All GNURadio flowgraphs are at [https://github.com/gallicchio/learnSDR](https://github.com/gallicchio/learnSDR)


