# Pulsed Laser Driver

<p align="center">
    <img src="https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/Output.png">
</p>

<p align="center">
    <b>Power uncorrupted.</b> -J. Williams
</p>

<p align="center">
[Placeholder for a hopefully impressive scope capture]
</p>

## Introduction
A good friend of mine was talking about his work at the Solid State Physics lab at TU Berlin. They are currently trying to build upon the work of Japanese researchers regarding UVC lasers. These lasers need short, sharp (that was an English adjective, in EE speak it's "fast rise time") current pulses to be properly evaluated. With The Art of Electronics: The X Chapters by my side, I decided to take this project up, and boy, was it worth it. 
## Project Motivation
Apparently pulsed laser drivers cost upwards of several tens of thousands of Euros, so being able to come up with a a solution (that will probably be orders of magnitude cheaper) would be a much welcome break to the Lab's budget. Since the requirements were not particularly challenging (~250V, 5A, 1us pulses), I decided it would be feasible to try making a pulsed current sink.
## Usage
### Specifications [temp: as promised]:
- 25ns rise/fall times
- 5A peak current
- 250V diode voltage
## List of Files
- Resources: 
  - Infographics
- Hardware: 
  - KiCAD PCB files
- Software:
  - Simulation: LTspice .asc file, libraries
## Application Examples
[under construction]
## Notes
- Laser diodes usually with several volts across them. Since this UVC laser is under on-wafer testing, the methods of supplying power to the die involve high-resistance contacts: needles on pads, hence the need for high voltages.
- The choice of LT1193 was arbitrary - there are op-amps available that are better suited to the task, but I wanted an excuse to use the LT1193 because of its unique inputs which enable it to Kelvin-sense the input signal and feedback from the shunt. 
- Rise time measurements in LTspice of initial simulation using an AO6408 (10nH, 10pF parasitics):

<p align="center">
    <img src="https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/risetime.PNG">
</p>

- Rise time measurement with GaN FET (GS66502) (10nH, 10pF parasitics):

<p align="center">
    <img src="https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/risetime2.png">
</p>

- GaN FETs which feature input, output and feedback capacitances that are at least an order of magnitude smaller than their regular silicon counterparts, are ideal for this application. Because of the low input capacitance (and the fact that the input capacitance is bootstrapped by Gm x source shunt resistor), the driving op-amp sees a significantly reduced capacitive load. On resistance and threshold voltage is comparable to a regular small switching MOSFET, but the drain-source breakdown voltage is significantly higher, almost touching 1kV. Of course, regular MOSFETs (or even a cascode to get the best of both worlds - easy drive with lots of transconductance and high-voltage drive capability) can be used with appropriate compensation "for the sake of a challenge", but GaN FETs save a lot of blood, sweat and tears.
- I decided to try using a smaller shunt resistor so the op-amp wouldn't have to swing as much to drive the gate and shunt voltage. This should theoretically increase bandwidth and therefore speed, but it did the opposite. One theory is that the threshold voltage of the MOSFET is much higher than the shunt voltage, so a smaller shunt voltage would mean a larger difference between it and gate threshold, so larger swing to get the same result. But a higher shunt voltage also means higher overall op-amp output, which should have a slowing effect. The answer can be found in AoE X - a higher shunt resistance means a higher bootstrapping voltage across gate-source capacitance through FET transconductance. 

<p align="center">
    <img src="https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/risetime3.PNG">
</p>

## Links
- https://x.artofelectronics.net/
  - pg. 193 3x.5 "MOSFETs as Linear Transistors"
  - pg. 206 3x.7 "Bandwidth of the Cascode; BJT versus FET"
  - pg. 386 4x.26 "Nodal Loop Analysis: MOSFET Current Source"
- https://www.analog.com/media/en/technical-documentation/data-sheets/1193fb.pdf
- https://www.analog.com/media/en/technical-documentation/application-notes/an133f.pdf
- https://gansystems.com/wp-content/uploads/2022/07/GS-065-008-1-L-DS-Rev-220712.pdf
