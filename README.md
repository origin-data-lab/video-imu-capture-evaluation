# Video + IMU Capture Evaluation

### Origin Data Lab — Technical Field Note #01

[![Physical AI](https://img.shields.io/badge/Physical_AI-Technical_Evidence-111827)](https://origindatalab.io)
[![Multimodal](https://img.shields.io/badge/Multimodal-Video_%2B_IMU-0ea5e9)](https://origindatalab.io)
[![6-DoF IMU](https://img.shields.io/badge/6--DoF_IMU-Measured-14b8a6)](https://origindatalab.io)
[![Public Evidence](https://img.shields.io/badge/Status-Public_Evaluation-22c55e)](https://origindatalab.io)

Measured video and 6-DoF IMU capture characteristics from **12 consecutive segments generated during one continuous real-world field recording**.

This repository publishes the measurement methodology, observed results, timing limitations, and explicit technical boundaries for a tested Origin Data Lab capture configuration.

> **Measurement scope:** The 12 measured units are consecutive server-side segments from one continuous field recording. They are not 12 independent experimental sessions.

---

## Evaluation Overview

A continuous real-world agricultural produce sorting and portioning task was recorded and subsequently divided into **12 consecutive server-side capture segments**.

Each segment was evaluated independently from its recorded timestamps to examine:

- Effective video frame rate
- Native accelerometer sampling rate
- Native gyroscope sampling rate
- Application-level IMU sampling characteristics
- Timestamp monotonicity
- Duplicate timestamps
- Video–IMU temporal coverage
- Observed timing gaps

The purpose of this evaluation is to publish **measured capture behavior rather than nominal device specifications**.

---

## Key Measured Results

| Measurement | Observed Result |
|---|---:|
| Measured segments | **12 consecutive segments** |
| Effective video FPS | **29.83–30.00 FPS** |
| Native accelerometer effective rate | **409.65–410.14 Hz** |
| Native gyroscope effective rate | **409.94–410.27 Hz** |
| Timestamp monotonicity violations | **0** |
| Duplicate timestamps | **0** |
| Video–IMU temporal bracket coverage | **12 / 12 segments** |

Across the evaluated continuous capture, native accelerometer and gyroscope streams remained close to **410 Hz** under the tested device and software configuration.

These measurements are observations from the evaluated configuration. They are **not presented as a guaranteed hardware specification or production SLA**.

---

## Measurement Methodology

### Effective IMU Rate

Effective sampling rate was calculated directly from raw sensor timestamps using:

**Effective Hz = (n − 1) / ((last timestamp − first timestamp) / 1e9)**

This avoids deriving the sampling rate from nominal configuration values or simple sample-count/session-duration approximations.

### Native Sensor Stream

The native sensor stream refers to timestamped accelerometer and gyroscope records parsed from **imu_native_v1.bin**.

These native timestamp records were used for the effective-rate and timing measurements reported in this evaluation.

### Application-Level Sensor Stream

Application-level accelerometer and gyroscope records were evaluated separately from **imu_metadata_v1.json**.

Native and application-level measurements are intentionally reported separately because they represent different capture layers.

### Video Measurement

Effective video FPS was evaluated using decoded frame count and container duration.

### Temporal Coverage

Native IMU timestamp coverage was compared against the recorded video timing interval within the available monotonic timing domain.

This evaluation establishes **capture-session temporal coverage**.

It does **not** establish hardware frame-level video–IMU synchronization.

---

## Aggregate Measurement Results

| Metric | Min | Median | Mean | Max |
|---|---:|---:|---:|---:|
| Effective video FPS | 29.8334 | 29.9837 | 29.9646 | 30.0004 |
| Video frame max gap (ms) | 66.63 | 66.65 | 102.74 | 499.80 |
| Native accelerometer (Hz) | 409.6461 | 409.8665 | 409.8693 | 410.1447 |
| Native gyroscope (Hz) | 409.9429 | 410.1112 | 410.1097 | 410.2659 |
| Native accel max gap (ms) | 25.98 | 28.02 | 27.50 | 30.46 |
| Native gyro max gap (ms) | 4.93 | 7.34 | 10.94 | 24.68 |
| App-level accelerometer (Hz) | 97.7867 | 99.0855 | 99.1258 | 100.7711 |
| App-level gyroscope (Hz) | 97.7937 | 99.2673 | 99.1824 | 100.6345 |
| App accel max gap (ms) | 163.80 | 205.78 | 280.85 | 589.34 |
| App gyro max gap (ms) | 103.65 | 207.00 | 276.75 | 599.08 |
| IMU pre-roll (ms) | 303.17 | 422.30 | 429.58 | 562.22 |
| IMU post-roll (ms) | 87.40 | 114.37 | 111.53 | 135.30 |

---

## Timestamp Integrity

Across the evaluated streams:

- **0 timestamp monotonicity violations**
- **0 duplicate timestamps**
- **12 / 12 segments achieved video–IMU temporal bracket coverage**

The native IMU stream began before the evaluated video interval and extended beyond it for all 12 measured segments.

This demonstrates temporal coverage for the evaluated capture.

It does **not** demonstrate hardware frame-level video–IMU synchronization.

---

## Observed Timing Limitations

### Video Timing

One of the 12 evaluated segments showed a maximum inter-frame gap above 100 ms.

**Maximum observed video gap: 499.80 ms**

The remaining segments did not show a comparable maximum gap.

### Application-Level IMU Timing

Application-level accelerometer and gyroscope streams showed gaps above 100 ms in all 12 evaluated segments.

Maximum observed gaps:

- **Accelerometer: 589.34 ms**
- **Gyroscope: 599.08 ms**

The native IMU streams did not show gaps of comparable magnitude in this evaluation.

The cause of the application-level timing gaps has **not been established**.

Therefore, this evaluation does not attribute the observed behavior to buffering, batching, Android scheduling, downsampling, resampling, or any other specific mechanism.

---

## Technical Boundaries

This public evaluation does **not** claim:

- Hardware frame-level video–IMU synchronization
- Sub-frame synchronization
- Camera-exposure-level timestamp synchronization
- A guaranteed 410 Hz hardware specification
- Guaranteed continuous 100 Hz application-level delivery
- 12 independent experimental sessions
- A determined cause for the observed timing gaps

The reported results describe the **tested device and software configuration during the evaluated continuous capture**.

They should not be interpreted as universal performance guarantees for every device, environment, capture architecture, or future project.

---

## Capture Context

The measurement batch originates from a continuous real-world **agricultural produce sorting and portioning task recorded in South Korea**.

For this public technical release, capture context is described independently from internal operational metadata.

Original internal records are retained internally and are not reproduced here.

Public technical materials do not expose precise GPS coordinates, contributor-identifying information, private operational identifiers, or customer-specific information.

---

## What This Evaluation Demonstrates

This evaluation provides public technical evidence for:

- Real-world video + 6-DoF IMU capture
- Measured native sensor timing characteristics
- Timestamp integrity validation
- Video–IMU temporal coverage analysis
- Native and application-level sensor stream comparison
- Identification and disclosure of observed timing gaps
- Explicit separation between measured evidence and unsupported synchronization claims

The objective is to make the boundary between **measured results, observed limitations, and capability claims** clear.

---

## Public Evidence Structure

**Real-World Field Capture → Video + 6-DoF IMU → Raw Timestamp Measurement → Temporal & Integrity Validation → Measured Results → Limitations → Public Technical Evidence**

This repository is one component of Origin Data Lab's public technical evidence framework for Physical AI, robotics, embodied AI, and multimodal data production.

---

## Related Technical Evidence

### Technical Field Note #01 — Web Version

Full web presentation of the measurement methodology, results, limitations, and technical boundaries:

**Origin Data Lab — Measured Video + IMU Capture Characteristics**  
https://origindatalab.io/technical-field-notes/video-imu-capture-evaluation.html

### Real-World Data Operations

Origin Data Lab's broader capture-to-delivery framework covering field collection, metadata, validation, QC, privacy processing, and structured delivery:

**GitHub — Real-World Data Operations**  
https://github.com/origin-data-lab/real-world-data-operations

### Hugging Face Evidence

A dedicated public Hugging Face evidence dataset corresponding to this evaluation will be linked here after publication.

---

## About Origin Data Lab

**Origin Data Lab** designs and operates custom real-world data collection and dataset production programs for Physical AI, robotics, embodied AI, computer vision, and autonomous systems.

Core capabilities include:

- Egocentric human demonstration data
- Multimodal video + IMU capture
- Real-world task and environment sourcing
- Human demonstration collection
- Sensor and capture metadata
- Technical validation
- Quality control
- Privacy-aware processing
- Structured dataset delivery
- Multi-region field operations

Origin Data Lab operates project-specific data programs rather than forcing every project into a fixed dataset configuration.

### Official Links

**Website:** https://origindatalab.io  
**GitHub:** https://github.com/origin-data-lab  
**Hugging Face:** https://huggingface.co/origindatalab

---

## Evidence Status

**Public Technical Evidence — Technical Field Note #01**

The measurements published here describe a specific evaluated capture configuration and continuous field recording.

They are provided for technical review and evidence-based evaluation and are not presented as universal device specifications or guaranteed performance levels.

---

**Origin Data Lab**

*Real-World Data Production for Physical AI, Robotics & Embodied AI*
