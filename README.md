# EXAMEN-ELECTRONICA
PROYECTO DE LA OBRA FINAL
```
#include <Servo.h>

Servo servo;
int currentAngle = 90; // Comienza en una posición media

void setup() {
  servo.attach(9); // Conecta el servo al pin digital 9
  servo.write(currentAngle);
  randomSeed(analogRead(A0)); // Inicializa el generador de números aleatorios
}

void loop() {
  int newAngle;

  // Elegir un nuevo ángulo aleatorio que esté al menos a 30 grados del ángulo actual
  do {
    newAngle = random(0, 181); // 0 a 180 grados
  } while (abs(newAngle - currentAngle) < 30); // Asegura un movimiento significativo

  servo.write(newAngle); // Mover el servo
  currentAngle = newAngle;

  delay(300); // Tiempo entre movimientos (puedes ajustarlo para más velocidad)
}
```

##
