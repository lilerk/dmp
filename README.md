# dmp
RFID Based Door Lock Security System using Arduino

Project proposal  
In this project, I will design an RFID Based Door Lock Security System utilizing the RC5222 Module and Arduino Nano.

An RFID-based door lock security system is an electronic access control system that uses Radio Frequency Identification (RFID) technology to authenticate and grant or
deny access to a secured area, such as a room, building, or facility. It provides a convenient, secure, and automated way to manage access without the need for 
physical keys.

RC522 is the highly integrated RFID card reader which works on non-contact 13.56mhz communication, is designed by NXP as low power consumption, low cost and compact 
size read and write chip, is the best choice in the development of smart meters and portable hand-held devices.

How does it work?

-The user presents their RFID tag/card near the RFID reader.  
-The RFID reader generates a low-frequency electromagnetic field that powers the RFID tag (for passive tags).  
-The tag transmits its unique identifier back to the reader.  

-The RFID reader sends the identifier to the control system.  
-The control system verifies the identifier against a pre-stored database of authorized tags.  
-If the tag's identifier matches an authorized entry in the database, the system sends a signal to the electronic lock to unlock the door.  
-If the identifier is not recognized, the system denies access, and the lock remains engaged.  

Component list  
Arduino Nano Board: Receives signals from the RFID reader, processes them, and subsequently sends commands to either grant or deny access. https://www.aliexpress.com/item/1005002998391675.html?aff_fcid=bb1f3e13845941a9bd42805b2698ebd4-1733873524735-09483-_DFdXwN9&tt=CPS_NORMAL&aff_fsk=_DFdXwN9&aff_platform=shareComponent-detail&sk=_DFdXwN9&aff_trace_key=bb1f3e13845941a9bd42805b2698ebd4-1733873524735-09483-_DFdXwN9&terminal_id=8ab5d9558887459a9e6c487c8583a49a&afSmartRedirect=y  
RFID Module RC522: Reads the RFID card or tag presented by the user. If the RFID data aligns with the stored information, it sends a signal to the Arduino for 
further action.  
1602A LCD Display: This display module offers feedback to the user. It can showcase messages such as "Access Granted", "Access Denied", or "Scan your RFID card".  
LED: Indicates lock and unlock status in the system  
Channel Relay Module: This electrically operated switch is activated when the Arduino sends a command to grant access.  
Resistor  
Capacitor 100uF/35V: Used to filter and smooth out fluctuations or noise in the power supply.  
Wires  
Breadboard  
