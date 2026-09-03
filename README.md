const int relayPin = 3; 

// Variable to keep track of the relay state
int relayState = LOW;         

void setup() {
  Serial.begin(9600);
  
  pinMode(relayPin, OUTPUT);
  digitalWrite(relayPin, relayState);
  
  Serial.println("System Ready. Send 'A' in the Serial Monitor to toggle the relay.");
}

void loop() {
  // Check if data is available to read from the laptop
  if (Serial.available() > 0) {
    // Read the incoming character
    char incomingChar = Serial.read();

    // Trigger only if the character is 'A' or 'a'
    if (incomingChar == 'A' || incomingChar == 'a') {
      
      // Toggle the relay state
      relayState = !relayState; 
      digitalWrite(relayPin, relayState);
      
      // Print the status to the Serial Monitor
      if (relayState == HIGH) {
        Serial.println("Solenoid Valve ON (Triggered via Serial)");
      } else {
        Serial.println("Solenoid Valve OFF (Triggered via Serial)");
      }
    }
  }
}
