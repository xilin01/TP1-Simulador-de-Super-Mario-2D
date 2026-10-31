# Simulador de Super Mario 2D

![Java](https://img.shields.io/badge/Java-21-orange?logo=openjdk)
![JUnit](<https://img.shields.io/badge/tests-JUnit%205-25A162?logo=junit5>)

Juego de Super Mario por turnos que se ejecuta en la consola, desarrollado en Java para la asignatura **Tecnología de la Programación I**.

```
Time: 100
Points: 0
Lives: 3

     0   1   2   3   4   5   6   7   8   9   10  11  12  13  14  15  16  17  18  19  20  21  22  23  24  25  26  27  28  29 
   ┌————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————┐
  0┃                                                                                                                        ┃0
  1┃                                                                                                                        ┃1
  2┃                                                    ????                                                                ┃2
  3┃                                                                                                                        ┃3
  4┃                                                                                                                        ┃4
  5┃                                                 🐻                             ????                                    ┃5
  6┃                                            ▓▓▓▓▓▓▓▓????▓▓▓▓▓▓▓▓                                                        ┃6
  7┃                                                                                                                        ┃7
  8┃                         🍄                                                          🍄                  🐻             ┃8
  9┃                ▓▓▓▓????▓▓▓▓0000                                     🐻     ▓▓▓▓▓▓▓▓▓▓▓▓                ▓▓▓▓            ┃9
 10┃                                                                    ▓▓▓▓▓▓▓▓                        ▓▓▓▓▓▓▓▓            ┃10
 11┃         🧍                                                         ▓▓▓▓▓▓▓▓                    ▓▓▓▓▓▓▓▓▓▓▓▓            ┃11
 12┃         🧍              🐻                  🐻          🐻         ▓▓▓▓▓▓▓▓             🐻 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓         🚪 ┃12
 13┃▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃13
 14┃▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓┃14
   └————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————┘

Command > action right right up
```

---

## Características

- Tablero de 30 × 15 casillas con Mario, Goombas, suelo, cajas sorpresa, champiñones y puerta de salida.
- Física simple por turnos: gravedad, colisiones, Mario grande/pequeño, puntos, vidas y tiempo.
- Varios niveles predefinidos y carga/guardado de partidas desde fichero de texto.
- Comando `addObject` para modificar el mapa en tiempo de ejecución.
- Vista en color (códigos ANSI) o en texto plano.
- Batería de tests de aceptación con JUnit 5.

---

## Comandos

| Comando                               | Atajo  | Descripción                                            |
| ------------------------------------- | ------ | ------------------------------------------------------- |
| `action [RIGHT\|LEFT\|UP\|DOWN\|STOP]+` | `a`  | Mario realiza una o varias acciones (`a r r u`)       |
| `update` o línea vacía            | `u`  | Avanza un ciclo sin acción                             |
| `addObject <objeto>`                | `aO` | Añade un objeto, p. ej. `aO (12,3) Mario LEFT SMALL` |
| `reset [nivel]`                     | `r`  | Reinicia la partida o carga otro nivel                  |
| `save <fichero>`                    | `s`  | Guarda el estado actual                                 |
| `load <fichero>`                    | `l`  | Carga una partida (p. ej. `load conf_1`)              |
| `help`                              | `h`  | Muestra la ayuda                                        |
| `exit`                              | `e`  | Sale del juego                                          |

---

## Cómo ejecutarlo

Requisitos: **Java 21** o superior.

```bash
cd SuperMario
javac -d bin $(find src -name "*.java" ! -name "Test*")
java -cp bin tp1.Main 1            # nivel 1 con colores
java -cp bin tp1.Main 1 NO_COLORS  # sin colores (consolas sin ANSI)
```

También se puede importar la carpeta `SuperMario` como proyecto existente en **Eclipse**.

En Windows se recomienda usar Windows Terminal para que se vean los emojis.

---

## Tests

`src/tp1/Tests_V3.java` ejecuta las partidas de `tests/pr3/` y compara la salida con la esperada. Se lanzan desde Eclipse (*Run As → JUnit Test*) con `SuperMario` como directorio de trabajo.

---

## Estructura

```
SuperMario/
├── src/tp1/
│   ├── Main.java
│   ├── control/            # Controller y comandos (patrón Command)
│   ├── logic/              # Game, contenedor de objetos, configuraciones de nivel
│   │   └── gameobjects/    # Mario, Goomba, Box, Mushroom, Land, ExitDoor (+ factoría)
│   ├── view/               # Vistas de consola y mensajes
│   ├── exceptions/         # Jerarquía de excepciones propias
│   └── util/
├── tests/                  # Entradas y salidas esperadas de cada práctica
└── conf_*                  # Partidas guardadas de ejemplo
Diagramas/                  # Diagramas UML de las prácticas 1, 2 y 3
```

---

## Diseño

- **MVC**: `Controller` lee comandos, `Game` contiene la lógica y `GameView` la pinta.
- **Command**: cada comando es una clase y `CommandGenerator` los parsea.
- **Factory**: `GameObjectFactory` crea objetos a partir de texto (para `addObject` y `load`).
- **Interfaces** `GameModel`, `GameWorld` y `GameStatus` limitan lo que ve cada parte del juego.

Diagramas UML: [Práctica 1](<Diagramas/Pr%C3%A1ctica%201.pdf>) · [Práctica 2](<Diagramas/Pr%C3%A1ctica%202.pdf>) · [Práctica 3](<Diagramas/Pr%C3%A1ctica%203.pdf>)
