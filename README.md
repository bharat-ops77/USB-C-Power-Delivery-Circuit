#  • USB-C-Power-Delivery-Circuit
A custom hardware and firmware solution for negotiating Power Delivery (PD) contracts from USB-C sources. This project utilizes an Arduino-compatible microcontroller alongside the FUSB302B USB Type-C controller to request specific voltage and current profiles from a compatible USB-C charger.
##  • Features 
###  • FUSB302B TCPC Integration: 
 • Full Type-C Port Controller implementation over I2C.   
 • Dynamic Voltage Switching: Cycle through available Power Data Objects (PDOs) offered by the charger using a physical pushbutton.  
 • Status Indicators: Onboard LED provides visual feedback for state changes and debugging.  
 • Customizable Sink Capabilities: Default sink profiles request 5V, 9V, and 20V at 500mA, with the driver supporting configurations up to 60W (12V       max operating, 5A peak). 
##  • Schematic 
<img width="2067" height="1384" alt="Screenshot 2026-09-22 221122" src="https://github.com/user-attachments/assets/eb9dbc4c-b8c9-48b3-a957-8ab5d3972372" />

# • Hardware Specifications
## Pin Mapping
### The firmware expects the following pin connections to the microcontroller:
<img width="2816" height="1536" alt="Gemini_Generated_Image_mlpsymlpsymlpsym" src="https://github.com/user-attachments/assets/4805a769-6458-4107-a4de-6d9a26a32252" />

# • System Limits
The safety boundaries defined in the firmware (usb_pd_driver.h) are:
Maximum Power: 60 W   
Maximum Current: 5 A   
Maximum Voltage: 12 V

# • Firmware Architecture
The firmware acts as a USB-C PD Sink (UFP). It is divided into three primary layers:   
### • TCPM (Type-C Port Manager):
Handles the I2C communication with the FUSB302B, pushing physical layer resets, managing the RX/TX FIFOs, and measuring CC pin states.   
### • PD Protocol Layer:
A state machine (usb_pd_protocol.c) that handles message transmission, GoodCRC acknowledgments, Hard/Soft resets, and contract negotiations.
### • PD Policy Engine: 
Determines which voltages to accept and request based on the capabilities advertised by the source charger (usb_pd_policy.c)

# • Getting Started
### • Prerequisites
 1. Arduino IDE (or PlatformIO).
 2. An ESP8266, ESP32, or similar Arduino-compatible board containing D3, D4, and D5 pins.
 ### • Installation & Flashing
 1. Clone this repository to your local machine.
 2. Open Firmware/usb-c-pd-trigger.ino in your Arduino IDE.   
 3. Ensure the Wire library is available for your target board.
 4. Compile and upload the firmware to your microcontroller.

 # • Usage
 1. Connect the board to a USB-C PD power supply.
 2. The state machine will initialize in PD_STATE_SNK_DISCONNECTED and automatically negotiate the first available voltage contract (usually 5V).     3. Press the pushbutton (D4): The trigger board will initiate a soft reset. Upon recovering the connection, it steps to the next available source   capability index.   
 4. Observe the LED (D5): The LED state toggles on each successful button press to confirm the interaction.
 ## • Connection Diagram
 <img width="2816" height="1536" alt="sch" src="https://github.com/user-attachments/assets/e5bdf421-ac69-424e-86c5-c1cc2d24f2b0" />

# • Designed PCB
<table>
  <tr>
    <th>First Layer</th>
    <th>Second Layer</th>
  </tr>
  <tr>
    <td><img width="480"  alt="Screenshot 2026-09-27 001140" src="https://github.com/user-attachments/assets/9ccea75f-d88b-4366-904b-67a9c6183073" />
</td>
    <td><img width="480"  alt="Screenshot 2026-09-27 001158" src="https://github.com/user-attachments/assets/81d62cc9-8140-43f4-b3f5-1980fe6c7412" />
</td>
  </tr>
</table>

# • Rendered PCB (Without Components)
<table>
  <tr>
    <th>First Layer</th>
    <th>Second Layer</th>
  </tr>
  <tr>
    <td><img width="480"  alt="image" src="https://github.com/user-attachments/assets/68c85a95-2e65-4047-b2ad-b04ba9bc812c" />
  </td>
    <td><img width="480"  alt="image" src="https://github.com/user-attachments/assets/be08ffe0-09bc-4ef1-aed1-915f8358ea1c" />

</td>
  </tr>
</table>

# • 3D Model (With Components)
<img width="1992" height="1381" alt="image" src="https://github.com/user-attachments/assets/84525e6c-ff2f-4707-9597-c90779a8c0db" />


# • Repository Structure

```
usb-c-pd-trigger/
├── Firmware/
│   ├── usb-c-pd-trigger.ino       # Main Arduino sketch
│   ├── FUSB302.c / FUSB302.h      # FUSB302B chip driver
│   ├── tcpm_driver.cpp / .h       # Hardware I2C wrapper
│   ├── usb_pd_policy.c            # USB PD policy engine
│   ├── usb_pd_protocol.c          # USB PD state machine
│   ├── usb_pd_driver.c / .h       # Sink capabilities and board definitions
│   ├── usb_pd.h                   # Core PD protocol definitions
│   └── usb_pd_tcpm.h              # Type-C Port Manager interface
├── Hardware/
│   ├── Schematics/                # PDF schematics of the trigger board
│   ├── Gerbers/                   # ZIP file containing Gerber files for PCB fabrication
│   └── Source/                    # KiCad/Altium/Eagle project files
├── Docs/
│   ├── images/                    # High-resolution photos of the populated board
│   └── datasheets/                #  FUSB
├── LICENSE                        # GNU License
└── README.md                      # Project documentation (Template below)
```
