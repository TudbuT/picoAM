# picoAM
A simple but capable AM transmitter for the Raspbery Pi pico!

## USE Arduino Mbed OS RP2040 Boards VERSION 3.x! 4.x+ is not currently compatible.

![Image of assembled circuit](https://media.discordapp.net/attachments/1077080199847489626/1102196399577247774/20230430_133433.jpg)
(image deviates slightly from current version of the circuit, apologies!)

## Disclaimer!!

The Pi is, to my knowledge, not able to output enough power to disrupt anything significantly as long as you're not near an airport (if you 
are, then it ABSOLUTELY IS), but with a long enough antenna, will get you in trouble and annoy others. Please use this only for experimental 
and educational purposes and do NOT use this in a way which might cause any disruption!

My antenna for this is barely large enough for half of my room to have reception. Please don't go much further than that!

**Also**, this project will overclock your pi. However, 200MHz is fine for 99.9% of picos and is SUPER unlikely to damage it unless you
leave it running for a very long time (days or something in a closed environment).

### Most important disclaimer

Legal restrictions likely aren't enough for some people to not do this. Including me actually (tho minisenders with low power like
this are actually allowed where i live, but they have to be certified). However, there is one **EXTREMELY** importatnt thing to add:

This uses square waves, so there are GOING to be harmonics. One of those is near 99.6MHz, in the FM band. You will hear the sender there 
as well in some cases as FM receivers *can usually* receive AM, its just gonna be really noisy. Your neighbors, sadly, might also hear it
there, as 99MHz FM is is in the FM radio bands. MAKE SURE YOUR ANTENNA IS SMALL!!!

There is also a MUCH STRONGER harmonic at ~155.726MHz FM, in the 2m amateur radio band. PLEASE, PLEASE, PLEASE don't use a large 
enough antenna for it to be able to send that very far. And this signal will actually reach FURTHER than the AM one because it 
is a shorter wavelength and therefore sends better using a short antenna. ***__PLEASE add the low pass filter I described.__***

## How it works

The Pi generates a 1557kHz PWM signal, which will be the carrier wave. The frequency is not changed, only the pulse width.
(Sadly, I was not able to make an FM version because FM would require more precise frequency shifts, which the pico just can't do.)
Then, an audio input is taken in on the right side of the breadboard (blue and green wire), which is clamped and slightly loaded 
so that we don't get nasty interference.
Then, this clean signal is given to the pico on pin 26. The pico does pulse width changes according to the signal, and outputs the 
AM signal on pin 15.

## Circuit Diagram and explanation

![Image of circuit diagram](https://user-images.githubusercontent.com/48156391/235515258-df6d10fa-90f5-4997-813d-1cf969dbf8a0.png)

The part which prepares the audio for the pico is not strictly needed, but if you use line inputs, you reeeally should have it.
It has the following jobs:
- D1 and D2 clamp the signal to acceptable voltages
- **An extra resistor of about 50-400 ohms may be added from the AI+ point to the AI- point to load the signal.** This is optional, but
  *can* clean up a little bit of noise if you have long cables.

**ERRATA :warning:**<br>
If you aren't an asshole, ***PLEASE*** add the low pass filter as mentioned in the Disclaimer:
- Add the 100ohm resistor (R3 in new schematic) between pico and antenna
- Wire a 2nF (2000pF) capacitor (C1 in new schematic) between the new start of the antenna and ground

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

## PCBs

I am currently doing DIY small-scale production of PCBs for this project. Costs per 4 PCBs is around 3€ + labor, and I'm selling them for 
1€ + shipping each (email me: pcb@mail.tudbut.de). The gerber and KiCad files will be uploaded here shortly as well if you want to make your own.

![first prototype](https://github.com/TudbuT/picoAM/assets/48156391/777238d4-18bf-4856-8728-9882879e48a9)
This is the first prototype. It was made using the Toner Transfer Method, but all future PCBs will be made using the professional dry film method,
so they will look much better. TTM is much cheaper however, and I will make you a PCB with it for 70 cents + shipping.

Image of a PCB made using the photographic process (not yet populated):
![second prototype](https://github.com/TudbuT/picoAM/assets/48156391/52075eeb-c9e0-4b73-842b-776b8e0631c0)
