# Distance-Relay-Simulation-for-Power-System-Protection
Project Overview
This project simulates an impedance-type distance relay for protecting a 220 kV transmission line using MATLAB/Simulink. The relay detects faults by measuring line impedance and operates in three zones (Z1, Z2, Z3) with configurable time delays. The simulation includes:

Fault analysis (phase-to-phase, phase-to-ground).

Relay coordination with backup protection (Relay 1 and Relay 2).

Tripping logic integrated with circuit breakers.

Real-world data from KDA to Pipri West transmission line (33 km).

Key Components
1. System Modeling
Network Components:

550 MVA generator (18 kV) → Step-up transformer (18 kV/220 kV).

Distributed parameter transmission line (220 kV).

Step-down transformer (220 kV/11 kV) → Load (800 kW + 100 kVAR).

Fault Injection:

Three-phase faults at variable distances (0.5 km to 30 km).

2. Distance Relay Design
Impedance Calculation:

Copy
Z = V/I (per-phase impedance measured via RMS blocks).  
Zone Settings:

Zone	Coverage	Time Delay	Reactance (X)
Z1	85% of protected line	0 sec	3.38 Ω
Z2	100% line + 50% next line	1 sec	4.89 Ω
Z3	100% line + 115% next line	2 sec	6.13 Ω
3. Fault Analysis & Results
Case 1: Fault at 20 km (within Z1) → Instantaneous tripping.

Case 2: Fault at 2 km into adjacent line (Z2) → Tripping after 1 sec delay.

Case 3: Fault at 5 km beyond Z3 → Relay inactive (handled by downstream relay).

Relay Coordination:

Relay 1 (primary) clears faults within its zones.

Relay 2 (backup) clears faults near line termination (85–100% of line).

4. Tripping Circuit
Logic: Compares measured impedance (Z_measured) with zone thresholds (Z1, Z2, Z3).

Output: Triggers circuit breaker via on/off delay blocks.

Repository Structure
/simulink_models:

Distance_Relay_Model.slx (Main Simulink model).

Impedance_Calculation_Block.slx (Subsystem for impedance measurement).

/docs:

Project report (Bachelors_Project_Report.pdf).

Relay setting calculations (Excel/PDF).

/results:

Plots of fault currents, voltages, and tripping signals.

How to Use
Run the Simulation:

Open Distance_Relay_Model.slx in MATLAB/Simulink.

Adjust fault location (Fault_Block parameters) and simulate.

Modify Relay Settings:

Update zone reactance/time delays in Relay_Settings.m.

Analyze Outputs:

Check Scope blocks for voltage/current waveforms.

Verify tripping times against zone settings.

Key Results
Fault Location	Relay Action	Tripping Time
20 km (Z1)	Instantaneous trip	0 sec
2 km into adjacent line	Delayed trip (Z2)	1 sec
5 km beyond Z3	No action (Relay 2 handles)	N/A
Dependencies
MATLAB R2020a or later.

Simulink + Simscape Electrical (for power system components).

References
Project report (NED University, Karachi).

MATLAB Distance Relay Tutorials.
