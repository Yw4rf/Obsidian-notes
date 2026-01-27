##### Windows Startup
- Una vez que Windows termina de cargar el **Kernel** y el **HAL** el sistema necesita saber qué programas deben abrirse automaticamente al iniciar el sistema. Para ello, Windows consulta el **Windows Registry**, los dos más importantes que se suelen usar son: 
	- **HKEY_LOCAL_MACHINE (HKLM)** Es la configuración de la **máquina**. Todo lo que esté aquí se inicia **siempre**, sin importar quién inicie sesión. Suele contener drivers, antivirus y servicios del sistema.
	- **HKEY_CURRENT_USER (HKCU)** Es la configuración del **usuario**. Lo que esté aquí solo se inicia cuando se inicia sesión. 
- Dentro de esos registros se encuentran diferentes tipos de entradas las cuales les dicen a Windows con qué frecuencia ejecutar algo: 
	- **Run**: Se ejecuta siempre quie el usuario (o el sistema) inicia.
	- **RunOnce**: Se ejecuta una sola vez y luego Windows borra la entrada. Es tipico despues de instalar un programa que requiere un reinicio para terminar.
	- **Userinit**: Es una entrada crítica. Lanza el proceso `explorer.exe` (desktop, folders y taskbar). Si esto falla, luego de iniciar sesión la pantalla se ve negra.
- Es posible modificar estas entradas o registros a mano aunque no se recomienda debido a que cualquier error puede llevar a que Windows se corrompa. Para ello, existe `msconfig.exe` **(Configuración del Sistema)** la cual es una herramienta que permite ser usada para ver y cambiar el arranque de aplicaciones al iniciar el sistema.
1. **General:**
    - Normal:_ Carga todo (ideal).
    - Diagnostic: Solo lo mínimo (para cuando algo falla).
    - Selective: Tú eliges qué sí y qué no (para pruebas).
2. **Boot (Arranque):** Aquí configuras el **Safe Boot (Modo Seguro)**. Si Windows no arranca por un driver malo, marcas esta opción para que inicie sin drivers pesados.
3. **Services (Servicios):** Lista de programas que corren de fondo sin ventana. **Tip técnico:** Siempre marca "Ocultar todos los servicios de Microsoft" para ver solo los que instalaron terceros (como Google Update o Adobe).
4. **Startup (Inicio):** En versiones modernas de Windows, esta pestaña te redirige al **Administrador de Tareas**. Aquí es donde ves el "Impacto de inicio" (si un programa hace que tu PC tarde más en prender).
5. **Tools (Herramientas):** Un acceso rápido a otras utilidades técnicas (Monitor de rendimiento, Información del sistema, etc.).

##### Shutdown
- **shutdown** es un comando de línea de comandos en Windows que permite apagar, reiniciar, cerrar sesión o hibernar el equipo local o remoto.  Es una herramienta potente para automatizar tareas de gestión del sistema, especialmente útil cuando se necesita programar un apagado o reinicio sin intervención manual. 

Para usar el comando, abre el **Símbolo del sistema (CMD)** como administrador y ejecuta una de las siguientes sintaxis
- **Apagar el equipo en 10 minutos**:  
    `shutdown /s /t 600`  
    → `/s` indica apagado, `/t 600` establece un retraso de 600 segundos (10 minutos). 
- **Reiniciar el equipo después de apagar**:  
    `shutdown /r /t 300`  
    → `/r` reinicia tras el apagado, `/t 300` es un retraso de 5 minutos. 
- **Apagar inmediatamente y forzar cierre de aplicaciones**:  
    `shutdown /s /f /t 0`  
    → `/f` fuerza el cierre de todas las aplicaciones sin advertencias. 
- **Cancelar un apagado programado**:  
    `shutdown /a`  
    → Solo funciona si hay un apagado pendiente y se ejecuta durante el tiempo de espera. 

- **`/s`**: Apaga el equipo. 
- **`/r`**: Apaga y reinicia.
- **`/g`**: Apaga, reinicia y restaura aplicaciones registradas. 
- **`/t xx`**: Tiempo de espera en segundos (0 para inmediato). 
- **`/f`**: Fuerza el cierre de aplicaciones. 
- **`/c "comentario"`**: Añade un mensaje visible durante el apagado. 
- **`/d p:xx:yy`**: Registra el motivo del apagado (planeado, usuario, etc.).