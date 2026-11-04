<h1 align="center">
    <br>
    <b>3-Axis Seismometer Based on MMA7361L and MCP6002 for Low Frequency Seismic Wave Acquisition</b>
    <br>
</h1>

<p align="center">
    Seismometer, either known as Geophone, is a device that could detect and record the signal of seismic wave.
    The mechanism behind it relies on the mechanical part that moved because of the vibration which later converted into electrical signal.
    Seismometer could have a wide range frequency detection, but usually it's just around 1 Hz up to 40 Hz with high sensitivity.
    The downside of Seismometer is it could only detect in 1-axis at a single time and it's expensive.
    Here is the thing, imagine if you want to build 3-axis seismic wave detection system for monitoring purpose, but not only in one place, it need to be build at several places at a same time like in an active volcanic mountain.
    <br>
    Thus, this project aims to make a seismic wave detector that could detect 3-axis simultaneously (from 0.1 - 100 Hz) and come in a small single board PCB. Its based on MMA7361L (capacitive MEMS Accelerometer) and MCP6002 (single-supply op-amp). Small, low-cost, reliable, and easy enough to make. 
    This could be a breakthrough for any vibration monitoring/detection related activities.
    </br>
</p>

---
## Table of Contents
- [Schematic](#schematic)
- [PCB Final Product](#pcb-final-product)
- [Testing](#testing)
- [Performance Analysis](#performance-analysis)
- [Conclusion](#conclusion)
- [Recommendation for Future Improvements](#recommendation-for-future-improvements)
---

## Schematic
This 3-Axis Seismometer was built based on integrator circuit using op-amp.
It's actually a low-pass filter but have a significant slope value for the frequency response plot, it's -20dB/decade. 
In addition, the circuit will also shift the signal wave phase at 90 degrees from its original phase.
With this slope value and phase shift, the acceleration wave could be converted into a proportionally velocity wave.
But, in order to do that, the signal need to past the cut-off frequency value to get the integration to work.

<div align="center">
    <img src="https://github.com/Satriyo-Wibowo/3-Axis-Seismometer/blob/main/documentation/schematic.png">
</div>

## PCB Final Product
Both schematic and PCB was designed with EasyEDA, as it's a same corporation as JLCPCB.
PCB layout was heavily optimized to be as small as possible and better noise reduction, resulting in 5x5 cm board.
The optimizations including separation of power and analog area, via stitching, and accelerometer ideal placement.

<div align="center">
    <img src="https://github.com/Satriyo-Wibowo/3-Axis-Seismometer/blob/main/documentation/PCB_product.jpeg">
</div>

> [!Note]
> Why the board red? coz it's cool. Why there is a witcher symbol in the board? coz I like the game.

## Testing
The test phase is done by placing the seismometer at the top of a subwoofer.
It will mimic the vibration of seismic wave with spesific value of frequency.
A power supply circuit and vibration exciter is needed to energize the subwoofer.
Beside of that, the board still needed to tested with a vibration that contain random range of frequency.
To do that, we can place the board at a flat surface such as table an give it a manual vibration.
The output signal could be recorded by Picoscope and it's dedicated software at laptop.

<div align="center">
    <img src="https://github.com/Satriyo-Wibowo/3-Axis-Seismometer/blob/main/documentation/testing_environment.jpg">
</div>

## Performance Analysis
The data from testing phase then added into a Python-based code to produce gain (frequency response) and phase plot for later analyzation.
The gain plot shows that the circuit start to integrating the input signal at 1 Hz.
But, when it comes to mid-high frequency range, the circuit start to significantly attenuating the signal.
This could be caused by limitation of the components.
<div align="center">
    <img src="https://github.com/Satriyo-Wibowo/3-Axis-Seismometer/blob/main/documentation/gain_output.png">
</div>

The phase plot shows that the output signal have a tendency to keep phase shift at 90 degrees.
<div align="center">
    <img src="https://github.com/Satriyo-Wibowo/3-Axis-Seismometer/blob/main/documentation/phase_output.png">
</div>

## Conclusion
Although the bigger aims of this project have achieved successfully, which are make a Seismometer that could detect 3-axis simultaneously,
the board is small enough, cost less than the Geophone, and easy to make, but the board still come with some big flaws.
The integration process just work at limited frequency range, around 1 Hz to 40-ish Hz.
The noise reduction also not near like what it's expected to be, a lot of noise at the lower and higher frequency range.
But this project could be one step closer to a reliable 3-axis Seismometer.

## Recommendation For Future Improvements
The fact that the components I was used are not in a good condition, like the accelerometer or the op-amp 
(it have refurbished several times, CRAZY!, I know) due to fund limitation, 
I think this also plays a big role in not-good-enough performance of the Seismometer.
I do also think that grounding method of the board is not good enough. 
The area of the analog and power sure is separated by the components placement, 
but the ground plane is still connected in a single plane,
not in separated plane then connected by a via like star grounding method.
This could led to a loop ground phenomenon and worsening the EMI effect. 
The via stitching only helped for the signal to have a shorter return to the ground pad.