int xPin = A0;           // Joystick X-axis
int yPin = A1;           // Joystick Y-axis
int buttonPin = 2;       // Joystick button (switch)

int xVal = 0;
int yVal = 0;
int buttonState = 0;

const int threshold = 200;    // Sensitivity threshold from center

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);  // Joystick button
  Serial.begin(9600);                // Start serial communication
}

void loop() {
  xVal = analogRead(xPin);           // Read joystick X-axis
  yVal = analogRead(yPin);           // Read joystick Y-axis
  buttonState = digitalRead(buttonPin); // Read joystick button

  String direction = "";

  // Determine direction based on thresholds
  if (xVal < (512 - threshold)) {
    direction = "LEFT";
  } else if (xVal > (512 + threshold)) {
    direction = "RIGHT";
  }

  if (yVal < (512 - threshold)) {
    if (direction != "") direction += " & ";
    direction += "UP";
  } else if (yVal > (512 + threshold)) {
    if (direction != "") direction += " & ";
    direction += "DOWN";
  }

  if (direction == "") direction = "CENTER";

  Serial.print("X: ");
  Serial.print(xVal);
  Serial.print(" | Y: ");
  Serial.print(yVal);
  Serial.print(" | Button: ");
  Serial.print(buttonState == LOW ? "Pressed" : "Released");
  Serial.print(" | Direction: ");
  Serial.println(direction);

  delay(150);
}
