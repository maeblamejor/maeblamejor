#include <Servo.h>

Servo myservo;  // Crea el objeto servo
int buttonPin = 2;  // Pin del botón (según tu conexión)
int buttonState = 0;  // Variable para almacenar el estado del botón
int lastButtonState = HIGH;  // Estado previo del botón (para detectar cambios)
bool servoMoved = false;  // Verifica si el servo ya se movió

void setup() {
  myservo.attach(9);  // Conecta el servomotor al pin 9
  pinMode(buttonPin, INPUT_PULLUP);  // Configura el pin del botón como entrada con resistencia pull-up
}

void loop() {
  // Leer el estado actual del botón
  buttonState = digitalRead(buttonPin);

  // Si el botón fue presionado (cambio de HIGH a LOW)
  if (buttonState == LOW && lastButtonState == HIGH && !servoMoved) {
    myservo.write(90);  // Gira el servomotor 90 grados
    servoMoved = true;  // Marca que el servo ya ha sido movido
    delay(200);  // Anti-rebote, evita múltiples lecturas rápidas
  }

  // Actualiza el estado previo del botón
  lastButtonState = buttonState;
}
