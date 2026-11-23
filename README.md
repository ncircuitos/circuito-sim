[README.md](https://github.com/user-attachments/files/35302743/README.md)
# Ω Ncircuitos — Simulador de Circuitos Electrónicos en Tiempo Real

Simulador interactivo de circuitos electrónicos en tiempo real diseñado para ejecutarse directamente en el navegador en un único archivo autónomo (`index.html`), sin dependencias externas.

---

## Novedades de la Última Versión (Changelog)

### 1. Nuevos Componentes Electrónicos (44 tipos en total)
- **MOSFET Canal-P (`pmos`)**: Terminales Gate (`G`), Source (`S`) y Drain (`D`), conducción por umbral $V_{SG} > |V_{th}|$, parámetros `vth`, `kp`, `maxPower`, diodo parásito (*body diode*) $D \to S$ y protección térmica.
- **Fuente de Pulso / PWM (`pulse_source`)**: Generador configurable con niveles `vLow` y `vHigh`, `frequency` (Hz), `dutyCycle` (5% a 95%) y retardo inicial `delay` (ms) para ensayos de PWM y respuesta al escalón en redes RC/RL.
- **Transformador Acoplado (`transformer`)**: Cuatro terminales (`P1`, `P2` en primario; `S1`, `S2` en secundario) con relación de espiras configurable `ratio` ($N_2/N_1$), resistencia de devanado `rWinding`, aislamiento galvánico e integración tanto en simulación transitoria como en barrido AC (Diagrama de Bode).
- **Contador Binario de 4 Bits (`counter_4bit`)**: Entradas síncronas `CLK` (disparo por flanco ascendente) y `RST` (reinicio asíncrono), con salidas `Q0..Q3` alineadas pin a pin con las entradas `D0..D3` del Display de 7 Segmentos (`seven_seg`).

### 2. Modelos Comerciales Reales en el Inspector
- Selector desplegable **"Modelo comercial"** para cargar con un clic parámetros de hojas de datos reales (pasando automáticamente a *"Personalizado"* si luego se ajusta algún slider manualmente):
  - **Diodos (`diode`)**: Genérico (0.7 V), `1N4148` (0.72 V, 0.3 A), `1N4007` (0.7 V, 1 A), `1N5819 Schottky` (0.32 V, 1 A).
  - **Transistores NPN (`npn`)**: Genérico ($\beta=100$), `2N2222` ($\beta=150$), `BC547` ($\beta=250$), `TIP31` ($\beta=50$, 5 W).
  - **Transistores PNP (`pnp`)**: Genérico ($\beta=100$), `2N3906` ($\beta=150$), `BC557` ($\beta=250$), `TIP32` ($\beta=50$, 5 W).
  - **MOSFET Canal-N (`nmos`)**: Genérico, `2N7000` ($V_{th}=2.1\text{ V}$, $K_p=0.1$), `IRFZ44N` ($V_{th}=3.0\text{ V}$, $K_p=1.2$, 15 W).
  - **MOSFET Canal-P (`pmos`)**: Genérico, `BS250` ($|V_{th}|=2.2\text{ V}$, $K_p=0.1$), `IRF9540N` ($|V_{th}|=3.0\text{ V}$, $K_p=1.0$, 15 W).
  - **Amplificadores Operacionales (`opamp`)**: Genérico, `LM741` ($A_{OL}=100\,000$, $\pm 15\text{ V}$), `TL071` ($A_{OL}=200\,000$, $\pm 15\text{ V}$).

### 3. Rediseño Minimalista del Catálogo y Command Palette
- **Estética Oscura y Compacta**: Tarjetas estilizadas con bordes finos, iconos SVG uniformes y botón **`Lista` / `Grilla`** para alternar entre grilla de 2/3 columnas y lista densa.
- **Tira Fija "Recientes / Favoritos"**: Muestra hasta 6 componentes de acceso rápido combinando favoritos fijados con estrella (`★`, guardados en `localStorage`) y los últimos componentes colocados en el lienzo.
- **Categorías en Fila Única y Memoria de Secciones**: Navegación por *pills* horizontales sin ocupar altura extra y persistencia de secciones plegadas/expandidas en `localStorage`.
- **Búsqueda Inteligente por Sinónimos y Prefijos (`/` o `Ctrl + F` o `⌘K`)**: Reconoce nombres, prefijos exactos (`R`, `C`, `L`, `Q`, `M`, `D`, `U`, `V`, `T`), atajos y sinónimos en español/inglés (*"bobina"*, *"pila"*, *"transistor"*, *"trafo"*, *"pwm"*, *"zumbador"*, etc.).
- **Drag & Drop Directo al Lienzo + Pie Informativo**: Permite arrastrar componentes desde el catálogo directamente hacia la grilla (con vista previa fantasma en vivo) y muestra en el pie del panel una descripción de 1 línea junto con la lista de pines (ej. `Pines: G · D · S`).

### 4. Análisis AC (Bode), Osciloscopio con Trigger, Redo y Exportaciones
- **Diagrama de Bode Interactivo (Análisis AC)**: Barrido logarítmico en frecuencia con solver matricial complejo, detección automática de frecuencia de corte $f_c$ ($-3\text{ dB}$), cursores de magnitud (dB o V) y fase (°), y botón **"Exportar CSV"**.
- **Sincronización por Trigger y Cursores Estabilizados**: Disparo configurable por canal (`Trigger Source`), nivel (`Trigger Level`, botones `50%` y `0V`) y flanco (`Rising` / `Falling`), con tiempos de cursor `t₁` y `t₂` relativos a la ventana visible, interpolación sub-muestra y ancho tabular fijo (`tabular-nums`).
- **Modo SPICE (`proMode`) y Sonda Interactiva (`P`)**: Vista esquemática técnica limpia estilo LTSpice/KiCad y punta de prueba para medir tensión nodal/diferencial o corriente (`Alt + Clic`).
- **Rehacer (`Redo`) y Exportación `PNG`**: Pila `redoStack` vinculada a `Ctrl + Y` y `Ctrl + Shift + Z`, y botón **`PNG`** en la barra superior para descargar una captura limpia del esquemático.

### 5. Optimizaciones de Rendimiento (-40.5% tiempo total por frame)
- **Solver MNA (`solver.js`)**: Cacheo de topología entre frames (`getTopology`), pre-estampado de red conductora fija en `staticA` y componentes lineales en `baseA` (`Float64Array`), reduciendo el trabajo dentro del lazo de Newton-Raphson exclusivamente a los elementos no lineales.
- **Osciloscopio (`oscilloscope.js`)**: Reciclado de muestras `{ t, v, i }` mediante *Object Pooling* (`_samplePool`) y cacheo de claves para eliminar presión sobre el *Garbage Collector*.
- **Renderizador Canvas (`renderer.js`)**: Cacheo por firma geométrica de obstáculos de etiquetas, uniones T y redes conectadas, cacheo de `measureText` y trazado agrupado de partículas de corriente sin `shadowBlur` por partícula.

---

## Características Generales

- **Motor Físico MNA en Tiempo Real**: Resolución matricial nodal modificada (Modified Nodal Analysis) con integración trapezoidal y Newton-Raphson para componentes lineales, no lineales y digitales.
- **Analizador Osciloscopio Expandido**: Doble clic en cualquier gráfico para abrir la vista superior ampliada con cursores interactivos para medir $\Delta t$, $\Delta V$, $\Delta I$, frecuencia ($1/\Delta t$) y pendientes ($\Delta V/\Delta t$), además de auto-detección de constante de tiempo ($1\tau$ al $63.2\%$) y picos mín/máx.
- **Punto de Operación DC (`.op`)**: Tabla modal con tensiones de nodo respecto a GND, terminales conectados, caída de tensión, corriente y potencia por rama, balance de conservación de potencia ($P_{\text{fuentes}}$ vs $P_{\text{disipada}}$) y copia a CSV.
- **Compartir Circuito mediante Enlace (URL Hash)**: Compresión `deflate-raw` en tokens URL-safe (`#c=z...`), copia al portapapeles y carga automática validada.
- **Etiquetas de Red (Net Labels)**: Conexiones equipotenciales virtuales entre nodos con el mismo identificador (`VCC`, `GND`, `0V`, `CLK`, `V_IN`, `V_OUT`).

---

## Atajos de Teclado

| Tecla | Acción |
| :--- | :--- |
| `Espacio` | Pausar / Reanudar simulación |
| `Shift + R` | Reiniciar simulación desde `t = 0` |
| `W` | Modo Trazar Cable |
| `P` | Herramienta Medir / Sonda interactiva (`Alt + Clic` para corriente) |
| `Shift + P` | Abrir / Cerrar tabla de Punto de Operación DC (`.op`) |
| `R` | Rotar componente 90° |
| `V` | Mostrar / Ocultar etiquetas de voltaje en los nodos |
| `C` | Centrar la vista y zoom en el circuito |
| `G` | Anclar / Quitar gráfico del componente o nodo en el panel derecho |
| `Tab` | Alternar ancho rápido del panel derecho |
| `B` | Minimizar / Expandir catálogo lateral izquierdo |
| `/` o `Ctrl + F` | Abrir catálogo / Command Palette y enfocar buscador |
| `Ctrl + Clic` / Arrastrar en fondo | Selección múltiple de componentes y cables |
| `Ctrl + A` | Seleccionar todo el circuito |
| `Ctrl + D` | Duplicar selección |
| `Ctrl + Z` | Deshacer último cambio (Undo) |
| `Ctrl + Y` / `Ctrl + Shift + Z` | Rehacer cambio (Redo) |
| `Supr` / `Backspace` | Eliminar elementos o nodos seleccionados |
| `1` – `9`, `0`, `M` | Inserción rápida de componentes frecuentes |
