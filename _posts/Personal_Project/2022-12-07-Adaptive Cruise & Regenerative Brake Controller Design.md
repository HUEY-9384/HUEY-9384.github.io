---
layout: post
title:  "Adaptive Cruise & Regenerative Brake Controller Design"
date:   2022-12-07 +0530
categories: Personal_Project
---
Here is the document converted to Markdown:

---

# AUTE 3500U - Team 5 Presentation

## Adaptive Cruise & Regenerative Brake Controller Design

**Course:** AUTE3500: Automotive Instrumentation & Controls Project  
**Instructor:** Dr. Xianke Lin  

**Team 5 Members:**  
- Jarif Khan (S1)  
- Hyungsuk Seo (S2)  
- Joshua Albert Lusabia (S3)  
- Garth Anthony Martin (S4)  

---

## Project Objective

Design, development, and construction of: 

- Vehicle dynamics model
- Cruise control system
- Regenerative braking system
- C-code from the controllers

---

## Concept Generation: Cruise Controller

- Ego car will drive at a desired speed with no lead car to reference  
  - **Desired speed (dsp)**

- If the lead car is present, the Ego car will try to maintain a desired distance and match the speed of the lead car  
  - **Lead car speed**  
  - **Desired relative distance**  

- Consider the error involved with relative distance between both vehicles  
  - **Error of relative distance**

---

## Concept Generation: Regenerative Braking Controller

*(Content for regenerative braking controller concept generation)*

---

## Vehicle Dynamic Model

**Vehicle Body Block:** Receives disturbance physical inputs and sends out physical signal outputs. Accounts for various vehicle & road parameters

**Inputs:** 
- Wind Velocity
- Road Incline
- H (mechanical output of the wheel hub assembly)

**Outputs:**
- NR (rear normal force)
- NF (front normal force) 
- V (velocity)

---

### Tesla Model S Standard Range

- Vehicle's total mass: 2135 Kg
- Horizontal distance from CG to front axle: 1.46 m
- Horizontal distance from CG to rear axle: 1.52 m
- CG Height above ground: 0.52 m
- Frontal area: 2.32 m²
- Air density: 1.202 kg/m³
- Drag coefficient: 0.3
- Coefficient of Road/Tire adhesion: 0.015
- Tire radius: 0.3 m
- Maximum torque: 600 Nm
- Maximum Power: 750 kW
- Motor and Drive efficiency: 100%

---

## Vehicle Dynamic Model (Ego Car) Specifications

### Motor System

**Ego Car (vehicle dynamic model) subsystem**

---

## Vehicle Dynamic Model (Lead Car)

**Lead car parameters:**
- No Vehicle Dynamic system
- Uses drive cycle source block (used to control lead car simulation)

**Outputs:**
- Lead car velocity (m/s)

**Initial conditions:**
- Position

---

## Controllers - Adaptive Cruise Control

**Inputs:**
- Lead car displacement
- Ego car displacement
- Desired speed
- Reaction time
- Cruise speed
- Current speed of ego car

**Outputs:**
- Desired Distance
- Acceleration
- Deceleration

**Initial conditions:**
- Set distance = 10 m
- Reaction time = 2 s
- Cruise speed = 30m/s

---

### Adaptive Cruise Control Main Subsystem

Subsystem contains the following minor subsystems:
- Distance sensor
- Speed decider
- Speed controller

---

### Adaptive Cruise Control Subsystem - Distance Sensor

**Inputs:**
- Lead car displacement
- Ego car displacement

**Outputs:**
- Relative Distance (RD)  
  *(rs = Lead car - ego car)* 
- Position difference

If the relative distance is greater than 100 m, the subsystem sends a value of -100 m to the position difference output.

---

### Adaptive Cruise Control Subsystem - Speed Decider

**Inputs:**
- Relative Distance (from displacement sensor)
- Desired displacement (set by Manufacturer)
- Reaction time
- Cruise speed (set by driver)
- Current speed

**Outputs:**
- Desired Speed

**Details:**
- Receives and validates the position difference between the lead car and the ego car.
- If the lead car is not within 100 m, the function will send a large number.

**Code:**

*(Code for the speed decider)*

**Equation:**

\[ ad = (\text{desired distance} + \text{current speed} \times \text{reaction time}) \]

Stopping distance (ad) is the projected distance that accounts for reaction time and current vehicle speed.

- Reaction Time = Current speed / Deceleration rate
- 1.5~2 seconds reaction time should be used
- Increasing reaction time will increase ad, but slow the overall response of the system
- Decreasing reaction time will lower the value of ad, which can lead to improper vehicle separation

---

### Adaptive Cruise Control Subsystem - Speed Decider

- Receives the desired distance and ad values
- Sends the lowest of the two input values as a base measurement for stopping distance

**Code:**

*(Additional code details)*

\[ \text{Error} = (\text{relative distance}) - ad \]  
\[ \text{Desired speed} = \frac{\text{Error}}{\text{reaction time}} \]

**Inputs:**
- Calculated Desired Speed
- Cruise speed

Sends the lowest of the two input values as a base measurement for the maximum vehicle speed.

Note: If the lead vehicle is beyond 100 m, the position difference derivative will also be large, automatically making ‘u’ > cruise speed.

---

### Adaptive Cruise Control Subsystem - Speed Controller

**Inputs:**
- Vehicle speed (from Speed decider)
- Current vehicle speed

**Outputs:**
- Acceleration
- Deceleration

**Vehicle Speed Error**

**Velocity Feed Forward Gain:**
Where: \( K = 0.001 \)

**PID controller:**
- Proportional gain value = 0.4
- Integral gain value = 0.001

Tuned using Transfer function based method (PID tuner app)

Note: dsp represents the vehicle speed (from Speed decider)

---

### Adaptive Cruise Control Subsystem - Speed Controller

**Feed forward gain:**
- Controls the sensitivity of the system to reduce disturbances
- A higher feedforward gain indicates that the output of the system is more responsive to changes in the input.
- A lower feedforward gain produces a less responsive and more stable system (Performance improvement)

Original K value  
Increased K value  
Reduced K value

**Throttle Delay Transfer Function:**
- Represents throttle dynamics
- Average value of the throttle delay is 0.5
- The transfer function block prevents algebraic loops and provides a more realistic simulation

**Saturation Function Block:**
- Continuously converts the input value
- The input signal is limited to the upper and lower saturation values of 1 and -1 respectively.
  - 1 represents 100% acceleration, and -1 represents 100% deceleration.

**Acceleration and Deceleration Function Blocks:**
- Both take the value given from the saturation function block.
- The value received represents the same decimal (%)
  - yacc output value is between 0~1
  - ydec output value is between -1~0

---

## Controllers - Regenerative Braking

**Inputs:**
- State of charge, SOC (%)
- Wheel Torque, WT (N*m)
- Brake signal, Brk
- Vehicle speed, spd (mph)

**Outputs:**
- Friction brakes (N*m)
- Regenerative brakes (N*m)

---

## Regenerative Brake System

- **Function #1**
- **Function #2**
- **Function #3**
- **Function #4**

### Function #1

**Code:**

```matlab
function [y,y2] = fcn(SOc,u)
if SOc>=0.85
    y=u;
    y2=0;
else
    y2=u;
    y=0;
end
```

### Function #2

**Code:**

```matlab
function [y,y2] = fcn(u)
if u<=600
    y=u;
    y2=0;
else
    y2=u;
    y=0;
end
```

### Function #3

**Code:**

```matlab
function [RB, FB] = fcn(u)
if u > 600
    RB = 600;
    FB = u-600;
else
    RB=0;
    FB=0;
end
```

### Function #4

**Code:**

```matlab
function y = fcn(u,spd)
if spd>0
    y = u;
else
    y=0;
end
```

---

### Friction Brakes

- Receives brake signal from friction brake output in regenerative braking block and applies to the wheel cylinder piston.
- Model uses double shoe brakes. (Drum brakes)
- Input directed from Wheel torque (N*m).

### Regenerative Brakes

- Receives brake signal from Regen brake output in regenerative braking block.
- Value subtracted from the throttle input for electric motor controller.
- Input directed from Wheel torque (N*m).

---

## Simulation

[Simulation Link](https://docs.google.com/file/d/1nbiJ_53HkKu7Zy_7XVbaOEz79rMBLNZX/preview)

---

## Results and Discussion: Cruise Controller

- Acceleration plot of the vehicle model shows varying values of acceleration over vehicle operation time.
- Deceleration plot of the vehicle model shows varying values of deceleration and braking over vehicle operation time.
- Relative distance of the vehicle model from the lead car over time.

---

### Results and Discussion: Cruise Controller

Vehicle velocity plot of the vehicle model and the lead car

---

### Results and Discussion: Cruise Controller

Vehicle displacement plot of the vehicle model and the lead car

---

## Results and Discussion: Regenerative Brakes



- Simulation data for regenerative brakes was generated using a step input.

### Regenerative Brake Outputs

- Braking system is capable of delivering maximum torque of 600 N*m.
- System can function with 0% SOC.
- System can function with 0 mph vehicle speed.

### Results and Discussion: Regenerative Brakes

Torque distribution is done only to one braking source when:

- State of charge > 85% (Brake Torque)
- Wheel torque < 600 N*m (Brake Torque)

Both torque sources function normally when these conditions are not met.

### Regenerative Brake System Outputs

- Input step was set at 750 N*m.  
  *(Value is based on our drive cycle control block)*

- Results show a maximum torque value of 600 N*m.  

- Torque distribution is done only to one braking source when:

  1. SOC > 85% 
  2. Wheel torque < 600 N*m

- The system functions normally when these conditions are not met.

---

## Conclusion

- Developed functional simulation of ACC and RBS using Simulink.
- Cruise control allows ego vehicle to follow a lead vehicle at a safe distance.
- Regenerative braking allows energy recovery while maintaining braking performance.
- Successfully generated C-code from controllers for ECU implementation.

---

## Future Work

- Implement control system on an actual vehicle for real-world testing.
- Refine control algorithms for improved performance and efficiency.
- Explore additional features like lane-keeping assistance.

---