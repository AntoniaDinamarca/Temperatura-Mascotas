Para poder probar estos códigos se necesita un USB CH340G, LilyPad, Sensor AHT20, luz LED RGB, cables macho-hembra y hembra-hembra. En el Arduino hay que descargar en la biblioteca Wire.h, Adafruit_AHTX0.h, Adafruit_Sensor.h


**Prueba Sensor AHT20**

```
#include <Wire.h>
#include <Adafruit_AHTX0.h>

Adafruit_AHTX0 aht;

void setup() {
  Serial.begin(9600);
  while (!Serial) delay(10);

  Serial.println("--- PRUEBA DE SENSOR AHT20 ---");

  // Inicializar sensor en pines I2C (A4 = SDA, A5 = SCL)
  if (!aht.begin()) {
    Serial.println("Error: No se detecta el sensor AHT20. Revisa VCC, GND, A4 (SDA) y A5 (SCL).");
    while (1) delay(10);
  }
  
  Serial.println("¡Sensor AHT20 detectado correctamente!");
}

void loop() {
  sensors_event_t humedad, temp;
  aht.getEvent(&humedad, &temp);

  Serial.print("Temperatura: ");
  Serial.print(temp.temperature);
  Serial.print(" °C  |  Humedad: ");
  Serial.print(humedad.relative_humidity);
  Serial.println(" %");

  delay(1000); // Lee datos cada 1 segundo
}
```
*Para que funcione en el Arduino tiene que estar a 19200 baud*

**Prueba Luz LED RGB y Sensor AHT20**

```
#include <Wire.h>
#include <Adafruit_AHTX0.h>

Adafruit_AHTX0 aht;

const int PIN_ROJO  = 2;
const int PIN_VERDE = 3;
const int PIN_AZUL  = 4;

// Umbrales térmicos en °C
const float UMBRAL_FRIO = 20.0;
const float UMBRAL_CALOR = 28.0;

void fijarColorRGB(bool rojo, bool verde, bool azul) {
  digitalWrite(PIN_ROJO,  rojo  ? HIGH : LOW);
  digitalWrite(PIN_VERDE, verde ? HIGH : LOW);
  digitalWrite(PIN_AZUL,  azul  ? HIGH : LOW);
}

void setup() {
  Serial.begin(9600);

  pinMode(PIN_ROJO, OUTPUT);
  pinMode(PIN_VERDE, OUTPUT);
  pinMode(PIN_AZUL, OUTPUT);

  // Apagar el LED al inicio
  fijarColorRGB(false, false, false);

  // Inicializar sensor AHT20
  if (!aht.begin()) {
    Serial.println(F("Error: No se encontro el sensor AHT20. Revisa VCC, GND, A4 (SDA) y A5 (SCL)."));
    // Parpadeo de error en color Rojo
    while (1) {
      fijarColorRGB(true, false, false);
      delay(200);
      fijarColorRGB(false, false, false);
      delay(200);
    }
  }

  Serial.println(F("--- PRUEBA SISTEMA AHT20 + LED RGB REGISTRADA ---"));
}

void loop() {
  sensors_event_t humedad, temp;
  aht.getEvent(&humedad, &temp);

  float t = temp.temperature;
  float h = humedad.relative_humidity;

  Serial.print(F("Temperatura: "));
  Serial.print(t, 1);
  Serial.print(F(" °C | Humedad: "));
  Serial.print(h, 1);
  Serial.println(F(" %"));

  // Lógica del semáforo térmico en módulo RGB
  if (t < UMBRAL_FRIO) {
    // Encender solo Azul
    fijarColorRGB(false, false, true);
    Serial.println(F("Estado LED: AZUL (Frio)"));
  } 
  else if (t >= UMBRAL_FRIO && t <= UMBRAL_CALOR) {
    // Encender solo Verde
    fijarColorRGB(false, true, false);
    Serial.println(F("Estado LED: VERDE (Zona de confort)"));
  } 
  else {
    // Encender solo Rojo
    fijarColorRGB(true, false, false);
    Serial.println(F("Estado LED: ROJO (Alerta calor)"));
  }

  Serial.println(F("---------------------------------------------"));
  delay(1500);
}
```

