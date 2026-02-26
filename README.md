# TETRA Transmitter (PlutoSDR)

## 📌 Overview
This project implements a **TETRA DMO transmitter** using an **Analog Devices PlutoSDR**, GNU Radio, and custom Python/C++ blocks.  
It encodes and transmits audio signals in DMO mode, which can be received and played back on a TETRA handset.  

---

## 🛠️ Features
- Real-time audio encoding and modulation for TETRA DMO  
- Transmission via **PlutoSDR** hardware  
- Custom GNU Radio blocks in Python and C++  
- Verified end-to-end system with TETRA handset reception  

---

## 🔧 Tools & Technologies
- **Hardware:** PlutoSDR  
- **Software:** GNU Radio, Python, C++  
- **OS:** Linux (Ubuntu recommended)  
- **Protocols:** TETRA DMO  

---

## 🚀 How to Run
1. Clone this repo:  
   ```bash
   git clone https://github.com/yourusername/tetra-transmitter.git  
2. Install dependencies (GNU Radio, PlutoSDR drivers, Python libraries).  
3. Connect PlutoSDR device. 
4. Run the GNU Radio flowgraph / transmitter application.  

## 📊 Results

- Encoded and transmitted audio via TETRA DMO

- Audio successfully received on a TETRA handset

## 📚 Learning & Contribution

- RF transmission and SDR integration

- Digital modulation and TETRA DMO protocol

- SDR development in Python and C++

- End-to-end system testing and validation

---

## Additional Notes

The project aims to implement a TETRA DMO transmitter using a PlutoSDR device, GNU Radio toolkit, and custom Python/C++ blocks; successfully encoded, modulated and transmitted voice from PC microphone; audio received live on a TETRA handset.

1. USER_INTERFACE
- Designed in GNU Radio, with microphone as input.
- Use a QT GUI Push Button as the PTT (Push-To-Talk) button.
- Allow TalkGroup selection.

2. AUDIO_SOURCE
- Can the push_button variable be used to control the audio_source so that it only starts operating when the button is pressed?
- If not, then control should instead be applied so that the source encoder only operates when push_button is ON.

3. PlutoTx_SINK
- Similarly, is it possible to use the push_button to control the pluto_sink so that it only starts operating when the button is pressed?
- Does PlutoTx transmit only when burst data is sent to it (based on a BURST ACTIVE signal), or does it transmit continuously — and if the input is zero, automatically not radiate?
- The IQ Encoder / IQ Mapping module should be responsible for modulating signals according to burst timing.
4. WORKFLOW
When the PTT button is pressed:
- Start Frame Counter
- Send DMAC_call_setup bursts
- Send speech bursts on TN1
- If burst numbers 6 and 12 → also send DSB on TN3
- If burst number 18 → send DMAC-Sync

### DMO GroupCall setup sequence 

### DMO GroupCall terminate sequence

### Block Diagram  
![image](https://github.com/user-attachments/assets/4baf6ebf-0444-4bd7-bf9d-24bff403059f)

pi4DQPSK Modulator: Successfully implemented in a Python block.

Practical observations during testing:
- The TETRA receiver only cares about decoding its intended signal and does not care about time slots or interference.
- If IQ is modulated continuously, including inactive bursts (like TMO signals), the TETRA handset still receives normally.
- After synchronizing timing with the transmitter, the TETRA handset only processes its assigned time slot and ignores other signals, whether noisy or not.
- Guard symbols can be kept or removed without affecting reception performance.
- IQ can be modulated per burst, or continuously across the entire signal (including inactive bursts).
- Inactive bursts can be zeroed out to avoid unnecessary interference during transmission.
