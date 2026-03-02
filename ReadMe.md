**Author:** Jared Walker and James Hohn
**Course:** CST-410 — Computer Graphics
**University:** Grand Canyon University

---

## Project Overview

This project demonstrates how different **shininess values** affect specular highlights
using the **Phong lighting model** in C++/OpenGL. Eight cubes are rendered in a 2x4 grid,
each with a unique shininess exponent: **2, 4, 8, 16, 32, 64, 128, and 256**.

The program visually proves that as shininess increases, the specular highlight becomes
smaller, tighter, and more mirror-like — while low shininess values produce a broad,
soft, matte-like glow across the surface.

---

## Assignment Details

The assignment required:

- Writing C++/OpenGL code that reproduces the "Lighting Graphic" reference image
- Demonstrating the visual impact of 8 different shininess values on identical cubes
- Applying the Phong illumination model with ambient, diffuse, and specular components
- Displaying each cube with its corresponding shininess label underneath
- Producing complete, commented code including shaders, illumination, and mesh logic
- Providing documentation covering theoretical background, math concepts, and algorithm flowcharts

---

## Theoretical Background

### Phong Illumination Model

The Phong reflection model breaks lighting into three components:
```
I = Ka·Ia + Kd·max(N·L, 0)·Id + Ks·max(R·V, 0)^shininess·Is
```

| Symbol | Meaning |
|--------|---------|
| Ka, Kd, Ks | Ambient / diffuse / specular material coefficients |
| Ia, Id, Is | Ambient / diffuse / specular light intensities |
| N | Surface normal (unit vector) |
| L | Direction from surface to light |
| R | Perfect reflection of L about N |
| V | Direction from surface to camera |
| shininess (α) | Exponent controlling highlight tightness |

### Shininess Values Explained

| Value | Visual Effect |
|-------|--------------|
| 2 | Extremely broad glow — nearly the entire face is lit. Resembles chalk or raw concrete. |
| 4 | Wide highlight, still very soft. Similar to unfinished wood. |
| 8 | Highlight begins to condense. Resembles matte paint. |
| 16 | Moderate highlight. Resembles satin fabric. |
| 32 | Clearly defined circular highlight. Resembles polished plastic. |
| 64 | Compact bright highlight. Resembles lacquered wood. |
| 128 | Near-mirror quality. Resembles polished chrome. |
| 256 | Tiny intense dot. Resembles highly polished metal or glass. |

---

## What Was Done in This Assignment

1. **Built the OpenGL scene** using GLUT with a perspective camera positioned at `(0, 0, 20)`
2. **Configured Phong lighting** using `GL_LIGHT0` with:
   - Low ambient (`0.15`) for strong face contrast
   - Full white diffuse and specular light
   - Directional light from upper-right `(0.5, 0.7, 1.0)`
3. **Rendered 8 cubes** using `glutSolidCube` in a 2-row × 4-column grid
4. **Applied identical rotation** (`-20° X, +30° Y`) to every cube so only shininess changes the appearance
5. **Drew bitmap labels** beneath each cube using `glutBitmapCharacter`
6. **Set material properties** per cube — only `GL_SHININESS` changes between cubes
7. **Tuned lighting values** so low-shininess cubes show broad highlights and high-shininess cubes show tight specular dots

---

## Algorithm (High-Level Flowchart)
```
START
│
├─ glutInit() — initialize GLUT window system
├─ glutInitWindowSize(1000, 700)
├─ glutCreateWindow("Shininess Comparison")
│
├─ initLighting()
│   ├─ Enable GL_LIGHTING, GL_LIGHT0, GL_DEPTH_TEST
│   ├─ Set light position (directional, upper-right)
│   ├─ Set ambient, diffuse, specular light colors
│   └─ Set base material diffuse + specular colors
│
├─ display() [called each frame]
│   ├─ glClear(COLOR | DEPTH)
│   ├─ gluLookAt(0,0,20 → 0,0,0)
│   │
│   ├─ TOP ROW (i = 0..3): shininess = 2, 4, 8, 16
│   │   └─ drawCubeWithShininess(x, +2.0, shininessValues[i])
│   │       ├─ glTranslatef(x, y, 0)
│   │       ├─ glRotatef(-20, X) then glRotatef(+30, Y)
│   │       ├─ glMaterialf(GL_SHININESS, shininess)
│   │       ├─ glutSolidCube(1.5)
│   │       └─ drawText label underneath
│   │
│   └─ BOTTOM ROW (i = 4..7): shininess = 32, 64, 128, 256
│       └─ drawCubeWithShininess(x, -2.0, shininessValues[i])
│
└─ glutMainLoop() — keep window open
```

---

## Project Structure
```
project_6/
├── project_6.cpp       # Complete commented C++ source
├── README.md           # This file
└── README.txt          # Plain text instructions and software requirements
```

---

## How to Compile and Run

### Requirements

| Dependency | Install Command |
|------------|----------------|
| g++ (C++17) | `sudo apt-get install build-essential` |
| FreeGLUT | `sudo apt-get install freeglut3-dev` |
| GLEW | `sudo apt-get install libglew-dev` |
| GLU | included with `freeglut3-dev` |

### Compile
```bash
g++ project_6.cpp -o project_6 -lGL -lGLU -lGLEW -lglut -std=c++17
```

### Run
```bash
./project_6
```

### One-Line Compile and Run
```bash
g++ project_6.cpp -o project_6 -lGL -lGLU -lGLEW -lglut -std=c++17 && ./project_6
```

---

## Controls

| Key | Action |
|-----|--------|
| ESC | Exit the program |

---

## Screenshot

> *(Insert screenshot of your running program here)*

---

## References

de Vries, J. (2021). *Basic lighting*. LearnOpenGL.
https://learnopengl.com/Lighting/Basic-Lighting

Khronos Group. (2024). *OpenGL wiki: Fragment shader*.
https://www.khronos.org/opengl/wiki/Fragment_Shader

Phong, B. T. (1975). Illumination for computer generated pictures.
*Communications of the ACM, 18*(6), 311–317.
https://doi.org/10.1145/360825.360839

Shreiner, D., Sellers, G., Kessenich, J., & Licea-Kane, B. (2013).
*OpenGL programming guide* (8th ed.). Addison-Wesley.

The Khronos Group. (2024). *GLUT documentation*.
https://www.opengl.org/resources/libraries/glut/
