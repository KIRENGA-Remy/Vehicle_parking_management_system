# Automated License Plate Recognition & Parking Gate Control System

This project is a real-time **ANPR (Automatic Number Plate Recognition)** system using YOLOv8 and Tesseract OCR for recognizing plate numbers and controlling a physical gate (via Arduino). It also logs the entry and calculates the parking fee based on the time a vehicle spends before exiting.

---

## 🔧 Features

- Real-time number plate detection using YOLOv8
- Optical Character Recognition (OCR) with Tesseract
- Automatic gate control via Arduino
- Entry logging in a CSV file
- Charge calculation based on parking duration
- Windows 11 compatible

---

## 📁 Project Structure

project/
│
├── best.pt # Trained YOLOv8 model for license plates
├── plates/ # Directory where plate images are saved
├── plates_log.csv # CSV log file for plate entries
├── entry_gate.py # Entry control script
├── exit_gate.py # Exit control & charge calculation script (not shown here)
└── README.md # This file

yaml

---

## ✅ Requirements

- Windows 11 OS
- Python 3.8+
- Webcam
- Arduino board (e.g., Uno) with USB connection
- Ultrasonic sensor connected to Arduino
- YOLOv8 pretrained weights (`best.pt`)
- Tesseract OCR installed and configured

---

## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/KIRENGA-Remy/Vehicle_parking_management_system.git.git
cd Vehicle_parking_management_system
2. Install Python dependencies
Make sure you have Python installed, then run:

bash
Copy
Edit
pip install -r requirements.txt
requirements.txt should include:

nginx
Copy
Edit
ultralytics
opencv-python
pytesseract
pyserial
3. Install and configure Tesseract OCR
Download and install from:
🔗 https://github.com/tesseract-ocr/tesseract

After installing, add its path (e.g., C:\Program Files\Tesseract-OCR) to your system's Environment Variables > Path.

Set the Tesseract path in your script if needed:

pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
4. Prepare YOLOv8 model
Make sure you have a trained best.pt file placed in the project root.
Train your own model using Ultralytics if needed.

🖥️ Running the Entry System
Run the script for vehicle entry:


python entry_gate.py
When a vehicle approaches (detected via ultrasonic), the system will:

Detect and validate license plates

Log the plate in plates_log.csv

Trigger Arduino to open/close the gate

💸 Running the Exit & Billing System
⚠️ You mentioned this part is under development. Ensure you have a script like exit_gate.py.

That script should:

Detect the same vehicle again

Find its entry time from plates_log.csv

Calculate the time difference

Display or log the amount to be charged

Trigger gate opening once payment is confirmed

Let me know if you want me to help write this script too!

⚙️ Arduino Configuration
Your Arduino sketch should handle gate opening based on serial commands:

void setup() {
  pinMode(8, OUTPUT);  // Gate control pin
  Serial.begin(9600);
}

void loop() {
  if (Serial.available()) {
    char cmd = Serial.read();
    if (cmd == '1') {
      digitalWrite(8, HIGH);  // Open gate
    } else if (cmd == '0') {
      digitalWrite(8, LOW);   // Close gate
    }
  }
}
🪟 Windows 11 Configuration Notes
Ensure Tesseract is in PATH: Go to System Properties > Environment Variables and add the installation path.

Allow Python in Windows Defender Firewall if using camera or serial port.

Run Python as Administrator if needed to access hardware.

Check Arduino COM port: Use Device Manager to confirm the COM port number. The script auto-detects it.

📊 Example Output

[SENSOR] Distance: 40 cm
[VALID] Plate Detected: RAB123C
[SAVED] RAB123C logged to CSV.
[GATE] Opening gate (sent '1')
...
[GATE] Closing gate (sent '0')
🧾 License
This project is open-source and available under the MIT License.

✉️ Contact
Created by GITOLI Remy Claudien
Feel free to reach out at gitoliremy@gmail.com for collaboration or questions.

Happy coding! ❤️