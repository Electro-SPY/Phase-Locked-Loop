# Charge Pump Phase-Locked-Loop
<p align="center">
<img src="https://user-images.githubusercontent.com/52507285/128625641-990a2fc1-f01e-475d-8135-c5de70467646.png"> 
 </p>
 
It is an exciting way to explore different aspects of our stream Electronics and Communication like control system analysis, modelling and testing of circuits in analog and digital electronics. It can resolve various design problems such as jitter reduction, skew suppression, frequency synthesis and clock recovery. This project aims to successfully implement a Charge-Pump Based PLL (CP-PLL) circuit and compare the effects of different Voltage Controlled Oscillators (VCO)s on the performance of PLL considering the following parameters: Power consumption, phase noise, gain linearity and jitter.Implementation of a PLL requires the design of various blocks which are as follows: Phase Detector, Charge Pump, Loop filter, VCO and Frequency Divider Circuit.  Industry grade VLSI tools and technologies will be used in this project to implement different blocks on circuit level. The following specifications are required to be achieved using 180 nm CMOS technology:  Total power budget in the range of 20 mW-40 mW, tuning range of 500 MHz-1 GHz, jitter less than 25 ps.
## Phase Frequency Detector
<p align="center">
<image src="https://user-images.githubusercontent.com/52507285/128626154-bce9e137-2a93-470b-8910-c69dab8568e2.png" height=300 width=300> <image src="https://user-images.githubusercontent.com/52507285/128626205-cb53306a-5dfd-40a9-bdce-89a9b6f2c777.png" height=300>
 </p>
 We wish to have our PLL lock despite the initial output frequency. A phase detector does not give a meaningful output when the frequency difference between the reference and output is quite large. A frequency detector might seem the immediate solution but again due to finite gain and offset, the convergence of the output frequency to input frequency is denied.  
To overcome the problems of the phase detector and frequency detector we employ a circuit know as a Phase Frequency Detector. The working of Phase Frequency Detector is simple as it works as both a frequency and phase detector. So, when the frequency difference is quite large it works as a frequency detector and brings the output frequency close enough to the reference frequency. From there it works as a phase detector and ensures the convergence of the output frequency to the reference frequency.
  
## Charge Pump
  
 <p align="center">
<image height =300 src="https://user-images.githubusercontent.com/52507285/128626531-83103737-00d3-4636-98ba-53a13df8714b.png"> <image height =300 src="https://user-images.githubusercontent.com/52507285/128626549-5af05c3b-3ae7-4f95-acd8-14fe0c3b7c84.png">
  </p>
  A charge Pump is a circuit that injects or pulls out a charge for a controlled amount of time. In the CP-PLL it is placed after the PFD and before the loop filter. The combined effect of all the three elements is to produce a voltage that is proportional to the phase error between the VCO’s output and the reference. Charge pump along with the loop filter averages out the voltage given out of the PFD thus creating the control voltage for the VCO. The charge pump is basically a combination of two current sources and two switches that switches the sources. We have implemented Gate Switched Charge Pump in our project.
  
## Voltage Controlled Oscillator
  <p align="center">
<image height=200 width=600 src="https://user-images.githubusercontent.com/52507285/128626847-866a5951-aa29-40ac-aa82-aac50f4bd622.png"> <image height =200 width=600 src="https://user-images.githubusercontent.com/52507285/128626896-20c7dec3-bebd-44e7-b92b-8edb5b0ac306.png">
  </p>
  The frequency of oscillation of an output signal can be tuned by varying a parameter electronically within the oscillator, e.g., a resistance, a capacitance, or an inductance. If the control is a voltage quantity, we call the circuit a voltage-controlled oscillator (VCO). A voltage-controlled oscillator is an electronic oscillator whose oscillation frequency is proportional to input voltage as shown in the following equation:
 

The tuning characteristic of a VCO is ideally a straight line. 
With the help of a phase detector and charge pump, we have successfully generated a control voltage that is proportional to the phase difference between the reference voltage signal and output voltage signal. Therefore, if we feed this control voltage to a VCO, we will be able to synchronize frequencies of both signals, thus tune our output signal to the reference signal.
In a ring oscillator, operating frequency is inversely proportional to the propagation delay (t) and number of inverters (n) as shown in the following equation,

<p align="center"> f=  1/2nt <p>

For our phase-locked loop, the topology that we have selected is a voltage-controlled ring oscillator as shown in the following schematic. In this topology, the delay of PMOS and NMOS will be regulated by controlling the voltage supply fed to each inverter in the loop. The internal circuitry of a CMOS based inverter consists of a PMOS and NMOS transistor used as pull-up and pull-down resistor.  The other four inverters in cascade including a self-biased inverter are used in waveshaping of the generated waveform of the tuned frequency.
  
## Frequency divider  
  <p align="center">
<image height=150 width=400 src="https://user-images.githubusercontent.com/52507285/128627145-342416fb-e428-4931-9c64-89a44fd42066.png"> 
  </p>
  <p align="center">ωout=ωin/N</p>
A frequency divider, also called a clock divider is a circuit that takes an input signal of a frequency, fin, and generates an output signal of a frequency: fin/n where n is an integer
Phase-locked loop frequency synthesizers make use of frequency dividers to generate a frequency that is a multiple of a reference frequency. 
A feedback divider is used to divide the VCO frequency with a factor to bring it back to the range of reference frequency to compute phase error. This enables us to lock different ranges of frequencies, just by changing the factor with which VCO frequency is divided. Till now we have implemented it using verilog A.

## Outputs
 <p align="center">
<image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627606-4c7494fb-0853-48b8-901f-1fff2ed0bac5.png">
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627622-0a02e95c-ec3b-4045-bafb-d0f6704d15e8.png">
  <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627500-8d57fca4-51b4-44d6-8729-949ce20fe848.png">
   </p>


  
  

   

