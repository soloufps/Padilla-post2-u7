# Arquitectura de Computadores  
## Unidad 7: Manejo de Pantalla y Teclado — Post-Contenido 2  
### Ingeniería de Sistemas — 2026  
### Estudiante: Sebastian Jose Padilla Escalante  

---

##  Descripción del laboratorio

En este laboratorio se trabajó con lenguaje ensamblador x86 utilizando DOSBox y NASM.  
El objetivo principal fue comprender el manejo de entrada/salida de bajo nivel mediante:

- Interrupción INT 16h para lectura de teclado
- Acceso directo al segmento de video B800h
- Manipulación de atributos de color en modo texto
- Uso de instrucciones como REP STOSW para optimización de pantalla

Este laboratorio permite entender cómo el hardware y el software interactúan sin depender del sistema operativo.

---

## ⌨️ 1. Lectura de teclado con INT 16h

Se utilizó la interrupción BIOS INT 16h para capturar teclas presionadas por el usuario.

### Características:

- AH = scan code
- AL = ASCII
- Detección de teclas normales y extendidas
- Finalización del programa con tecla ESC

### Resultado:

El programa muestra en pantalla:
- Código hexadecimal del scan code
- Código ASCII de la tecla

Esto permite identificar teclas especiales como flechas, F1–F12, Insert, Delete, etc.

---

## 2. Acceso directo a memoria de video (B800h)

Se trabajó con el segmento de memoria VGA en modo texto:


Segmento: B800h
Modo: texto 80x25


Cada celda de pantalla ocupa 2 bytes:
- Byte 1: carácter ASCII
- Byte 2: atributo de color

### Fórmula de cálculo de posición:


offset = (fila * 80 + columna) * 2


### Resultado:

Se logró escribir caracteres directamente en pantalla sin usar INT 10h, controlando:

- Posición exacta
- Color de texto
- Color de fondo

---

## 3. Relleno de pantalla con REP STOSW

Se utilizó la instrucción REP STOSW para optimizar la escritura en memoria de video.

### Funcionamiento:

- AX contiene carácter + atributo
- ES:DI apunta a memoria de video
- CX controla cantidad de posiciones

### Resultado:

- Limpieza completa de pantalla
- Fondo uniforme
- Escritura eficiente sin interrupciones BIOS

---

## 4. Mini editor de texto (INT 16h + B800h)

Se implementó un editor básico que:

- Lee teclado en tiempo real con INT 16h
- Escribe caracteres directamente en B800h
- Avanza el cursor automáticamente
- Mantiene escritura en una fila fija

### Resultado:

El usuario puede escribir texto que aparece instantáneamente en pantalla sin usar funciones del sistema operativo.

---

## Estructura del repositorio
apellido-post2-u7/
│
├── post2a.asm → Lectura de teclado (INT 16h)
├── post2b.asm → Escritura directa en B800h
├── post2c.asm → REP STOSW (limpieza de pantalla)
├── post2d.asm → Mini editor de texto
├── README.md → Documentación del laboratorio
└── capturas/
##Evidencias

Las capturas muestran la ejecución en DOSBox:

- Lectura de scan codes y ASCII
- Escritura directa en pantalla
- Limpieza de pantalla con REP STOSW
- Funcionamiento del mini editor

---

##Conclusión

Este laboratorio permitió comprender el funcionamiento interno del teclado y la memoria de video en arquitectura x86.

Se aprendió a:

- Capturar entradas del teclado a bajo nivel
- Manipular directamente la memoria VGA
- Controlar colores y posiciones en pantalla
- Optimizar operaciones con instrucciones de cadena

Estos conceptos son fundamentales para entender cómo los sistemas operativos interactúan con el hardware.
