# DigitalVoltmeter_EmbeddedC

DIGITAL VOLTMETER AND AMMETER USING PIC18F6520

**Project Overview:**
This project implements a Digital Voltmeter and Ammeter using a PIC18F6520 microcontroller and a 16×2 LCD display. The system measures the analog voltage across a resistor on a burn-in driver card and calculates the corresponding current. The measured voltage and current values are displayed on the LCD in real-time.

**System Description:**
The microcontroller uses its 10-bit Analog-to-Digital Converter (ADC) module to convert the analog input voltage to a corresponding digital value. This value is then processed to calculate voltage and current using the formula:

voltage = ((ADRESH × 256) + ADRESL) × 0.00488

current = voltage / R (where R = 560 Ω)

**Hardware Used:**

-PIC18F6520 Microcontroller

-16×2 LCD Display

-Burn-in Driver Card

-Resistor (560 Ω)

-Power Supply (5V)

**A/D Conversion Procedure:**

1. Configure the A/D Module:
   
  a. Configure analog pins, voltage reference, and digital I/O via ADCON1
  
  b. Select the A/D input channel through ADCON0
  
  c. Set the A/D conversion clock using ADCON2
  
  d. Turn on the A/D module via ADCON0

2. Configure A/D Interrupt (optional):

  a. Clear the ADIF bit
  
  b. Set the ADIE bit
  
  c. Enable the global interrupt using GIE

3. Wait for the required acquisition time.

4. Start Conversion:

  a. Set the GO/DONE bit in ADCON0 to begin the conversion

5. Wait for Conversion to Complete:

  a. Poll for the GO/DONE bit to clear, or
  
  b. Wait for the A/D interrupt

6. Read the Conversion Result:

  a. Store the 10-bit result from ADRESH and ADRESL into variables 'reghigh' and 'reglow'

7. Calculate Voltage and Current:
  
  a. voltage = ((reghigh × 256) + reglow) × 0.00488
  
  b. current = voltage / 560

8. Repeat Steps as Needed:
  
  A minimum delay of 2× TAD is required before starting the next acquisition.

**Display Output:**

The 16×2 LCD displays the measured Current (A) and Voltage (V) in the following format:

   CURRENT=0.123A

   VOLTAGE=5.000V
   
**Project Files:**

1. main.c — Source code for ADC configuration, calculation, and LCD display

2. lcd1.h — Header file for LCD interfacing functions

3. config_bits.c — Microcontroller configuration bits

**Notes:**

-Ensure that the microcontroller clock is set to 8 MHz.

-Make sure the LCD connections and control lines match the configuration in lcd1.h.

-The system can be extended to support multiple analog input channels or averaged readings for display stability.
