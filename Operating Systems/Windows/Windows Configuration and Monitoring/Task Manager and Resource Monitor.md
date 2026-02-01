#### Task Manager
- El **Task Manager (Administrador de Tareas)** de Windows provee información acerca del software que se ejecuta y en general el rendimiento de la computadora.
- **Processes**: Lista todos los programas y procesos que se encuentran en ejecución. Muestra la CPU, Memoria, Disco y la utilización de la Red de cada proceso. Las propiedades de un proceso pueden examinarse o finalizarse si no se ha realizado correctamente o se ha parada.
- **Performance**: Para ver las estadísticas de rendimiento. Se muestra el uso de la CPU, la Memoria, el Disco y el rendimiento de la Red. 
- **App History**: Muestra el historial de todos los procesos para ver cómo se ha ejecutado desde que se inició la computadora. Sirve para ver las aplicaciones que consumen más recursos de los que deberían. 
- **Startup**: Muestra todas las aplicaciones y servicios que se ejecutan cuando la computadora es iniciada. Es posible deshabilitar programas de este tipo desde esta pestaña.
- **Users**: Muestra todos los usuarios que estan logeados en la computadora. También muestra todos los recursos, como que aplicaciones y procesos están usando cada usuario. 
- **Details**: Similar a la pestaña de procesos, esta pestaña provee información y opciones adicionales para los procesos. Como ajustar la prioridad de los mismos, la afinidad con el CPU para determinar que core o CPU un programa usará, también una caracteristica interesante llamada **Analyze wait chain (Analizar cadena de espera)**  la cual muestra cualquier proceso para el cual otro proceso está esperando. Esta función ayuda a determinar si un proceso simplemente está esperando o está parado.
- **Services**: Todos los servicios cargados se muestran en esta pestaña. Se muestra su **PID (Process ID)**, una breve descripción del servicio y su estado (**Running** o **Stopped**).


#### Resource Monitor
- El monitor de recursos muestra información más detallada acerca de los recursos utilizados del sistema. 

- **Descripción general**: La pestaña muestra el uso general de cada recurso. Si selecciona un solo proceso, se filtrará en todas las pestañas para mostrar solo las estadísticas de ese proceso.
- **CPU**: Se muestra el PID, la cantidad de subprocesos, qué CPU utiliza el proceso y el uso promedio de CPU de cada proceso. Se puede ver información adicional sobre cualquier servicio en el que se base el proceso y los controladores y módulos asociados expandiendo las filas inferiores.
- **Memoria**: En esta pestaña se muestra toda la información y estadísticas sobre cómo cada proceso utiliza la memoria. Además, debajo de la fila Procesos se muestra una descripción general del uso de toda la RAM.
- **Disco**: En esta pestaña se muestran todos los procesos que utilizan un disco, con estadísticas de lectura/escritura y una descripción general de cada dispositivo de almacenamiento.
- **Red**: Todos los procesos que utilizan la red se muestran en esta pestaña, con estadísticas de lectura/escritura. Lo más importante es que se muestran las conexiones TCP actuales, junto con todos los puertos que están escuchando. Esta pestaña es muy útil cuando se intenta determinar qué aplicaciones y procesos se comunican a través de la red. Permite saber si un proceso no autorizado está accediendo a la red, escuchando una comunicación y la dirección con la que se está comunicando.