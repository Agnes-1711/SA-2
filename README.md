# SA-2

2.Write an assembly language program in 8051 to generate a 5 second delay using Timer 0 in Mode 1 and toggle Port 2.7 continuously.

# AIM

To develop an 8051 microcontroller assembly program that uses Timer 0 in Mode 1 to generate a 10 ms delay and toggles an LED connected to Port 2.7. 8051.

# APPARATUS REQUIRED
8051 Microcontroller Trainer Kit (or simulator such as Keil µVision, Proteus, or 8051 IDE).LED (connected to Port 2.7).10kΩ Resistor (current limiting resistor)
.Connecting wires and breadboard (for hardware setup).Computer with IDE/Assembler for program development and simulation

# ALGORITHM

Initialize Port 2 as output by writing 00H to it.Configure Timer 0 in Mode 1 (16-bit timer mode) by loading the TMOD register with 01H.Load TH0 and TL0 registers with suitable values to generate a delay of approximately 50 ms (since 5 s is too long for a single timer overflow, we will repeat the 50 ms delay 100 times).Clear TF0 (Timer 0 overflow flag) and start Timer 0 (SETB TR0).Wait until TF0 = 1 (polling).Stop Timer 0 (CLR TR0) and clear TF0 (CLR TF0).Repeat the delay loop 100 times to achieve approximately 5 seconds total delay.Toggle Port 2.7 using CPL P2.7.Go back to step 3 and repeat the process indefinitely.

# PROGRAM

```
ORG 0000H

MAIN:   
    MOV P2, #00H          ; Initialize Port 2 as output (all low)

HERE:
    ACALL DELAY5S         ; Call 5-second delay
    CPL P2.7              ; Toggle bit 7 of Port 2
    SJMP HERE             ; Repeat forever

;-----------------------------
; SUBROUTINE: 5-second delay
;-----------------------------
DELAY5S:
    MOV R7, #76            ; 76 overflows × ~65.536 ms ˜ 5 sec

REPEAT:
    MOV TMOD, #01H         ; Timer 0 Mode 1 (16-bit)
    MOV TH0, #00H          ; High byte
    MOV TL0, #00H          ; Low byte
    SETB TR0               ; Start Timer 0

WAIT_OV:
    JNB TF0, WAIT_OV       ; Wait until Timer 0 overflows
    CLR TR0                ; Stop Timer
    CLR TF0                ; Clear overflow flag
    DJNZ R7, REPEAT        ; Repeat until 76 overflows done

    RET                    ; Return to main

END
```
# OUTPUT:

![WhatsApp Image 2025-10-27 at 20 44 33_af233862](https://github.com/user-attachments/assets/a1ae418a-bffa-44b3-a237-e2952edfd91e)

![WhatsApp Image 2025-10-27 at 20 45 00_8f6eb105](https://github.com/user-attachments/assets/7490fd43-4169-46e0-b459-294780041d5f)


# RESULT:

Successfully designed and verified an 8051 Assembly program to toggle an LED at Port 2.7 with a precise 5s interval using Timer 0 in Mode 1. Demonstrated timer initialization, delay loop, and I/O port manipulation in 8051 Assembly.
