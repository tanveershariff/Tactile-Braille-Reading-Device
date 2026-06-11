# Tactile-Braille-Reading-Device
This is a project developed for fulfilling the need of blind people for accessing the refreshable braille device for most affordable price
<div align="center">

<img src="https://img.shields.io/badge/Status-In%20Development-teal?style=for-the-badge" />
<img src="https://img.shields.io/badge/Phase-Year%201%20%E2%80%94%20Software-blue?style=for-the-badge" />
<img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
<img src="https://img.shields.io/badge/Platform-Raspberry%20Pi-red?style=for-the-badge" />

<br /><br />

# 🤏 Democratizing Touch
### An Affordable Refreshable Braille Reading Device

*Compact · Electromechanical · Open-Source Inspired · Built for the 15 million*

<br />

> **"Access to information is a right, not a privilege."**
> This project engineers a single-cell refreshable Braille reader the size of a carrom coin — at under ₹80 per cell — for visually impaired individuals in low-resource environments.

<br />

## Prototype Simulation Preview

<p align="center">
  <img src="assets/demo.gif" width="850">
</p>

<p align="center">
  <i>3D simulation of the compact refreshable Braille cell showing real-time pin actuation.</i>
</p>

---

</div>

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [How It Works](#-how-it-works)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Project Roadmap](#-project-roadmap)
- [Simulation Preview](#-simulation-preview)
- [Getting Started](#-getting-started)
- [Folder Structure](#-folder-structure)
- [Team](#-team)
- [References](#-references)

---

## 🧠 About the Project

**Democratizing Touch** is a student-built assistive technology project from the Department of Computer Science Engineering. It aims to create a **compact, affordable, and electronically refreshable single-cell Braille reading device** using an electromechanical cam-and-electromagnet mechanism — as a low-cost alternative to expensive piezoelectric commercial products.

The device is approximately the size of a **carrom coin**, designed to be held between the thumb and index finger. The thumb rests on the Braille surface and senses the six raised cylindrical pins that represent each character.

The project is split into two development phases:

| Phase | Focus | Timeline |
|-------|-------|----------|
| Year 1 | Software, 3D Simulation, CAD Design, Concept Validation | Current |
| Year 2 | Physical Hardware, Braille Cell Fabrication, Electronics Integration | Upcoming |

---

## ⚠️ The Problem

| Metric | Reality |
|--------|---------|
| Blind population in India | ~15 million |
| India's share of global blind population | ~33% |
| Braille literacy rate in India | **Only 1%** |
| Cost of a commercial 40-cell Braille display | **$4,000 – $6,000** |
| Cost of a commercial 80-cell Braille display | **$8,000 – $12,000** |
| Piezoelectric cell cost (OEM) | ~$35 per cell |

Commercial refreshable Braille displays use **piezoelectric actuators** — they are reliable but prohibitively expensive, placing them entirely beyond the reach of most individuals in developing countries.

---

## 💡 Our Solution

Instead of piezoelectric actuators, this project uses an **electromechanical cam-and-electromagnet mechanism**:

- 🔩 **Rotating eccentric cams** with embedded rare-earth micromagnets
- ⚡ **Electromagnetic coils** that reverse polarity to flip the cam between two stable positions
- 📌 **Bistable design** — no power needed to hold a pin up or down (energy only consumed during transition)
- 🖨️ **3D-printed housing** — original compact circular design (~25 mm diameter)
- 💰 **Target cost: under ₹80 per cell** (~97% cheaper than commercial alternatives)

The system is paired with a **Raspberry Pi processing unit** that handles text storage, text-to-Braille conversion, and character-by-character actuation at an adjustable reading speed.

---

## ⚙️ How It Works

```
User / Caretaker loads text
           │
           ▼
  Raspberry Pi Processing Unit
  ┌─────────────────────────────┐
  │  Text Storage (SD Card)     │
  │  Text → Braille Mapping     │
  │  6-bit Pattern Generator    │
  │  Speed Controller           │
  └────────────┬────────────────┘
               │  Serial / GPIO
               ▼
     Braille Cell Driver Board
  ┌─────────────────────────────┐
  │  H-Bridge / Motor Driver    │
  │  Coil Polarity Control      │
  │  6× Electromagnetic Coils   │
  └────────────┬────────────────┘
               │
               ▼
     Physical Braille Cell
  ┌─────────────────────────────┐
  │  6 Eccentric Cams           │
  │  6 Rare-Earth Micromagnets  │
  │  6 Cylindrical Braille Pins │
  │  Original 3D Housing        │
  └─────────────────────────────┘
               │
               ▼
       Thumb reads raised pins
```

---

## 🏗️ System Architecture

```
┌────────────────────────────────────────────────────────┐
│                   AlgoPilotX (Software Layer)          │
│                                                        │
│   ┌──────────────┐      ┌───────────────────────────┐  │
│   │  Text Input  │─────▶│  Braille Mapping Engine   │  │
│   │  (File/CLI)  │      │  (Unicode Grade 1 Table)  │  │
│   └──────────────┘      └──────────────┬────────────┘  │
│                                        │               │
│                         ┌─────────────▼─────────────┐  │
│                         │   Speed & Timing Control  │  │
│                         │   (1s – 10s per char)     │  │
│                         └─────────────┬─────────────┘  │
│                                       │                │
└───────────────────────────────────────┼────────────────┘
                                        │ GPIO / Serial
┌───────────────────────────────────────▼────────────────┐
│              Hardware Actuation Layer                  │
│                                                        │
│   ┌──────────────────┐    ┌────────────────────────┐   │
│   │  Driver Board    │───▶│  Braille Cell (1-cell) │   │
│   │  H-Bridge IC     │    │  6 Pins | 6 Cams       │   │
│   │  Coil Switching  │    │  6 Coils | Housing     │   │
│   └──────────────────┘    └────────────────────────┘   │
└────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Hardware
| Component | Detail |
|-----------|--------|
| Processing Unit | Raspberry Pi 4 Model B |
| Microcontroller (Phase 2) | Arduino UNO (actuation control) |
| Actuation Mechanism | Eccentric cam + rare-earth micromagnet + EM coil |
| Driver IC | L293D / DRV8833 H-bridge |
| 3D Printing | PLA / PETG, 0.1 mm layer height |
| PCB (Later Phase) | Custom via JLCPCB / PCBWay |
| CAD Tool | Fusion 360 / KiCad 7 |

### Software
| Tool | Purpose |
|------|---------|
| Python 3.9+ | Braille translation engine, GPIO actuation driver |
| Raspberry Pi OS | Operating system on the processing unit |
| Three.js | 3D browser-based simulation of the device |
| HTML5 / JS (ES2020) | Web simulation front-end |
| Node.js 18 LTS | Local dev server for simulation |
| Thonny IDE | Hardware-side Python development |
| KiCad 7 | PCB schematic and layout (Phase 2) |

---

## 🗺️ Project Roadmap

```
Year 1 — Software & Simulation Phase (Current)
──────────────────────────────────────────────
 ✅  Project scoping and hardware direction finalized
 ✅  Electromechanical cam mechanism selected
 ✅  Text-to-Braille conversion module (Python)
 ✅  3D simulation — Three.js, animated Braille pins
 ✅  CAD housing design (updated for cam mechanism)
 ✅  Research paper — Chapters 1–3 completed
 🔄  Web UI refinement (particle background, premium aesthetic)
 🔄  Full simulation with speed control slider

Year 2 — Hardware Fabrication Phase (Upcoming)
───────────────────────────────────────────────
 ⬜  3D print cam components and housing (0.1 mm precision)
 ⬜  Wind electromagnetic coils (36–40 AWG wire)
 ⬜  Perfboard prototype and wiring
 ⬜  GPIO actuation driver integration
 ⬜  Full hardware + software integration test
 ⬜  Custom PCB design and order
 ⬜  Final prototype with reading speed control
```

---

## 🖥️ Simulation Preview

The web-based 3D simulation allows real-time visualization of the Braille cell before the physical hardware is built.

**Features:**
- 🎯 Real-time text-to-Braille conversion
- 🔵 Six independently animated cylindrical pins
- 🎚️ Adjustable reading speed slider
- 📊 Braille pattern visualization panel
- ✨ Premium UI — soft white, silver, grey, teal palette
- 🌌 Dynamic particle background

**To run the simulation locally:**

```bash
git clone https://github.com/tanveershariff/Tactile-Braille-Reading-Device.git
cd democratizing-touch/simulation
npx serve .
# Open http://localhost:3000 in your browser
```
---

## 🚀 Getting Started

### Prerequisites

```bash
# Raspberry Pi side
sudo apt update
sudo apt install python3 python3-pip
pip3 install RPi.GPIO

# Simulation side (on your computer)
node --version   # Node.js 18+
```

### Clone the Repository

```bash
git clone https://github.com/tanveershariff/Tactile-Braille-Reading-Device.git
cd democratizing-touch
```

### Run the Braille Translation Module (Raspberry Pi)

```bash
cd software/
python3 braille_engine.py
# Enter text when prompted — the Braille cell will actuate character by character
```

### Run the 3D Web Simulation (Browser)

```bash
cd simulation/
npx serve .
# Visit http://localhost:3000
```

---

## 📁 Folder Structure

```
democratizing-touch/
│
├── simulation/               # Three.js web-based Braille simulation
│   ├── index.html
│   ├── main.js
│   ├── assets/
│   │   ├── base.glb          # 3D model — device housing
│   │   └── pins.glb          # 3D model — Braille pins
│   └── style.css
│
├── software/                 # Raspberry Pi Python modules
│   ├── braille_engine.py     # Text-to-Braille conversion
│   ├── actuation_driver.py   # GPIO pin actuation controller
│   ├── speed_controller.py   # Reading speed manager
│   └── braille_map.py        # Unified English Braille Grade 1 lookup table
│
├── hardware/                 # CAD files and hardware design
│   ├── housing_v1.stl        # 3D printable housing
│   ├── cam_design.stl        # Eccentric cam model
│   └── schematic.kicad_sch   # Circuit schematic (KiCad)
│
├── docs/                     # Research paper and documentation
│   ├── research_paper_ch1_ch3.docx
│   └── system_architecture.png
│
├── README.md
└── LICENSE
```

---

## 👥 Team

| Name | Role | USN |
|------|------|-----|
| **Tanveer Shariff** | Project Lead — Hardware & Software | 1AT23CS170 |
| *Syed Allaam Siddick* | *Research and UI Design* | *1AT23CS166* |

**Team No:** 12
**Institution:** *Atria Institute Of Technology*
**Department:** Computer Science Engineering
**Batch:** 2023 – 2027

---

## 📚 References

1. V. Agarwal et al., "Refreshable Braille Display: A Review of Existing Technologies and a Proposed Method," 2023.
2. J. Kim et al., "Braille Display for Portable Device Using Flip-Latch Structured Electromagnetic Actuator," *IEEE Transactions on Haptics*, 2020.
3. A. Kulkarni et al., "Raspberry Pi-Driven Affordable Image-To-Braille Converter for Visually Impaired Users," Springer, 2024.
4. Open Source Project, "Electromechanical Refreshable Braille Module," Hackaday.io, 2023.
5. M. Etezad et al., "Advancements in Refreshable Braille Display Technology," Chapman University, 2024.

---

<div align="center">

**Built with purpose. Designed for access. Engineered for the 99% left behind.**

<br />

*If this project helped you or inspired your work, please consider giving it a ⭐*

<br />

![Made with ❤️ for accessibility](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%EF%B8%8F%20for-Accessibility-teal?style=flat-square)
![CSE Student Project](https://img.shields.io/badge/CSE-Student%20Project-blue?style=flat-square)
![India](https://img.shields.io/badge/Made%20in-India%20🇮🇳-orange?style=flat-square)

</div>
