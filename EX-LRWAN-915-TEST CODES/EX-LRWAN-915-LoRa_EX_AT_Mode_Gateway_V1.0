// This program reads data from a RAK 4631 module over Serial1 and prints it to Serial
// It uses millis() to set a fixed interval for checking Serial1
unsigned long previousMillis = 0; // stores the last time the Serial1 was checked
const unsigned long interval = 5000; // interval at which to check Serial1

void setup() {
  Serial1.begin(115200, RAK_AT_MODE); // open Serial1 at 115200 baud for communication with RAK 4631 module
  Serial.begin(115200); // open Serial at 115200 baud for debugging
}

void loop() {
  unsigned long currentMillis = millis(); // get the current time
  if (currentMillis - previousMillis >= interval) { // check if it is time to read from Serial1
    previousMillis = currentMillis;
    if (Serial1.available()) { // check if there is data available on Serial1
      String returnString = " ";
      returnString = Serial1.readStringUntil('\r'); // read the data until '\r' is received
      Serial.println(returnString); // print the data to Serial
    }
  }
}
