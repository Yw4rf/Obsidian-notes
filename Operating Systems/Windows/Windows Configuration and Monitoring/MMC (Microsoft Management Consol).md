### MMC
- **Microsoft Management Console (MMC)** es una herramienta integrada en Windows que proporciona una interfaz gráfica unificada para administrar componentes del sistema operativo.
- El archivo ejecutable principal es **`mmc.exe`**, ubicado normalmente en `C:\Windows\System32\mmc.exe`
- Se puede iniciar buscando `mmc` en el menú, ejecutando `(Win + R)` o desde la línea el **CLI (Command Line Interface)**. 
- Aunque es seguro, algunos virus pueden usar el nombre `mmc.exe` para ocultarse; por ello, es posible verificar su ubicación y hash si se sospecha de actividad maliciosa. 
- MMC permite acceder a herramientas como el **Administrador de dispositivos**, **Visor de eventos**, **Gestión de discos**, **Servicios**, **Políticas de grupo** y más, todo desde una interfaz común.

#### Tools 
- Es posible acceder a esta lista de herramientas esenciales para la administración, monitoreo y resolución de incidentes desde **MMC**:
	- **`eventvwr.msc`**: **Visor de Eventos** – Fundamental para auditoría y análisis de eventos del sistema, aplicaciones y seguridad. ([[Windows Event Viewer]])
	- **`secpol.msc`**: **Directiva de Seguridad Local** – Configuración de políticas de contraseñas, auditoría y derechos de usuario. ([[Local Security Policy]])
	- **`services.msc`**: **Servicios** – Gestión de servicios del sistema, clave para diagnóstico y control de procesos. [[Services.msc]]
	- **`compmgmt.msc`**: **Administración de Equipos** – Incluye herramientas integradas como Administrador de dispositivos, servicios, discos y usuarios. 
	- **`devmgmt.msc`**: **Administrador de Dispositivos** – Diagnóstico y gestión de hardware. 
	- **`diskmgmt.msc`**: **Administración de Discos** – Manejo de particiones, volúmenes y almacenamiento. 
	- **`gpedit.msc`**: **Editor de Directivas de Grupo Local** – Configuración avanzada de políticas del sistema (versiones Pro/Enterprise). [[Local Security Policy]] 
	- **`lusrmgr.msc`**: **Usuarios y Grupos Locales** – Gestión de cuentas locales y permisos.  [[Local Users, Groups and Domains]]
	- **`perfmon.msc`**: **Monitor de Rendimiento** – Supervisión del rendimiento del sistema. 
	- **`taskschd.msc`**: **Programador de Tareas** – Automatización de tareas administrativas. 
	- **`wf.msc`**: **Firewall con Seguridad Avanzada** – Configuración de reglas de entrada/salida y perfiles de red. 
	- **`certlm.msc`**: **Certificados del Equipo Local** – Gestión de certificados para autenticación y cifrado. 
	- **`fsmgmt.msc`**: **Carpetas Compartidas** – Supervisión de recursos compartidos, sesiones y archivos abiertos. 
	- **`rsop.msc`**: **Conjunto Resultante de Directivas** – Verificación de políticas aplicadas a nivel local. [[Local Security Policy]]
	- **`tpm.msc`**: **Administración del TPM** – Gestión del módulo de plataforma segura (clave en seguridad física). 
	- **`wmimgmt.msc`**: **Control WMI** – Administración de la instrumentación del sistema. [[WMI (Windows Management Instrumentation)]]