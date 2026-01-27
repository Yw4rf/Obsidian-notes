##### Windows Processes
Un proceso en Windows es una instancia de un programa en ejecución acompañada de todos los recursos del sistema operativo necesarios para su funcionamiento. Informalmente, un proceso es cualquier programa que se encuentra en ejecución dentro del sistema operativo.
![[Pasted image 20260120210554.jpg]]
- Cada proceso incluye: 
	- **Espacio de direcciones virtual privado**, uno o más **Threads**, un **Token de Seguridad** (**SID, privilegios**), tabla de **handles**, contexto de ejecución, información contable (**CPU, memoria, I/O**), Prioridad base, Módulos cargados (**DLLs**)
- Internamente el kernel representa cada proceso con una estructura llamada `EPROCESS`, esta estructura vive en el **kernel mode** y contiene las referencias a todo lo anterior.
- Cada proceso tiene su propio espacio de memoria virtual aislado del resto.  Un proceso no puede leer ni escribir en memoria de otro proceso directamente. El aislamiento se logra mediante **MMU** (**Memory Management Unit**), **tabla de páginas**, **protección por modo** (**user/kernel mode**).
- En cuanto a seguridad, romper este aislamiento suele implicar **exploits de kernel**, **token stealing**, o **DLL injection**. 

- Ciclo de vida de un proceso: 
	- 1. Creación `CreateProcess`, 2. Inicialización, 3. Ejecución, 4. Terminación `ExitProcess`
- Durante la creación del mismo: 
	- Se le asigna un **PID (Process Identificator)**, se crea el espacio de direcciones, se carga la imagen ejecutable, se inicializa el thread principal, se heredan handles (si corresponde) y se asigna el token de seguridad
Procesos críticos de Windows: Cualquier anomalia en `lsass.exe`, `services.exe` o `winlogon.exe` es considerada **alta severidad**. 

| Proceso        | Función                     |
| -------------- | --------------------------- |
| `System`       | Kernel wrapper (PID 4)      |
| `smss.exe`     | Session Manager             |
| `csrss.exe`    | Client/Server Runtime       |
| `wininit.exe`  | Inicialización del sistema  |
| `services.exe` | Service Control Manager     |
| `lsass.exe`    | Autenticación (muy crítico) |
| `winlogon.exe` | Logon interactivo           |

##### Windows Threads
- Los threads (o subprocesos) son la unidad minima de ejecución que el scheduler (no existe nada más chico que el scheduler pueda ejecutar, el minimo ejecutable es el thread) puede ejecutar en un CPU. EL thread es el que ejecuta el código del programa.
- Un proceso no ejecuta código, quien ejecuta código es el **thread**.
- Cada thread tiene: **Contexto de CPU (Registros, Intruction Pointer)**, un **Stack Propio**, un **Estado de Ejecución (running, ready, waiting)**, **Prioridad**, **Afinidad a CPU**, etc. Todo lo que el CPU necesita para ejecutar. A su vez, cada thread tiene su propio identificador de thread (**TID**) y comparte recursos con otros threads del mismo proceso.
- En el Kernel se representa como `ETHREAD` 
- **Un proceso es un contenedor de recursos que NO ejecuta código.** Contiene memoria, DLLs, Handles, Seguridad y Threads. Si un proceso **no tiene Threads** entonces está muerto, no ejecuta nada. Por el contrario si **tiene 1 Thread** puede ejecutar código. Por otro lado si tiene muchos más, puede ejecutar N (cantidad de threads) flujos de ejecución (en paralelo o alternados).

##### Task Scheduler y Multicore
- El Task Scheduler de Windows es una herramienta integrada en el OS que permite automatizar la ejecución de programas, scripts o tareas en horarios específicos, despues de intervalos de tiempo o cuando ocurren eventos definidos.
- El Scheduler de Windows realiza esta tarea miles de veces por segundo: 
	- Mira qué **Threads** están listos para ejecutarse, elige **UNO**, lo asigna a un CPU core, carga su contenido (registros, stack, IP/Instruction Pointer), el CPU ejecuta instrucciones de ese Thread, lo pausa (context switch), pasa a otro Thread.
- El Scheduler **NO ELIGE PROCESOS**, elige **THREADS**.
- Ejemplo: Un CPU con **4 Cores** tendra un proceso con **4 Threads**. Resultado: Cada Thread puede ejecutarse **realmente en paralelo** y por lo tanto, **4 IP/Intruction Pointer** ejecutandose al mismo tiempo. 
- Si hay **8 Threads**, 4 se ejecutan, 4 esperan, el scheduler alterna.

- Esto es crítico en cuanto a seguridad debido a que el código malicioso se suele ejecutar como **Thread** y/o se inyecta como **Thread**. Técnicas Reales: `CreateRemoteThread`, `QueueUserAPC`, `Thread Hijacking`. Por lo tanto, no se inyectaria "un proceso", se inyecta un thread dentro de un proceso.

	**"El Scheduler planifica Threads; El CPU ejecuta Threads; El proceso solo los contiene"**.

##### Windows Services
- Un proceso (o parte de uno) diseñado para ejecutarse en segundo plano, sin interacción directa con el usuario, controlado por el **Service Control Manager (SCM)**
![[Pasted image 20260122173753.jpg]]

- El proceso responsable de **SCM** es `services.exe`, es una base de datos de servicios que se encarga de iniciar servicios, detener servicios, monitorear estado, aplicar dependencias, gestionar cuentas.  
- El SCM se comunica con los servicios mediante una API específica. No cualquier `.exe` puede ser un servicio; debe estar programado para responder a los comandos del **SCM (Start, Stop, Pause)**. 
- Cada servicio tiene una subclave con: 
	- ImagePath, StartType, ServiceType, Dependencias, Cuenta de ejecución.

- Estructura de un servicio: 
	- **Service Executable:** El archivo binario (`.exe`) que contiene el código.
	- **Service Program:** El código interno que incluye una función especial llamada `ServiceMain`.
	- **Service Configuration:** Información guardada en el Registro de Windows (`HKLM\SYSTEM\CurrentControlSet\Services`) que le dice al **SCM** cómo debe ejecutarse ese servicio.

- Tipos de Cuentas: 
	- **LocalSystem**: La cuenta con mas poder. Tiene acceso total al sistema local, pero no a la red (actúa como máquina).
	- **NetworkService**: Tiene privilegios limitados en el equipo local, pero puede autenticarse en la red usando las credenciales del equipo.
	- **LocalService**: La más restringida. No tiene acceso a la red y privilegios minimos locales. Ideal para tareas básicas.
- En cuanto a seguridad se refiere los servicios son el lugar favorito de los atacantes para mantener acceso. Si se logra instalar un servicio malicioso, el código se ejecutará cada vez que la PC se encienda. También pueden ser utilizaados para escalar privilegios, por ejemplo, si un servicio corre como `LocalSystem` pero sus permisos de archivo son débiles, un atacante puede reemplazar el `.exe` del servicio con uno malicioso para ganar control total del sistema **(técnica conocida como Weak Service Permissions)**.
##### svchost.exe (Service Host)
- Muchos servicios no son un `.exe` independiente, sino una **DLL (Direct Link Library)**.
- `svchost.exe` es un proceso "contenedor" que carga estas **DLLs** de servicios. Esto ahorra recursos, en lugar de tener 50 procesos distintos, Windows agrupa servicios similares en un solo proceso llamado `svchost.exe`





