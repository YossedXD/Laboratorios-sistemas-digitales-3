# Laboratorio 2 — Interacción inicial con Pepper

## Introducción

En este laboratorio tuvimos la primera experiencia con el robot **Pepper** en el salón de robótica.  
La idea principal fue empezar a conocer cómo se programa y se controla el robot, tanto usando la aplicación **Choregraphe** como desde la terminal con **SSH**.  

Lo que se nos pidió fue:  
- Investigar las librerías que usa Pepper para poder funcionar.  
- Instalar y probar **Choregraphe**, creando una coreografía sencilla con movimientos y frases.  
- Conectarnos al robot por medio de **SSH** (`ssh nao@ip_Pepper`) y hacer unos pasos básicos en Python usando las librerías vistas.  
- Documentar todo el proceso y subirlo al repositorio en la carpeta **Laboratorio 2** junto con este `README.md`.  

Este trabajo lo realizamos:  
- Miguel Angel Montaña Sánchez  
- Jeferson Jair Hernández Garzón  
- Yossed Mauricio Riaño Páez  

## Librerías que investigamos
Las librerías que vimos para poder programar a Pepper fueron:  

- **qi** → la que permite comunicarse con el sistema NAOqi del robot (movimiento, voz, sensores, etc.).  
- **argparse** → sirve para manejar parámetros en los scripts desde la línea de comandos.  
- **sys** → da acceso a cosas internas de Python como argumentos y salidas.  
- **os** → permite trabajar con archivos, directorios y comandos del sistema.  
- **almath** → librería matemática especial de SoftBank para cálculos de posiciones y movimientos.  
- **math** → la librería matemática normal de Python (seno, coseno, raíces, etc.).  
- **motion** → el módulo ALMotion que controla directamente los movimientos de Pepper.  
- **httplib** → para manejar conexiones HTTP (más usado en Python 2).  
- **json** → para trabajar con datos en formato JSON.  

---

