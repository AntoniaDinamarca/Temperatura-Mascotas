**Este código sirve para pasarlo desde el computador al Lilypad para que pueda funcionar con la batería.**
```
#include <Wire.h>
#include <Adafruit_AHTX0.h>

Adafruit_AHTX0 aht;

// Asignación de pines probada y calibrada
const int PIN_ROJO  = 3; // Pin 3 al canal R
const int PIN_VERDE = 2; // Pin 2 al canal G
const int PIN_AZUL  = 4; // Pin 4 al canal B

const bool LOGICA_INVERTIDA = false; // Cátodo común (HIGH enciende)

// Umbrales térmicos en °C
const float UMBRAL_FRIO  = 20.0; // < 20°C: Azul
const float UMBRAL_CALOR = 28.0; // > 28°C: Rojo (Alerta de golpe de calor)

void fijarColor(bool rojo, bool verde, bool azul) {
  if (LOGICA_INVERTIDA) {
    digitalWrite(PIN_ROJO,  rojo  ? LOW : HIGH);
    digitalWrite(PIN_VERDE, verde ? LOW : HIGH);
    digitalWrite(PIN_AZUL,  azul  ? LOW : HIGH);
  } else {
    digitalWrite(PIN_ROJO,  rojo  ? HIGH : LOW);
    digitalWrite(PIN_VERDE, verde ? HIGH : LOW);
    digitalWrite(PIN_AZUL,  azul  ? HIGH : LOW);
  }
}

void setup() {
  Serial.begin(9600);
  delay(500); // Pausa de estabilización necesaria para arranque con batería

  pinMode(PIN_ROJO, OUTPUT);
  pinMode(PIN_VERDE, OUTPUT);
  pinMode(PIN_AZUL, OUTPUT);

  // Apagar LED inicialmente
  fijarColor(false, false, false);

  // Inicializar sensor AHT20
  if (!aht.begin()) {
    // Si no detecta el sensor, parpadea en Rojo para indicar error
    while (1) {
      fijarColor(true, false, false);
      delay(200);
      fijarColor(false, false, false);
      delay(200);
    }
  }
}

void loop() {
  sensors_event_t humedad, temp;
  aht.getEvent(&humedad, &temp);

  float t = temp.temperature;

  // Semáforo térmico
  if (t < UMBRAL_FRIO) {
    fijarColor(false, false, true);  // AZUL (Frío)
  } 
  else if (t >= UMBRAL_FRIO && t <= UMBRAL_CALOR) {
    fijarColor(false, true, false);  // VERDE (Confort)
  } 
  else {
    fijarColor(true, false, false);  // ROJO (¡Alerta de calor!)
  }

  delay(1500); // Actualización cada 1.5 segundos
}
```
