
# Autonomous Driving Visual System with Classical Image Processing

A real-time self-driving visual system using **classical image processing** on a **Raspberry Pi 5**. It performs **lane detection**, **obstacle detection**, and generates **driving decisions** using only traditional computer vision — no deep learning.

Ideal for low-power edge devices like the Raspberry Pi where efficiency matters.


---

## 🔍 Features

- **Lane Detection**  
  - HSV filtering → Yellow/white lane isolation  
  - Canny edges + Hough Transform → Line extraction  

- **Obstacle Detection**  
  - MOG2 background subtraction  
  - Morphological filtering  
  - Bounding box detection  

- **Decision Logic**  
  Generates:
  - `STOP`
  - `STEER LEFT` / `RIGHT`
  - `CAUTION`

- **Real-Time Visualization**  
  - Green lane overlays  
  - Red obstacle boxes  
  - Driving decision text

- **Multithreaded**  
  Parallel frame capture, processing, and display

- **Region of Interest (ROI)**  
  Trapezoidal mask to focus on the road and boost speed

---

## 🗂️ Project Structure

```plaintext
project/
├── main.ipynb          # Run lane & obstacle detection on pre-recorded video
├── main_picam.ipynb    # Run real-time detection with Raspberry Pi Camera
└── README.md
````

---

## ⚙️ Requirements

* Python 3.10+
* `opencv-python`
* `numpy`
* Raspberry Pi 5
* Pi Camera Module
* `picamera2` (for live camera input)

---

## 🛠️ Installation

1. **Clone the Repository**

```bash
git clone https://github.com/Talha-2/Autonomous-Driving-Using-Classical-Image-Processing-DIP.git
```

2. **Install Dependencies**

```bash
pip install opencv-python numpy
```

3. **Install PiCamera2 (for Raspberry Pi 5)**

```bash
sudo apt update
sudo apt install -y python3-picamera2
```

> ✅ `picamera2` is the official library for accessing Pi Camera on Raspberry Pi OS (Bullseye or newer).

4. **Hardware Setup**

* Connect a compatible **Pi Camera Module** to your Raspberry Pi.
* Enable the camera via:

  ```bash
  sudo raspi-config
  ```

  Go to `Interface Options` > `Camera` > Enable.
* Reboot the Pi.

---

## ▶️ Usage

### 🧪 Option 1: Run on Pre-recorded Video

> **File**: `main.ipynb`

1. Open in Jupyter Notebook
2. Upload or set path to a test video
3. Run all cells to:

   * Detect lanes (green lines)
   * Detect obstacles (red boxes)
   * Show driving decision text


<img width="831" height="485" alt="image" src="https://github.com/user-attachments/assets/880e5f0b-00cd-4c11-829e-4f39718af21c" />

### 📷 Option 2: Real-Time with Pi Camera

> **File**: `main_picam.ipynb`

1. Run this notebook directly on your Raspberry Pi
2. Captures live video using the Pi Camera
3. Displays real-time annotations and driving commands

💡 Use **VNC Viewer** or **SSH + X forwarding** to view the live OpenCV window remotely.

---

## 🧠 Methodology

### 🎞 Frame Capture + Multithreading

* Separate threads for:

  * Frame acquisition
  * Processing (lane + obstacle detection)
  * Visualization
* Keeps real-time performance smooth

### 🛣️ Lane Detection

* **Color Filtering (HSV)** → Detect yellow/white
* **Canny Edges** → Boundary extraction
* **Hough Transform** → Detect straight lines
* Classifies left/right based on slope

### 🚧 Obstacle Detection

* **MOG2** → Background subtraction
* **Morph ops** → Remove noise
* **Contours** → Draw red bounding boxes

### 🧭 Decision Making

* Based on lane center and obstacle positions:

  * Obstacle directly ahead → `STOP`
  * Obstacle on side → `STEER`
  * Safe → Continue

---

## ⚠️ Known Limitations

* Struggles in poor lighting or lane markings
* No semantic understanding like deep learning models
* Frame rate drops slightly with heavy processing on Pi

---

## 🚀 Future Enhancements

* Add LIDAR or ultrasonic sensors
* Optimize for faster FPS on Pi
* Hybrid pipeline (classical + lightweight DL)

---

