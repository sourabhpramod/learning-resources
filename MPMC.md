### MODULE 4


Timers and counters are essential components of the 8051 microcontroller, used for timing operations and event counting. The 8051 has two 16-bit timers/counters, Timer 0 and Timer 1, which can operate in different modes. These timers can be used to generate time delays, count external events, or generate baud rates for serial communication.

### Timer/Counter Overview

1. **Timer/Counter Registers**:
   - **TH0/TL0**: Timer 0 High and Low registers.
   - **TH1/TL1**: Timer 1 High and Low registers.
   - These registers hold the 16-bit count value.

2. **TMOD (Timer Mode) Register**:
   The TMOD register controls the operation mode of Timer 0 and Timer 1. It's an 8-bit register, with the higher nibble controlling Timer 1 and the lower nibble controlling Timer 0.

   ```
   TMOD: GATE C/T M1 M0 GATE C/T M1 M0
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            |    |   |   |    |   |   |
            7----6---5---4----3---2---1---0
   ```

   - **GATE**: Gating control when set, timer/counter is enabled while the INTx pin is high and TRx control bit is set.
   - **C/T**: Timer or Counter select bit.
     - `0` for Timer operation (internal clock).
     - `1` for Counter operation (external clock on T0/T1 pins).
   - **M1, M0**: Mode selection bits.
     - `00` - Mode 0 (13-bit timer/counter).
     - `01` - Mode 1 (16-bit timer/counter).
     - `10` - Mode 2 (8-bit auto-reload).
     - `11` - Mode 3 (Split timer mode).

3. **TCON (Timer Control) Register**:
   The TCON register is used to control the operation of the timers/counters and to check their status.

   ```
   TCON: TF1 TR1 TF0 TR0 IE1 IT1 IE0 IT0
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           |   |   |   |   |   |   |   |
           7---6---5---4---3---2---1---0
   ```

   - **TF1**: Timer 1 overflow flag.
   - **TR1**: Timer 1 run control bit.
   - **TF0**: Timer 0 overflow flag.
   - **TR0**: Timer 0 run control bit.
   - **IE1, IT1, IE0, IT0**: Interrupt flags and controls.

### Modes of Operation

1. **Mode 0 (13-bit Timer/Counter)**:
   - Timer operates as a 13-bit counter, where TLx holds the lower 5 bits, and THx holds the upper 8 bits. The upper 3 bits of TLx are ignored.

2. **Mode 1 (16-bit Timer/Counter)**:
   - Timer operates as a 16-bit counter. Both THx and TLx are used as a single 16-bit counter.

3. **Mode 2 (8-bit Auto-Reload Timer/Counter)**:
   - Timer operates as an 8-bit counter with auto-reload. The value in THx is loaded into TLx when TLx overflows.

4. **Mode 3 (Split Timer Mode)**:
   - Timer 0 is split into two 8-bit timers: TL0 and TH0. Timer 1 continues to operate in its normal mode.

### Assembly Programs Using Timers

Here are a few basic examples of assembly programs using Timer 0.

#### Example 1: Simple Delay Using Timer 0 in Mode 1

This program creates a simple delay using Timer 0 in Mode 1.

```assembly
ORG 0000H       ; Origin
MOV TMOD, #01H  ; Set Timer 0 in Mode 1 (16-bit timer)
MOV TH0, #3CH   ; Load high byte (initial count value)
MOV TL0, #0B0H  ; Load low byte (initial count value)
SETB TR0        ; Start Timer 0

HERE: JNB TF0, HERE  ; Wait here until Timer 0 overflows
CLR TR0        ; Stop Timer 0
CLR TF0        ; Clear overflow flag
SJMP HERE      ; Repeat
END
```

#### Example 2: Generating a Square Wave Using Timer 0 in Mode 2

This program generates a square wave on P1.0 using Timer 0 in Mode 2.

```assembly
ORG 0000H       ; Origin
MOV TMOD, #02H  ; Set Timer 0 in Mode 2 (8-bit auto-reload)
MOV TH0, #0F3H  ; Load TH0 with reload value for desired frequency
SETB TR0        ; Start Timer 0

TOGGLE: CPL P1.0 ; Toggle P1.0
HERE: JNB TF0, HERE  ; Wait here until Timer 0 overflows
CLR TF0        ; Clear overflow flag
SJMP TOGGLE    ; Repeat

END
```

#### Example 3: Counting External Events Using Timer 0 in Mode 1

This program counts the number of external pulses on pin T0.

```assembly
ORG 0000H       ; Origin
MOV TMOD, #05H  ; Set Timer 0 in Mode 1 (16-bit counter mode)
SETB TR0        ; Start Timer 0

CHECK: MOV A, TL0  ; Read low byte of Timer 0
      MOV B, TH0  ; Read high byte of Timer 0
      ; Process count value as needed
SJMP CHECK

END
```


Timer 0 in the 8051 microcontroller can operate in four different modes: Mode 0, Mode 1, Mode 2, and Mode 3. Each mode configures the timer to behave differently based on the application requirements. Here is a detailed explanation of each mode:

### 1. **Mode 0 (13-bit Timer/Counter)**
   - **Operation**: In Mode 0, Timer 0 functions as a 13-bit timer/counter. The lower 5 bits of `TL0` (Timer Low Byte) and all 8 bits of `TH0` (Timer High Byte) are used.
   - **Configuration**:
     - **TMOD Register**: `M1 = 0`, `M0 = 0` for Timer 0.
   - **Counting Range**: The timer can count from `0000H` to `1FFFH` (13-bit).
   - **Use Case**: This mode is rarely used because of the limited 13-bit range.
   - **Example**:
     ```
     TH0 (8 bits) | TL0 (5 bits) | Overflow
        XXH         XXXXX         -> TF0 Set (Overflow)
     ```

### 2. **Mode 1 (16-bit Timer/Counter)**
   - **Operation**: In Mode 1, Timer 0 functions as a 16-bit timer/counter. Both `TL0` and `TH0` are used as a combined 16-bit register.
   - **Configuration**:
     - **TMOD Register**: `M1 = 0`, `M0 = 1` for Timer 0.
   - **Counting Range**: The timer can count from `0000H` to `FFFFH` (65536 counts).
   - **Use Case**: This mode is commonly used for generating longer time delays and event counting.
   - **Example**:
     ```
     TH0 (8 bits) | TL0 (8 bits) | Overflow
        XXH         XXH          -> TF0 Set (Overflow)
     ```

### 3. **Mode 2 (8-bit Auto-Reload Timer/Counter)**
   - **Operation**: In Mode 2, Timer 0 functions as an 8-bit timer with auto-reload. The `TH0` register is loaded with a value, which is then copied into `TL0` every time it overflows. This allows the timer to automatically reload a value after every overflow.
   - **Configuration**:
     - **TMOD Register**: `M1 = 1`, `M0 = 0` for Timer 0.
   - **Counting Range**: The timer counts from the value in `TL0` (8 bits) up to `FFH` (256 counts). After `FFH`, `TL0` is reloaded with the value from `TH0`.
   - **Use Case**: This mode is useful for generating periodic interrupts, square waves, or baud rate generation in serial communication.
   - **Example**:
     ```
     TH0 = Reload Value -> TL0 counts from TH0 to FFH -> Overflow -> Reload from TH0
     ```

### 4. **Mode 3 (Split Timer Mode)**
   - **Operation**: In Mode 3, Timer 0 is split into two independent 8-bit timers: `TL0` and `TH0`. `TL0` operates as an 8-bit timer, while `TH0` is treated as a separate 8-bit timer. Timer 1 can still function in Modes 0, 1, or 2.
   - **Configuration**:
     - **TMOD Register**: `M1 = 1`, `M0 = 1` for Timer 0.
   - **Counting Range**: Each 8-bit timer counts independently from `00H` to `FFH`.
   - **Use Case**: Mode 3 is used when two separate 8-bit timers are needed. For example, `TL0` can be used for generating baud rates, while `TH0` can be used for generating time delays.
   - **Example**:
     ```
     TL0: Independent 8-bit Timer | TH0: Independent 8-bit Timer
     ```

### Summary of Timer 0 Modes

| Mode | Operation Description                     | TMOD Configuration (M1, M0) | Counting Range | Use Case                                         |
|------|-------------------------------------------|-----------------------------|----------------|------------------------------------------------|
| 0    | 13-bit Timer/Counter                       | (0, 0)                      | 0000H to 1FFFH | Limited range applications, rarely used         |
| 1    | 16-bit Timer/Counter                       | (0, 1)                      | 0000H to FFFFH | Common for longer delays and event counting     |
| 2    | 8-bit Auto-Reload Timer/Counter            | (1, 0)                      | 00H to FFH     | Periodic interrupts, baud rate generation       |
| 3    | Split Timer Mode (Two Independent 8-bit)   | (1, 1)                      | 00H to FFH     | Applications requiring two separate 8-bit timers|

These modes provide flexibility for various applications, from simple time delays to complex pulse generation and event counting.




### Applications

- **Delay Generation**: Timers can be used to create precise time delays for tasks.
- **Event Counting**: When used as counters, they count external events like pulses.
- **Pulse Width Modulation (PWM)**: Timers can generate PWM signals for controlling devices like motors.
- **Baud Rate Generation**: Timers can be used to generate baud rates for serial communication.

Understanding how to configure and use timers/counters in the 8051 microcontroller is essential for implementing time-dependent operations in embedded systems.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Serial Communication

Serial communication in the 8051 microcontroller is an essential feature for transferring data between the microcontroller and external devices such as other microcontrollers, computers, or sensors. It uses the UART (Universal Asynchronous Receiver/Transmitter) protocol for serial data communication.

### Basics of Serial Communication in 8051

1. **Serial Data Transmission**:
   - **Asynchronous Communication**: Data is sent and received without any clock signal. Instead, start and stop bits are used for synchronization.
   - **Full-Duplex Mode**: Data can be transmitted and received simultaneously using the TxD (P3.1) and RxD (P3.0) pins.

2. **Special Function Registers Involved**:
   - **SBUF (Serial Buffer Register)**:
     - 8-bit register used for both transmission and reception.
     - Writing data to SBUF loads it for transmission.
     - Reading from SBUF gets the received data.
   - **SCON (Serial Control Register)**:
     - Controls the operation of serial communication.
     - Configures the mode of operation, baud rate, and other control settings.
   - **PCON (Power Control Register)**:
     - Contains the SMOD bit, which doubles the baud rate when set.

3. **SCON Register Configuration**:
   The SCON register is 8 bits and controls the mode of operation, data reception, and transmission status.

   ```
   SCON: SM0 SM1 SM2 REN TB8 RB8 TI RI
          |   |   |   |   |  |  |  |
          |   |   |   |   |  |  |  |
          |   |   |   |   |  |  |  |
          |   |   |   |   |  |  |  |
          7   6   5   4   3  2  1  0
   ```

   - **SM0, SM1**: Select the mode of operation.
   - **SM2**: Multiprocessor communication (not commonly used).
   - **REN**: Receiver enable bit. When set, enables reception.
   - **TB8**: 9th bit for transmission in 9-bit modes (Mode 2 and Mode 3).
   - **RB8**: 9th bit for reception in 9-bit modes (Mode 2 and Mode 3).
   - **TI (Transmit Interrupt Flag)**: Set when data has been transmitted.
   - **RI (Receive Interrupt Flag)**: Set when data has been received.

4. **Serial Communication Modes**:
   The 8051 supports four modes of serial communication:

   | Mode | Operation Description                              | Baud Rate                                      |
   |------|----------------------------------------------------|------------------------------------------------|
   | 0    | 8-bit Shift Register (Synchronous)                 | Fosc/12                                        |
   | 1    | 8-bit UART (Variable Baud Rate)                    | Timer 1 controls the baud rate                 |
   | 2    | 9-bit UART (Fixed Baud Rate)                       | Fosc/64 (SMOD = 0) or Fosc/32 (SMOD = 1)       |
   | 3    | 9-bit UART (Variable Baud Rate)                    | Timer 1 controls the baud rate                 |

### Mode Details

1. **Mode 0 (Synchronous 8-bit Shift Register)**:
   - Data is transmitted and received through the TxD pin.
   - The clock signal is provided on the TxD pin.
   - Baud rate is fixed at Fosc/12.

2. **Mode 1 (8-bit UART, Variable Baud Rate)**:
   - 8-bit data is transmitted with a start and stop bit.
   - Baud rate is determined by Timer 1.
   - Commonly used for standard UART communication.

3. **Mode 2 (9-bit UART, Fixed Baud Rate)**:
   - 9-bit data is transmitted with a start and stop bit.
   - The 9th bit is often used for multiprocessor communication.
   - Baud rate is fixed at Fosc/64 or Fosc/32, depending on the SMOD bit in the PCON register.

4. **Mode 3 (9-bit UART, Variable Baud Rate)**:
   - Similar to Mode 2, but the baud rate is variable and controlled by Timer 1.

### Baud Rate Calculation for Mode 1 and Mode 3

For Modes 1 and 3, the baud rate is generated by Timer 1, which is set in 8-bit auto-reload mode (Mode 2). The formula for calculating the baud rate is:

\[ \text{Baud Rate} = \frac{\text{Oscillator Frequency}}{12 \times (256 - \text{TH1})} \]

If the SMOD bit in the PCON register is set to 1, the baud rate is doubled:

\[ \text{Baud Rate} = \frac{\text{Oscillator Frequency}}{32 \times (256 - \text{TH1})} \]

### Assembly Programs for Serial Communication

#### Example 1: Transmitting Data in Mode 1

This program continuously sends the character "A" over serial communication.

```assembly
ORG 0000H          ; Start of code
MOV TMOD, #20H     ; Set Timer 1 in Mode 2 (8-bit auto-reload)
MOV TH1, #0FDH     ; Load TH1 for 9600 baud rate (11.0592 MHz crystal)
MOV SCON, #50H     ; Set Serial Mode 1 (8-bit UART) and enable receiver
SETB TR1           ; Start Timer 1

SEND: MOV SBUF, #'A' ; Load 'A' into the buffer
WAIT: JNB TI, WAIT   ; Wait until transmission is complete (TI = 1)
CLR TI              ; Clear TI for next transmission
SJMP SEND           ; Repeat sending 'A'
END
```

#### Example 2: Receiving Data in Mode 1

This program waits to receive a character and then sends it back (echo).

```assembly
ORG 0000H          ; Start of code
MOV TMOD, #20H     ; Set Timer 1 in Mode 2 (8-bit auto-reload)
MOV TH1, #0FDH     ; Load TH1 for 9600 baud rate (11.0592 MHz crystal)
MOV SCON, #50H     ; Set Serial Mode 1 (8-bit UART) and enable receiver
SETB TR1           ; Start Timer 1

HERE: JNB RI, HERE ; Wait until a character is received (RI = 1)
MOV A, SBUF        ; Move received data to accumulator
CLR RI             ; Clear RI for next reception
MOV SBUF, A        ; Echo the received character back
WAIT: JNB TI, WAIT ; Wait until transmission is complete (TI = 1)
CLR TI             ; Clear TI for next transmission
SJMP HERE          ; Repeat process
END
```

#### Example 3: Serial Communication Using Interrupts

This program uses interrupts to handle serial data reception and transmission.

```assembly
ORG 0000H          ; Start of code
MOV TMOD, #20H     ; Set Timer 1 in Mode 2 (8-bit auto-reload)
MOV TH1, #0FDH     ; Load TH1 for 9600 baud rate (11.0592 MHz crystal)
MOV SCON, #50H     ; Set Serial Mode 1 (8-bit UART) and enable receiver
SETB TR1           ; Start Timer 1
SETB EA            ; Enable global interrupts
SETB ES            ; Enable serial interrupts

MAIN: SJMP MAIN    ; Infinite loop

ORG 0023H          ; Serial interrupt vector location
JNB RI, TX_INT     ; Check if it's a receive interrupt
MOV A, SBUF        ; Move received data to accumulator
CLR RI             ; Clear RI

TX_INT: MOV SBUF, A ; Send the received data back (echo)
CLR TI             ; Clear TI
RETI               ; Return from interrupt
END
```

### Summary

Serial communication in the 8051 microcontroller is versatile and can be configured for various modes depending on the application requirements. The 8051’s built-in UART makes it easy to send and receive data, making it suitable for projects that involve communication with other devices. Understanding how to configure and control serial communication through assembly language is essential for embedded system development.
