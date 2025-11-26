# Inductores L1 y L2
## Caracterización física
Las bobinas `L1` y `L2` constituyen las entradas del circuito ZVS que se conectan a la fuente DC e impiden que la señal de radiofrecuencia retorne a la fuente DC. Este comportamiento
es consecuencia de la ley de Lenz.

<h1 align="center">$V_{ind}=-L \cdot \dfrac{di}{dt}$</h1> 

### Análisis desde la fuente DC

Debido a que $\dfrac{di}{dt} \approx 0$ para la fuente DC, el voltaje inducido en la bobina es nulo y, en consecuencia, la corriente cruza a través de la bobina como si esta 
fuera simplemente, un conductor ideal (cable).

### Análisis desde el tanque LC (AC)

Debido a que la frecuencia operativa del circuito es de alrededor de $f=100kHz$, la corriente cambia de dirección "violentamente y "$\dfrac{di}{dt}$ es enorme. En consecuencia $V_{ind}$
se convierte en un voltaje igualmente grande y opuesto; esto implica que la bobina induce un contravoltaje que impide que la oscilación se propague hacia la fuente.

## Análisis en términos de impedancia

La impedancia de un inductor se expresa matemáticamente como:

<h1 align="center">$X_L=2\pi \cdot f \cdot L$</h1> 

Debido a que la frecuencia de una fuente DC es nula, la impedancia de la bobina es, a su vez, prácticamente nula $X_L \approx 0$; sin embargo, en régimen AC, la frecuencia de la señal
que alimenta operativamente al circuito es $100kHz$, en consecuencia $X_L=2\pi \cdot (100kHz) \cdot L > 0$. Así, la señal de regreso encontraría un camino resistivo que impediría su
retorno a la fuente de alimentación.
