// Include required libraries
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <Adafruit_ADS1X15.h>

// Define LoRaSerial as Serial2
#define LoRaSerial Serial2

// Define screen dimensions
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

// Define OLED reset pin
#define OLED_RESET -1

// Create SSD1306 display object
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

// Define time interval for data processing
unsigned long previousMillis = 0;
const unsigned long interval = 20000;

// Callback function for received LoRa data
void recv_cb(String data) {
  // Split the received data into parts using the colon separator
  String parts[5];
  int partIndex = 0;
  String temp = "";
  for (int i = 0; i < data.length(); i++) {
    char c = data.charAt(i);
    if (c == ':') {
      parts[partIndex] = temp;
      temp = "";
      partIndex++;
    } else {
      temp += c;
    }
  }
  parts[partIndex] = temp;

  // Extract event type, signal strength, spreading factor, and received data from the parts array
  String event = parts[1];
  int signal_strength = parts[2].toInt();
  int spreading_factor = parts[3].toInt();
  String received_data = parts[4];

  // Convert received data from string to an array of ASCII codes
  int received_data_len = received_data.length();
  uint8_t received_data_int[received_data_len];
  for (int i = 0; i < received_data_len; i++) {
    received_data_int[i] = (uint8_t)received_data.charAt(i);
  }

  // Convert ASCII codes to string
  String received_data_ascii = "";
  for (int i = 0; i < received_data_len; i++) {
    received_data_ascii += char(received_data_int[i]);
  }

  // Convert ASCII string to output string
  String asciiString = received_data_ascii;
  String outputString = "";
  for (int i = 0; i < asciiString.length(); i += 2) {
    int asciiCode = (int)strtol(asciiString.substring(i, i + 2).c_str(), NULL, 16);
    outputString += (char)asciiCode;
  }

  // Print the extracted values
  Serial.print("Event: ");
  Serial.println(event);
  Serial.print("Signal Strength: ");
  Serial.print(signal_strength);
  Serial.println(" dBm");
  Serial.print("Spreading Factor: ");
  Serial.println(spreading_factor);
  Serial.print("Received Data (ASCII): ");
  Serial.println(outputString);
  Serial.println();
}

void sendCommand(String command, String expectedResponse, int timeout) {
  LoRaSerial.println(command);

  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(WHITE);
  display.setCursor(0, 0);
  display.println(command);
  display.display();

  delay(500);

  unsigned long start = millis();
  String response = "";
  while (millis() - start < timeout) {
    while (LoRaSerial.available()) {
      char c = LoRaSerial.read();
      response += c;
    }

    if (response.indexOf(expectedResponse) != -1) {
      display.clearDisplay();
      display.setTextSize(1);
      display.setTextColor(WHITE);
      display.setCursor(0, 0);
      display.println("Received :");
      display.println(response);
      display.display();
      delay(1000);
      return;
    } else {
      display.clearDisplay();
      display.setTextSize(1);
      display.setTextColor(WHITE);
      display.setCursor(0, 0);
      display.println("erro response:");
      display.println(response);
      display.display();

      LoRaSerial.println(command);
      delay(1000);
    }

    delay(1000);
  }

  return;
}


void setup() {
  // Start serial communication with the computer
  Serial.begin(115200);

  // Start serial communication with the LoRa module
  LoRaSerial.begin(115200, SERIAL_8N1, 32, 0);

  // Wait for LoRa module to initialize
  delay(1000);

  // Initialize I2C communication with OLED display
  Wire.begin(16, 17);

  // Initialize OLED display
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);

  // Check if OLED display initialization was successful
  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println(F("SSD1306 allocation failed"));
    for (;;);
  }

  // Clear OLED display
  display.clearDisplay();
  display.display();

  // Set text size, color, and cursor position for OLED display
  display.setTextSize(1);
  display.setTextColor(WHITE);
  display.setCursor(0, 0);

  // Print "LORA: " on OLED display
  display.print("LORA: ");
  display.display();

  // The first argument is the AT command to be sent, the second argument is the expected response, and the third argument is the timeout in milliseconds
  sendCommand("AT+ATM", "OK", 10000); // Set module to AT mode
  sendCommand("AT", "OK", 10000); // Check if module is responding
  sendCommand("AT+NWM=0", "OK", 5000); // Set network mode to private network mode
  sendCommand("AT+PFREQ=928000000", "OK", 5000); // Set RF frequency to 928 MHz
  sendCommand("AT+PSF=12", "OK", 5000); // Set spreading factor to 12
  sendCommand("AT+PCR=1", "OK", 5000); // Set coding rate to 4/5
  sendCommand("AT+PPL=8", "OK", 5000); // Set payload length to 8 bytes
  sendCommand("AT+PTP=22", "OK", 5000); // Set preamble length to 22 symbols
  sendCommand("AT+P2P=928000000:12:0:0:8:22", "OK", 5000); // Set P2P parameters
  sendCommand("AT+PRECV=0", "OK", 5000); // Set module to receive mode with no timeout
  sendData("TEST01");
  sendCommand("AT+PRECV=65535", "OK", 5000); // Set module to receive mode with timeout of 65535 ms
}


void sendData(String data) {

  String command = "AT+PSEND=" + data;
  sendCommand(command, "OK", 5000);
}

void loop() {
  if (LoRaSerial.available()) {
    String response = "";
    while (LoRaSerial.available()) {
      char c = LoRaSerial.read();
      response += c;
    }
    display.clearDisplay();
    display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(0, 0);
    display.println("Data:");
    // If LoRa module receives data from another device
    if (response.indexOf("EVT:RXP2P:") != -1) {
      // Call the recv_cb function to handle the received data
      recv_cb(response);
      // Set LoRa module to receive mode
      sendCommand("AT+PRECV=0", "OK", 5000);
      // Send data using LoRa module
      sendData("12345");
      // Set LoRa module to continuous receive mode
      sendCommand("AT+PRECV=65535", "OK", 5000);
    }
    display.display();
    delay(2000);
  }

  unsigned long currentMillis = millis();
  // If time interval has elapsed
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    display.clearDisplay();
    display.display();
    // Set LoRa module to receive mode
    sendCommand("AT+PRECV=0", "OK", 5000);
    delay(200);
    // Send data using LoRa module
     sendCommand("AT+PSEND=12345", "OK", 5000);
    ///sendData("12345");
    // Set LoRa module to continuous receive mode
    sendCommand("AT+PRECV=65535", "OK", 5000);
  }
}
