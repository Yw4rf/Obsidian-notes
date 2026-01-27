![boot-process](boot-process.png)
##### Boot Process
- Bootear es el proceso de iniciar un OS en una computadora, muchas cosas ocurren de fondo al presionar el boton de encendido de la misma y antes de que Windows este totalmente cargado y listo para usarse. 
##### Firmware
- Firmware es un tipo de software de bajo nivel que se integra directamente en el hardware de un dispositivo electrónico, actuando como puente entre el hardware y el software.
- En las computadoras principalmente existen dos tipos de firmware: **BIOS** y **UEFI**
##### BIOS (Basic Input-Output System) 
- El firmware BIOS fue creado en los 80s y funciona de la misma manera desde que fue creado. A medida de que las computadoras fueron evolucionando, se volvio dificil para BIOS soportar las nuevas caracteristicas requeridas por los usuarios.
- En el firmware BIOS el proceso comienza con la fase de inicialización del mismo, esto es cuando los dispositivos del hardware comienzan a operar y se realiza el proceso **POST (Power-on self-test)**.
- POST se realiza para asegurarse de que todos los dispositivos se estan comunicando correctamente. Cuando el disco del sistema es descubierto, POST acaba. La ultima instrucción en POST es mirar el **MBR (Master Boot Record)**. En palabras simples, POST es el auto-diagnostico al encender.
- BIOS utiliza **MBR (Master Boot Record)**, siendo este el primer sector del disco duro el cual contiene un pequeño programa que es responsable de localizar y cargar el OS de Windows.
##### UEFI (Unified Extensible Firmware Interface) 
- UEFI fue designado para reemplazar BIOS y soporta nuevas caracteristicas que este ultimo no. 
- El firmware UEFI usa `.efi` files en una partición especial del disco llamada **ESP (EFI System Partition)**. Más organizado y dificil de corromper que MBR. 
- Una computadora con UEFI almacena el código de booteo en el firmware. Esto ayuda a incrementar la seguridad de la computadora al bootear debido a que la computadora pasa directamente a `bootmgr.exe` directamente al **protected mode**.

##### Bootmgr.exe y BCD
- El gestor de arranque `bootmgr.exe` **(Windows Boot Manager)** es el directorio de orquesta. Realiza el proceso de pasar del **real mode** (donde la pc es muy limitada) al **protected mode** (donde es posible usar toda la RAM disponible)
    - En el **Real Mode** la CPU actúa como si fuera un procesador antiguo (8086), limitado a 1 MB de RAM.
    - En el **Protected Mode**. `Bootmgr.exe` "desbloquea" el procesador para que Windows pueda ver y proteger toda la memoria RAM, evitando que un programa sobrescriba el espacio de otro.
- **BCD (Boot Configuration Database)** es la base de datos de configuración. Contiene cualquier codigo necesario para iniciar la computadora junto con cualquier indicación acerca de si la computadora viene de una hibernacion o si es un inicio limpio. 
- En caso de ser una hibernación el proceso de booteo continua con ``Winresume.exe``. Este ultimo permite a la computadora leer el archivo ``Hiberfil.sys`` el cual contiene el estado de la computadora cuando fue puesto en hibernación. 
- Si la computadora tiene un inicio limpio entonces ``Winload.exe`` es ejecutado. Este archivo contiene una grabación de la configuración del hardware en el registro. 
- ``Winload.exe`` usa **Kernel Mode Code Signing (KMCS)** para asegurarse de que todos los drivers esten digitalmente firmados. Esto asegura que todos los drivers sean seguros para cargar cuando la computadora inicia. 
- Luego de que los drivers son examinados, `Winload.exe` ejecuta `Ntoskrnl.exe` el cual inicia el **Windows Kernel** y configura el **HAL (Hardware Abstraction Layer)**.
- Finalmente, el **Session Manager Subsystem (SMSS)** lee el registro para crear el entorno del usuario, inicia el **Winlogon Service** y prepara cada escritorio de usuario/s a iniciar.
- El **SMSS.exe** es técnicamente el primer proceso de **User Mode** que se crea. Es el responsable de lanzar:
	- **Winlogon.exe:** El proceso que maneja el inicio de sesión.
	- **LSASS.exe:** El servidor de autoridad de seguridad local (el que verifica si tu contraseña es correcta).

