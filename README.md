# Cub3D

Motor 3D por **raycasting** al estilo de Wolfenstein 3D, escrito en C con **MiniLibX**. Proyecto en
pareja del Common Core de **42 Madrid**: lee un mapa desde un fichero `.cub` y lo pinta en primera
persona y en tiempo real, con texturas en las paredes, colisiones y un minimapa.

**Nota: 115/100** (con bonus)

## Características

- Raycasting con algoritmo DDA y una textura distinta para cada orientación de pared (N, S, E, O).
- Colores de suelo y techo configurables.
- Movimiento con colisiones y rotación de la cámara.
- Minimapa (bonus).
- Validación completa del fichero `.cub`, con un mensaje de error para cada fallo. En `maps/invalid/` hay
  decenas de mapas mal formados para probarla.

## Compilar y ejecutar

Necesita GCC y Make. En Linux, además, las librerías de X11 (`libx11-dev`, `libxext-dev`). Las dos
versiones de MiniLibX vienen en el repo.

```sh
git clone https://github.com/VolmerES/Cub3D.git
cd Cub3D
make            # Linux (por defecto)
make macos      # macOS
./cub3D maps/valid/map_cave.cub
```

### Controles

| Tecla | Acción |
|---|---|
| `W` `A` `S` `D` | Moverse |
| `←` `→` | Girar la vista |
| `ESC` | Salir |

## Formato del mapa

Un fichero `.cub` lleva las cuatro texturas, los colores de suelo (`F`) y techo (`C`) en RGB y, al
final, el mapa:

```txt
NO ./textures/wall_1.xpm
SO ./textures/wall_2.xpm
WE ./textures/wall_3.xpm
EA ./textures/wall_4.xpm

F 205,180,219
C 189,224,254

1111111111
1000000001
10N0000001
1000000001
1111111111
```

| Carácter | Significado |
|:-:|---|
| `1` | Pared |
| `0` | Espacio libre |
| `N` `S` `E` `W` | Posición inicial del jugador y hacia dónde mira |

El mapa tiene que estar cerrado por paredes y llevar un solo jugador.

## Estructura

| Carpeta | Contenido |
|---|---|
| `src/parsing/` | Lectura y validación del `.cub` |
| `src/rendering/` | Raycasting y dibujo de cada fotograma |
| `src/movement/` | Movimiento, rotación y colisiones |
| `src/textures/` | Carga de las texturas XPM |
| `src/bonus/minimap/` | Minimapa |
| `maps/` | Mapas válidos, inválidos y de bonus |

Para buscar fugas de memoria: `valgrind --leak-check=full ./cub3D maps/valid/map_cave.cub`.

## Autores

- **Sergio Marín Álvarez** (`smarin-a`) · [@sermaal11](https://github.com/sermaal11)
- **Juan Bautista Delorme** (`jdelorme`) · [@VolmerES](https://github.com/VolmerES) ·
  [portafolio](https://juandelorme-portfolio.volmer.es) · [LinkedIn](https://www.linkedin.com/in/jdelorme/)
