# Power Electronics and Integrated Circuit Control (PEIC) 

---

## 📝 Homework 1: Buck Converter Fundamentals & Simulation

### Objective
Establish core foundations in DC-DC power conversion by analyzing both a non-ideal Boost converter in Continuous/Discontinuous Conduction Modes (CCM/DCM) and a Buck converter operating near its critical boundary.

### Key Tasks
* **Theoretical Analytical Analysis:** * Sketched output voltage ($V_o$) waveforms for a Boost converter factoring in both capacitor Equivalent Series Resistance (ESR) and Equivalent Series Inductance (ESL) to investigate edge spikes.
    * Derived the mathematical voltage gain expression for a DCM Boost converter as a function of duty cycle ($D$) and load resistance ($R$).
* **Critical Boundary Calculations:**
    * Analyzed a steady-state Buck converter ($V_g = 10\text{ V}$, $V_o = 0.5\text{ V}$, Diode $D_1$ forward voltage $V_F = 0.5\text{ V}$, $L = 10\mu\text{H}$, $C = 100\mu\text{F}$, $f_s = 2\text{ MHz}$).
    * Derived the critical resistance boundary ($R_{crit}$) governing the CCM/DCM transition.
    * Calculated precise peak-to-valley values for $V_o$, inductor current ($i_L$), capacitor current ($i_C$), switching node voltage ($SW$), and the adjusted operating duty cycle ($D$) under a heavy load condition ($R = 0.1 \times R_{crit}$).
* **Circuit Simulation Verification:**
    * Constructed and simulated the power stage in LTspice / SIMPLIS to extract steady-state waveforms.
    * Annotated calculated versus simulated peak/valley parameters to evaluate cross-domain validation and highlighted non-ideal structural offsets.
### Documentation
📄 Refer to:  
- [`doc`](./HW/hw1/PEIC-HW1%20-%202026.pdf)

---

## 📝 Homework 2: Synchronous Power Stage & Driver Circuit Design

### Key Tasks
* **Equivalent Model & Efficiency Derivations:**
    * Formulated exact expressions for the internal equivalent output resistance ($R_o$) and overall power efficiency ($\eta$) of an open-loop synchronous buck converter ($F_{sw} = 6\text{ MHz}$, $V_{in} = 1.8\text{ V}$, $V_o = 0.9\text{ V}$, Inductor $L_s = 120\text{ nH}$ with $r_L = 100\text{ m}\Omega$).
    * Substituted transistor design targets ($R_{dson} = 100\text{ m}\Omega$, $C_{iss} = 14\text{ pF}$, $C_{oss} = 7\text{ pF}$) to quantify conduction vs. switching loss trade-offs.
* **Smart Driver Implementation:**
    * Designed a functional gate driver block to independently drive high-side ($M_P$) and low-side ($M_N$) switches.
    * Implemented adaptive **Dead-Time Control** to safely suppress shoot-through currents.
    * Integrated a **Zero Current Detection (ZCD)** block to force tri-state discontinuous operation when $i_L$ attempts to reverse polarity under light loads.
* **Advanced Parameter Analysis:**
    * Investigated why full-load converter efficiency drops off dramatically (dominated by $I_o^2 R_{eq}$ losses).
    * Calculated maximum quiescent current ($I_q$) budgets for an AIoT system PMIC demanding $\ge 85\%$ efficiency at a micro-power load ($I_o = 0.1\text{ mA}$).
### Documentation
📄 Refer to:  
- [`doc`](./HW/hw1/PEIC-HW2%20-%202026.pdf)

---

## 📝 Homework 3: Closed-Loop Voltage-Mode Control & Compensation

### Key Tasks
* **Control Theory & Architecture Mapping:**
    * Mapped negative feedback loop criteria for pulse-width modulators (PWM), confirming steady-state control voltage ($V_c$) limits and comparator input node polarities.
    * Contrasted multiple control laws including Peak Current Mode, Valley Control, Constant Off-Time, Hysteretic, and Constant ON-Time (COT) modulations.
* **Compensator Loop Design:**
    * Designed an automated Type-III (or advanced Type-I) compensation network tailored to a buck converter with customized circuit elements ($V_g = 10\text{ V}$, $V_{out} = 5\text{ V}$, $V_{ref} = 1\text{ V}$, $R = 1\ \Omega$, external ramp $V_M = 1\text{ V}$ to $5\text{ V}$).
    * Utilized **Impedance Asymptote Plots** in the log-frequency (dB) axis to rapidly estimate and place compensator poles ($p$) and zeros ($z$) to counteract the power stage's double-pole resonance.
* **Performance Metrics Exploration:**
    * Simulated uncompensated vs. compensated open-loop gains to optimize closed-loop bandwidth ($f_c$) and phase margin ($PM$).
    * Quantified **Line Regulation** capability by injecting a $100\text{ mV}$ sinusoidal perturbation at $1\text{ kHz}$ onto $V_g$, measuring audio-susceptibility dampening before and after closing the control loop.
### Documentation
📄 Refer to:  
- [`doc`](./HW/hw1/PEIC-HW3%20-%202026.pdf)

---

## 📝 Homework 4: Transistor-Level Error Amplifier Design

### Key Tasks
* **Behavioral Parameter Constraints (Level 2 Model):**
    * Established real-world macro-model parameters for the amplifier (finite DC Open-Loop Gain $A_{v0}$ and $3\text{dB}$ Bandwidth $BW$) required to sustain the loop phase margin and target crossover frequency defined in Homework 3.
    * Verified performance utilizing an intermediate behavioral model with non-ideal parameters to map the sharp loop phase drop ($\ge 100^\circ$) induced by amplifier pole limitations.
* **Transistor-Level Design Synthesis:**
    * Architected a high-performance CMOS operational amplifier down to physical transistor structures utilizing an advanced commercial technology node.
    * Documented a rigorous systematic sizing procedure balancing transconductance ($g_m$), output impedance ($r_o$), and capacitive load constraints.
* **Multi-Level Model Co-Simulation & Verification:**
    * Executed comparative sweeps evaluating circuit behavior across three abstraction tiers:
        1.  **Level 1:** Fully Ideal Behavioral Model
        2.  **Level 2:** Non-Ideal Macro-Model (Finite Gain & Bandwidth)
        3.  **Level 3:** Full Transistor-Level FinFET Schematic
    * Analyzed loop gains, compensator profiles, and load transient waveforms to evaluate the impacts of circuit parasitics on overall phase margin.
### Documentation
📄 Refer to:  
- [`doc`](./HW/hw1/PEIC-HW4%20-%202026.pdf)

---

## Final Project: Transistor-Level $V^2$ Constant ON-Time Buck Converter PMIC

### Project Context
Modern CPU/GPU microprocessors in mobile devices demand ultrafast transient recovery during deep sleep-to-wake transitions alongside low component footprints. To meet this challenge, this project presents the complete design and verification of a **$V^2$ Constant ON-Time (COT) controlled Point-of-Load (POL) Buck Converter**, designed at the transistor level using a **16nm FinFET process technology**.

### System Specifications
* **Input Voltage ($V_{in}$):** $12\text{ V}$
* **Target Output Voltage ($V_o$):** $1.2\text{ V}$
* **Maximum Load Current ($I_o$):** $4\text{ A}$ (Dynamic range: $1\text{ A} \leftrightarrow 4\text{ A}$)
* **Switching Frequency ($f_s$):** $300\text{ kHz}$
* **Output Filter Components:** $L_s = 1.8\ \mu\text{H}$, $C_o = 800\ \mu\text{F}$
* **Capacitor ESR ($R_{Co}$):** Extremely low $175\ \mu\Omega$ (Ceramic design target)

### Design Challenges Addressed
Standard COT control structures suffer from severe **sub-harmonic oscillations** when deployed alongside modern ceramic capacitors. Because ceramic capacitors feature minimal ESR, the inductor current ripple phase information fed to the modulator gets delayed by the dominant capacitive integral ($\int i_c \, dt / C_o$). 

To overcome this structural instability without relying on power-hungry current-sensing resistors, we implemented an internal **External Ramp Compensation Network** ($S_e = 3 \cdot S_f = 350\text{ mV/}\mu\text{s}$) to restore loop stability, optimize phase margin, and prevent control loop bifurcation.

### Core Analog Sub-Blocks Designed (Transistor Level)

1.  **High-Speed Hysteretic Comparator:**
    * Features a built-in input hysteresis window ($5\text{ mV} - 20\text{ mV}$) to guarantee clean, chatter-free pulse generation.
    * Achieved ultra-low propagation delay ($	au_{pd, rise} = 355\text{ ps}$, $	au_{pd, fall} = 164\text{ ps}$) under a nominal $1\text{ V}$ supply and $60\ \mu\text{A}$ reference bias.
2.  **Folded-Cascode Operational Amplifier (Type-I Compensation):**
    * Designed as an optimal high-gain error integrator block to minimize steady-state DC offsets.
    * **Performance Metrics:** Open-Loop Gain = **$94.89\text{ dB}$**, Common Mode Rejection Ratio (CMRR) = **$101.4\text{ dB}$**, Phase Margin = **$101.4^\circ$**, and a Gain-Bandwidth Product (GBW) of **$86.28\text{ MHz}$**.
3.  **Resistorless Auto-Biased Current Reference Circuit:**
    * Implemented a highly reliable Oguey-style layout to optimize silicon area utilization and eliminate thermal drift errors linked with physical resistors.
    * Generated an incredibly stable reference bias current of **$300.1\ \mu\text{A}$** with a rapid startup settling window of **$7.72\text{ ns}$**.

### Closed-Loop System Simulation Results (SIMPLIS)
* **Stability Metrics:** Achieved a stable loop crossover frequency of $31\text{ kHz}$ with a highly robust Phase Margin of **$89.4^\circ$** and a Gain Margin of **$17.1\text{ dB}$**.
* **Step-Down Transient Response ($4\text{ A} \rightarrow 1\text{ A}$):** Peak voltage overshoot restricted to just **$1.5\text{ mV}$** ($1.210\text{ V}$ absolute maximum peak) with a rapid settling time of **$20.38\ \mu\text{s}$** (roughly $6 \cdot T_{sw}$).
* **Step-Up Transient Response ($1\text{ A} \rightarrow 4\text{ A}$):** Peak voltage undershoot limited to **$1.8\text{ mV}$** ($1.197\text{ V}$ absolute minimum valley) with a smooth settling time of **$18.43\ \mu\text{s}$** ($5 \cdot T_{sw}$).

### Documentation
📄 Refer to:  
- [`doc`](./FinalProject/PEIC-final.pptx)

---

## 🛠️ Tools Used
* **Behavioral Modeling & System Simulation:** SIMPLIS, LTspice
* **Transistor-Level IC Schematic Design & Verification:** Cadence Virtuoso
* **Process Node Layout Target:** Commercial 16nm FinFET PDK (N16ADFP)
