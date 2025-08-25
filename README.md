#Non-Inverting Amplifier: Ideal vs Real Op-Amp

##Overview
I built and compared two non-inverting amplifier circuits in LTSpice: one using an ideal op-amp model and the other using a real LT1006 op-amp. The goal was to see how closely a real op-amp tracks the ideal model at low frequency and to validate that an idealized simulation is reasonable for early-stage design.

##What I measured
- Small-signal gain (expected ~10x)
- Input and output waveforms (amplitude and phase)
- Visual comparison between ideal and real op-amp outputs

##Circuit summary
- Input: AC sine, 50 mV amplitude, 60 Hz
- Power rails: +5 V and -5 V (two DC sources)
- Resistors: R1 = 10 kΩ (to ground from inverting input), RF = 90 kΩ (feedback)
- Configurations:
  - Circuit A: Ideal op-amp model (non-inverting)
  - Circuit B: LT1006 real op-amp (non-inverting)
- Connections: Non-inverting input receives V1. Inverting input tied to RF and R1 as the feedback network. Both circuits powered from ±5 V.

##How to run the simulation (LTSpice)
1. Open the appropriate .asc file from Circuit Files in LTSpice.
2. Set the AC source or transient source as needed (for the transient run set V1 to a 60 Hz sine, 50 mV amplitude).
3. Run a transient analysis long enough to capture steady-state cycles (for example, 100 ms).
4. Plot Vin and Vout for both circuits and compare amplitude and phase. For amplitude ratio, use a cursor to read peak values or use .measure commands.

##Placeholders for images (replace with actual files in Images folder)
- <img width="1920" height="1080" alt="Ideal Op_Amp" src="https://github.com/user-attachments/assets/a94f0af5-a0eb-47c4-b6ad-ec503d409625" />(schematic: ideal op-amp)
- <img width="1920" height="1080" alt="Real Op_Amp" src="https://github.com/user-attachments/assets/eddb36f6-1941-487c-a48e-e4ed9a266a01" />(schematic: LT1006)
-<img width="1920" height="1080" alt="Real vs Ideal Input" src="https://github.com/user-attachments/assets/8527fd69-2e16-462e-8c8b-0bfee691a6d7" />(plot: vin overlay)
- <img width="1920" height="1080" alt="Real vs Ideal Output" src="https://github.com/user-attachments/assets/72191e4c-ebe7-4969-9a98-a7e13bc3a71e" />(plot: vout overlay)

##Observed results
- Measured gain for both circuits was approximately 10x, as expected from the resistor values (1 + RF/R1 = 10).
- At 60 Hz, the LT1006 behaved almost identically to the ideal op-amp: no noticeable amplitude or phase difference in the plotted waveforms.
- Because the input amplitude and frequency are small/low, the non-idealities of the LT1006 (input offset, input bias current, finite bandwidth, slew rate limits) did not significantly affect the response in this setup.

##Interpretation and notes
- For low-frequency, small-signal work like this, a real precision op-amp such as the LT1006 can be effectively approximated by an ideal op-amp model in early design and verification.
- If you push frequency, amplitude, or load conditions, expect differences to appear due to finite slew rate, bandwidth, output drive limitations, and input bias/offset. Re-run with higher frequencies or larger amplitudes if you want to observe those non-ideal effects.
- If you need tighter agreement across conditions, include the op-amp's SPICE model and run AC sweep and transient analyses with worst-case supply/load to reveal differences.

##Suggested additions (if I continue)
- AC sweep comparing magnitude and phase vs frequency for both models.
- Harmonic distortion or slew-limited transient for a larger input step.
- Load variation to test output drive differences.

##Files included
- All circuit files are in the folder: Circuit Files
- All images (plots and screenshots) are in the folder: Images
