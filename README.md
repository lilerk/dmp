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
-Arduino Nano Board: Receives signals from the RFID reader, processes them, and subsequently sends commands to either grant or deny access.  
https://www.aliexpress.com/item/1005002998391675.html?aff_fcid=bb1f3e13845941a9bd42805b2698ebd4-1733873524735-09483-_DFdXwN9&tt=CPS_NORMAL&aff_fsk=_DFdXwN9&aff_platform=shareComponent-detail&sk=_DFdXwN9&aff_trace_key=bb1f3e13845941a9bd42805b2698ebd4-1733873524735-09483-_DFdXwN9&terminal_id=8ab5d9558887459a9e6c487c8583a49a&afSmartRedirect=y  
-RFID Module RC522: Reads the RFID card or tag presented by the user. If the RFID data aligns with the stored information, it sends a signal to the Arduino for 
further action.  
https://www.sunfounder.com/products/rfid-kit-blue?ref=how2electronics  
-1602A LCD Display: This display module offers feedback to the user. It can showcase messages such as "Access Granted", "Access Denied", or "Scan your RFID card".  
https://www.sunfounder.com/products/i2c-lcd1602-module  
-LED: Indicates lock and unlock status in the system  
-Resistor  
-Buzzer: Used to produce sounds.  
-servo motor: Used to unlock a lock.  
-Wires  
-Breadboard  

code:  
```cpp
#include <SPI.h>
#include <MFRC522.h>
#include <LiquidCrystal.h>
#include <Servo.h>

#define SS_PIN 10
#define RST_PIN 9
#define SERVO_PIN 8
#define GREEN_LED A0
#define RED_LED A1
#define BUZZER_PIN A2

MFRC522 mfrc522(SS_PIN, RST_PIN);  
LiquidCrystal lcd(7, 6, 5, 4, 3, 2); 
Servo doorServo;

//ID: 67 9B B8 B5
byte authorizedUID[] = {0x67, 0x9B, 0xB8, 0xB5};  

void setup() {
    Serial.begin(9600);    
    SPI.begin();           
    mfrc522.PCD_Init();    
    lcd.begin(16, 2);      
    doorServo.attach(SERVO_PIN); 
    doorServo.write(0);
    lcd.print("Scan Your Card");  

    pinMode(GREEN_LED, OUTPUT);
    pinMode(RED_LED, OUTPUT);
    pinMode(BUZZER_PIN, OUTPUT);

    digitalWrite(GREEN_LED, LOW);
    digitalWrite(RED_LED, LOW);
    digitalWrite(BUZZER_PIN, LOW);
}

void loop() {
    if (!mfrc522.PICC_IsNewCardPresent() || !mfrc522.PICC_ReadCardSerial()) {
      return;
    }

    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Card UID:");

    for (byte i = 0; i < mfrc522.uid.size; i++) {
        lcd.print(mfrc522.uid.uidByte[i], HEX);
        lcd.print(" ");
    }
    delay(1000);

    bool authorized = true;
    for (byte i = 0; i < mfrc522.uid.size; i++) {
        if (mfrc522.uid.uidByte[i] != authorizedUID[i]) {
            authorized = false;
            break;
        }
    }

    if (authorized) {
        lcd.clear();
        lcd.print("Access Granted!");
        digitalWrite(GREEN_LED, HIGH);
        digitalWrite(BUZZER_PIN, HIGH);  
        doorServo.write(90);
        delay(5000);
        digitalWrite(GREEN_LED, LOW);
        digitalWrite(BUZZER_PIN, LOW);   
        doorServo.write(0);
        lcd.clear();
        lcd.print("Door Locked");
        delay(2000);
        lcd.clear();
        lcd.print("Scan Your Card");
    } 
    else {
        lcd.clear();
        lcd.print("Access Denied!");
        digitalWrite(RED_LED, HIGH);
        delay(3000);
        digitalWrite(RED_LED, LOW);
        lcd.clear();
        lcd.print("Scan Your Card");
    }
}
```

![WhatsApp Image 2025-01-07 at 11 40 21 PM (2)](https://github.com/user-attachments/assets/460ea5ba-91d6-49e7-8439-79aec8819e04)
![WhatsApp Image 2025-01-07 at 11 40 21 PM](https://github.com/user-attachments/assets/b1b2a4cf-a7b8-4a9d-9761-def5884b57bf)
![WhatsApp Image 2025-01-07 at 11 40 21 PM (1)](https://github.com/user-attachments/assets/4e69471a-c9d4-434c-b1ca-cf3ae80654c0)
