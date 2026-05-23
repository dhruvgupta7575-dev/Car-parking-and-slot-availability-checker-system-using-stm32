# Car Parking and Slot Availability Checker System using STM32

## Overview

This project implements a real-time smart parking monitoring system using an STM32F446RE Nucleo board and FreeRTOS. The system detects vehicle presence in parking slots using IR sensors and continuously updates slot availability through UART communication displayed on TeraTerm.

The project demonstrates important RTOS concepts such as:

- Task Management
- Priority Scheduling
- Inter-task Communication using Queues
- Real-Time Monitoring

---

# Features

- Real-time parking slot detection
- Empty slot counting
- UART-based live monitoring
- FreeRTOS multitasking implementation
- Queue-based inter-task communication
- Modular embedded system architecture

---

# Hardware Requirements

| Component                | Quantity    |
| ------------------------ | ----------- |
| STM32F446RE Nucleo Board | 1           |
| IR Sensors               | 2           |
| Jumper Wires             | As required |
| USB Cable                | 1           |
| PC with TeraTerm         | 1           |

---

# Software Requirements

- STM32CubeIDE
- STM32 CubeMX
- TeraTerm / PuTTY

---

# RTOS Concepts Used

| RTOS Concept         | Description                                                            |
| -------------------- | ---------------------------------------------------------------------- |
| Task Management      | Separate tasks created for sensing, processing, and UART communication |
| Priority Scheduling  | Different priorities assigned to tasks                                 |
| Queues               | Used for safe inter-task communication                                 |
| Real-Time Monitoring | Continuous slot status updates                                         |

---

# System Architecture

```text
IR Sensors
    ↓
SensorTask
    ↓
SensorQueue
    ↓
ManagerTask
    ↓
UARTQueue
    ↓
UARTTask
    ↓
TeraTerm Output
```

---

# Task Description

## 1. SensorTask

- Reads IR sensor values
- Detects occupied and empty slots
- Sends data to SensorQueue

Priority: High

---

## 2. ManagerTask

- Receives sensor data
- Calculates available parking slots
- Sends processed data to UARTQueue

Priority: Normal

---

## 3. UARTTask

- Receives processed parking data
- Displays output on TeraTerm using UART

Priority: Low

---

# Queue Description

## SensorQueue

Transfers data from:

```text
SensorTask → ManagerTask
```

---

## UARTQueue

Transfers data from:

```text
ManagerTask → UARTTask
```

---

# Pin Connections

| IR Sensor    | STM32 Pin |
| ------------ | --------- |
| Sensor 1 OUT | PA0       |
| Sensor 2 OUT | PA1       |
| VCC          | 5V        |
| GND          | GND       |

UART Communication:

- USART2 used for TeraTerm output
- Connected internally through ST-Link USB

---

# UART Configuration

| Parameter | Value  |
| --------- | ------ |
| Baud Rate | 115200 |
| Data Bits | 8      |
| Stop Bits | 1      |
| Parity    | None   |

---

# Example Output

```text
===== Parking Status =====
Slot 1 : Occupied
Slot 2 : Empty
Available Slots : 1
============================
```

---

# Project Workflow

1. IR sensors detect vehicle presence.
2. SensorTask reads sensor states.
3. Sensor data sent to SensorQueue.
4. ManagerTask processes parking status.
5. Processed data sent to UARTQueue.
6. UARTTask prints live data on TeraTerm.

---

# Folder Structure

```text
/Core
    ├── Inc
    ├── Src
    │   ├── main.c
    │   ├── freertos.c
    │   ├── stm32f4xx_it.c
    │   └── gpio.c
/Drivers
/Middlewares
README.md
```

---

# Future Improvements

- LCD/OLED display integration
- Automatic gate control using servo motor
- RFID-based vehicle authentication
- WiFi-based parking monitoring
- Mobile application integration
- Fire and safety monitoring
- Cloud dashboard support

---

# Learning Outcomes

Through this project, the following concepts were learned:

- STM32 GPIO interfacing
- Sensor interfacing
- UART communication
- FreeRTOS task management
- Queue-based inter-task communication
- Embedded system design
- Real-time monitoring systems

---

# Author

Dhruv Gupta

---

# License

This project is intended for educational and learning purposes.

