# 📡 Signal Resilience Simulator: Channel Coding Lab

[![Tool: MATLAB](https://img.shields.io/badge/Tool-MATLAB-ED1C24?logo=mathworks&logoColor=white)]()
[![Field: Telecommunications](https://img.shields.io/badge/Field-Information--Theory-blue)]()
[![Status: Analytical](https://img.shields.io/badge/Status-Complete-success.svg)]()

**Signal Resilience Sim** is a comprehensive MATLAB-based simulation designed to analyze the effectiveness of Channel Coding in noisy environments. By implementing convolutional encoding and interleaving, the project evaluates how data integrity is maintained across impaired communication channels.

## 🏗️ The Communication Pipeline
The simulation replicates a full digital communication chain:
1.  **Source Encoding:** Generation of the raw bitstream.
2.  **Convolutional Encoder:** Adding structured redundancy to the signal to allow for error correction.
3.  **Interleaving:** Shuffling the bit sequence to distribute burst errors, making them easier to correct at the receiver.
4.  **Noisy Channel (AWGN):** Transmission over a simulated Additive White Gaussian Noise channel.
5.  **Decoding:** Reconstructing the original signal and calculating the **Bit Error Rate (BER)**.

## 🧪 Technical Features
*   **Convolutional Coding:** Implementation of trellis-based encoding to provide forward error correction (FEC).
*   **Interleaver Logic:** Mitigation of deep fades and burst noise by decorrelating adjacent bits.
*   **Performance Metrics:** Detailed calculation of BER vs. $E_b/N_0$ (Signal-to-Noise Ratio).
*   **Noise Modeling:** Configurable AWGN (Additive White Gaussian Noise) levels to simulate various environmental conditions.

## 📊 Performance Analysis
> **Technical Insight:** The simulation demonstrates the "coding gain"—the reduction in required transmit power achieved by using convolutional codes compared to uncoded transmission.

## 🚀 Getting Started
1. **Clone the repo:**
   ```bash
   git clone [https://github.com/khaled-kk/Signal-Resilience-Sim.git](https://github.com/khaled-kk/Signal-Resilience-Sim.git)

2. **Open in MATLAB:**

* Run the main_simulation.m script.

* Adjust the SNR_dB parameters to observe changes in signal reconstruction quality.

---
*Developed by Khaled Walid*
