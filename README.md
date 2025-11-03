# SA-2

9.Write an assembly language program in 8051 to generate a 2 second delay using Timer 0 in Mode 1 and blink an LED connected to Port 3.7.


# AIM

To develop an 8051 microcontroller assembly program that uses Timer 0 in Mode 1 to generate a 2s delay using Timer 0 in mode 1 and LED connected to Port 3.7.

# APPARATUS REQUIRED

  1	       8051 Microcontroller            Used to execute the program                        
  2	       LED	                            Connected to Port 3.7 (P3.7) to indicate blinkin   
  3	       Resistor (330Ω – 1kΩ)           Current limiting resistor for LED                  
  4	       Connecting wires /              For connections                                    
             Breadboard           
  5	       Power Supply (5V DC)            To power the 8051 circuit                          
  6	       Keil µVision Software           For writing and simulating the assembly program    
  7	       Proteus Software	            For circuit simulation and observation of LED                                                  blinking

# ALGORITHM
1. Start the Program

2. Initialize Port 3 as Output:
   Configure Port 3 to connect LED on bit P3.7.

3. Configure Timer 0:
         Set Timer 0 in Mode 1 (16-bit timer mode).
         → TMOD = 01H
         Load the timer registers TH0 and TL0 with initial values to generate delay.

4. Turn ON the LED:
      Make P3.7 = 1.

5. Call Delay Subroutine:
        Start Timer 0 and wait until the overflow flag (TF0) is set.
        Stop timer and clear TF0 flag.
        Repeat timer cycle enough times to create a total 2-second delay.

6. Turn OFF the LED:
       Make P3.7 = 0.

7. Call Delay Subroutine Again:
       Delay for another 2 seconds (LED remains OFF).

8. Repeat the Process Continuously (Infinite loop).

9. End Program

# PROGRAM

```
ORG 0000H

MAIN:
    MOV TMOD, #01H      ; Timer 0, Mode 1 (16-bit)
AGAIN:
    CPL P3.7             ; Toggle LED
    ACALL DELAY
    SJMP AGAIN

DELAY:
    MOV R7, #20          ; 20 × 100 ms = 2 seconds
DELAY_LOOP:
    MOV TH0, #0B1H
    MOV TL0, #0E0H
    SETB TR0
WAIT:
    JNB TF0, WAIT
    CLR TR0
    CLR TF0
    DJNZ R7, DELAY_LOOP
    RET

END
```
# OUTPUT:
![WhatsApp Image 2025-11-03 at 11 18 41_8c074218](https://github.com/user-attachments/assets/59524781-d946-4e66-8cee-75bb15062966)



# RESULT:

Successfully designed and verified an 8051 Assembly program to blink an LED at Port 3.7 with a precise 2s interval using Timer 0 in Mode 1. Demonstrated timer initialization, delay loop, and I/O port manipulation in 8051 Assembly.
