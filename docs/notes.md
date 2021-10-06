

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

FLL Band-edge
  needs samples per symbol
  the filter rolloff factor (alpha)
  prototype filter size sps * 2 + 1
  loop bandwidth: 2*math.pi / sps / 100

Need a shift that is 

How do you actually form a filter in the time domain to get that response.
There are some nice mathematical forms of the humps. 


Lesson 18


