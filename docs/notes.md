

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



Carrier Phase Synchronization with a Costas Loop

By end of today, we have all the tools:
timing synchronizations
carrier phase synchronization

No matter how good your clocks, you have to deal with frequency offsets and phase offsets

Simplified diagram from last time 

Symbol Sync block using a polyphase filterbank, MF
Now we look at the Costas loop
clocks matched to something like a part per billion

How does the Costas loop do its thing producing (at least for BPSK) to a purely real?

1. If we knew theta, we could "derotate" by ze^{-i\theta}
2. If we can estimate θ, we can drive it to zero with a control loop

data: z = x + iy = e^{i\phi}
a = a_I + i a_Q = e^{i \phi_a}

$$z a^* = e^{i(\phi - \phi_a)} $$
$$\theta = \arg(z)$$

For small values of θ, we can use the small-angle approximation. We're going to use $$\theta \approx \Im(z a^*)$$.

Costas loop needs to know the number of constellation points

constellation.arity() gives the order

----------

Resolving phase ambiguity and differential encoding

Two techniques to handle.
1. send a unique word with a lot of transitions; Costas loop will lock. Then ask did I get the right sign (BPSK) or the right one of 4 phases (QPSK).
2. Differential encoding

for BPSK, start in some state. To send 0, stay in the state. To send a 1, switch states.
**
