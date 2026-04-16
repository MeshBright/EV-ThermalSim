# 🔋 EV ThermalSim: Advanced Battery Thermal Management Lab
![MATLAB](https://img.shields.io/badge/MATLAB-App%20Designer-blue.svg?logo=mathworks)
![Status](https://img.shields.io/badge/Status-Active_Development-brightgreen.svg)
![Version](https://img.shields.io/badge/Version-1.0.0-lightgrey.svg)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

> **A high-fidelity, full-stack mechatronics simulation environment for electric vehicle battery cooling.** EV ThermalSim goes beyond simple plotting. It is an interactive digital twin that models the physical latency, sensor mathematics, hardware constraints, and digital quantization of a real-world Electric Vehicle (EV) Thermal Management System (TMS).

---

## 📑 Table of Contents
1. [System Architecture & Features](#-system-architecture--features)
2. [Mathematical Models](#-mathematical-models)
3. [Recommended System Specifications](#-recommended-system-specifications)
4. [Installation & Usage](#-installation--usage)
5. [Collaboration Guidelines](#-collaboration-guidelines)

---

## 🚀 System Architecture & Features

This application bridges the gap between physical hardware and digital control by simulating four core mechatronic domains:

### 1. The Physical Plant (3D Animation Engine)
* **X-Ray Visualization:** Real-time 3D rendering of an EV chassis housing a vertically stacked array of 18650 Li-ion cells.
* **Thermal Color Mapping:** Battery cells dynamically shift from blue to red based on active thermal states.
* **Fluid Dynamics:** Particle animation engine runs on a 0.05-second timer, tracking fluid flow through a corrugated serpentine cooling ribbon.

### 2. Sensor Integration (NTC Thermistor)
Accurately maps the non-linear electrical response of an NTC thermistor inside a 5V voltage divider circuit, calculating dynamic sensitivity ($mV/°C$) based on the current operating point on the curve.

### 3. Actuator Constraints (BLDC Pump)
Models realistic mechanical limitations instead of ideal curves. Features a hardcoded **1.5V deadband** to simulate the initial starting torque required to overcome static friction and fluid inertia before flow begins.

### 4. Data Acquisition (DAQ) & Microcontroller Logic
Actively calculates how the digital controller "sees" physical changes by modeling ADC quantization errors.
| ADC Tier | Resolution | Typical Automotive Use Case |
| :--- | :--- | :--- |
| **10-bit** | Low | Standard Sensor Nodes |
| **12-bit** | Medium | Standard EV ECUs |
| **16-bit** | High | Advanced BMS Controllers |

---

## 🧮 Mathematical Models

The simulation engine is built on rigorous physical and electrical equations.

### NTC Thermistor (Steinhart-Hart Beta Model)
The resistance of the thermistor is calculated using the Beta parameter equation, assuming a base resistance of $10k\Omega$ at **25°C** and a $\beta$ value of **3950**:

$$R_{thermistor} = R_{25} \cdot e^{\beta \cdot \left(\frac{1}{T_K} - \frac{1}{298.15}\right)}$$

### Real-World Mechanical Latency & Decoupled Rendering
The system enforces a **0.8-second delay** on user inputs to simulate the real-world latency of a hydraulic system coming up to pressure. To prevent UI lockups, heavy 3D graphic updates are decoupled from the continuous knob states and only re-render when $\Delta > 0.1$.

### Adiabatic Cooling Loop
Once flow is established, the application dynamically applies an active cooling algorithm over time against a **25°C** coolant baseline:

$$\Delta T = -h \cdot \text{FlowRate} \cdot (T_{current} - T_{coolant})$$

*(Where $h$ is the simulated convection coefficient).*

---

## ⚙️ Installation & Usage

1. Clone the repository to your local machine:
   ```bash
   git clone [https://github.com/YourUsername/EV-ThermalSim.git](https://github.com/YourUsername/EV-ThermalSim.git)
