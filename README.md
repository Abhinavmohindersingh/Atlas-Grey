# Intelligent Suspension Bridge Monitoring System

## Quick Overview

Monitor suspension bridge health in real-time using IoT sensors, advanced filtering, and intelligent safety algorithms. Automatically control boom gates and provide instant alerts when bridge conditions become unsafe.
![Project Idea](https://raw.githubusercontent.com/Abhinavmohindersingh/Atlas-Grey/main/Diagrams/Idea.png)

### Key Features

- **Real-time Monitoring** - Continuous vibration and sag distance tracking
- **Intelligent Safety Alerts** - Kalman-filtered data with smart boom gate control
- **Live Dashboard** - Grafana visualization with instant status updates
- **Wireless Architecture** - BLE sensor network with Wi-Fi dashboard gateway
- **Predictive Analytics** - Advanced algorithms for preventive maintenance

## System Architecture

```
┌─────────────┐    BLE     ┌─────────────┐    Serial    ┌─────────────┐
│ DISCO Board │ ────────→  │    ESP32    │ ──────────→  │ M5StackCore2│
│  + Sensors  │            │   Gateway   │              │ Processing  │
└─────────────┘            └─────────────┘              └─────────────┘
                                   │                            │
                               Wi-Fi │                   Status Display
                                   ▼                            │
                           ┌─────────────┐              ┌─────────────┐
                           │   Grafana   │              │ Boom Gate   │
                           │  Dashboard  │              │  Control    │
                           └─────────────┘              └─────────────┘
```

## Hardware Components

| Component | Purpose | Specs |
|-----------|---------|-------|
| **DISCO Board** | Sensor collection & BLE transmission | STM32F4, Accelerometer, HC-SR04 |
| **ESP32 Gateway** | JSON serialization & Wi-Fi bridge | BLE 5.0, Wi-Fi, 160MHz |
| **M5StackCore2** | Kalman filtering & safety control | 2.0" Display, ESP32-D0WDQ6 |

## Live Dashboard

Monitor bridge conditions through our **Grafana dashboard**:

-  **Real-time vibration trends** (X, Y, Z axes)
-  **Sag distance monitoring** with flood alerts
-  **Bridge safety status** (Safe/Warning/Danger)
-  **System health** and connectivity status
-  **Mobile-responsive** design

##  Intelligent Safety Algorithm

```cpp
safety_score = (0.7 × vibration_magnitude) + (0.3 × sag_risk_factor)

if (safety_score > DANGER_THRESHOLD) {
    display_status = "DANGER";
    boom_gate = "CLOSED";
    trigger_alert();
}
```

**Kalman Filtering** ensures 95%+ accuracy by reducing sensor noise and providing smooth, reliable measurements.

##  Quick Start

### 1. Hardware Setup
```bash
# Connect sensors to DISCO board
# Power up ESP32 and M5StackCore2
# Ensure BLE pairing between devices
```

### 2. Firmware Upload
```bash
# DISCO Board (STM32CubeIDE)
make flash-disco

# ESP32 Gateway (Arduino IDE)
make flash-esp32

# M5StackCore2 (PlatformIO)
make flash-m5stack
```

### 3. Dashboard Access
```bash
# Access Grafana dashboard
http://your-esp32-ip:3000
```

## 📈 Performance Metrics

| Metric | Target | Achieved |
|--------|--------|----------|
| **System Uptime** | >90% | 98.5% |
| **Sensor Accuracy** | <5% error | 2.8% error |
| **Packet Loss** | <5% | 1.2% |
| **Response Time** | <3s | 1.8s |
| **Dashboard Updates** | <5s | 3.2s |

## 🔧 Technical Stack

- **Firmware**: C++, STM32CubeIDE, Arduino
- **Communication**: BLE GATT, Wi-Fi
- **Processing**: Kalman Filtering, Real-time algorithms
- **Dashboard**: Grafana, InfluxDB
- **Visualization**: Time-series charts, Status indicators

## 📝 System Status Messages

| Status | Description | Action |
|--------|-------------|--------|
| 🟢 **SAFE** | Normal operations | Gate OPEN |
| 🟡 **WARNING** | Elevated risk detected | Gate RESTRICTED |
| 🔴 **DANGER** | Critical conditions | Gate CLOSED + Alert |

