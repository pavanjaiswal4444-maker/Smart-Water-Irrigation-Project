# 🌱 Automatic Smart Water Irrigation System

> Automatically waters your plants when the soil gets dry — powered by Arduino Uno or ESP32.

![Platform](https://img.shields.io/badge/platform-Arduino%20%7C%20ESP32-blue)
![Language](https://img.shields.io/badge/language-C%2B%2B-orange)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-brightgreen)

---

## 📖 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Components](#components)
- [Circuit Connections](#circuit-connections)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Serial Monitor Output](#serial-monitor-output)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Manual watering is wasteful and unreliable. This project uses a **soil moisture sensor** to monitor soil conditions in real time. When the soil is dry, the microcontroller triggers a relay to turn on a water pump — and turns it off automatically once moisture is sufficient.

Works with both **Arduino Uno** (basic version) and **ESP32** (Wi-Fi enabled version).

---

## Features

- ✅ Automatic pump control based on soil moisture
- ✅ Serial monitor logging (real-time moisture values)
- ✅ LED status indicator (pump ON/OFF)
- ✅ Configurable dry/wet threshold
- ✅ ESP32 Wi-Fi variant for remote monitoring
- ✅ Non-blocking code (ESP32 version uses `millis()`)

---

## Components

| Component                | Qty | Notes                                     |
|--------------------------|-----|-------------------------------------------|
| Arduino Uno **or** ESP32 | 1   | ESP32 required for Wi-Fi version          |
| Soil Moisture Sensor     | 1   | Analog output module                      |
| Relay Module (5V)        | 1   | Active LOW                                |
| Water Pump               | 1   | 5V or 12V — match to your power supply    |
| Jumper Wires             | ~10 |                                           |
| Breadboard               | 1   |                                           |
| Power Supply / Battery   | 1   | Separate supply recommended for 12V pumps |
| Pipes / Tubing           | —   | As needed                                 |
| LED (optional)           | 1   | Status indicator                          |

---

## Circuit Connections

### Soil Moisture Sensor → Arduino Uno
| Sensor Pin | Arduino Pin |
|------------|-------------|
| VCC        | 5V          |
| GND        | GND         |
| A0         | A0          |

### Relay Module → Arduino Uno
| Relay Pin | Arduino Pin |
|-----------|-------------|
| IN        | D7          |
| VCC       | 5V          |
| GND       | GND         |

### Water Pump
- Connect pump to relay's **COM** and **NO** (Normally Open) terminals.
- Use a **separate power supply** for 12V pumps — do not draw from Arduino 5V pin.

> See [`hardware/wiring_diagram.md`](hardware/wiring_diagram.md) for the full ASCII wiring diagram.

---

## Getting Started

### Prerequisites
- [Arduino IDE 2.x](https://www.arduino.cc/en/software) or [PlatformIO](https://platformio.org/)
- USB cable (Type-B for Uno, USB-C/Micro for ESP32)

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/smart-irrigation.git
cd smart-irrigation
```

### 2. Open in Arduino IDE
- Navigate to `src/`
- Open `smart_irrigation.ino` (Uno) or `smart_irrigation_esp32_wifi.ino` (ESP32)

### 3. Configure (ESP32 Wi-Fi only)
Edit these lines in `smart_irrigation_esp32_wifi.ino`:
```cpp
const char* WIFI_SSID     = "YOUR_SSID";
const char* WIFI_PASSWORD = "YOUR_PASSWORD";
```

### 4. Select board & port
- **Tools → Board → Arduino Uno** (or ESP32 Dev Module)
- **Tools → Port → COMx** (Windows) or `/dev/ttyUSB0` (Linux/Mac)

### 5. Upload & monitor
- Click **Upload (→)**
- Open **Serial Monitor** at **9600 baud** (Uno) or **115200 baud** (ESP32)

---

## Project Structure

```
smart-irrigation/
│
├── src/
│   ├── smart_irrigation.ino              # Arduino Uno — basic version
│   └── smart_irrigation_esp32_wifi.ino   # ESP32 — Wi-Fi enabled version
│
├── hardware/
│   └── wiring_diagram.md                 # Detailed ASCII wiring reference
│
├── schematics/
│   └── schematic_notes.md                # Component specs & schematic tips
│
├── platformio/
│   └── platformio.ini                    # PlatformIO config (alternative IDE)
│
├── docs/
│   ├── project_report.md                 # Full project report
│   └── CALIBRATION.md                    # Sensor calibration guide
│
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

## How It Works

```
[Soil Moisture Sensor]
         │
         ▼  analog value (0–1023 on Uno / 0–4095 on ESP32)
[Arduino / ESP32]
         │
         ▼  value > threshold → relay LOW (pump ON)
[Relay Module]
         │
         ▼
[Water Pump] ──► 💧 Waters the plant
```

| Moisture Reading | Soil State | Pump   |
|------------------|------------|--------|
| > 700 (Uno)      | 🟤 Dry     | ON ✅  |
| ≤ 700 (Uno)      | 🌿 Wet     | OFF ❌ |

> **ESP32 threshold** is ~2800 (12-bit ADC). Adjust based on calibration — see [`docs/CALIBRATION.md`](docs/CALIBRATION.md).

---

## Serial Monitor Output

```
=== Smart Irrigation System Started ===
Dry threshold: 700
Moisture level: 823  → DRY  | Pump: ON
Moisture level: 756  → DRY  | Pump: ON
Moisture level: 612  → WET  | Pump: OFF
Moisture level: 589  → WET  | Pump: OFF
```

---

## Future Improvements

- [ ] Wi-Fi dashboard with real-time charts (ESP32)
- [ ] Mobile app (Blynk or custom Flutter app)
- [ ] LCD / OLED display for local readings
- [ ] Weather API — skip watering if rain is forecast
- [ ] Solar-powered operation
- [ ] Multi-zone irrigation (multiple sensors + solenoid valves)
- [ ] Data logging to SD card or cloud (ThingSpeak / Firebase)
- [ ] Capacitive moisture sensor (more durable than resistive)

---

## Contributing

Contributions are welcome! Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before submitting a PR.

1. Fork the repo
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push: `git push origin feature/your-feature`
5. Open a Pull Request

---

## License

MIT License — see [`LICENSE`](LICENSE) for details.

---

*Made with ❤️ for smart agriculture and home automation.*
