# RTOS-Based Program for STM32F1

This project is an RTOS-based firmware designed for the STM32F1 series microcontroller. It uses the CMSIS-RTOS and HAL libraries for managing tasks, peripherals, and hardware abstraction. The program includes functionality to read inputs from a pushbutton and a potentiometer (via ADC) and send data to a PC through the serial interface.

[https://github.com/dennysyahrul393/RTOS/issues/1#issue-2588567143](https://github.com/user-attachments/assets/e6b1eea9-81e5-47cf-9426-f17d77986757)

## Features
- **FreeRTOS**: A real-time operating system to manage multiple tasks.
- **Pushbutton and ADC (Potentiometer)**: Reads input from a physical pushbutton and a potentiometer (using ADC).
- **Serial Communication**: Outputs readings from the pushbutton and ADC to the PC via UART/Serial.
- **Peripheral Management**: HAL (Hardware Abstraction Layer) for STM32F1 peripherals such as timers, GPIO, ADC, UART, etc.

## Project Structure

```plaintext
RTOS_test2/
│
├── Core/
│   ├── Inc/              # Header files
│   ├── Src/              # Source files (main.c, freertos.c, etc.)
│   └── Startup/          # Initialization files for the STM32
│
├── Drivers/              # STM32 HAL Drivers
│
├── Middlewares/          # FreeRTOS and other middleware
│
├── .project              # Eclipse project file
├── STM32F103C8TX_FLASH.ld # Linker script
└── RTOS_test2.ioc        # Configuration file for STM32CubeMX
```

## Main Components

### `main.c`
This is the entry point of the application. It initializes the system, configures the peripherals, and starts the FreeRTOS scheduler.

Key sections include:
- **System Initialization**: Initial setup of the STM32 hardware.
- **Task Creation**: FreeRTOS tasks are created to handle different parts of the application.
- **Pushbutton and ADC Handling**: A task is responsible for reading the state of the pushbutton and the ADC value of the potentiometer.
- **Serial Communication**: The values of the pushbutton state and the potentiometer ADC readings are sent to the PC via UART for monitoring on the serial terminal.
- **OLED Display Handling**: The SSD1306 driver is used to manage the OLED display.

### `freertos.c`
This file contains the FreeRTOS-related code, including task definitions and the RTOS setup. It creates and schedules tasks to handle the pushbutton, ADC reading, and communication tasks.

### `ssd1306.c`
This file implements the driver for the SSD1306 OLED display. It handles the communication with the display and allows you to render text and graphics.

### `stm32f1xx_it.c`
Contains the interrupt handlers for the STM32F1 microcontroller.

### Pushbutton and Potentiometer (ADC) Integration
- **Pushbutton**: A digital input pin is used to read the state of a pushbutton (pressed or not pressed).
- **Potentiometer**: The analog input is connected to a potentiometer, and the ADC is used to convert the analog value to a digital one.
- **UART Communication**: The ADC value and pushbutton status are sent over UART/serial to a PC, allowing the data to be viewed in a terminal program (like PuTTY or Tera Term).

## Getting Started

1. **Prerequisites**:
   - STM32CubeMX
   - STM32CubeIDE or any other IDE supporting STM32 development
   - STM32 HAL and FreeRTOS libraries (included)
   - UART-to-USB cable for connecting STM32 to a PC for serial communication

2. **Building the Project**:
   - Open the `.ioc` file in STM32CubeMX to review and regenerate code.
   - Build the project using STM32CubeIDE.

3. **Flashing the Microcontroller**:
   - Use the built-in programmer or an external ST-Link to flash the binary onto the STM32F1 device.

4. **Running the Program**:
   - Connect the STM32F1 to your PC via UART/USB.
   - Open a serial terminal (like PuTTY or Tera Term) on your PC.
   - Set the baud rate to match the UART configuration in the firmware (typically 115200 bps).
   - Observe the pushbutton state and potentiometer readings displayed in the terminal.
