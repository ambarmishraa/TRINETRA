<div align="center">

# 👁️ TRINETRA

### *"The Third Eye"*

**An IoT-based assistive navigation device for visually impaired individuals**

[![Language](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=flat-square&logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![Platform](https://img.shields.io/badge/Platform-Arduino_Nano-00979D?style=flat-square&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Type](https://img.shields.io/badge/Type-IoT_%2F_Assistive_Tech-8B5CF6?style=flat-square)](https://github.com/ambarmishraa/TRINETRA)
[![Sensors](https://img.shields.io/badge/Sensors-Ultrasonic_HC--SR04-orange?style=flat-square)](https://github.com/ambarmishraa/TRINETRA)

</div>

---

## 🔍 What is TRINETRA?

**TRINETRA** (Sanskrit: *त्रिनेत्र* — "The Third Eye") is an IoT-based wearable assistive device built to help visually impaired individuals navigate their environment safely and independently.

The device uses **dual ultrasonic sensors** to continuously measure the distance to objects in front of the user. When an obstacle is detected within **70 cm**, the corresponding buzzer activates immediately — giving the user real-time audio feedback without any screen, app, or internet connection required.

Named after Shiva's mythological third eye — a symbol of perception beyond ordinary sight — TRINETRA aims to extend that same ability to those who need it most.

---

## ⚡ How It Works

```
  [Ultrasonic Sensor 1]  →  Detects obstacle on LEFT
  [Ultrasonic Sensor 2]  →  Detects obstacle on RIGHT

  Distance ≤ 70 cm  →  Buzzer activates  (⚠️ obstacle alert)
  Distance > 70 cm  →  Buzzer silent     (✅ path is clear)
```

**The sensing loop:**

1. The Arduino sends a **10 µs trigger pulse** to each ultrasonic sensor
2. The sensor emits an ultrasonic burst and waits for the echo
3. The Arduino measures the **echo pulse duration**
4. Distance is calculated: `distance = (duration / 2) / 29.1` (cm)
5. If distance ≤ 70 cm → the paired buzzer is activated
6. Both sensors are polled continuously in the main loop

Additionally, typing `display distance` into the **Serial Monitor** (9600 baud) prints the live readings from both sensors — useful for testing and calibration.

---

## 🔧 Hardware Required

| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Nano | 1 | Microcontroller — runs the C++ logic |
| HC-SR04 Ultrasonic Sensor | 2 | Obstacle detection (left & right) |
| Buzzer (active) | 2 | Audio feedback for each sensor |
| Jumper wires | — | Connections |
| Breadboard or PCB | 1 | Circuit assembly |
| 5V power source | 1 | USB power bank or battery pack |

**Estimated build cost: < ₹500 / ~€6**

---

## 📌 Pin Configuration

```
Arduino Nano
│
├── Pin 5   →  Sensor 1 TRIG
├── Pin 6   →  Sensor 1 ECHO
├── Pin 8   →  Buzzer 1
│
├── Pin 9   →  Sensor 2 TRIG
├── Pin 10  →  Sensor 2 ECHO
└── Pin 12  →  Buzzer 2
```

| Arduino Pin | Connected To | Direction |
|-------------|-------------|-----------|
| 5 | HC-SR04 #1 — TRIG | OUTPUT |
| 6 | HC-SR04 #1 — ECHO | INPUT |
| 8 | Buzzer #1 | OUTPUT |
| 9 | HC-SR04 #2 — TRIG | OUTPUT |
| 10 | HC-SR04 #2 — ECHO | INPUT |
| 12 | Buzzer #2 | OUTPUT |

---

## 💻 The Code

The full source is in [`TRINETRA CODE.txt`](./TRINETRA%20CODE.txt) — paste it directly into the Arduino IDE.

**Core sensing function:**

```cpp
void SonarSensor(int trigPinSensor, int echoPinSensor) {
    digitalWrite(trigPinSensor, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPinSensor, HIGH);
    delayMicroseconds(10);            // 10µs trigger pulse
    digitalWrite(trigPinSensor, LOW);
    duration = pulseIn(echoPinSensor, HIGH);
    distance = (duration / 2) / 29.1; // Convert to cm
}
```

**Obstacle detection logic:**

```cpp
if (UltraSensor1 <= 70) {
    digitalWrite(buzzer1, HIGH);  // Obstacle within 70cm — alert!
} else {
    digitalWrite(buzzer1, LOW);   // Clear path — silent
}
```

**Serial debugging:**

Open Serial Monitor at **9600 baud** and type:
```
display distance
```
Output:
```
distance measured by the first sensor: 42 cm
distance measured by the second sensor: 118 cm
-
```

---

## 🚀 Getting Started

### 1. Install Arduino IDE

Download from [arduino.cc/en/software](https://www.arduino.cc/en/software)

### 2. Wire the circuit

Follow the pin configuration table above. Connect:
- Each HC-SR04 sensor: VCC → 5V, GND → GND, TRIG and ECHO to the pins listed
- Each buzzer: positive leg to the pin listed, negative to GND

### 3. Upload the code

1. Open Arduino IDE
2. Copy the contents of [`TRINETRA CODE.txt`](./TRINETRA%20CODE.txt)
3. Paste into a new sketch
4. Select **Board:** Arduino Nano
5. Select the correct **Port**
6. Click **Upload**

### 4. Power and test

Power the Arduino via USB or a 5V battery pack. Wave your hand in front of each sensor — you should hear the corresponding buzzer activate within 70 cm.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `TRINETRA CODE.txt` | Full C++ Arduino source code |
| `TRINETEA.jfif` | Photo of the assembled device |
| `TRINETRA PPT.pptx` | Project presentation slides |

---

## 🎯 Impact & Applications

- **Daily navigation** — wearable on wrist, stick, or vest for obstacle detection while walking
- **Indoor mobility** — detecting furniture, doors, and walls in familiar environments
- **Low-cost accessibility** — buildable for under ₹500, making it accessible in low-resource settings
- **No internet required** — fully offline, no app or phone dependency
- **Expandable** — can be extended with additional sensors, vibration motors, or voice feedback modules

---

## 👤 Author

**Ambar Mishra** — M.Sc. Computer Science, TU Darmstadt

[![Portfolio](https://img.shields.io/badge/Portfolio-ambarmishra.vercel.app-black?style=flat-square&logo=vercel)](https://ambarmishra.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin)](https://linkedin.com/in/ambar-mishra-5940922b4/)
[![Email](https://img.shields.io/badge/Email-ambar.mishra.cs@gmail.com-EA4335?style=flat-square&logo=gmail)](mailto:ambar.mishra.cs@gmail.com)

---

## 📄 License

This project is open source. Build it, improve it, share it — especially if it helps someone navigate the world more freely.
