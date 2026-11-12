#  Guía de Conexiones Eléctricas y Pinout

Esta sección detalla el mapa de conexiones, especificaciones de pines (*pinout*) y la distribución eléctrica entre el microcontrolador LilyPad Arduino, el sensor de temperatura/humedad AHT20 y el indicador LED RGB.

---

## Especificaciones de Alimentación

> ⚠️ **ADVERTENCIA CRÍTICA DE VOLTAJE:**  
> No utilice pilas de botón estándar **CR2032 (3.0V no recargables)**. La caída de tensión provocará el reinicio constante de la LilyPad al encender el LED RGB y fallos en la lectura del bus $I^2C$.  
> Usa exclusivamente una batería recargable **LIR2032 de Litio-Ion (3.6V - 3.7V)**.

---

##  Tablas de Mapeo de Pines (Pinout)

### 1. Sensor Ambientador AHT20 ($I^2C$)
| Pin Sensor AHT20 | Función | Pin LilyPad Arduino | Tipo de Conexión |
| :--- | :--- | :--- | :--- |
| **VCC** | Alimentación ($+3.3\text{V}$) | **VCC / (+)** | Hilo conductor / Pista eléctrica positiva |
| **GND** | Tierra ($0\text{V}$) | **GND / (-)** | Hilo conductor / Pista eléctrica masa |
| **SDA** | Línea de Datos ($I^2C$) | **A4** | Hilo conductor aislado |
| **SCL** | Línea de Reloj ($I^2C$) | **A5** | Hilo conductor aislado |

### 2. Actuador Lumínico LED RGB (Cátodo Común)
| Terminal LED RGB | Color / Estado | Pin LilyPad Arduino | Rango Térmico Representado |
| :--- | :--- | :--- | :--- |
| **Ánodo Verde (G)** | Verde (Confort) | **Pin Digital 2** | $20^\circ\text{C} \le T \le 28^\circ\text{C}$ |
| **Ánodo Rojo (R)** | Rojo (Alerta) | **Pin Digital 3** | $T > 28^\circ\text{C}$ (Riesgo Golpe de Calor) |
| **Ánodo Azul (B)** | Azul (Frío) | **Pin Digital 4** | $T < 20^\circ\text{C}$ |
| **Cátodo (-)** | Retorno Común | **GND / (-)** | Masa común del circuito |

### 3. Sistema de Alimentación y Broches (*Snaps*)
| Origen (Portabaterías) | Elemento de Interconexión | Entrada LilyPad |
| :--- | :--- | :--- |
| **Batería (+)** | Broche metálico a presión (*Snap* #1) | **VCC / (+)** |
| **Batería (-)** | Broche metálico a presión (*Snap* #2) | **GND / (-)** |

---

## Esquema Eléctrico del Circuito

![Esquema de conexiones del circuito](../../imagenes/esquema_circuito.png)

---

🔗 **Navegación:**  
* ⬅️ [Volver al Inicio](../README.md)  
* ➡️ [Ir a la Guía de Costura y Confección E-Textil](costura.md)
