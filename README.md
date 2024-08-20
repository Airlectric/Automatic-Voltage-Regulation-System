# Automatic Voltage Regulator Circuit for Project P8

This project involves designing and developing a voltage regulator circuit to provide a power supply for Project P8. The circuit detects under-voltage and over-voltage conditions, controlling an LED and buzzer for low voltage conditions and cutting off power during high voltage conditions. The circuit uses operational amplifiers (op-amps), diodes, Zener diodes, resistors, capacitors, and NPN transistors.

## Table of Contents
1. [Components Used](#components-used)
2. [Circuit Description](#circuit-description)
   - [AC to DC Conversion](#ac-to-dc-conversion)
   - [Voltage Regulation](#voltage-regulation)
   - [Undervoltage Detection (4V Threshold)](#undervoltage-detection-4v-threshold)
   - [Overvoltage Detection (8V Threshold)](#overvoltage-detection-8v-threshold)
   - [Capacitor Functionality](#capacitor-functionality)
   - [Normal Operation](#normal-operation)
3. [Circuit Construction Steps](#circuit-construction-steps)
4. [Status Table](#status-table)
5. [Proteus Simulation Setup](#proteus-simulation-setup)
6. [Conclusion](#conclusion)

## Components Used
- **Transformer (TR1)**
- **Bridge Rectifier (BR1)**
- **Capacitors**:
  - C1: 10µF
  - C2: 10µF
  - C3: 10µF
  - C4: 2200µF
- **Resistors**:
  - R1: 1kΩ
  - R2: 1Ω
  - R3: 50Ω
  - R4: 50Ω
  - R5: 500Ω
  - R6: 1kΩ
  - R7: 2kΩ
  - R8: 1kΩ
- **Zener Diode**: 1N4735A (6.2V)
- **Diodes**:
  - D1: 1N4735A
  - D2, D3, D4: 1N4007
  - D5: LED (Green)
  - D6: LED (Red)
- **Operational Amplifiers**:
  - U1: LM358N
  - U2: LM358N
- **NPN Transistors**:
  - Q1: 2N2222
  - Q2: 2N2222
- **Relay**: 6V, 2P2S (RL1)
- **Buzzer**: 9V (BUZ1)
- **Voltage Regulator**: 9V Battery (B1)

## Circuit Description

### AC to DC Conversion

- **Transformer and Rectifier**: The AC input voltage is stepped down by the transformer (TR1) and rectified by the bridge rectifier (BR1) to produce a pulsating DC voltage.
- **Smoothing Capacitor**: A large capacitor (C4) with a value of 2200µF smooths the pulsating DC output. The ripple voltage \( V_r \) is calculated using:

To present the given equations and explanation in the right Markdown format for GitHub, you can follow this structure:

---

## Ripple Voltage Calculation

The ripple voltage (\(V_r\)) in a DC power supply can be calculated using the formula:

$$
V_r = \frac{I_{load}}{f \cdot C}
$$

Where:
- \(I_{load}\) is the load current,
- \(f\) is the frequency of the AC input, and
- \(C\) is the capacitance of the smoothing capacitor.

Given the following values:
- Load current (\(I_{load}\)) = 100 mA,
- Frequency (\(f\)) = 50 Hz, and
- Capacitance (\(C\)) = 2200 µF,

we substitute these values into the formula:

$$
V_r = \frac{0.1}{50 \cdot 2200} = \frac{0.1}{110000} = 0.0009 \text{ V} = 0.9 \text{ mV}
$$

This calculation shows that the ripple voltage is minimized to approximately 0.9 mV, ensuring a smooth DC output from the power supply.


### Voltage Regulation

- **Zener Diode**: A 6.2V Zener diode (D1) maintains a stable reference voltage across the load. 
- **Series Resistor (R1)**: Limits current through the Zener diode. The value of \( R1 \) is calculated as:



## Objective

The primary goal is to calculate the resistor values for voltage dividers that are part of the undervoltage (4V threshold) and overvoltage (8V threshold) detection systems within an AVR circuit. These systems are designed to operate with a nominal input voltage of 12V.

## Assumptions

- The circuit utilizes voltage dividers to scale down the input voltage to levels suitable for comparator inputs.
- The comparators are configured to trigger at predefined threshold voltages (4V for undervoltage and 8V for overvoltage).
- The input voltage to the voltage dividers is consistently 12V.

## Calculations

### Undervoltage Detection (4V Threshold)

The voltage divider for undervoltage detection should output 4V when the input is 12V. The formula for a voltage divider is given by:

$$
V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2}
$$

Given \(V_{out} = 4V\) and \(V_{in} = 12V\), we rearrange the formula to solve for \(R_1\):

$$
R_1 = R_2 \times \left(\frac{V_{in}}{V_{out}} - 1\right)
$$

Assuming \(R_2 = 1kΩ\) for simplicity, we calculate \(R_1\):

$$
R_1 = 1kΩ \times \left(\frac{12}{4} - 1\right) = 1kΩ \times 2 = 2kΩ
$$

Therefore, for undervoltage detection at a 4V threshold, \(R_1 = 2kΩ\) and \(R_2 = 1kΩ\).

### Overvoltage Detection (8V Threshold)

For overvoltage detection at 8V, we apply a similar approach. Using the same voltage divider formula and assuming \(R_2 = 1kΩ\) for consistency, we solve for \(R_1\):

$$
R_1 = R_2 \times \left(\frac{V_{in}}{V_{out}} - 1\right) = 1kΩ \times \left(\frac{12}{8} - 1\right) = 1kΩ \times 0.5 = 500Ω
$$

Hence, for overvoltage detection at an 8V threshold, \(R_1 = 500Ω\) and \(R_2 = 1kΩ\).

## Summary of Resistor Values

- **Undervoltage Detection (4V Threshold)**: \(R_1 = 2kΩ\), \(R_2 = 1kΩ\)
- **Overvoltage Detection (8V Threshold)**: \(R_1 = 500Ω\), \(R_2 = 1kΩ\)

These resistor values ensure the voltage dividers output the desired voltages at the comparator inputs, facilitating accurate detection based on the specified thresholds.



- **Op-Amp Comparator**: The inverting input of op-amp \( U1 \) is connected to the voltage divider output. The non-inverting input is connected to the 6.2V reference. When the input voltage exceeds 8V, the op-amp output goes low, turning off transistor \( Q1 \), deactivating the relay (RL1), and cutting off power.

### Capacitor Functionality

- **Capacitors \( C1 \), \( C2 \), and \( C3 \)**: These 10µF capacitors are used for decoupling and stabilizing op-amp circuits.

### Normal Operation

- **Green LED (D5)**: Indicates normal operation when the voltage is between 4V and 8V.

## Circuit Construction Steps

1. **Step-Down Transformer and Rectification**:
   - Connect the transformer \( TR1 \) to the AC mains and the rectifier \( BR1 \) to obtain a stable DC voltage using capacitor \( C4 \).

2. **Voltage Regulation**:
   - Connect the rectifier output to a series resistor \( R1 \) and Zener diode \( D1 \) to stabilize the voltage at 6.2V. Use capacitor \( C1 \) for additional filtering.

3. **Voltage Dividers**:
   - For undervoltage detection, connect \( R7 \) (2kΩ) and \( R8 \) (1kΩ) across the 12V DC output.
   - For overvoltage detection, connect \( R5 \) (500Ω) and \( R6 \) (1kΩ) across the 12V DC output.

4. **Op-Amp Comparators**:
   - Connect voltage dividers to op-amps \( U2 \) and \( U1 \) for undervoltage and overvoltage detection, respectively.

5. **Transistor and Relay Connections**:
   - Connect op-amp outputs to transistors \( Q1 \) and \( Q2 \) to control the relay and buzzer.

6. **LED Indicators**:
   - Connect LEDs to indicate normal operation and undervoltage conditions.

7. **Final Checks**:
   - Verify all connections and test

 the circuit on a breadboard or in Proteus before final implementation.

## Status Table

## Device Status Table

| AC Voltage (V) | DC Voltage (V) | Buzzer and LED Status | Device Status |
|---------------|---------------|------------------------|---------------|
| 230           | 11.9          | OFF                    | Disconnected  |
| 200           | 10.3          | OFF                    | Disconnected  |
| 170           | 9.29          | OFF                    | Disconnected  |
| 150           | 9.23          | OFF                    | Disconnected  |
| 150           | 8.57          | OFF                    | Connected     |
| 110           | 6.6           | OFF                    | Connected     |
| 90            | 5.22          | ON                     | Connected     |
| 85            | 4.85          | ON                     | Connected     |
| 80            | 4.51          | ON                     | Connected     |
| 70            | 3.8           | ON                     | Connected     |

This table provides a clear and concise overview of the system's behavior under different AC voltage conditions. The columns indicate the AC voltage, DC voltage, buzzer and LED status, and device connection status.


## Conclusion

## Proteus Simulation Setup

![Proteus Setup](images/setup.JPEG)  
*Figure 1: Proteus simulation setup for the voltage regulator circuit.*

## Conclusion

This circuit is designed to ensure the safe operation of Project P8 by detecting and responding to both undervoltage and overvoltage conditions. The README provides a detailed explanation of the circuit, calculations, and construction steps. This guide serves as a comprehensive resource for understanding and replicating the design.

