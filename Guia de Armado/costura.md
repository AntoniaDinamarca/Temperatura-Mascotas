# 🧵 Guía de Confección E-Textil y Costura

Esta guía documenta el procedimiento físico de intervención del arnés canino comercial, la elaboración de bolsillos de protección para la electrónica y el ruteo seguro de las pistas con hilo conductor de acero.

---

##  Materiales e Insumos de Confección

| Insumo | Cantidad | Función en la Prenda |
| :--- | :---: | :--- |
| **Hilo conductor de acero (3 cabos)** | 2–3 metros | Creación de las pistas eléctricas cosidas |
| **Broches metálicos de presión (*snaps*)** | 2 pares | Conexión eléctrica desmontable para el portabaterías |
| **Tela de poliéster / Fieltro reforzado** | Pliego pequeño | Fabricación de bolsillos protectores |
| **Esmalte transparente / Barniz textil** | 1 frasco | Aislamiento dieléctrico de cruces de hilo |
| **Aguja de costura manual** | 1 unidad | Cosido del hilo de acero y fijación de módulos |

---

##  Paso a Paso del Montaje Físico

### 1. Confección del Bolsillo Protector de la LilyPad
1. Cortar un rectángulo de tela reforzada dejando un margen de $1.5\text{ cm}$ alrededor del perímetro de la tarjeta LilyPad.
2. Coser el bolsillo en el lomo superior del arnés canino para evitar que la electrónica tenga contacto o roce directo con el pelaje y cuerpo del perro.

### 2. Instalación de Broches Metálicos (*Snaps*)
1. Coser las dos bases macho de los broches metálicos a la estructura fija del arnés utilizando hilo conductor.
2. Coser las dos piezas hembra al portabaterías recargable LIR2032.
3. **Verificación:** Los broches sirven como **puente de corriente e interruptor mecánico**: al desabrochar el portabaterías se corta la alimentación y se puede retirar para lavar el arnés.

### 3. Ruteo de Pistas de Hilo Conductor
1. Utilizar puntadas continuas y ajustadas para reducir la resistencia eléctrica del hilo de acero.
2. Mantener una **distancia mínima de $1\text{ cm}$** entre pistas paralelas para prevenir cortocircuitos durante el movimiento del animal.
3. Pasar las líneas del bus $I^2C$ ($SDA$ y $SCL$) por el lateral opuesto a las líneas de alimentación ($VCC$ y $GND$).

### 4. Aislamiento y Protección Dieléctrica
1. Cubrir todos los nudos y terminales de los componentes cosidos con una gota de esmalte de uñas transparente o silicona flexible.
2. Aplicar barniz textil en los puntos donde las líneas deban cruzarse inevitablemente.

---

## Mantenimiento y Lavado

* **Antes de lavar:** Desconectar y retirar la batería LIR2032 desabrochando los *snaps*.
* **Método de lavado:** Lavar a mano con agua fría y detergente suave. No usar secadora.
* **Secado:** Asegurarse de que el hilo conductor esté 100% seco antes de reinsertar la batería para evitar la corrosión por electrólisis.

---

##  Fotografías del Proceso

![Proceso de confección y costura](../../imagenes/proceso_costura.jpg)

---

🔗 **Navegación:**  
* ⬅️ [Volver a la Guía de Conexiones Eléctricas](Conexiones.md)  
* 🏠 [Volver al Inicio](../README.md)
