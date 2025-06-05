# 🧠 CPU del Robot - Descripción del Problema

## Objetivo General

Diseñar una clase `CPU` en Python que funcione como el "cerebro" de un robot, capaz de:

1. Leer instrucciones desde un archivo `instructions.asm`.
2. Ejecutar cada instrucción en una cuadrícula bidimensional.
3. Dibujar el estado del campo tras cada instrucción.
4. Marcar visualmente la trayectoria del robot, el punto inicial (`S`), el punto final (`E`), y su dirección actual (`↑`, `→`, `↓`, `←`).

---

## Especificaciones Técnicas

### Clase: `CPU`

- **Atributos principales**:
  - `filename`: nombre del archivo `.asm` que contiene las instrucciones.
  - `grid_size`: tamaño del campo (10x10).
  - `field`: matriz de caracteres que representa el campo.
  - `x, y`: coordenadas actuales del robot (inicia en el centro).
  - `angle`: orientación actual del robot en grados (0=arriba, 90=derecha, 180=abajo, 270=izquierda).

### Métodos:

- `__init__`: Inicializa la CPU, el campo, las coordenadas y el ángulo.
- `load_instructions`: Lee el archivo `.asm` y convierte cada línea en una instrucción.
- `execute`: Ejecuta cada instrucción, actualiza el campo y dibuja tras cada paso.
- `turn(angle)`: Cambia el ángulo del robot.
- `move(steps)`: Avanza en la dirección actual cierta cantidad de pasos, marcando su camino con `*`.
- `get_direction()`: Retorna el vector de movimiento según el ángulo.
- `get_direction_symbol()`: Retorna el símbolo de dirección visual (`↑`, `→`, `↓`, `←`).
- `draw_field()`: Dibuja el campo en consola.

---

## Formato de Instrucciones (`instructions.asm`)

El archivo `.asm` debe contener líneas con el siguiente formato:


- MOV,3
- TURN,90
- MOV,2
- TURN,90
- MOV,4

MOV,n: Mueve al robot n pasos en la dirección actual.
TURN,angle: Gira el robot angle grados en sentido horario.

## Validaciones

- El robot no puede salirse de los límites del campo (10x10).
- Si intenta hacerlo, el programa se detiene mostrando un error.
- Solo se permite avanzar dentro del rango [0, 9] en ambas coordenadas.
