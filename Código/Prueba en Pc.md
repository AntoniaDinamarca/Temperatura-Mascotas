```
#include <Wire.h>
#include <Adafruit_AHTX0.h>

Adafruit_AHTX0 aht;

// Asignación de pines ajustada según prueba de colores
const int PIN_ROJO  = 3; // El Pin 3 controla el canal Rojo
const int PIN_VERDE = 2; // El Pin 2 controla el canal Verde
const int PIN_AZUL  = 4; // El Pin 4 controla el canal Azul

const bool LOGICA_INVERTIDA = false; 

// Umbrales térmicos (°C)
const float UMBRAL_FRIO  = 20.0;
const float UMBRAL_CALOR = 28.0;

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
  while (!Serial) delay(10);

  pinMode(PIN_ROJO, OUTPUT);
  pinMode(PIN_VERDE, OUTPUT);
  pinMode(PIN_AZUL, OUTPUT);

  // Inicialización del sensor AHT20
  if (!aht.begin()) {
    Serial.println(F("ERROR: No se detecta el sensor AHT20. Revisa A4 (SDA) y A5 (SCL)."));
    while (1) {
      fijarColor(true, false, false);
      delay(200);
      fijarColor(false, false, false);
      delay(200);
    }
  }

  Serial.println(F("=== SISTEMA TÉRMICO LISTO Y CALIBRADO ==="));
}

void loop() {
  sensors_event_t humedad, temp;
  aht.getEvent(&humedad, &temp);

  float t = temp.temperature;
  float h = humedad.relative_humidity;

  Serial.print(F("Temperatura: "));
  Serial.print(t, 1);
  Serial.print(F(" °C  |  Humedad: "));
  Serial.print(h, 1);
  Serial.println(F(" %"));

  // Lógica del semáforo
  if (t < UMBRAL_FRIO) {
    fijarColor(false, false, true); // Azul
    Serial.println(F("Estado: AZUL (Frío)"));
  } 
  else if (t >= UMBRAL_FRIO && t <= UMBRAL_CALOR) {
    fijarColor(false, true, false); // Verde
    Serial.println(F("Estado: VERDE (Zona de confort)"));
  } 
  else {
    fijarColor(true, false, false); // Rojo
    Serial.println(F("Estado: ROJO (¡Alerta calor!)"));
  }

  Serial.println(F("---------------------------------------------"));
  delay(1500);
}
```
