# picoAM
A simple but capable AM transmitter for the Raspbery Pi pico!

![Image of assembled circuit](https://media.discordapp.net/attachments/1077080199847489626/1102196399577247774/20230430_133433.jpg)

## Disclaimer!!

The Pi is not able to output enough power to disrupt anything significantly, but with a long enough antenna, will get you in 
trouble and annoy othere. Please use this only for experimental purposes and do NOT use this in a way which might cause any disruption!

My antenna for this is barely large enough for half of my room to have reception. Please don't go much further than that!

## How it works

The Pi generates a 1557kHz PWM signal, which will be the carrier wave. The frequency is not changed, only the pulse width.
(Sadly, I was not able to make an FM version because FM would require more precise frequency shifts, which the pico just can't do.)
Then, an audio input is taken in on the right side of the breadboard (blue and green wire), which is clamped and slightly loaded 
so that we don't get nasty interference.
Then, this clean signal is given to the pico on pin 26. The pico does pulse width changes according to the signal, and outputs the 
AM signal on pin 15.

## Circuit Diagram and explanation

![Image of circuit diagram](https://media.discordapp.net/attachments/1077080199847489626/1102203487363792956/SmartSelect_20230430_140248_Flexcil.jpg)

The part which prepares the audio for the pico is not strictly needed, but if you use line inputs, you reeeally should have it.
It has the following jobs:
- R2 and R3 try to pull AI- a between the two voltages to be able to record the whole signal in case it is not a grounded one (not needed,
  it can also just be connected to ground. this is basically just extra fanciness with nonzero but very small benefit.)
- R1 makes sure there isn't too much strain put on the input
- D1 and D2 clamp the signal to acceptable voltages
- **An extra resistor of about 50-100 ohms may be added from the AI+ point to the AI- point to load the signal.** This is optional, but
  *can* clean up a little bit of noise if you have long cables.

## How to use it

- Flash the ino file using the Arduino IDE
- Cut open an audio cable and take one of the channels and the ground out of the cable's mantle
- Connect those to jumper wires
- Take a breadboard and put the pico on there, wire the circuit
- Add the audio inputs
- Add a **sufficiently long but not too long** antenna. Mine is about 2m-ish long.
- Connect the Pi to your PC using the USB port for power
- Connect the audio input to your PC
- Tune in to 1557kHz AM
