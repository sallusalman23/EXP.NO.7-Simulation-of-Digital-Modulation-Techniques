# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques

# AIM
i) Amplitude Shift Keying (ASK)
ii) Frequency Shift Keying (FSK)
iii) Phase Shift Keying (PSK)

# SOFTWARE REQUIRED
Google colab

# ALGORITHMS
```
Amplitude Shift Keying (ASK)
   Define a binary input signal (e.g., [1, 0, 1, 1, 0]).
   Set a carrier frequency.
   Multiply the carrier by the bit (1 or 0) to get ASK modulated signal.
   Plot the input signal, carrier, and ASK signal.
Frequency Shift Keying (FSK)
   Define two carrier frequencies: one for bit 1, another for bit 0.
   Multiply bit 1 with one frequency, bit 0 with the other.
   Concatenate all modulated bits.
   Plot the input signal and FSK signal.
Phase Shift Keying (PSK)
   Use a single frequency carrier.
   For bit 1, send the signal with phase 0.
   For bit 0, invert the signal (phase shift by 180°).
   Plot the input signal and PSK signal.
```
# PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt

# --------- Parameters ---------
data = [1, 0, 1, 1, 0, 1]        # Binary input
bit_rate = 1                    # Bit rate in bits per second
fs = 1000                       # Sampling frequency in Hz
Tb = 1 / bit_rate               # Time per bit in seconds

# Time vector for 1 bit duration
t_bit = np.linspace(0, Tb, int(fs * Tb), endpoint=False)

# Carrier settings
fc = 8                       # Carrier frequency for ASK/PSK
f1 = 8                        # Frequency for FSK when bit = 1
f0 = 5                          # Frequency for FSK when bit = 0
A1 = 1                          # Amplitude for bit = 1 (ASK)
A0 = 0                          # Amplitude for bit = 0 (ASK)

# --------- Signal Containers ---------
digital_signal = []
ask_signal = []
fsk_signal = []
psk_signal = []

# --------- Modulation Process ---------
for bit in data:
    # Digital waveform (square wave)
    digital_bit = np.ones_like(t_bit) * bit
    digital_signal.extend(digital_bit)
    
    # ASK
    amplitude = A1 if bit == 1 else A0
    ask_bit = amplitude * np.sin(2 * np.pi * fc * t_bit)
    ask_signal.extend(ask_bit)
    
    # FSK
    freq = f1 if bit == 1 else f0
    fsk_bit = np.sin(2 * np.pi * freq * t_bit)
    fsk_signal.extend(fsk_bit)
    
    # PSK
    phase = 0 if bit == 1 else np.pi
    psk_bit = np.sin(2 * np.pi * fc * t_bit + phase)
    psk_signal.extend(psk_bit)

# Time axis for complete signals
t_total = np.linspace(0, Tb * len(data), int(fs * Tb * len(data)), endpoint=False)

# --------- Plotting ---------
plt.figure(figsize=(14, 10))

# Digital Input
plt.subplot(4, 1, 1)
plt.plot(t_total, digital_signal, color='black')
plt.title("Digital Input Signal")
plt.ylabel("Amplitude")
plt.ylim(-0.5, 1.5)
plt.grid(True)

# ASK
plt.subplot(4, 1, 2)
plt.plot(t_total, ask_signal, color='blue')
plt.title("Amplitude Shift Keying (ASK)")
plt.ylabel("Amplitude")
plt.grid(True)

# FSK
plt.subplot(4, 1, 3)
plt.plot(t_total, fsk_signal, color='orange')
plt.title("Frequency Shift Keying (FSK)")
plt.ylabel("Amplitude")
plt.grid(True)

# PSK
plt.subplot(4, 1, 4)
plt.plot(t_total, psk_signal, color='green')
plt.title("Phase Shift Keying (PSK)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()
```
# OUTPUT
![image](https://github.com/user-attachments/assets/0c97b15a-416e-47b9-ac9e-08e405096725)

 
# RESULT / CONCLUSIONS
The simulation of digital modulation techniques such as ASK, FSK, and PSK was successfully implemented using Python. The differences between amplitude, frequency, and phase modulation were clearly observed in the plotted waveforms.
