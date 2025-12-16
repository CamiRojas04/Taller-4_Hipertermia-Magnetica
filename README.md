# Diseño y Análisis de Oscilador de Potencia ZVS (100 kHz)
**Asignatura:** Electrónica Análoga  
**Aplicación:** Hipertermia Magnética  
**Topología:** Oscilador Royer Auto-resonante (Push-Pull ZVS)

## Descripción del Proyecto
Este repositorio documenta el diseño, análisis de señal y simulación de un inversor resonante auto-oscilante en configuración *Zero Voltage Switching* (ZVS). El objetivo del circuito es generar una corriente alterna de alta frecuencia ($f_0 \approx 100 \text{ kHz}$) sobre una carga inductiva de baja impedancia ($6 \mu H$), minimizando las pérdidas por conmutación en los semiconductores de potencia mediante la activación en el cruce por cero de la tensión $V_{DS}$.

## Especificaciones de Diseño
El sistema se modeló como un circuito tanque RLC paralelo sub-amortiguado excitado por una etapa de potencia Push-Pull.

* **Frecuencia de Resonancia ($f_0$):** $100 \text{ kHz}$ (Objetivo).
* **Inductancia de Carga ($L$):** $6 \mu H$ (Solenoide de aire).
* **Capacitancia de Sintonía ($C$):** $0.42 \mu F$ (Calculada).
* **Alimentación ($V_{CC}$):** $12\text{V} - 48\text{V}$ DC.
* **Tensión Pico en Tanque:** $\approx \pi \cdot V_{CC}$.

## Análisis de Selección de Componentes
La selección de dispositivos se realizó mediante el análisis de la Zona de Operación Segura (SOA) y parámetros dinámicos, utilizando las hojas de datos oficiales:

### 1. Elementos de Conmutación (Q1, Q2)
**Dispositivo:** MOSFET Canal N - **IRFP260N**
* **Justificación de Tensión:** La topología Royer genera picos de tensión resonante de $V_{DS(peak)} = \pi \cdot V_{CC}$. Para $V_{CC}=48\text{V}$, $V_{peak} \approx 150\text{V}$. El IRFP260N soporta un $V_{DSS} = 200\text{V}$, garantizando un margen de seguridad del 25%.
* **Eficiencia Térmica:** Posee una resistencia en conducción $R_{DS(on)} = 0.04 \Omega$, minimizando las pérdidas por conducción estática ($P_{cond} = I_{D}^2 \cdot R_{DS(on)}$) ante corrientes continuas de hasta $50\text{A}$.

### 2. Red de Retroalimentación (D1, D2)
**Dispositivo:** Rectificador Ultrarrápido - **MUR1520**
* **Análisis Dinámico:** Para mantener la oscilación a $100 \text{ kHz}$ ($T = 10 \mu s$), el diodo de *gate-discharge* debe bloquearse instantáneamente. El MUR1520 ofrece un tiempo de recuperación inversa ($t_{rr}$) de **35 ns**, despreciable frente al periodo de oscilación, evitando conducción cruzada.
* **Tensión Inversa:** Soporta un $V_{RRM} = 200\text{V}$, coincidiendo con la protección de los MOSFETs.

### 3. Protección de Compuerta (Z1, Z2)
**Dispositivo:** Diodo Zener - **1N53 Series** (5 Watts)
* **Regulación:** Clava la tensión $V_{GS}$ para proteger el óxido de compuerta frente a transitorios del tanque LC.
* **Disipación:** Seleccionado por su alta capacidad de disipación de **5 W**, superior a los diodos convencionales, para soportar picos de energía en el arranque del oscilador.

### 4. Tanque Resonante (C_Tank)
**Dispositivo:** Capacitor de Polipropileno Metalizado - **CBB22**
* **Comportamiento en AC:** Específico para circuitos de alta corriente y alta frecuencia.
* **Pérdidas:** Factor de disipación $\le 0.001$ a $1 \text{ kHz}$, crítico para evitar embalamiento térmico debido a las altas corrientes reactivas ($I_{C} \approx Q \cdot I_{source}$) que circulan en el tanque paralelo.

## Validación Teórica y Simulación
El diseño prescinde de resultados experimentales en esta fase, validándose mediante modelos SPICE (NI Multisim 14.1) y cálculo analítico:
1.  **Sintonización LC:** Se determinó la capacitancia necesaria despejando $C = \frac{1}{L(2\pi f)^2}$ para centrar la frecuencia en el punto de máxima transferencia de energía magnética.
2.  **Análisis Transitorio:** Las simulaciones confirman la conmutación ZVS, donde $V_{DS}$ cae a cero antes de la activación del gate, eliminando teóricamente las pérdidas de potencia por conmutación ($P_{sw} \approx 0$).

## Estructura del Repositorio
* `Análisis Físico`: Cálculos teóricos de impedancia y frecuencia.
* `Circuito ZVS.md14`: Archivos de simulación SPICE (LTspice/Multisim).
* `Datasheets`: Hojas de datos y diagramas esquemáticos.

---
**Nota:** Este proyecto se centra en el diseño y análisis de la etapa de potencia analógica. La implementación física requiere consideraciones adicionales de disipación térmica activa.
