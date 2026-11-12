# Monitoreo Térmico Canino: Arnés E-Textil con Alerta Semafórica

Sistema vestible autónomo e interactivo diseñado para traducir las condiciones de temperatura del entorno directo de un perro en señales de luz intuitivas, previniendo el estrés térmico y el golpe de calor.

* **Asignatura:** Dispositivos Low-Tech e Interfaces Interactivas
* **Equipo:** Los Firulais
* **Licencia:** Open Source Hardware & Software (MIT / CERN OHL)

## Equipo

| Integrantes |
|---|
| Antonia Dinamarca |
| Luka Morales |

---

## Descripción del Proyecto

Este proyecto aborda la comunicación entre el perro y su tutor mediante una interfaz e-textil no invasiva. Consiste en un arnés canino equipado con electrónica vestible que mide constantemente el microclima térmico en el que se encuentra la mascota. 

Dado que los perros no pueden manifestar verbalmente su incomodidad térmica hasta que el malestar es avanzado, el arnés actúa como un puente de comunicación visual, procesa las lecturas del sensor y las refleja en un LED RGB mediante un código semafórico básico (Azul = Frío, Verde = Confort, Rojo = Alerta Térmica). El dispositivo es 100% autónomo, portátil y lavable gracias a su sistema de broches eléctricos desmontables.

---

## Problema y Contexto Biológico

### 1. La Fisiología del Perro frente al Calor
A diferencia de los seres humanos, los perros no poseen glándulas sudoríparas distribuidas por el cuerpo para regular su temperatura corporal. Su mecanismo principal de enfriamiento es el jadeo y la liberación de calor por las almohadillas de las patas. Esta limitación biológica provoca que:
* Su temperatura suba a un ritmo exponencialmente más rápido que la de una persona en las mismas condiciones.
* La acumulación de calor en capas de pelaje denso o en entornos cerrados genere hipertermia severa en cuestión de minutos.

### 2. El Problema de la Detección Tardía
En la vida cotidiana, los tutores suelen identificar que su perro tiene calor únicamente cuando el animal muestra signos clínicos evidentes:
* Jadeo excesivo y saliva espesa.
* Ladeo de cabeza, cansancio extremo o negativa a seguir caminando.
* Encías rojas y ritmo cardíaco acelerado.

Cuando estos síntomas aparecen, el perro ya se encuentra en un estado de estrés térmico avanzado. Existe una falta de indicadores preventivos en tiempo real que adviertan el peligro *antes* de que ocurra el daño físico.

### 3. Factor Entorno y "Efecto Microclima"
La temperatura medida por una app del clima en el teléfono celular refleja la temperatura del aire general a la sombra, pero no el entorno real del perro. El asfalto radiante, la radiación solar directa sobre la espalda del animal o el calor atrapado en un auto/habitación crean un microclima crítico que requiere medición directa en la vestimenta del animal.

---

## Usuarios y Escenarios de Uso

### Perfil de Usuario Principal (Tutores)
* **Público objetivo:** Personas con mascotas que realizan paseos al aire libre, actividades deportivas, trayectos urbanos sobre asfalto o que dejan a sus perros en espacios del hogar con variaciones térmicas (patios, balcones, departamentos soleados).
* **Casos críticos prioritarios:**
  * **Perros de razas braquicefálicas** (Pug, Bulldog, Boxer): Tienen vías respiratorias reducidas y menor capacidad de refrigeración por jadeo.
  * **Perros de pelaje oscuro o denso** (Husky, Pastor Alemán, San Bernardo): Absorben mayor radiación solar.
  * **Perros seniors o con cardiopatías:** Vulnerables a descompensaciones rápidas por calor.

### Escenarios de Aplicación Real
1. **El Paseo Urbano:** Identificar si la temperatura cercana al suelo supera los límites seguros para el animal.
2. **El Descanso en el Hogar / Balcón:** Visualizar desde lejos si el lugar donde descansa la mascota se ha vuelto demasiado frío o caluroso a lo largo del día.
3. **Pausas de Hidratación:** El cambio a luz Roja le indica de forma inequívoca al tutor que debe detener la marcha, suministrar agua y buscar sombra inmediatamente.

---

##  Lógica de Funcionamiento (Semáforo de Alerta)

El microcontrolador procesa la temperatura ambiental capturada por el sensor y conmuta el estado de la interfaz lumínica:

| Rango de Temperatura ($T$) | Color LED | Estado Térmico | Acción Sugerida para el Tutor |
| :--- | :--- | :--- | :--- |
| **$T < 20^\circ\text{C}$** | 🔵 **Azul** (Pin 4) | Confort Bajo / Frío | Considerar abrigo o trasladar a zona templada. |
| **$20^\circ\text{C} \le T \le 28^\circ\text{C}$** | 🟢 **Verde** (Pin 2) | Confort Térmico Óptimo | Permite actividad física normal y paseos seguros. |
| **$T > 28^\circ\text{C}$** | 🔴 **Rojo** (Pin 3) | **Alerta: Riesgo de Golpe de Calor** | Detener paseo, dar agua fresca y buscar sombra inmediatamente. |

---

##  Especificaciones Técnicas de Hardware (BOM)

Para mantener la ligereza y adaptabilidad al cuerpo del perro, se utilizaron componentes e-textil y de bajo consumo:

* **Microcontrolador:** LilyPad Arduino (ATmega328P, 3.3V / 8MHz) — Diseñado específicamente para coser en tela.
* **Sensor de Entorno:** AHT20 ($I^2C$) — Alta precisión para medir temperatura ($^\circ\text{C}$) y humedad relativa ($\%$).
* **Actuador Lumínico:** LED RGB Cátodo Común (Pines 2=Verde, 3=Rojo, 4=Azul).
* **Fuente de Poder:** Batería Recargable Litio-Ion **LIR2032 (3.6V - 3.7V)** para evitar caídas de tensión al conmutar los canales del LED.
* **Conectividad:** Hilo conductor de acero inoxidable de 3 cabos y broches de presión metálicos (*snaps*).

---

##  Integración E-Textil y Construcción Física

1. **Bolsillos de Protección:** La placa LilyPad y la batería se protegen en bolsillos de tela reforzada cosidos al arnés, evitando la fricción directa con el pelaje del animal.
2. **Broches de Presión (*Snaps*) como Conectores:** El portabaterías utiliza broches metálicos que cumplen una doble función: actúan como puente eléctrico conductivo e interruptor desmontable para retirar la energía al lavar el arnés.
3. **Circuitos Cosidos:** El bus $I^2C$ y las líneas de alimentación están cosidas internamente entre las capas del textil para prevenir cortocircuitos.

---

## Índice de la bitácora

- [S01 - Entrega 01](bitacora/S01.md)
- [S02 - Entrega 02](bitacora/S02.md)
- [S03 - Entrega 03](bitacora/S03.md)



