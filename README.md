# Dynamic OTP Secure Access System

## 🔌 Module-by-Module Integration & Workflow

1. **Keypad (4×4)**  
   Connected: R3–R0 → P0.15–P0.12, C3–C0 → P0.11–P0.8  
   Logic: Scan one row LOW, read columns, debounce, display to LCD

2. **LCD (16×2)**  
   Data: D4–D7 to P0.12–P0.15  
   Control: RS → P0.4, RW → P0.5, EN → P0.6  
   Ability: Initialize & display strings or characters  

3. **GSM Module**  
   Interface: UART0 (TX → GSM RX, RX → GSM TX)  
   Use AT commands: `AT+CMGF=1`, `AT+CMGS="number"` + content + Ctrl+Z  
   Implementation: Interrupt-driven UART routines  

4. **Motor / Bulb via L293D**  
   Motor: DC motor or bulb for lock/unlock signal  
   Inputs: GPIO for direction, PWM pin (e.g. P0.1) for speed or timing  

## 🛠 Recommended Development Steps
- Test each module separately (LED, keypad, EEPROM, UART, RTC, GSM)  
- Integrate in `projectmain.c`:
  - Initialize peripherals  
  - Login with keypad + EEPROM-validated password  
  - Generate OTP, send via GSM, track RTC time  
  - Accept OTP input, validate within time window  
  - Activate motor/bulb if correct; terminate otherwise  
  - External interrupt triggers password update in EEPROM  

## 📋 Functional Structure Summary

| Step            | Module         | Role                                |
|-----------------|----------------|-------------------------------------|
| Folder Setup    | Project folder | Organize code files modularly       |
| Module Testing  | LED, Keypad…   | Validate functionality individually |
| OTP Flow        | projectmain.c  | Main application logic              |
| Actuation       | Motor / Bulb   | Signal user access granted/failure  |
| Password Change | Interrupt ISR  | Modify and store new password       |

<img width="750" height="433" alt="image" src="https://github.com/user-attachments/assets/46511ce6-79b6-4a6c-bd4d-63e8fe522153" />
<img width="750" height="701" alt="image" src="https://github.com/user-attachments/assets/a86bc112-1d78-48e3-8a8a-8f32e4a6c2a5" />
<img width="750" height="607" alt="image" src="https://github.com/user-attachments/assets/0a0d8f69-274d-44de-9de8-4546dfd4e5d0" />
<img width="600" height="553" alt="image" src="https://github.com/user-attachments/assets/a072020a-b246-48f7-a785-ad4e5e37a24b" />




