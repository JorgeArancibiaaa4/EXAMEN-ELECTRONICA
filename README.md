# EXAMEN-ELECTRONICA
PROYECTO DE LA OBRA FINAL

## descripcion conceptual del proyecto

Siempre me han interesado los robots, pero no los que son perfectos o pulidos. Me atraen más los que están hechos con materiales humildes, con cierta torpeza, sin buscar ser elegantes. Cuando la tecnología se junta con materiales cotidianos aparece cierto "caracter" del material. 
Desde ahí empiezo a pensar en un tipo de agotamiento: ese moverse sin saber bien para qué. El movimiento constante, sin dirección clara. Me interesa esa presencia que nace desde la falla, desde lo desprolijo, erratico. Como si el movimiento fuera un "acá estoy".

## Descripcion tecnica

El proyecto consta de un cuerpo humanizado, el cual puede mover su brazo y cabeza con servomotores. Y estos controlados por arduinos.

Se encuentra suspendido por tres alambres, sujetos a dos tornillos ubicados cerca de una ventana.


#  imagenes;


<p align="center">
  <img src="https://github.com/user-attachments/assets/4ef365b7-a328-475b-aa23-ce3df5a0b334" width="300">
  <img src="https://github.com/user-attachments/assets/08b119ee-9fcb-447a-ae26-eb5e8b8595ab" width="300">
  <img src="https://github.com/user-attachments/assets/6bc4d772-3b09-43cf-899e-7a83e0d08b50" width="300">
  <img src="https://github.com/user-attachments/assets/278a7b54-f66a-4749-9b9d-cf41f50a0101" width="300">
  <img src="https://github.com/user-attachments/assets/089b9cb0-f4c8-4265-89f8-039a0fde2e28" width="300">
</p>



# Diagrama:  
<img src="https://github.com/user-attachments/assets/71f1c31b-7ff7-4aab-9b8b-125921019d7c" width="600" />  
<img src="https://github.com/user-attachments/assets/284f7fa6-675b-4384-ae82-315d01759506" width="600" />




```
brazo, articulacion "codo"
```
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
```
CABEZA Y "HOMBRO"
```
```
#include <Servo.h>

Servo servoA;  // Servo en pin 10 (antes estaba en 9, se mueve entre 0 y 100 grados con pausa)
Servo servoB;  // Servo en pin 11 (antes estaba en 10, se mueve entre 0 y 180 grados con más pausa)

int angleA = 0;
int angleB = 90;

unsigned long lastMoveA = 0;
unsigned long lastMoveB = 0;

unsigned long delayA = 1000;             // 1 segundo de pausa entre movimientos para servoA
unsigned long delayB = 3000 + random(0, 1001); // Entre 3 y 4 segundos para servoB

void setup() {
  servoA.attach(10); // Ahora está en el pin 10
  servoB.attach(11); // Ahora está en el pin 11

  servoA.write(angleA);
  servoB.write(angleB);

  randomSeed(analogRead(A0)); // Semilla aleatoria
}

void loop() {
  unsigned long currentMillis = millis();

  // Movimiento servoA (ahora en pin 10) entre 0 y 100 grados con pausa
  if (currentMillis - lastMoveA >= delayA) {
    angleA = random(0, 101); // ángulo entre 0 y 100
    servoA.write(angleA);
    lastMoveA = currentMillis;
  }

  // Movimiento servoB (ahora en pin 11) entre 0 y 180 grados con pausa de 3-4 segundos
  if (currentMillis - lastMoveB >= delayB) {
    angleB = random(0, 181); // ángulo entre 0 y 180
    servoB.write(angleB);
    lastMoveB = currentMillis;
    delayB = 3000 + random(0, 1001); // Nueva pausa aleatoria entre 3000 y 4000 ms
  }
}

```
##
