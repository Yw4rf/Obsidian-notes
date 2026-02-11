#### Services.msc
- Los servicios en Windows son procesos que se ejecutan, normalmente sin necesitad de interacción directa con el usuario. Los servicios son controlados por el **Service Control Manager (SCM)**. Más específicamente, los servicios se encuentran definidos en el **registro de Windows** ([[The Windows Registry]]) que apuntan a ejecutables `.exe` o `DLL` ubicados en el sistema de archivos, administrados por `services.exe` y ejecutados normalmente bajo una **cuenta de servicio**.
	- **Ubicación del registro**: `HKLM\SYSTEM\CurrentControlSet\Services\<NombreDelServicio>`
	- Muchos servicios se implementan como **DLL (Dynamic Link Library)** y **son alojados por** `svchost.exe`. Generalmente los servicios se alojan en grupos([[Local Users, Groups and Domains]]) (**-k**) definidos en el registro. E.g: `svchost.exe -k netsvcs`
- `services.msc` es la consola **MMC (Microsoft Management Console)** para administrar servicios de Windows.
- Cada servicio tiene un **modo de arranque** que determina **cuándo se inicia**: 
	- **Automático**: arrancan con Windows de manera automática, se inicia al boot. E.g: `WinDefend`, `EventLog`. 
	- **Automático (inicio retrasado)**: arrancan después del boot, reduce impacto en inicio. E.g: servicios de actualización. 
	- **Manual**: solo se inicia cuando algo lo necesita, no arranca solo. 
	- **Deshabilitado**: no se puede iniciar, generalmente usado para hardening o troubleshooting. 
- **Estados de un servicio**. Un servicio puede estar diferentes estado, entre ellos:  
	- **Running (Ejecución)**, **Stopped (Detenido)**, **Paused (Pausado)** o **Starting / Stopping**. 
- **Dependencias entre servicios**: Muchos servicios dependen de otros para funcionar correctamente. Es posible verlo en la pestaña de "Dependencias" de cada servicio. E.g: el servicio `DHCP Client` depende de `AFD` y `TCP/IP`, si uno no funciona, el otro tampoco.

#### Services Security
- **Cada servicio se ejecuta bajo una cuenta de usuario específica**, que define su contexto de seguridad y permisos. Esta cuenta puede ser una de las siguientes:
	- **LocalSystem**: cuenta con privilegios máximos a nivel local, superiores a los de un Administrator estándar con acceso completo a todos los recursos del equipo local. 
	- **NetworkService**: cuenta con privilegios limitados, que puede acceder a recursos de red utilizando credenciales del equipo. 
	- **LocalService**: cuenta con privilegios aún más reducidos que **NetworkService**, con acceso limitado a recursos locales y red.
	- **Cuenta de usuario o de dominio**: permite asignar permisos específicos y es recomendable para servicios que necesitan acceso a ciertos recursos o para cumplir políticas de seguridad.
- Un **servicio registrado como DLL** cargado fuera de `svchost.exe` es **muy sospechoso**. Al igual, un `svchost.exe` **cargando una DLL rara** es **igual de sospechoso**. 
- Los atacantes pueden crear servicios como persistencia, configurándolos como automáticos y ejecutándose como **LocalSystem**.
- **Eventos** asociados a servicios en **System Event Log**: 
	- `EventID: 7045` → servicio creado.
	- `EventID: 7035` → cambio de estado de servicio.
	- `EventID: 7036` → el servicio cambió efectivamente de estado.
	- `EventID: 7024` → error al iniciar servicio.
- Servicios con **ACLs débiles** (**Access Control Lists**) pueden permitir **escalada de privilegios locales**.

#### Services.msc vs CLI 
- **SC** es una herramienta de línea de comandos en sistemas operativos Windows que permite gestionar servicios del sistema:
~~~CMD
sc query
sc qc [SERVICIO]
sc start [SERVICIO]
sc stop [SERVICIO]
sc query type= service
sc queryex
sc sdshow [SERVICIO]
~~~

- Comandos de **PowerShell**:
~~~PowerShell 
Get-Service
Get-Service | Where-Object {$_.Status -eq "Stopped"}
~~~
