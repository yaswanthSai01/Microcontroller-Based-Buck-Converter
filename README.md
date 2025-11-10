# Design-and-Implementation-of-a-Microcontroller-Based-Buck-Converter

This project presents the **design, simulation, and hardware implementation** of a **DC-DC Buck Converter** controlled by an **AT89C52 (8051) microcontroller**.  
The system takes a high-voltage AC input, rectifies it to DC, and efficiently **steps down** the voltage to a **regulated DC output**.

The **output voltage (Vₒ)** is directly controlled by the **duty cycle (D)** of the PWM signal, following the fundamental buck converter relationship:

\[
V_o = D \times V_{in}
\]

---

## 🧱 Circuit Design

The circuit is divided into **four main functional blocks**:

### 1. AC-DC Power Supply
- AC input is passed through a **step-down transformer (TR1)** and a **full-bridge rectifier (D1–D4)** to obtain an unregulated DC output.  
- **Filter capacitors (C1, C2)** smooth out the ripples in the rectified voltage.

### 2. Control Logic Power Supply
- A **7815 voltage regulator (U2)** converts the unregulated DC into a **stable +15 V rail** for the control ICs (microcontroller and gate driver).

### 3. PWM Generation (AT89C52)
- The **AT89C52 (8051)** microcontroller generates a **Pulse Width Modulated (PWM)** signal using timer interrupts.  
- The PWM duty cycle determines the buck converter’s output voltage.

### 4. Driver & Buck Power Stage
- The PWM output from the 8051 is fed into an **IR2110 high/low-side MOSFET driver (U3)**, which provides high-speed, high-voltage gate signals.  
- The **IRF250 MOSFET (Q1)** acts as the main switching device, paired with:
  - **Freewheeling diode (D5)**
  - **Inductor (L1)**
  - **Output capacitor (C4)**
- Together, these components form the **buck converter** stage, filtering the pulsating DC into a smooth, lower-level DC output.

---

## 🔩 Key Components

| Component | Description | Function |
|------------|--------------|-----------|
| **AT89C52 (8051)** | 8-bit microcontroller | PWM generation |
| **IR2110** | High/low-side MOSFET driver | Drives MOSFET gate |
| **IRF250** | N-channel MOSFET | Main switching element |
| **7815 Regulator** | Linear voltage regulator | Provides +15 V for control section |
| **1N4007 Diodes (D1–D4)** | Bridge rectifier | AC to DC conversion |
| **L1, C4** | Inductor and capacitor | LC filter for output smoothing |

---

## 🧮 Working Principle

1. **Rectification:** AC input is rectified to DC using a bridge rectifier.
2. **Regulation:** The +15 V rail powers control and driver circuits.
3. **PWM Control:** The 8051 generates a PWM signal whose duty cycle controls the buck output.
4. **Switching & Filtering:** The IRF250 MOSFET switches the DC input at high frequency; the LC filter smooths the output voltage.

---

## 📐 Schematic

> ![Schematic Diagram](circuit%20diagram.png)

---

## 🧪 Results

### 🧰 Simulation
- The circuit was first simulated to verify correct switching operation, gate driver functionality, and the relationship between **Vout** and **PWM duty cycle**.
- Waveforms show:
  - PWM signal from the 8051  
  - MOSFET gate voltage (from IR2110)  
  - Buck output voltage (Vout)  
 
> ![Simulation Results](output%20waveforms.png)

### ⚙️ Hardware Implementation
- A prototype was built and tested on a hardware setup.
- Measured results validated the expected buck converter behavior — **Vout increased linearly with duty cycle**.
- The +15 V regulator and gate driver stages operated stably under varying load conditions.


> ![Hardware Setup](Hardware_Imp.png)

---

## 🧾 Observations

- The buck converter successfully demonstrated step-down operation from an unregulated DC input.  
- Hardware results closely matched simulation outputs.  
- The system is scalable for use in **regulated DC supplies**, **battery chargers**, and **motor control applications**.

---

## 🧠 Key Learnings

- PWM generation using **8051 timers**  
- Interfacing **IR2110 gate driver** with microcontroller logic  
- DC-DC buck converter design and component selection 
