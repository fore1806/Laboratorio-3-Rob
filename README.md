# Tercer Laboratorio - Robótica Industrial No. 2 - Entradas y Salidas :robot: 
 
Tercer laboratorio de la asignatura Robótica de la Universidad Nacional de Colombia en su sede Bogotá. 
 
## Autores :busts_in_silhouette: 
 
|              Nombre              |GitHub nickname| 
|----------------------------------|---------------| 
| Nikolai Alexnder Caceres Penagos |[nacaceresp](https://github.com/nacaceresp)| 
|    Andrés Felipe Forero Salas    |[fore1806](https://github.com/fore1806)| 
| Iván Mauricio Hernández Triana   |[elestrategaactual](https://github.com/elestrategaactual)| 
 
## Introducción 
La realización de tareas de forma automatizada cobra una mayor importancia en la vida del ser humano con el paso de los años, y es aquí donde la utilización y programación de sistemas robóticos automatizados capaces de seguir con fidelidad y precisión una serie de directrices definidas por un usuario se convierte en una necesidad dentro de la formación profesional de un ingeniero mecatrónico. Sin embargo, en muchos casos se hace necesario la utilización de dispositivos de entrada y salida para la ejecución de programas o con el simple hecho de permitir la operación del sistema de forma más simplificada buscando que este pueda ser manejado por operarios menos calificados. De esta forma, mediante la realización de este laboratorio, se genera un primer acercamiento a la programación de bucles y condicionales para el robot con el fin de obtener secuencias lógicas a partir de diferentes entradas y generar salidas que ejecuten una función adicional en el sistema robotizado. 
 
## Solución planteada. 
 
### Elementos previos necesarios 
Este laboratorio se basa en el desarrollo del Laboratorio 1 el cual se encuentra disponible aquí https://github.com/fore1806/Laboratorio-1-Rob, en este repositorio se podrá encontrar información sobre la herramienta trabajo, la creación de work objects dentro del espacio del sistema, así como la creación de trayectorias para la realización de los caracteres. 
 
### Reconocimiento entradas y salidas del robot 
Como primer paso se realiza un reconocimiento de las entradas y salidas presentes en el Robot para este caso solo se van a utilizar entradas y salidas digitales por lo cual mediante el uso del FlexPendant se procede a verificar las salidas digitales y entradas programadas en el robot 

 

![](https://github.com/fore1806/Laboratorio-3-Rob/blob/master/Imagenes/Salidas%20Digitales%20Robot%201%20LAB_SIR.jpeg) 
 
 ![](https://github.com/fore1806/Laboratorio-3-Rob/blob/master/Imagenes/Entradas%20Digitales%20Robot%201%20LAB_SIR.jpeg) 
Una vez identificadas estas se procede a identificar la correspondencia de estas con los pulsadores e indicadores lumínicos presentes en el tablero del laboratorio obteniéndose el siguiente esquema 
 

 ![](https://github.com/fore1806/Laboratorio-3-Rob/blob/master/Imagenes/Tablero_I-O_LAB_SIR.png) 
 
 
### Programación del robot 
 
Para la programación del robot; se tiene como base el programa del laboratorio 1; adicionalmente se crea una nueva posición que facilitará el montaje y desmontaje de herramientas. Este punto se agrega a una nueva ruta llamada *ToolMoving* que permite desplazar el robot a la postura especificada a la hora de crear el target. En este punto el sistema esperará hasta que se presione el primer pulsador dentro del tablero (*DI_02*) para desplazarse a la posición de acercamiento; botón que no debe accionarse hasta que la herramienta no se encuentre debidamente asegurada.  
 
A continuación, el robot es llevado a la postura de acercamiento en la que espera a una nueva confirmación por parte del usuario para comenzar el proceso de escritura; para esto se emplea la segunda entrada digital del sistema, correspondiente al botón 2 del tablero (*DI_02*). Una vez se pulsa este botón, comienza el proceso de escritura identificado con el testigo verde que es identificado en el sistema robotizado como la salida digital 1 (* DO_01*). 
 
Finalmente, al terminar el segundo carácter se apaga el testigo verde y se espera nuevamente por el accionamiento del pulsador 1, que permita al usuario del sistema revisar que no exista ninguna barrera física o alguna persona, previniendo de esta forma cualquier posible accidente o alguna avería del sistema robotizado; antes de llevar al robot nuevamente a la posición de *Home*. 
 
La secuencia del programa se muestra en el código a continuación. 
 
```AMPL 
    PROC main() 
        !Añada aquí su código 
        Homing; 
        ToolMoving; 
        WaitDI DI_01,1; 
        MidGoing; 
        WaitDI DI_02,1; 
        SetDO DO_01,1; 
        IRoute; 
        FRoute; 
        SetDO DO_01,0; 
        WaitDI DI_01,1; 
        MidGoing; 
        ToolMoving; 
        Homing; 
    ENDPROC 
``` 
 
 
### VIDEO 
En el siguiente video se puede evidenciar los resultados obtenidos en el laboratorio 
[![Alt text](https://github.com/fore1806/Laboratorio-3-Rob/blob/master/Imagenes/Imagen%20Video.png)](https://www.youtube.com/watch?v=FElJ00nn7_k) 
 
### Conclusiones 
 
 
-   Es muy importante tener diferentes entradas y salidas digitales que le permitan al operario, no tan calificado, manipular el robot de una manera sencilla por medio de pulsadores y de la misma manera observar y/o verificar por medio de lámparas el proceso que el robot se encuentre ejecutando. 
-   Se encuentra en el uso de dispositivos de entrada tales como botones, dotan al sistema de un mayor control de proceso; lo que termina traduciéndose en mayor seguridad al momento de la operación. 
-   El correcto cableado de los dispositivos usados como entradas o salidas es de vital importancia ya que este es un punto crítico donde se puede presentar fallas en un proceso industrial. 

