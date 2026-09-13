# Analog Front-End Design & Signal Processing

**Authors:** Mehrshad Arshad & Mahshad Ghoddousi

This repository contains a comprehensive three-part analog IC design and signal processing project. It spans state-variable active filter synthesis, phase/delay engineering for Active Noise Cancellation (ANC), and high-frequency transistor modeling (MOSFET/BJT) with RF impedance matching.

## Technologies Used
* **Simulation:** LTspice, MATLAB/Simulink
* **Concepts:** Laplace/KCL derivations, Bode analysis, Group Delay Engineering, Miller Effect, High-Frequency Small-Signal Modeling, RF Impedance Matching.

## Project Team & Contributions
This was a collaborative two-person project:
* **Mehrshad Arshad:** Lead designer for **Part I** (Sharif Analog Filter Synthesis & Notch Filter) and **Part III** (High-Frequency Transistor Amplifiers & RF Matching).
* **Mahshad Ghoddousi:** Lead designer for **Part II** (Phase Engineering & Active Noise Cancellation System).

## Project Breakdown & Key Results

### Part I: Sharif Analog Filter (SAF) Synthesis
Derived a 3-op-amp universal active filter from first principles (nodal/KCL to Laplace transfer functions) and synthesized component values for a target $f_c = 20\text{ kHz}$ and $Q = 0.75$.
* **Component Synthesis:** Calculated $R_G = R_Q = 200\text{ k}\Omega$ and $R_{F1} = R_{F2} \approx 7.958\text{ k}\Omega$.
* **SPICE Validation:** Simulated using non-ideal OP747 models, achieving $f_c = 19.49\text{ kHz}$ (2.55% error) and $Q \approx 0.728$ (~3% error).
* **Notch Filter Design:** Extended the SAF topology with a summing stage, successfully achieving $\sim 36\text{ dB}$ stopband attenuation at $19.49\text{ kHz}$.

### Part II: Phase Engineering & Active Noise Cancellation (ANC)
Designed a group-delay-controlled analog signal path to align audio phases for a closed-loop ANC system.
* **All-Pass Delay Network:** Engineered a 2nd-order active all-pass filter yielding a constant $\sim 45\mu\text{s}$ group delay across a 50x frequency span (100 Hz – 5 kHz).
* **System Integration:** Cascaded a 10x gain amplifier, the delay network, and a subtractor stage, verifying near-ideal common-mode cancellation. Integrated the full closed-loop system in Simulink for audio processing.

### Part III: High-Frequency Transistor Amplifiers & RF Matching
Analyzed small-signal parasitic capacitances ($C_{gs}, C_{gd}, C_\pi, C_\mu$) and their impact on amplifier bandwidth.
* **Transition Frequency ($f_T$):** Derived short-circuit current gains and matched theoretical hand-calculations to SPICE simulations with exceptional accuracy:
  * **MOSFET $f_T$:** $9.62\text{ GHz}$ (Theory) vs. $9.67\text{ GHz}$ (Sim) -> $<0.5\%$ error.
  * **BJT $f_T$:** $2.39\text{ GHz}$ (Theory) vs. $2.39\text{ GHz}$ (Sim) -> Near-exact match.
* **Miller Effect & Bandwidth:** Validated single-pole Miller roll-off for a CS amplifier (GBW $314.7\text{ MHz}$ vs unity crossing $313.3\text{ MHz}$). Successfully diagnosed CE amplifier GBW divergence as non-dominant pole effects ($r_x/C_\mu$) rather than simulation error.
* **RF Extensions:** Derived inductive source degeneration ($L_s$) and gate inductor ($L_g$) matching networks for a $50\Omega$ input match, alongside transformer-loaded tuned-amplifier derivations.
