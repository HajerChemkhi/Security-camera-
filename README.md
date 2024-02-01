# Raspberry Pi Security Camera with Ultrasonic Sensor

This project uses a Raspberry Pi along with a camera module and an ultrasonic sensor to create a simple security system. When motion is detected by the ultrasonic sensor, the Raspberry Pi captures a photo using the camera module and sends it to a specified email address via SMTP.

## Requirements

- Raspberry Pi (tested on Raspberry Pi 3 Model B+)
- Raspberry Pi Camera Module
- Ultrasonic Sensor (HC-SR04)
- Python 3
- RPi.GPIO library
- picamera library
- smtplib library

## Installation

1. Connect the Ultrasonic Sensor and Camera Module to the Raspberry Pi.
2. Clone this repository to your Raspberry Pi:

   ```bash
   git clone https://github.com/YourGitHubUsername/rpi-security-camera.git
