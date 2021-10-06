

They have 
What they are missing: stuff aiming up. From the perspective overhead.


Pulse Shapes — Constellation Modulator

sps = 16

parameters to the root raised cosine filter
sample rate
symbol rate
alpha
num taps: 11 * sps (is popular)


constellation.airity

Frequency locked loops (FLL)

automate the slider that adjusts the offset

The received spectrum isn't centered around zero.
I want the spectrum that is centered around zero.

Do a band-edge filter on the spectrum
offers balance metaphor
turns on and then falls offers

You can create an entire filter in the time domain.
Take incoming data stream, pass through filter, 
Smooth error signal, and then nudge the 

AGC = automatic gain control
rate 100u
reference 1
gain 1
max gain 65.536k

FLL Band-edge
  needs samples per symbol
  the filter rolloff factor (alpha)
  prototype filter size sps * 2 + 1
  loop bandwidth: 2*math.pi / sps / 100

Need a shift that is 

How do you actually form a filter in the time domain to get that response.
There are some nice mathematical forms of the humps. 


Lesson 18 Symbol Timing Synchronization (clock recovery)

error signal is the data times the slope or sign(x) x-dot

For this to work, you need to have transitions. 
y[n] y'[n] maximum likelihood
sps
expected TED gain 1.0
loop bandwidth 0.045
damping factor 1.0
maximum deviation 1.5
output samples/symbol 1
interpolating resampler: polyphase filterbank, matched filter
nfilts (number of filters) 
rcc_taps

RRC Filter Taps
gain: nfilts
sample rate nfilts*samp_rate
symbol rate: samp_rate/sps
Excess BW: alpha
num taps: 11*sps*nfilts [spans 11 symbols]
