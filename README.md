# ⚡ PROTO Web — Simulador de Circuitos Electrónicos en Tiempo Real

Simulador interactivo de circuitos electrónicos en tiempo real inspirado en **PROTO**, diseñado para ejecutarse directamente en el navegador sin dependencias externas.

## ✨ Características Principales

- **Motor Físico MNA en Tiempo Real**: Resolución matricial nodal modificada (Modified Nodal Analysis) con integración trapezoidal y Newton-Raphson para componentes lineales, no lineales y digitales.
- **Más de 25 Componentes Interactivos**:
  - **Fuentes**: Batería DC, Generador AC Senoidal, Generador de Pulsos / PWM, Tierra (GND).
  - **Pasivos**: Resistencia, Capacitor, Inductor, Potenciómetro interactivo, Transformador, Fusible.
  - **Semiconductores**: Diodo Rectificador, Diodo Zener, LED con brillo dinámico, Transistor NPN / PNP, MOSFET Canal-N, Amplificador Operacional (Op-Amp), Lámpara incandescente.
  - **Interruptores y Lógica Digital**: Interruptor SPST, Pulsador NO, Conmutador SPDT, Entrada/Salida Lógica, Compuertas AND, OR, NOT, NAND, XOR.
  - **Instrumentos**: Voltímetro y Amperímetro integrados.
- **Gráficos de Señales Múltiples y Control Temporal**:
  - Panel lateral redimensionable con **múltiples monitores de señal (`V` e `I`)** simultáneos.
  - Selector de **Paso de Tiempo (`⏱ Δt`)** desde `1 ms/s` hasta `5 s/s` + avance paso a paso (`⏭ +Δt`).
  - Selector de **Velocidad de Avance del Gráfico (`📈 Gráfico`)** con modo **Ultra Rápido (Flancos)** y cursor interactivo de medición para analizar subidas y bajadas bruscas.
- **Edición Avanzada**:
  - **Selección múltiple** arrastrando recuadro en el fondo o con `Ctrl + Clic`.
  - Buscador rápido de catálogo con ventana emergente (`/` o `Ctrl + F` + `Enter`).
  - Nodos conectores visibles, resaltado completo de redes eléctricas y simulación térmica de sobrecarga.

## ⌨️ Atajos de Teclado

| Tecla | Acción |
| :--- | :--- |
| `Espacio` | Pausar / Reanudar simulación |
| `Shift + R` | Reiniciar simulación desde `t = 0` |
| `W` | Modo Trazar Cable |
| `R` | Rotar componente 90° |
| `G` | Anclar / Quitar gráfico del componente en el panel derecho |
| `Ctrl + Clic` / Arrastrar en fondo | Selección múltiple de componentes y cables |
| `Ctrl + A` | Seleccionar todo el circuito |
| `Supr` / `Backspace` | Eliminar elementos seleccionados |
| `Ctrl + D` | Duplicar selección |
| `Ctrl + Z` | Deshacer último cambio |
| `B` | Minimizar / Expandir catálogo izquierdo |
| `/` o `Ctrl + F` | Buscar componente (`Enter` abre selector emergente) |
| `1` – `9`, `0`, `M` | Inserción rápida de componentes |
