# Control-LED-Brightness-using-PWM-and-Potentiometer.
### 1. Aim

To control the brightness of an LED using **Pulse Width Modulation (PWM)** by varying the output of a **potentiometer** using an Arduino board.

### 2. Apparatus Required

| S. No. | Component             |    Quantity |
| ------ | --------------------- | ----------: |
| 1      | Arduino Uno           |           1 |
| 2      | LED                   |           1 |
| 3      | Potentiometer (10 kΩ) |           1 |
| 4      | Resistor (220 Ω)      |           1 |
| 5      | Breadboard            |           1 |
| 6      | Jumper wires          | As required |
| 7      | USB cable             |           1 |

### 3. Software Required

* Arduino IDE
* Arduino USB driver, if required
* Arduino C/C++ programming language

### 4. Theory

A potentiometer produces a variable analog voltage when its knob is rotated. The Arduino reads this voltage using an **analog input pin**.

The `analogRead()` function gives a value from **0 to 1023**. This value is converted to a PWM value from **0 to 255** using the `map()` function.

The PWM value is then sent to a PWM-enabled digital pin using `analogWrite()`.

* PWM value **0** → LED OFF
* PWM value **255** → LED maximum brightness
* Intermediate values → Corresponding LED brightness

### 5. Circuit Diagram

```text
                 Arduino UNO
              +----------------+
              |                |
   Potentiometer               |
              |                |
   Left  -----+ 5V             |
   Middle ---- A0              |
   Right ----- GND             |
              |                |
              |                |
              |       D9       |------[220 Ω]------>|------ GND
              |                |                    LED
              +----------------+
```

**Potentiometer connections:**

* One outer pin → **5V**
* Other outer pin → **GND**
* Middle/wiper pin → **A0**

**LED connections:**

* Arduino **D9 (PWM)** → **220 Ω resistor** → LED anode (+)
* LED cathode (−) → **GND**

> **Note:** Pin D9 is used because it is a PWM-enabled pin on the Arduino Uno.

### 6. Procedure

1. Connect the potentiometer to the Arduino:

   * One terminal to 5V.
   * The other terminal to GND.
   * The middle terminal to analog pin A0.
2. Connect the LED to PWM pin D9 through a 220 Ω resistor.
3. Connect the LED's cathode to GND.
4. Connect the Arduino Uno to the computer using a USB cable.
5. Open the **Arduino IDE**.
6. Select the appropriate Arduino board and COM port.
7. Enter the program given below.
8. Compile the program and upload it to the Arduino.
9. Open the Serial Monitor if you want to observe the potentiometer and PWM values.
10. Rotate the potentiometer.
11. Observe that the LED brightness changes according to the potentiometer position.

### 7. Program

```cpp
const int potPin = A0;
const int ledPin = 9;

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // Read potentiometer value
  int potValue = analogRead(potPin);

  // Convert 0-1023 to 0-255
  int pwmValue = map(potValue, 0, 1023, 0, 255);

  // Set LED brightness
  analogWrite(ledPin, pwmValue);

  // Display values on Serial Monitor
  Serial.print("Potentiometer: ");
  Serial.print(potValue);
  Serial.print("  PWM: ");
  Serial.println(pwmValue);

  delay(10);
}
```

### 8. Output

When the potentiometer is rotated:

| Potentiometer Position | Analog Value | PWM Value | LED Brightness |
| ---------------------- | -----------: | --------: | -------------- |
| Minimum                |           ~0 |         0 | OFF            |
| Low                    |         ~256 |       ~64 | Dim            |
| Medium                 |         ~512 |      ~128 | Medium         |
| High                   |         ~768 |      ~191 | Bright         |
| Maximum                |        ~1023 |       255 | Maximum        |

**Serial Monitor output:**

```text
Potentiometer: 0    PWM: 0
Potentiometer: 256  PWM: 64
Potentiometer: 512  PWM: 128
Potentiometer: 768  PWM: 191
Potentiometer: 1023 PWM: 255
```

### 9. Result

Thus, the **brightness of the LED was successfully controlled using PWM and a potentiometer**. As the potentiometer was rotated, the analog input value changed and the corresponding PWM output varied, thereby changing the LED brightness.
