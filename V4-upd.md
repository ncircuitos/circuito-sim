# 🚀 Actualización: Análisis AC y Diagrama de Bode Interactivo

En esta actualización, el motor de **Ncircuitos** da un salto cualitativo al incorporar un sistema completo de **Análisis de Pequeña Señal (AC Sweep)**, permitiendo simular y visualizar la respuesta en frecuencia de filtros y redes reactivas directamente en el navegador.

## 🧠 Motor de Simulación y Análisis Numérico (MNA)
*   **Clase `Complex` Nativa:** Implementación de aritmética de números complejos pura en JavaScript (suma, resta, multiplicación, división, magnitud, fase y conversión a dB).
*   **Solver Lineal Complejo:** Expansión del motor MNA (*Modified Nodal Analysis*) para resolver matrices aumentadas con coeficientes complejos (`solveLinearSystemComplex`) utilizando eliminación Gaussiana y pivoteo parcial por magnitud.
*   **Barrido en Frecuencia (AC Sweep):** Nuevo método `runACSweep` que inyecta un estímulo de `1∠0° V` en la fuente AC principal y calcula la respuesta fasorial de toda la red a través de un rango logarítmico de frecuencias.

## 📊 Diagrama de Bode Interactivo (UI)
*   **Modal de Alta Precisión:** Nuevo lienzo dedicado (`bodeCanvas`) para trazar respuestas en frecuencia sin salir de la app.
*   **Parámetros Configurables en Vivo:** El usuario puede ajustar $f_{min}$, $f_{max}$ y los puntos por década, recalculando y redibujando el sistema al instante.
*   **Doble Eje Y Independiente:** 
    *   Las magnitudes se dibujan con líneas continuas y vibrantes.
    *   La fase (grados) se representa con líneas punteadas y translúcidas, referenciada al eje derecho.
*   **Escala Logarítmica Estándar:** Renderizado matemático de grillas semilogarítmicas (décadas principales y subdivisiones) idénticas a las hojas de cálculo técnicas.

## 🎛️ Dualidad dB / Lineal y Análisis Automático
*   **Selector de Escala Y:** Posibilidad de alternar el eje de magnitud entre **Decibelios (dB)** y **Tensión Lineal (V)** en tiempo real sin recalcular la simulación.
*   **Auto-Escalado Inteligente:** Al cambiar a modo lineal, el motor calcula dinámicamente un tamaño de paso (`vStep`) amigable (ej: 0.1V, 0.5V, 2V) adaptado al pico máximo de la señal.
*   **Detección de Frecuencia de Corte ($f_c$):** El algoritmo busca el máximo de la curva, resta `3.0103 dB` (o multiplica por $1/\sqrt{2} \approx 0.707$ en modo lineal), interpola el cruce y genera una cota visual marcando la frecuencia de corte exacta.

## 🖱️ Herramientas de Inspección
*   **Sondas Automáticas:** El barrido lee automáticamente los componentes `osc_probe` conectados en el circuito o, en su defecto, monitorea los nodos de interés.
*   **Tooltip (Crosshair) de Seguimiento:** Al pasar el mouse sobre el gráfico, un cursor vertical se ancla a la frecuencia simulada más cercana y despliega un recuadro flotante con la lectura exacta de: Frecuencia (Hz/kHz), Magnitud (dB o V) y Fase (grados) simultáneamente para todos los canales medidos.