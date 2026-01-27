##### Rings Protection
- Antiguamente, en las CPU con arquitectura x86 se utilizaba un sistema de anillos que definian niveles de privilegios.
- Ring 0: Seria actualmente el Kernel Mode. Maximo Privilegio.
- Ring 3: Seria actualmente el User Mode. Minimo Privilegio.
- Los Rings 1 y 2 existen pero actualmente no se usan en sistemas operativos modernos como Windows o Linux. 

![UserMode-KernelMode](usermode-kernelmode.png)
##### User Mode and Kernel Mode
- Dos modos diferentes en la que la CPU opera cuando la computadora tiene Windows instalado: el modo de usuario y el modo del kernel.
- Los programas o aplicaciones generalmente se ejecutan en el modo usuario y el código del sistema operativo se ejecuta en el modo kernel.
- En el modo Kernel el código que se ejecuta tiene acceso sin restricciones al hardware y es capaz de ejecutar instrucciones a la CPU. El modo kernel también puede referenciar cualquier dirección de memoria directamente las cuales generalmente estan reservadas para las funcionas mas confiables del sistema operativo.
- En el modo Usuario se ejecutan generalmente las aplicaciones/programas/software los cuales no tienen acceso directo a la memoria ni al hardware. El código que se ejecuta en el modo usuario debe ir a traves del sistema operativo para acceder a los recursos del hardware. La mayoria de programas en windows se ejecutan en user mode.
- Drivers del dispositivo: Piezas de software que permiten la comunicación entre el sistema operativo y el hardware las cuales pueden ejecutarse en kernel mode o user mode, dependiendo del driver.
- Todo el código que se ejecuta en el modo kernel usa el mismo espacio en la memoria.
- Los drivers del modo kernel no tienen aislamiento con el sistema operativo, por lo que si algun error surge con el driver ejecutandose en el modo kernel y es escrito en un espacio de memoria equivocado el sistema operativo o otro driver en el kernel mode podrian verse afectados negativamente causando que el sistema operativo sufra de un crasheo (como la pantalla azul de Windows)
- La tendencia moderna de Windows es mover tantos drivers como sea posible a User Mode para mejorar la estabilidad del sistema.

##### System Calls
- El user mode no puede simplemente saltar al kernel, para "pedirle algo" al hardware utiliza las llamadas System Calls (Llamadas al sistema). Cuando un programa necesita leer un archivo o enviar un paquete por red: 1. El programa ejecuta una instruccion especial 2. La CPU cambia de modo usuario a modo kernel 3. EL kernel valida la petición, la ejecuta y luego devuelve el control al programa bajando nuevamente al modo usuario. 
 
##### Memory Access
- En User Mode, cada proceso cree que tiene toda la memoria para si mismo (lo que se conoce como isolation o aislamiento), por ejemplo, el proceso A no puede ver la memoria del proceso B.
- En Kernel Mode, el código ve toda la memoria del sistema. Por eso un driver mal programado puede "pisar" datos de otro componente esencial.