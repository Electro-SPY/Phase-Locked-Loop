# Charge Pump Phase-Locked-Loop 
 This project aims to successfully implement a Charge-Pump Based PLL (CP-PLL) circuit and compare the effects of different Voltage Controlled Oscillators (VCO)s on the performance of PLL considering the following parameters: Power consumption, phase noise, gain linearity and jitter.Implementation of a PLL requires the design of various blocks which are as follows: Phase Detector, Charge Pump, Loop filter, VCO and Frequency Divider Circuit.  Industry grade VLSI tools and technologies will be used in this project to implement different blocks on circuit level. The following specifications are required to be achieved using 90 nm CMOS technology:  Total power budget in the range of 300uW-350uw tuning range of 800 MHz-3 GHz, jitter less than 25 ps.


## Table of Contents

- [Specifications](#Specs)
- [Tools Used](#Tools)

- [What is a PLL?](#PLL)
- [Components](#C)
  - [Phase Frequency Detector](#PFD)
  - [Charge Pump](#CP)
  - [Voltage Controlled Oscillator](#VCO)
  - [Frequency Divider](#FD)
  
  
- [Schematics](#SC)
  - [Phase Frequency Detector](#PFDS)
  - [Charge Pump](#CPS)
  - [Voltage Controlled Oscillator](#VCOS)  
  - [Complete PLL](#PLLS)

- [Output Waveforms](#OW)
  - [Transient Response](#TR)
  - [Steady State Response](#SSR)
  - [Output Frequency](#OF)
 
 

## Specifications<a name="Specs"></a>

| Parameter | Value|
| --- | --- |
| VDD | 1.8 v | 
| Frequency Range | 1 GHz - 3 GHz |
| Duty Cycle | 50% | 
| Jitter | <25ps | 
| Locking Time | < 5us | 
| Corner | TT | 
| Temperature | Room Temperature | 
 
## Tools Used<a name="Tools"></a>
Cadence Virtuoso was used for this project. GPDK90 technology node was used to implements all the blocks of the PLL.

 
## What is a PLL?<a name="PLL"></a>
<p align="center">
<img src="https://user-images.githubusercontent.com/52507285/128868622-397353d8-e0e4-4d50-b569-9f88f0444a02.png"> 
 </p>
PLL is a feedback system which synchronises the output oscillations of the VCO to that of the reference (Generally Crystal Oscillator). It does so by minimizing the rate of change of phase error between the two oscillators. 
The phase detector compares the phase error between the two oscillators and convert it into a voltage proportional to it. This voltage is further fed to a Low pass filter (Charge Pump + Loop filter in our case) which averages it out and send it to the VCO’s control input. The VCO changes its output frequency in accordance to it, thus in turn minimizing the phase error. This process goes on iteratively till the frequencies of the two oscillators are matched.
If we want to obtain a multiple of reference frequency, A divide by N circuit is placed in the feedback loop. If we do so the output will be N* ωref.

## Components : <a name ="C"></a>
## Phase Frequency Detector <a name="PFD"></a>
<p align="center">
<image src="https://user-images.githubusercontent.com/52507285/128626154-bce9e137-2a93-470b-8910-c69dab8568e2.png" height=300 width=300> 
 </p>
 The Phase Frequency Detector is a simple circuitry that detects the difference between the reference and VCO output phase\frequency.The output of a phase frequency detector is a signal which represents the phase\frequency difference of the reference and VCO output signal.This signal is further used by the consecutive circuitry to produce an average value which is fed to the VCO to control the output frequency. 
  
## Charge Pump<a name="CP"></a>
  
 <p align="center">
<image height =300 src="https://user-images.githubusercontent.com/52507285/128626531-83103737-00d3-4636-98ba-53a13df8714b.png"> 
  </p>
  A charge Pump is a circuit that injects or pulls out a charge for a controlled amount of time. In the CP-PLL it is placed after the PFD and before the loop filter. The combined effect of all the three elements is to produce a voltage that is proportional to the phase error between the VCO’s output and the reference. Charge pump along with the loop filter averages out the voltage given out of the PFD thus creating the control voltage for the VCO. The charge pump is basically a combination of two current sources and two switches that switches the sources. We have implemented Gate Switched Charge Pump in our project.
  
## Voltage Controlled Oscillator<a name="VCO"></a>
  <p align="center">
<image height=200 width=600 src="https://user-images.githubusercontent.com/52507285/128626847-866a5951-aa29-40ac-aa82-aac50f4bd622.png"> 
  </p>
  The frequency of oscillation of an output signal can be tuned by varying a parameter electronically within the oscillator, e.g., a resistance, a capacitance, or an inductance. If the control is a voltage quantity, we call the circuit a voltage-controlled oscillator (VCO). A voltage-controlled oscillator is an electronic oscillator whose oscillation frequency is proportional to input voltage as shown in the following equation:
 

The tuning characteristic of a VCO is ideally a straight line. 
With the help of a phase detector and charge pump, we have successfully generated a control voltage that is proportional to the phase difference between the reference voltage signal and output voltage signal. Therefore, if we feed this control voltage to a VCO, we will be able to synchronize frequencies of both signals, thus tune our output signal to the reference signal.
In a ring oscillator, operating frequency is inversely proportional to the propagation delay (t) and number of inverters (n) as shown in the following equation,

<p align="center"> f=  1/2nt <p>

For our phase-locked loop, the topology that we have selected is a voltage-controlled ring oscillator as shown in the following schematic. In this topology, the delay of PMOS and NMOS will be regulated by controlling the voltage supply fed to each inverter in the loop. The internal circuitry of a CMOS based inverter consists of a PMOS and NMOS transistor used as pull-up and pull-down resistor.  The other four inverters in cascade including a self-biased inverter are used in waveshaping of the generated waveform of the tuned frequency.
  
## Frequency divider <a name="FD"></a> 
  <p align="center">
<image height=150 width=400 src="https://user-images.githubusercontent.com/52507285/128627145-342416fb-e428-4931-9c64-89a44fd42066.png"> 
  </p>
  <p align="center">ωout=ωin/N</p>
A frequency divider, also called a clock divider is a circuit that takes an input signal of a frequency, fin, and generates an output signal of a frequency: fin/n where n is an integer
Phase-locked loop frequency synthesizers make use of frequency dividers to generate a frequency that is a multiple of a reference frequency. 
A feedback divider is used to divide the VCO frequency with a factor to bring it back to the range of reference frequency to compute phase error. This enables us to lock different ranges of frequencies, just by changing the factor with which VCO frequency is divided. Till now we have implemented it using verilog A.


## Schematics<a name="SC"></a>
#### Phase Frequency Detector<a name="PFDS"></a>
 <p align="center">
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128868976-c45c191c-1adb-46ee-891a-a54f7e6487d5.png">
 </p>
  
#### Charge Pump <a name="CPS"></a>
 
  <p align="center">
   <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869198-b483e781-a97d-4827-8040-796afcb8fabd.png">
   </p>  
   
#### Voltage Controlled Oscillator<a name="VCOS"></a>  
   
<p align="center">
<image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869213-5bbfe418-b8ff-450e-a4a7-a34190ea794d.png">
 </p>
      
#### NOR Gate
      
  <p align="center">     
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869240-f36e32dd-a7d4-456a-ba61-36259d27c998.png">
  </p>
   
#### NAND Gate
   
   <p align="center">
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869253-6dc5c211-c9f5-41c5-9fff-20eab5b4f886.png">
  </p>
    
#### Inverter
    
   <p align="center">
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869272-77730eda-9832-4c33-8e64-8bc9a054bddf.png">
  </p>
    
#### CP-PLL<a name="PLLS"></a>
    
   <p align="center">
 <image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128869295-c4f624ad-7cdb-410d-85d9-a43dad381ecb.png">
  </p>
    
### Outputs Waveforms <a name="OW"></a>
    
#### Transient Response<a name="TR"></a>
<p align="center">
<image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627606-4c7494fb-0853-48b8-901f-1fff2ed0bac5.png">
 </p>
 
 #### Steady State Response<a name="SSR"></a>
 <p align="center">
<image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627622-0a02e95c-ec3b-4045-bafb-d0f6704d15e8.png">
 </p>
  
  #### Output Frequency <a name="OF"></a>
 <p align="center">
<image height=400 width=800 src="https://user-images.githubusercontent.com/52507285/128627500-8d57fca4-51b4-44d6-8729-949ce20fe848.png">
 </p>   

  
  

   

