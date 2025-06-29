# STM32 SPI Sensor Reader with UART Output and Moving Average Filter

This is a beginner-friendly project I built using the STM32F103C8T6 development board. My goal was to read sensor data via SPI using an external ADC, filter the data to reduce noise, and then send the result to a PC using UART for visualization or logging.

---

##  What This Project Does

- Reads analog input from a sensor connected to the **MCP3008**, an SPI-based 10-bit ADC.
- Uses **SPI communication** to talk to the MCP3008.
- Applies a **10-point moving average filter** to smooth out the raw sensor readings.
- Sends the filtered data through **UART** at 9600 baud to any serial terminal.
- Intended for sensors like NTC thermistors, voltage dividers, or similar analog outputs.

---

##  What I Used

- **STM32F103C8T6 (Blue Pill)**  the main microcontroller
- **MCP3008**  8-channel, 10-bit SPI ADC
- **NTC Thermistor** or analog voltage source 
- **USB to Serial converter** 
- Breadboard, resistors , jumper wires, etc.
- **STM32CubeIDE** 
- **HAL Drivers**  I used STM32’s Hardware Abstraction Layer for easier SPI and UART handling

---

##  How It Works

1. **Analog Sensor Reading**  
   The sensor changes voltage based on temperature or other conditions. This analog voltage is fed into MCP3008 on channel 0.

2. **SPI Communication**  
   The STM32 communicates with MCP3008 over SPI to read the digital value.

3. **Filtering the Data**  
   I noticed raw sensor readings can jump around a bit. So I implemented a simple moving average filter using the last 10 values to make the output more stable.

4. **UART Transmission**  
   Every 500 ms, the filtered value is formatted as text and sent via UART to the computer. You can see the values live in a serial terminal.

---

##  How to Use

1. Clone or download this repo
2. Open it in **STM32CubeIDE**
3. Connect your hardware as follows:

| Pin | Function | Notes |
|-----|----------|-------|
| PA5 | SPI1_SCK | Clock to MCP3008 |
| PA6 | SPI1_MISO | Data from MCP3008 |
| PA7 | SPI1_MOSI | Data to MCP3008 |
| PA4 | CS (GPIO Output) | Manually controlled chip select |
| PA9 | USART1_TX | To USB-Serial TX |
| PA10 | USART1_RX | (optional) |

5. Flash the code to your STM32 board
6. Open a serial terminal on your PC at **9600 baud**, 8N1
7. See filtered ADC values printing every 0.5 seconds 

---

