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

Hardware Specifications
Pin MappingThe firmware expects the following pin connections to the microcontroller:
usb-c-pd-trigger/
├── Firmware/
│   ├── usb-c-pd-trigger.ino       # Main Arduino sketch
│   ├── FUSB302.c / FUSB302.h      # FUSB302B chip driver
│   ├── tcpm_driver.cpp / .h       # Hardware I2C wrapper
│   ├── usb_pd_policy.c            # USB PD policy engine
│   ├── usb_pd_protocol.c          # USB PD state machine
│   ├── usb_pd_driver.c / .h       # Sink capabilities and board definitions[cite: 8, 9]
│   ├── usb_pd.h                   # Core PD protocol definitions[cite: 4]
│   └── usb_pd_tcpm.h              # Type-C Port Manager interface[cite: 10]
├── Hardware/
│   ├── Schematics/                # PDF schematics of the trigger board
│   ├── Gerbers/                   # ZIP file containing Gerber files for PCB fabrication
│   └── Source/                    # KiCad/Altium/Eagle project files
├── Docs/
│   ├── images/                    # High-resolution photos of the populated board
│   └── datasheets/                # Reference datasheets (e.g., FUSB302B)
├── .gitignore                     # Standard C++ and Arduino gitignore
├── LICENSE                        # Open-source license (e.g., MIT)
└── README.md                      # Project documentation (Template below)
