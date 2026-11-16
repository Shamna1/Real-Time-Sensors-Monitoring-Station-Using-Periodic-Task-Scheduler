# Real-Time-Sensors-Monitoring-Station-Using-Periodic-Task-Scheduler

An embedded systems project developed using the **LPC2129 ARM7 microcontroller** to monitor environmental and safety parameters such as temperature, light intensity, voltage, vibration, and flame. The system uses **Timer0 interrupts for periodic scheduling** and displays sensor information on a terminal through **UART communication**, with LED/buzzer alerts.

## Project Overview

The Real-Time Sensor Monitoring Station is designed to monitor multiple sensor inputs, process the collected data, and provide real-time status updates.

The system consists of three main stages:

* **Input Stage:** Temperature sensor, LDR, potentiometer, vibration sensor, and flame sensor.
* **Processing Stage:** LPC2129 microcontroller acquires sensor data, processes readings, and checks alert conditions.
* **Output Stage:** Displays sensor readings on a computer terminal through UART communication and provides local alerts using LED/buzzer.

## System Architecture & Components

| Component | Signal Type | Function |
| :--- | :--- | :--
| **LPC2129 Microcontroller** | Controller | Processes sensor inputs and controls the monitoring system. |
| **Temperature Sensor** | Analog (ADC) | Measures temperature in Celsius. |
| **LDR Sensor** | Analog (ADC) | Measures ambient light intensity. |
| **Potentiometer** | Analog (ADC) | Provides a variable voltage input. |
| **Vibration Sensor** | Digital (GPIO) | Detects mechanical vibration. |
| **Flame Sensor** | Digital (GPIO) | Detects flame presence. |
| **UART0** | Serial Communication | Transmits sensor information to the Linux terminal. |
| **LED / Buzzer** | Digital Output | Provides visual and audible alerts. |

---

## Working Principle

1. **Sensor Input:** Sensors generate analog voltage signals or digital logic signals.
2. **Periodic Scheduling:** Timer0 generates a periodic 1-second interrupt.
3. **Data Acquisition:** The LPC2129 reads analog sensor values through ADC and digital sensor states through GPIO.
4. **Data Processing:** The microcontroller converts raw ADC values into meaningful readings and checks the required conditions.
5. **Alert Generation:** LED and buzzer outputs provide alerts when configured conditions are detected.
6. **UART Communication:** Processed sensor information is transmitted to the  terminal using UART0.

---

## Periodic Task Scheduling

Timer0 is configured to generate a 1-second timing reference.

The periodic monitoring schedule is:

| Sensor | Monitoring Interval |
| :--- | :--- |
| Temperature | Every 1 second |
| LDR | Every 2 seconds |
| Potentiometer | Every 3 seconds |
| Flame Sensor | Every 3 seconds |
| Vibration Sensor | Every 3 seconds |

Flame and vibration sensors are monitored together at the 4-second interval.

The Timer0 interrupt service routine updates the timing flag/counter, while sensor acquisition, processing, and UART transmission are performed in the main program loop.

---

## Communication Interface

**UART0** is used for serial communication between the LPC2129 microcontroller and the computer.

The sensor readings are transmitted through UART0 and displayed in the terminal.

**Baud Rate:** 9600 bps

---

## Repository Structure

```text
Real-Time-Sensors-Monitoring-Station/
│
├── main.c
├── header.h
├── adc_driver.c
├── uart0_driver.c
├── timer_interrupt_driver.c
└── README.md
```

---

## Sample Terminal Output

```text
TEMP: 28 C
LIGHT: 50%
VTG: 3.3 V
VIBRATIONS: NO
FLAME: NO
```



---

## Technologies Used

* Embedded C
* LPC2129 ARM7 Microcontroller
* ADC (Analog-to-Digital Converter)
* GPIO (General Purpose Input/Output)
* Timer0 Interrupt
* UART0 Serial Communication
* Keil µVision IDE
* Terminal

---

## Design Considerations & Future Enhancements

* Periodic monitoring is performed using Timer0 interrupts.
* The interrupt service routine is kept short to maintain predictable execution.
* Sensor readings are processed in the main loop.
* Periodic checking of flame and vibration sensors may miss short events occurring between scans.

### Future Enhancements

* Implement external interrupts for faster flame and vibration detection.
* Add data logging to store sensor readings.
* Introduce configurable alert thresholds.
* Develop a graphical dashboard for real-time sensor monitoring.
* Improve alert response time.

---

## Conclusion

The Real-Time Sensor Monitoring Station demonstrates the integration of multiple analog and digital sensors with the LPC2129 microcontroller. It uses ADC, GPIO, Timer0 interrupts, and UART communication to perform periodic sensor monitoring and display the collected information on a terminal.
