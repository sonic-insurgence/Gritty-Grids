# Gritty Grids - An Improved MIDI Implementation for Grids
Grids is a topographic (drum) sequencer for Eurorack modular synthesizers 
developed by Mutable Instruments.

If you use a setup that is primarily based on MIDI you might want to 
synchronize Grids to your MIDI master clock.
The stock firmware of Grids offers only rudimentary support for a MIDI 
interface. It resets the drum engine when it receives a MIDI Start message 
and uses MIDI Clock messages to advance. However it does not care about 
MIDI Stop or MIDI Continue messages. If, after pressing stop on your 
MIDI master device, the master does not cease sending MIDI Clocks 
(a behaviour quite a few MIDI devices exhibit) Grids will go on 
drumming forever.

The "Gritty Grids" firmware improves on this situation by properly 
reacting to all MIDI Start, Stop, Continue and Clock messages. See 
the [Gritty Grids demo video](https://youtu.be/vbTWLX3Ts00) on YouTube.

### A MIDI Interface for Grids
Fortunately Grids offers three pads on the back of its printed circuit 
board that are waiting to become a MIDI IN interface.

![Grids MIDI port](/images/grids-midi-port.jpg)

Just connect the following simple circuit. It can easily be built on a 
prototyping board.

![MIDI circuit](/images/midi-circuit.jpg)

As a quick hack you might even succeed if you only take a 5-pin female 
DIN jack making the following connections:
* pin 2 (shield / ground) to Grids GND
* pin 5 (current sink) to Grids RX>

But beware: This is a hack. It DOES NOT COMPLY with the specification 
of the MIDI standard. You lose the galvanic isolation of the MIDI 
interface. It might or might not work. Try at your own risk.


### Flashing the Firmware
Just use the in-system programmer of your choice (e. g. I use the 
AVRisp MkII from Atmel) to flash the "gritty-grids.hex" file to 
the AVR microcontroller on Grids. If you are not familiar with 
flashing AVR controllers search the web for instructions.

If you want to go back to the original stock firmware flash 
"grids_original.hex".


### User Manual
Enter the external clocking mode of Grids by turning the tempo knop to 
its minimum position. After receiving a  MIDI Start or MIDI Continue 
message Grids switches into a "clocked_by_midi" mode. In this mode its 
drum engine advances with every MIDI clock message. External clocking 
via the clock input jack is disabled.

Receiving a MIDI Start message resets the Grids drum engine whereas 
MIDI continue resumes from the current state.

As an external reset in "clocked_by_midi" mode or a tapped-in tempo 
would break the synchronization with the MIDI master device the 
function of the reset input as well as the TAP/reset button changes. 
They now assume a "mute" functionality that suppresses all drum and 
accent outputs. When muted all three output leds will light up 
permanently.

To leave the "clocked_by_midi" mode, turn the tempo knob to the right 
to activate internal clocking.

Besides the MIDI stuff I also disabled retriggering of the outputs 
when a signal at the reset input has been received. This avoids 
the annoying double triggers.


### Syncing other modules
If you have a sequencer module in your rack you might want to set the 
outputs configuration of Grids to ACC / CLK / RST. This gives you a 
clock and reset output which you can use to sync the sequencer to 
Grids and thereby to your MIDI master device.


### Website
Original Grids website: https://mutable-instruments.net/modules/grids/


### Author
* Author of the original Grids project is Émilie Gillet.
* Author of the Gritty Grids modification is Sonic Insurgence.


### License
This program is free software: you can redistribute it and/or modify 
it under the terms of the GNU General Public License as published by 
the Free Software Foundation, either version 3 of the License, or 
(at your option) any later version.


### Acknowledgments
Original Grids design by Émilie Gillet from Mutable Instruments. 
Many thanks for making it open source!

