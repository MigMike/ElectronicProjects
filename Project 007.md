# Design and Operation of a Multi-Output Regulated DC Power Supply for Electronics Applications
## **Abstract**
This article presents the detailed design and operation of a regulated multi-output DC power supply, suitable for powering multiple electronics circuits simultaneously. The system is constructed from fundamental analog components and is powered from a standard 220V AC mains. It delivers four regulated outputs: 24V, 12V, 5V, and 3.3V, using a step-down transformer, bridge rectifier, filter capacitors, LM317T linear regulators, and a Zener diode. The circuit is practical for prototyping labs, embedded system development, and electronics education.

### **Introduction**
Most electronics circuits require stable DC voltage for reliable operation, yet the power grid provides AC mains (220V in many countries). Converting AC to suitable DC levels involves multiple well-understood stages: voltage transformation, rectification, filtering, and regulation.
 This article describes a complete, beginner-friendly design that:

* Converts 220V AC to low-voltage DC

* Offers multiple output voltages (24V, 12V, 5V, 3.3V)

* Uses discrete, linear regulators (LM317T) instead of digital modules

* Demonstrates foundational principles of power electronics

  ## **Multisim and Bench circuit diagram**
  ![alt text](<images/images S2/image-15.png>)
 ![alt text](<images/images S2/power sup. image.jpg>)
 
## **Transformer Stage – Voltage Step-Down**
#### **EI-76X45 Transformer (24-0-24V, 5A, 50Hz)**
The power supply begins with a center-tapped step-down transformer, model EI-76X45, which converts the dangerous 220Vrms AC mains into a much safer 24-0-24Vrms AC at 5A.

* Center tap provides a grounded midpoint, enabling full-wave rectification.
Delivers dual 24V outputs, peaking at ~34V after rectification.

**Why use a center-tapped transformer?**
It is ideal for full-wave rectification application and provides a symmetric ground reference.
### **Multisim simulation:** 
* Using Multisim or any other simulation software, you can run a test on an oscilloscope to check the output signal from each stage of the power supply ;

![alt text](<images/images S2/image.png>)
> In this case the 24Vrms V1 source is the transformer output.

## **Rectification Stage – AC to DC Conversion**
**Bridge Rectifier using HER307 Diodes**

A full-wave bridge rectifier is formed using four HER307 high-speed diodes (D1–D4). These diodes convert the 24-0-24V AC into pulsating DC with both halves of the waveform utilized.

*HER307 Specs:*
* 3A average forward current
* 1000V peak reverse voltage
* Fast recovery time (ideal for large capacitors)

The following link provides more details about HER307 diodes ; <https://www.alldatasheet.com/datasheet-pdf/pdf/842834/DSK/HER307.html>

 ### Peak DC Calculation
  **Formula:**
 V_peak= V_rms × √2

Each 24V AC output (RMS) converts to a peak voltage of:

𝑉_
peak=
24
𝑉
×
√2
≈
33.9
𝑉

Accounting for two diode drops (~1.4V), the DC level after rectification is:

𝑉
DC
≈
33.9
𝑉
−
1.4
𝑉
≈
32.5
𝑉

### Multisim simulation:
The diagram shows the output signal on the oscilloscope after the voltage is rectified ;

![alt text](<images/images S2/Multisim OSC. rectifier Dis..png>)

## **Filtering Stage – Ripple Reduction**
 **Bulk Filter Capacitor (C1 = 4700µF, 50V)**

A large electrolytic capacitor (4700µF) smooths the pulsating DC output from the rectifier, reducing ripple and preparing the voltage for stable regulation.
* The larger the capacitance, the lower the ripple under load.
* Voltage rating (50V) provides ample margin over the 32.5V DC input.

 **Additional Filtering**

Smaller capacitors (100µF, 33µF) are added after each regulator to improve load response and suppress noise.
### Multisim simulation 
  ![alt text](<images/images S2/image-14.png>)
  - From the simulation , it can be determined that the output voltage after filtering still has ripples . That's why we need an Input capacitor at the beginning of regulation.
  
## **Voltage Regulation Stage – LM317T Adjustable Regulators**
#### Introduction to LM317T
The LM317T is a 3-terminal adjustable voltage regulator capable of supplying 1.2V to 37V at up to 1.5A. It maintains output voltage regardless of load current or input voltage (within limits).
For more details, I have provided a link ; {[https://www.alldatasheet.com/datasheet-pdf/pdf/441393/ISC/LM317T.html]}


𝑉
out=
1.25
𝑉
(
1
+
𝑅
2/
𝑅
1
)
 
Where:

- 𝑅
1
  and 
R 
2
​ 
   are feedback resistors

- Output voltage depends only on their ratio

 **First Regulator (U1) – 24V Output**

R1 = 1kΩ, R2 = 18.2kΩ

𝑉
out1=
1.25
(
1
+
18.2
𝑘/
1
𝑘
)
≈
24
𝑉

* This output is ideal for high-power modules such as motor drivers, relays, or analog audio amps.

C3 (300µF) and C5 (33µF) stabilize the output

  *Ensure LM317 has a large heat sink for 24V output* 

 **Second Regulator (U2) – 12V Output**

R1 = 1kΩ, R2 = 8.6kΩ

𝑉
out2=
1.25
(
1
+
8.6
𝑘/
1
𝑘
)
≈
12
𝑉

*Used for powering:*

* Logic circuits (TTL/CMOS)
* Op-amps
* Audio preamps
* Development boards (e.g., Arduino Uno)

 **Third Regulator (U3) – 5V Output**

R1 = 240Ω, R2 = 720Ω

𝑉
out3=
1.25
(
1
+
720R/
240R
)=
5
𝑉

*Suitable for:*

* Microcontrollers (e.g., ESP32, ATmega)
* Digital sensors
* USB-powered devices

 **Final Stage – 3.3V Zener Clamping**

 *Zener Diode (1N4728A)*

After the 5V output, a Zener diode (D5) is used to clamp the voltage to 3.3V. The 1N4728A is a 3.3V, 1W Zener that conducts when the voltage exceeds 3.3V, maintaining a fixed reference level.

> A series resistor (10Ω) limits current into the Zener.
 
*The clamped output is suitable for:*

* 3.3V microcontrollers (e.g., ESP8266)
* Low-voltage digital sensors

>> Note: Zener diodes are not efficient regulators for high current. This clamping is best used for low-current reference or logic circuits.

## **Thermal and Safety Considerations**
* Heat Sinks: Each LM317 must be mounted on a proper heat sink. For example, dropping from 32V to 5V at 1A = 27W of heat!
* Ventilation: Enclose the power supply in a well-ventilated metal or ABS box.
* Fuses: Add fuses or PTC resettable fuses after transformer output for overcurrent protection.
* Isolation: Ensure transformer provides safe electrical isolation from mains.

### Final Thoughts and Applications
This power supply is:

✅ Ideal for a lab or educational setting.

✅ Simple to build from readily available components.

✅ Offers multiple voltages in one compact unit

***Suitable For:***

* Prototyping microcontroller-based circuits
* Simultaneous powering of 5V/12V modules
* Audio circuits requiring 24V rails
* Logic level shifting or analog reference generation

## Conclusion
This detailed guide demonstrates how to design a robust, linear, multi-output DC power supply using:

* A 24-0-24V transformer
* HER307 diodes for high-speed full-wave rectification
* LM317T adjustable regulators to output 24V, 12V, and 5V
* A 3.3V Zener diode for low-current logic-level output

Each stage was explained step-by-step to teach the underlying principles and design considerations. This approach is ideal for beginners looking to build a power supply from scratch while learning core concepts of analog power electronics.

### Resources:
1. https://www.alldatasheet.com/datasheet-pdf/pdf/441393/ISC/LM317T.html
2. https://www.alldatasheet.com/datasheet-pdf/download/15025/PHILIPS/1N4728A.html 
3. https://www.alldatasheet.com/datasheet-pdf/pdf/842834/DSK/HER307.html