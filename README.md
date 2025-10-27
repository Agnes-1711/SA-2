# SA-2

2.Write an assembly language program in 8051 to generate a 10 ms delay using Timer 1 in Mode 1 and toggle an LED connected to Port 1.0 continuously.

# AIM

To develop an 8051 microcontroller assembly program that uses Timer 1 in Mode 1 to generate a 10 ms delay and toggles an LED connected to Port 1.0. 8051.

# APPARATUS REQUIRED

8051 Microcontroller Trainer Kit (or simulator like Keil uVision, Proteus, or 8051 IDE) LED (connected to Port 2.0) 10kΩ Resistor (as current limiter) Connecting Wires & Breadboard (for practical hardware) Computer with IDE/Assembler for code development and simulation.

# ALGORITHM

Set Port 1.0 as an output by initializing it low (P1.0 = 0). Configure Timer 1 in Mode.Load Timer 1 registers with TH1 = 0xDC and TL1 = 0x00 to obtain a 10 ms delay at 12 MHz. Clear TF1, start Timer 1 (TR1 = 1), and wait until TF1 becomes 1. Stop Timer 1 (TR1 = 0) and clear TF1. Toggle the state of Port 1.0 (P1 ^= 0x01). Repeat the delay and toggle steps indefinitely inside the main loop.

# PROGRAM

```
#include <reg51.h>   // 8051 register definitions

void delay(void);    // Function prototype

void main(void)
{
    P1 = 0x00;       // Initialize Port 1
    TMOD = 0x10;     // Timer1 in Mode 1 (16-bit timer)

    while(1)
    {
        P1 = 0xFF;   // Turn ON all LEDs
        delay();     // 10 ms delay
        P1 = 0x00;   // Turn OFF all LEDs
        delay();     // 10 ms delay
    }
}

void delay(void)
{
    TH1 = 0xD8;      // High byte for 10 ms delay
    TL1 = 0xF0;      // Low byte for 10 ms delay
    TR1 = 1;         // Start Timer 1

    while (TF1 == 0); // Wait until overflow flag is set

    TR1 = 0;         // Stop Timer 1
    TF1 = 0;         // Clear overflow flag
}
```
# OUTPUT:

<img width="1920" height="1200" alt="Screenshot 2025-10-27 231323" src="https://github.com/user-attachments/assets/b83400a3-ae40-4b7b-9ce7-d55304fdeb5b" />

# RESULT:

Successfully designed and verified an 8051 Assembly program to toggle an LED at Port 1.0 with a precise 10 ms interval using Timer 1 in Mode 1. Demonstrated timer initialization, delay loop, and I/O port manipulation in 8051 Assembly.
