# RQ-generation-plots

This folder contains scripts used to process ROS bag files and extract the data required to answer the research questions (RQs) from the study.

---

## Experimental Setup Validation

### Real-Time & Synchronization Settings
- **Benchmark scope:** 5,000 samples; per-component execution times measured across SiL, ViL, MR, and RW.
- **Simulator throughput:** ≈ **80 FPS** (≈ **12.5 ms** per frame) on AMD Ryzen 5, 16 GB RAM, NVIDIA RTX 2060.
- **Sensor rates:** Camera & LiDAR at **20 FPS** (50 ms).  
  - **Simulator camera:** **20 FPS** (matches real sensors).  
  - **Tracking feed:** **30 FPS** (downsampled from tracker output for sync).  
  - **Tracker raw output:** ≈ **99.93 Hz** (≈ **10.01 ms**); **downsampled** to 30 FPS for simulation alignment.  
- **Global sim cap:** **60 FPS** to avoid unnecessary system load.

### ADS Execution Timing
- **E2E ADS:** ≈ **15 ms** average per cycle.
- **Modular ADAS:** ≈ **20 ms** average per cycle.
- **Scheduling:** Inference triggers on arrival of each sensor message; parallel inference is supported, but in our measurements both pipelines **consistently finished before the next 20 FPS frame**.
- **Control rate:** Commands measured **on-vehicle** at ≈ **50.5 ms** per command; stable across experiments.

### Networking Setup
- **Router:** TP-Link Archer C6 dual-band gigabit WLAN (867 Mbit/s @ 5 GHz + 300 Mbit/s @ 2.4 GHz, 4× Gigabit LAN), configured as **local-only**.
- **Links:**  
  - Vehicle ↔ Workstation: **TCP over 5 GHz** (Intel-8265AC, 867 Mbit/s).  
  - Tracking ↔ Workstation: **Wired Gigabit Ethernet**.
- **Payloads:** JPEG camera images ≈ **800 kB**; control commands **< 30 bytes**.  
  At **20 Hz** sensing, bandwidth allowed ≈ **50** image transmissions and **thousands** of control messages **per cycle** with **no observed packet loss**.

### Tracking Accuracy Validation
- **Method:** Calibrated reference object with five retro-reflective markers (non-coplanar geometry) tracked by Vicon for 6-DoF pose.
- **Distance check:** Known marker spacing **240 mm**; measured **five times** at 30 s intervals in both rooms.  
  - **Mean:** 240 mm  
  - **MAE:** **0.40 mm**  
  - **Std dev:** **0.0253 mm**  
  Confirms **sub-millimeter position accuracy**; geometry matching also ensures accurate 3-axis orientation.

> **TL;DR:** All modalities (SiL, ViL, MR, RW) run in **real time**. Sensors at **20 FPS** set the upper bound; simulator camera is set to **20 FPS**, tracking is **30 FPS** (downsampled from ≈100 Hz), and the global sim is capped at **60 FPS** for stability. ADS cycles complete **well within** the 50 ms sensing period, and control commands at ≈ **50.5 ms** remain stable.



## Script Categories

### A. Perception Gap (Camera)

Scripts used to analyze camera-based perception performance, including lane and obstacle detection:

- `A_process_inputs_camera_lanes.py` |    Used to manually label lane splines
- `A_process_inputs_camera_obstacles.py`  |    Used to manually label obstacles bounding boxes
- `A_process_lane_results.py`  |    Processes the manually labeled data
- `A_process_obstacles_results.py`  |     Processes the manually labeled data
- `A_compare_camera.py`  |     Compares images for perception gap

---

### B. Perception Gap (LiDAR)

Scripts used to analyze LiDAR-based obstacle detection and perception accuracy:

- `B_process_inputs_lidar.py`    |    Used to manually label obstacles bounding boxes
- `B_process_inputs_lidar_multiple.py`    |    Used to manually label obstacles bounding boxes (2 obstacles per frame)
- `B_process_obstacles_results.py`  |    Processes the manually labeled data
- `B_process_obstacles_results_multiple.py`  |    Processes the manually labeled data
- `B_compare_lidar.py`  |     Compares pointclouds for perception gap

---

### C. Actuation Gap

Scripts for analyzing actuation behavior in throttle, steering, braking, and PID responses:

- `C_process_actuation_throttle.py`  
- `C_process_actuation_throttle_statistics.py`  
- `C_process_actuation_steering.py`  
- `C_process_actuation_steering_statistics.py`  
- `C_process_actuation_braking.py`  
- `C_process_actuation_braking_statistics.py`  
- `C_process_actuation_pid.py`  
- `C_process_actuation_pid_plots.py`  
- `C_process_actuation_waypoints.py`  

---

### D. Behaviour Gap (End-to-End)

Scripts focused on evaluating the behavior of end-to-end (E2E) autonomous driving systems:

- `D_process_e2e.py`  
- `D_process_e2e_merged_plot.py`
- `D_process_e2e_generalization.py`  

---

### E. Behaviour Gap (Modular)

Scripts focused on evaluating the modular autonomous driving pipeline:

- `D_process_modular.py`  
- `D_process_modular_merged_plot.py`  
- `D_process_modular_generalization.py`  
- `D_process_modular_lattice.py`  

---

## Notes

- Each script is designed to operate on `.bag` files containing recorded ROS topics from experiments.
