# Análisis de la Protección de Compuerta mediante Diodos Zener Serie 1N53

## 1. Función Operativa en el Circuito
En el oscilador ZVS, los diodos Zener de la serie **1N53** cumplen la función crítica de **enclavamiento de tensión (Voltage Clamping)** en las terminales Compuerta-Surtidor ($V_{GS}$) de los transistores MOSFET.

Dado que el circuito se alimenta con tensiones que pueden variar entre 12V y 48V, y la tensión resonante del tanque puede inducir transitorios elevados, existe el riesgo de que la tensión en la compuerta supere el límite de ruptura del óxido del MOSFET (típicamente $\pm 20V$). El diodo Zener, conectado en paralelo con la resistencia de *pull-down* y la compuerta, limita esta tensión a un valor nominal seguro (generalmente 12V o 15V), independientemente de las fluctuaciones en la alimentación principal.

## 2. Justificación de la Selección de Potencia (5 Watts)
La elección específica de la serie 1N53 se fundamenta en su capacidad de manejo de energía, superior a los diodos Zener convencionales de 0.5W o 1W:

* **Disipación en Estado Estacionario:** Según la hoja de datos, estos dispositivos soportan una disipación de potencia en estado estable de **5 Watts** a una temperatura de terminales de $25^{\circ}C$. Esto proporciona una robustez térmica necesaria para soportar la corriente continua que fluye desde las resistencias de polarización de la compuerta sin sufrir degradación térmica.
* **Capacidad de Sobrecarga (Surge):** Durante el arranque de la oscilación o ante cambios bruscos de carga en la bobina, pueden generarse picos de energía transitoria.
* La serie 1N53 está clasificada para soportar una potencia de sobrecarga de hasta **180 W** en un ancho de pulso de 8.3 ms. Esta característica asegura que el dispositivo pueda absorber picos energéticos breves sin entrar en fallo catastrófico, protegiendo la integridad del MOSFET.

## 3. Características de Regulación
La serie ofrece límites estrictos y mejores características operativas gracias a sus uniones pasivadas con óxido de silicio. Esto garantiza que el voltaje de enclavamiento se mantenga estable y dentro de la tolerancia especificada, asegurando que el MOSFET opere siempre en su región óhmica o de corte, y nunca en una región lineal no deseada por exceso o defecto de tensión de control.

---
**Referencia Técnica:**
*ON Semiconductor. (2013). 1N53 Series 5 Watt Surmetic 40 Zener Voltage Regulators Datasheet. Rev 15.*
