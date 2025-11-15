# uav-avionics

[![License](https://img.shields.io/badge/license-MIT-blue.svg)]()
[![Status](https://img.shields.io/badge/status-Work%20in%20Progress-orange.svg)]()

## 🚁 Overview

A complete UAV avionics project featuring flight-controller firmware, sensor integration (IMU, magnetometer, barometer), PID-based stabilization, communication protocols, and custom PCB designs for modern drones. This repository is organized to help both learners and developers build reliable, modular avionics systems — from low-level sensor drivers to full flight-control stacks and PCB layouts.

---

## 📌 Key Features

* Flight-controller firmware (C / C++) for ESP32 / STM32 / ATmega
* Sensor drivers: IMU (accelerometer + gyro), Magnetometer, Barometer, GPS interfaces
* Sensor fusion and attitude estimation (complementary filter, Madgwick, Mahony)
* PID-based stabilization and motor/ESC control
* Telemetry and communication modules (UART, MSP, MAVLink basics)
* PCB designs and KiCad/Altium source files for flight controller and power distribution
* Python tools: calibration utilities, log analysis, plotting
* Modular architecture to swap sensors, MCUs, or control algorithms easily

---

## 🏗️ Repo Structure

```
uav-avionics/
│
├── firmware/                 # Flight controller firmware
│   ├── platform/             # MCU-specific code (esp32/, stm32/, atmega/)
│   ├── drivers/              # Sensor drivers (imu/, mag/, baro/, gps/)
│   ├── controllers/          # PID, mixers, motor control
│   ├── sensor_fusion/        # Filters and estimators (Madgwick, Mahony)
│   └── utils/                # Comm, logging, config
│
├── hardware/                 # PCB, schematics, BOMs
│   ├── flight-controller/    # KiCad/Altium files and gerbers
│   ├── pwr-distribution/     # Power boards, MOSFETs, layout
│   └── sensor-modules/       # Breakout boards and reference designs
│
├── docs/                     # Design notes, wiring diagrams, theory
│   ├── wiring/
│   ├── theory/
│   └── calibration/
│
├── tools/                    # Python calibration, plotting, data tools
│
├── tests/                    # Unit and hardware-in-loop tests
│
└── LICENSE
```

---

## 🔧 Getting Started (Quick)

1. Clone the repository:

```bash
git clone https://github.com/<your-username>/uav-avionics.git
cd uav-avionics
```

2. Choose a platform folder under `firmware/platform/` and follow its README for build instructions.

3. For PC-side tools (calibration/log analysis):

```bash
cd tools
python3 -m venv venv
source venv/bin/activate    # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

4. Flash firmware using platform-specific tools (esptool, STM32CubeProgrammer, avrdude).

---

## 🧩 Hardware Recommendations

* MCU: ESP32 (development), STM32F4 (production-capable), or ATmega328 (simple prototypes)
* IMU: ICM-20689 / MPU6000 / BMI270
* Magnetometer: QMC5883L / LIS3MDL
* Barometer: BMP388 / MS5611
* ESCs: BLHeli / standard 4-in-1 ESCs
* Power: 5V/3A BEC (for logic), appropriate battery protection

---

## 🧠 Sensor Calibration

Calibration is required for reliable heading and attitude estimation.

* **Accelerometer & Gyro**: Run stationary zero-offset calibration (bias) and scale calibration routines.
* **Magnetometer**: Perform 3D soft/hard-iron calibration — collect samples while rotating the vehicle and compute offsets and scale matrix.
* **Barometer**: Calibrate sea-level pressure for accurate altitude or use GPS/known altitude references.

See `docs/calibration/` for calibration scripts and step-by-step guides.

---

## 🚀 How to Use (Typical Flow)

1. Wire sensors to the MCU (I2C/SPI) and verify communication with `i2cdetect` or MCU scan utility.
2. Flash a base firmware that prints raw sensor values to serial.
3. Run calibration utilities to generate offsets and save to the controller's config.
4. Flash control firmware with sensor fusion and PID controllers enabled.
5. Test with props removed first; verify attitude response with small motor commands.
6. Tune PID on the bench with motors restrained or in a test rig before a flight.

---

## 📚 Documentation & Theory

* `docs/theory/` contains notes on sensor fusion, coordinate frames, quaternion math, and PID tuning.
* `docs/wiring/` contains wiring diagrams and connector pinouts.

---

## 🤝 Contributing

Contributions are welcome!

* Fork the repo
* Create a branch for your feature: `feature/<short-desc>`
* Add tests and documentation
* Open a pull request with a clear description and any hardware testing notes

Please follow the coding style in `CONTRIBUTING.md` (coming soon) and keep commits small and focused.

---

## 📄 License

This project is available under the **MIT License**. See `LICENSE` for details.

---

## ✉️ Contact

Maintainer: **Harsh Saini**  
Email: [saini.harsh.in@gmail.com](mailto:saini.harsh.in@gmail.com)

---

 
