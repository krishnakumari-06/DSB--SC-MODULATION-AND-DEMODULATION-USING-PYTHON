 # DSB--SC-MODULATION-AND-DEMODULATION-USING-PYTHON

__AIM__:

To generate a Double Sideband Suppressed Carrier (DSB-SC) signal in Python (Google Colab), transmit it (optionally add noise), and recover the message using coherent (synchronous) demodulation with a low-pass filter. Observe time and frequency domain waveforms and measure demodulation performance

__APPARATUS REQUIRED__:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

__Theory__:

DSB-SC signal: s(t) = m(t) · cos(2πf_c t)
Coherent demodulation: multiply received s(t) by a synchronized carrier cos(2πf_c t) then low-pass filter (LPF) to remove double-frequency components:

r(t) = s(t)·cos(2πf_c t) = m(t)·cos²(2πf_c t) = 0.5 m(t) + 0.5 m(t)·cos(4πf_c t)
LPF extracts 0.5·m(t) → scale by 2 to recover m(t).

__Procedure__:

1) Import libraries and set parameters
2) Define message and carrier signals
3) Generate DSB-SC signal (modulation)
4) View spectra (FFT) of message and DSB-SC
5) (Optional) Add noise
6) Coherent demodulation (multiply by synchronized carrier)
7) Low-pass filter to recover message
   
__program__:

```
import numpy as np          # REQUIRED IMPORT
import matplotlib.pyplot as plt

Ac = 10.5
fc = 5070
Am = 7.5
fm = 570
fs = 50000

t = np.arange(0, 2/fm, 1/fs)

Wm = 2 * np.pi * fm
Wc = 2 * np.pi * fc

Em = Am * np.sin(Wm * t)
Ec = Ac * np.sin(Wc * t)

Edsbsc = ((Am / 2) * np.cos((Wc - Wm) * t)) - ((Am / 2) * np.cos((Wc + Wm) * t))

plt.figure(figsize=(10, 6))

plt.subplot(3, 1, 1)
plt.plot(t, Em)
plt.grid()

plt.subplot(3, 1, 2)
plt.plot(t, Ec)
plt.grid()

plt.subplot(3, 1, 3)
plt.plot(t, Edsbsc)
plt.grid()

plt.tight_layout()
plt.show()
```

   __Tabulation__:
![499299868-c93c44d5-5571-4e5b-93ae-09aa1e1d835a](https://github.com/user-attachments/assets/cb99471b-c3c6-4ca9-8a3b-2e4f4b84ab35)

   __Output__:
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/6579dbbc-e55e-4baf-a408-040386b2154b" />

   __Result__:
