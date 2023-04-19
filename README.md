# Flutter Bluetooth Project with Arduino UNO and HM10

This Flutter project is designed to communicate with an Arduino UNO board via Bluetooth using the HM10 module. The project is intended to serve as a starting point for developers looking to build their own Bluetooth-based projects.

## Getting Started

To get started with this project, you will need to have the following:

- Flutter SDK installed on your machine
- Android Studio or any other preferred IDE
- Arduino UNO board
- HM10 module
- Android or iOS device with Bluetooth capability

## Setting up the Hardware

1. Connect the HM10 module to the Arduino UNO board using the following pins:
   - HM10 VCC to Arduino 5V
   - HM10 GND to Arduino GND
   - HM10 RX to Arduino TX
   - HM10 TX to Arduino RX

2. Connect the Arduino UNO board to your computer via USB.

## Setting up the Software

1. Clone the repository to your local machine using the following command:

```git
git clone https://github.com/yourusername/flutter-arduino-bluetooth.git
```

2. Open the project in Android Studio or any other preferred IDE.

3. Install the required dependencies by running the following command:

```flutter
flutter pub get
```

4. Upload the `Bluetooth.ino` sketch to the Arduino UNO board using the Arduino IDE.

5. Run the application on your Android or iOS device.

## Testing the Project

1. Open the application on your device and press the `Connect` button to establish a Bluetooth connection with the Arduino UNO board.

2. Once the connection is established, press the `Send` button to send a message to the Arduino UNO board.

3. The Arduino UNO board should receive the message and respond with a message of its own, which will be displayed in the application.

## Conclusion

This project provides a basic template for building Bluetooth-based projects using Flutter and an Arduino UNO board. Developers can modify the project to suit their needs, adding additional functionality as required.

#### Bluetooth.ino

```arduino

#include <SoftwareSerial.h>

SoftwareSerial HM10(2, 3); // RX = 2, TX = 3

char appData;  

String inData = "";

void setup()

{

  Serial.begin(115200);

  Serial.println("HM10 serial started at 9600");

  HM10.begin(115200); // set HM10 serial at 9600 baud rate

  pinMode(13, OUTPUT); // onboard LED

  digitalWrite(13, LOW); // switch OFF LED
 


}


void loop()

{

  HM10.listen();  // listen the HM10 port

  while (HM10.available() > 0) {   // if HM10 sends something then read

    appData = HM10.read();

    inData = String(appData);  // save the data in string format

    Serial.write(appData);

  }


 

  if (Serial.available()) {           // Read user input if available.

    delay(10);

    HM10.write(Serial.read());

  }

  if ( inData == "F") {

    Serial.println("LED OFF");

    digitalWrite(13, LOW); // switch OFF LED

    delay(500);

  }

  if ( inData == "N") {

    Serial.println("LED ON");

    digitalWrite(13, HIGH); // switch ON LED

    delay(500);

    digitalWrite(13, HIGH); // switch ON LED

    delay(500);

    digitalWrite(13, LOW); // switch OFF LED

    delay(500);
    
    digitalWrite(13, HIGH); // switch ON LED

    delay(500);
    
    digitalWrite(13, LOW); // switch OFF LED

    delay(500);
    
    digitalWrite(13, HIGH); // switch ON LED

    delay(500);
    
    digitalWrite(13, LOW); // switch OFF LED

    delay(500);
    
    digitalWrite(13, HIGH); // switch ON LED

    delay(500);
    
    digitalWrite(13, LOW); // switch OFF LED

    delay(500);
    
    digitalWrite(13, HIGH); // switch OFF LED

    delay(500);

    

  }

}

```


