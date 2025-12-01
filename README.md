Mishell – Shell con Pipes y Miprof
Descripción General
Mishell es una shell interactiva escrita en C que incluye:
- Ejecución de comandos externos mediante execvp
- Manejo de múltiples pipes en una misma línea
- Prompt con el directorio actual
- Comando interno exit
- Comando miprof para medir tiempos, memoria y limitar ejecución
Compilación:
gcc mishell.c -o mishell -Wall
Ejecución:
./mishell
Características:
- Ejecución de comandos externos
- Soporte de pipelines
- miprof (ejec, ejecsave, maxtiempo)
- Manejo de señales
- exit
Estructura:
mishell.c - Implementación completa
Notas:
- Hasta 32 comandos en pipeline
- Parsing con strtok_r
- Timers con CLOCK_MONOTONIC
- RSS de ru_maxrss
