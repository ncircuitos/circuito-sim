# Ω Ncircuitos — Simulador de Circuitos Electrónicos en Tiempo Real

Simulador interactivo de circuitos electrónicos en tiempo real diseñado para ejecutarse directamente en el navegador sin dependencias externas.

## Características Principales

- **Motor Físico MNA en Tiempo Real**: Resolución matricial nodal modificada (Modified Nodal Analysis) con integración trapezoidal y Newton-Raphson para componentes lineales, no lineales y digitales.
- **Analizador Osciloscopio Expandido**: Doble clic en cualquier gráfico para abrir la vista superior ampliada con **cursores interactivos para medir Δt (ms), ΔV, ΔI, frecuencia (1/Δt) y pendientes (ΔV/Δt)**, además de auto-detección de constantes de tiempo RC (1τ al 63.2%) y picos mín/máx.
- **Punto de Operación DC (`.op`)**: Tabla modal de análisis nodal estático con tensiones de nodo respecto a GND, terminales conectados, caída de tensión por rama, corrientes instantáneas, disipación de potencia, balance de conservación de energía (P_fuentes vs P_disipada) y exportación a CSV con un solo clic (Atajo `P`).
- **Compartir Circuito mediante Enlace (URL Hash)**: Compresión y codificación de esquemáticos completos en tokens URL-safe (`#c=z...` con `CompressionStream`), copia automática al portapapeles y restauración instantánea con validación de seguridad e integridad.
- **Etiquetas de Red (Net Labels)**: Conexiones equipotenciales virtuales entre nodos con el mismo identificador (`VCC`, `GND`, `0V`, `V_IN`, `V_OUT`, etc.) para esquemáticos limpios sin cruces de cables.
- **Equipotencialidad Precisa de Nodos**: Medición idéntica y exacta de tensión en cualquier punto a lo largo de un mismo conductor ideal, manteniendo la animación de corriente.
- **Más de 35 Componentes Interactivos**:
  - **Fuentes**: Batería DC, Generador AC Senoidal, Generador de Pulsos / PWM, Tierra (GND).
  - **Pasivos**: Resistencia, Capacitor, Inductor, Potenciómetro interactivo, Transformador, Fusible.
  - **Semiconductores y Analógica**: Diodo Rectificador, Diodo Zener, Puente de Diodos Integrado (Graetz), LED con brillo dinámico, Transistor NPN / PNP, MOSFET Canal-N, Amplificador Operacional (Op-Amp), Lámpara incandescente.
  - **Módulos Integrados y Control**:
    - **Temporizador NE555**: Divisor resistivo 5k-5k-5k, comparadores 1/3 y 2/3 VCC, flip-flop interno, pin de descarga y salida totem-pole para configuraciones astables y monoestables.
    - **Regulador de Tensión LM7805**: Regulación precisa de 5 V con simulación de tensión de caída (*dropout*) y disipación de potencia.
    - **Relé Electromecánico SPDT**: Bobina de conmutación con histéresis y contacto conmutador móvil.
    - **Optoacoplador PC817**: Aislamiento galvánico por emisor infrarrojo y fototransistor con relación de transferencia de corriente (CTR).
  - **Sensores y Transductores**:
    - **Fotorresistencia (LDR)**: Control de iluminación ambiental (0–100%) y respuesta resistiva logarítmica.
    - **Termistor NTC**: Modelado por ecuación Beta / Steinhart-Hart con control de temperatura ambiental (-20 °C a 125 °C).
    - **Buzzer DC**: Alerta acústica y visual con umbral de activación.
  - **Visualización y Lógica Digital**: Display de 7 Segmentos (decodificador BCD / Hexadecimal 0–F), Interruptor SPST, Pulsador NO, Conmutador SPDT, Entrada/Salida Lógica, Compuertas AND, OR, NOT, NAND, XOR.
  - **Instrumentos y Conectividad**: Voltímetro, Amperímetro y Etiquetas de Red (Net Labels).
- **Gráficos de Señales Múltiples y Control Temporal**:
  - Panel lateral redimensionable con múltiples monitores de señal (`V` e `I`) simultáneos.
  - Selector de **Paso de Tiempo (Δt)** desde `1 ms/s` hasta `5 s/s`.
  - Selector de **Velocidad de Avance del Gráfico** con modo Ultra Rápido (Flancos) para analizar subidas y bajadas bruscas.
- **Edición y Productividad**:
  - Selección múltiple arrastrando recuadro en el fondo o con `Ctrl + Clic`.
  - Catálogo de componentes con buscador en tiempo real y vista previa.
  - Galería de Circuitos de Ejemplo precargados (Oscilador NE555, Fuente Regulada 7805, Rectificadores, RLC, etc.).
  - Eliminación directa de nodos sin cortar cables y simulación térmica de sobrecargas.

## Atajos de Teclado

| Tecla | Acción |
| :--- | :--- |
| `Espacio` | Pausar / Reanudar simulación |
| `Shift + R` | Reiniciar simulación desde `t = 0` |
| `W` | Modo Trazar Cable |
| `R` | Rotar componente 90° |
| `P` | Abrir / Cerrar tabla de Punto de Operación DC (`.op`) |
| `V` | Mostrar / Ocultar etiquetas de voltaje en los nodos |
| `C` | Centrar la vista en el circuito |
| `O` | Expandir / Plegar osciloscopio inferior |
| `G` | Anclar / Quitar gráfico del componente o nodo en el panel derecho |
| `Ctrl + Clic` / Arrastrar en fondo | Selección múltiple de componentes y cables |
| `Ctrl + A` | Seleccionar todo el circuito |
| `Supr` / `Backspace` | Eliminar elementos o nodos seleccionados |
| `Ctrl + D` | Duplicar selección |
| `Ctrl + Z` | Deshacer último cambio |
| `B` | Minimizar / Expandir catálogo lateral |
| `/` o `Ctrl + F` | Abrir catálogo y enfocar buscador |
| `1` – `9`, `0`, `M` | Inserción rápida de componentes básicos |
