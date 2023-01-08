# Pulsed Laser Driver
## Introduction
A good friend of mine was talking about his work at the Solid State Physics lab at TU Berlin. They are currently trying to build upon the work of Japanese researchers regarding UVC lasers. These lasers need short, sharp (that was an English adjective, in EE speak it's "fast rise time") current pulses to be properly evaluated. With The Art of Electronics: The X Chapters on my side, I decided to take this project up, and boy, was it worth it. 
## Project Motivation
Apparently pulsed laser drivers cost upwards of several tens of thousands of Euros, so being able to come up with a a solution (that will probably be orders of magnitude cheaper) would be a much welcome break to the Lab's budget. Since the requirements were not particularly challenging (~250V, 5A, 1us pulses), I decided it would be feasible to try making a pulsed current sink.
## Usage
### Specifications [temp: as promised]:
- 25ns rise/fall times
- 5A peak current
- 250V diode voltage
[under construction]
## List of Files
- Resources: Infographics
- Hardware: KiCAD PCB files
- Software:
  - Simulation: LTspice .asc file, libraries
## Application Examples
[under construction]
## Notes
- Laser diodes usually with several volts across them. Since this UVC laser is under on-wafer testing, the methods of supplying power to the die involve high-resistance contacts: needles on pads, hence the need for high voltages.
- The choice of LT1193 was arbitrary - there are op-amps available that are better suited to the task, but I wanted an excuse to use the LT1193 because of its unique inputs which enable it to Kelvin-sense the input signal and feedback from the shunt. 
- Infographic highlighting the effect of changes in element values in the compensation network (this would probably be more intuitive in the frequency domain):
![Infographic](https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/compensation.png)
- Rist time measurements in LTspice of initial simulation:
![Infographic](https://github.com/NNNILabs/Pulsed-Laser-Driver/blob/main/Resources/risetime.PNG)
## Links
- https://x.artofelectronics.net/
- https://www.analog.com/media/en/technical-documentation/data-sheets/1193fb.pdf
- https://www.analog.com/media/en/technical-documentation/application-notes/an133f.pdf
