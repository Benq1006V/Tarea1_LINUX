EADME – Mishell (Shell con Pipes y Miprof)
Descripción General

Mishell es una implementación sencilla de una shell interactiva escrita en C.
Incluye soporte para:

Ejecución de comandos externos mediante execvp.

Manejo de múltiples pipes en una misma línea.

Visualización de un prompt con el directorio actual.

Comando interno exit para cerrar la shell.

Implementación del comando especial miprof, que permite:

Medir tiempos de ejecución (real, usuario y sistema).

Registrar uso máximo de memoria (RSS).

Limitar tiempo máximo de ejecución de un comando.

Guardar el perfil de ejecución en un archivo.

El sistema está basado en llamadas POSIX como fork, execvp, pipe, dup2, waitpid y en métricas obtenidas con getrusage y clock_gettime.

Compilación

Compila con:

gcc mishell.c -o mishell -Wall

Ejecución

Ejecuta la shell con:

./mishell


El prompt mostrará:

mishell:/ruta/actual$


Puedes ejecutar comandos normales como:

ls
cat archivo.txt
ps aux

Características Principales
1. Ejecución de comandos externos

Mishell crea un proceso hijo y ejecuta el comando con execvp.
Si el comando no existe, muestra:

comando: comando no encontrado

2. Soporte de PIPES

Mishell soporta pipelines de cualquier longitud:

Ejemplos:

ls | grep .c
cat archivo.txt | wc -l
ps aux | grep firefox | wc -l


La implementación construye los pipes dinámicamente y conecta cada comando mediante dup2.

3. Comando Interno: miprof

miprof permite perfilar el rendimiento de cualquier comando.

Modos disponibles

Ejecución simple

miprof ejec comando args


Guardar resultados en archivo

miprof ejecsave archivo comando args


Límite máximo de tiempo

miprof maxtiempo N comando args

Ejemplos

Medir ejecución:

miprof ejec ls -l


Guardar resultado en log.txt

miprof ejecsave log.txt ls -l


Forzar tiempo máximo de 3 segundos

miprof maxtiempo 3 sleep 10

Salida típica
Comando: ls
Tiempo real: 0.002104 s
Tiempo usuario: 0.000315 s
Tiempo sistema: 0.001101 s
Memoria máxima (RSS): 3456 KB

4. Manejo de señales

La shell ignora Ctrl + C para no terminar.

Los procesos hijos sí reciben la señal.

5. Comando exit

Finaliza la shell de manera ordenada.

Estructura del Proyecto
Archivo	Descripción
mishell.c	Implementación completa de la shell con pipes y miprof.
Notas Importantes

El pipeline soporta hasta 32 comandos encadenados.

Los comandos se parsean con strtok_r.

miprof mide tiempos usando CLOCK_MONOTONIC para mayor precisión.

El uso máximo de memoria es tomado desde ru_maxrss.
