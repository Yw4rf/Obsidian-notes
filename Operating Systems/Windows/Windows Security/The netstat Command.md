#### Netstat Command
- La herramienta **netstat (network statistics)** es nativa del **CLI** en Windows, permite **inspeccionar el estado de las conexiones de red del sistema**. 
	- Permite inspeccionar: puertos abiertos, conexiones entrantes y salientes, servicios/procesos asociados, estado de las conexiones TCP, etc.
- Desde el punto de vista de **detección de malware**, es muy útil porque **cualquier comunicación de red deja rastro a nivel de sockets**.  
- Ejecutar el comando `netstat` (sin parametros) muestra: conexiones TCP activas, Dirección Local (IP:puerto), Dirección remota, Estado de la conexión. E.g de lo último: 
	- `LISTENING`: el sistema está esperando **conexiones inbound (entrantes)**
	- `ESTABLISHED`: conexión activa, **conexión entrante (inbound ) y saliente (outbound)**
	- `TIME_WAIT`, `CLOSE_WAIT`: estados normales del ciclo TCP
- La limitación de **netstat** no específica qué proceso abrió esa conexión. En sistemas Windows modernos el parámetro `-b` permite mostrar el nombre del binario/programa que creó la conexión, pero requiere privilegios de administrador para su ejecución.
- Si se muestra el mensaje **"Can not obtain ownsership information"**, el proceso corre en **kernel mode**, es un proceso protegido del sistema, no seria automaticamente malicioso, suele indicar componentes del sistema operativo.
- Comando para analisis: `netstat -abno` 
	- `-a`: muestra **todas** las conexiones y puertos en escucha (all)
	- `-b`: muestra el **binario/proceso** que creó la conexión (binary)
	- `-n`: muestra las IPs y puertos en formato numérico (no DNS)
	- `-o`: muestra el **PID** del proceso (process)
- Netstat indica: **Proto** (TCP/UDP), **Local Address** (IP:Puerto local), **Foreign Address** (IP:Puerto remoto), **State** (ESTABLISHED, TIME_WAIT, LISTENING, TIME_CLOSE)
~~~CMD
Proto  Local Address     Foreign Address   State      PID
TCP    0.0.0.0:3389      0.0.0.0:0         LISTENING  1396
  TermService
 [svchost.exe]
~~~

#### Security Importance
- El comando **netstat** permite responder preguntas como: 
	- ¿Hay puertos en LISTENING (escuchando) que no deberian? E.g sospechosos: 
		- Puertos altos (>1024) sin justificación. Servicios LISTENING en `0.0.0.0` sin necesidad. Puertos típicos de backdoors (444,1337, 6666, etc)
	 - ¿Qué proceso abrió ese puerto? 
		 - Binarios con nombres raros. Ejecutables fuera de rutas esperadas (E.g: `C:\Users\...\temp\svchost.exe`, `C:\ProgramData\random.exe`). Procesos que **no deberian usar red**. 
	- ¿Hay conexiones salientes (outbound) sospechosas?
		- Conexiones `ESTABLISHED` hacia: IPs públicas desconocidas, países inusuales, puertos no estandar (E.g: TCP/8088, TCP/9001, TCP/5555)
- Una vez que se conoce el **PID**, el flujo típico es: 
	- 1. Abrir **Task Manager**
	- 2. View --> Select Columns --> Active PID
	- 3. Analizar: 
		- Nombre del proceso, ruta del binario, usuario que lo ejecuta. 
	- Si es malicioso: 
		- Finalizar el proceso, aislar el host, realizar escaneo anti-malware / EDR. 
- Hay que tener en cuenta que **netstat** puede ser evadido por malware avanzado (rootkits, kernel drivers, etc), ademas hoy en dia suele complementarse con: `Get-NetTCPConnection` (**PowerShell**), EDRs, Sysmon, Windows Firewall logs, etc.