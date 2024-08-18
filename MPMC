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

### Applications

- **Delay Generation**: Timers can be used to create precise time delays for tasks.
- **Event Counting**: When used as counters, they count external events like pulses.
- **Pulse Width Modulation (PWM)**: Timers can generate PWM signals for controlling devices like motors.
- **Baud Rate Generation**: Timers can be used to generate baud rates for serial communication.

Understanding how to configure and use timers/counters in the 8051 microcontroller is essential for implementing time-dependent operations in embedded systems.
