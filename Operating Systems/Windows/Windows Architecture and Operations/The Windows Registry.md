##### The Registry
- Windows almacena toda la información del hardware, aplicaciones, usuarios y configuraciones en una gran base de datos conocida como **Registry**. 
- Antes de que existiera el registro los programas dependian de archivos `.ini` para guardar su información, pero eran dificil administrarlos. El registro centralizó eso.
- Al iniciar, el **Kernel** de Windows lee el Registro para saber qué controladores cargar y cómo configurar el entorno.
##### The Registry Structure
- El registro se organiza de forma similar a un explorador de archivos, con "carpetas" llamadas **Keys** y "archivos" llamados **Values**. 
- Existen 5 divisiones principales llamadas **Hives** (Colmenas), cada una con un proposito específico: 
	- `HKEY_CLASSES_ROOT` **(HKCR)**: Gestiona las asociaciones de archivos (por ejemplo, qué programa abre un `.pdf`) y datos de objetos **COM (Component Object Model)**.
	- `HKEY_CURRENT_USER` **(HKCU)**: Contiene la configuración específica del usuario que tiene la sesión iniciada **(fondos de pantalla, preferencias del mouse, etc).**
	- `HKEY_LOCAL_MACHINE` **(HKLM)**: Almacena los ajustes que afectan a todo el equipo, independientemente de quien inicie sesión **(drivers, configuraciones de red, etc.)**
	- `HKEY_USERS` **(HKU)**: Contiene los perfiles de todos los usuarios cargados en el sistema operativo.
	- `HKEY_CURRENT_CONFIG` **(HKCC)**: Guarda información sobre el perfil de hardware que se utiliza en el arranque. 
- Las claves del registro pueden contener subclaves o valores. Diferentes valores como los siguientes: 
	- **REG_BINARY -** Números o valores booleanos.
	- **REG_DWORD -** Números mayores a 32bit.
	- **REG_SZ -** Valores cadena.
##### Security and Permissions
- Como el registro contiene configuraciones críticas para el arranque y la estabilidad, Microsoft implementó un sistema de permisos basado en **ACLs (Access Control Lists)** muy similar al que se usa en el **File System NTFS (New Technology File System)**.
- No todos los procesos ni todos los usuarios pueden tocar cualquier parte del registro. Esto evita que un usuario estándar o un malware borre alguna o crítico.
- El sistema de permisos: 
	- **Owner (Propietario )**: Las claves críticas pertenecen al sistema `SYSTEM` o `TrustedInstaller`. Incluso un Administrador a veces debe "tomar posesión" de una clave antes de poder modificarla.
	- **Inheritance** (Herencia): Al igual que las carpetas, las subclaves suelen heredar los permisos de su "padre".
	- **Hives y su ubicación**: El registro no es solo un archivo. Se guarda en archivos llamados "**Hives**" en `%SystemRoot%\System32\config\`. Por ejemplo, el archivo `SYSTEM` o `SOFTWARE`.

##### Practical usage and warnings
- La herramienta principal de los registros es el **Editor del Registro** (`regedit.exe`). Es potente pero peligrosa, no tiene botón de deshacer. Si se borra una clave vital, el sistema podría no volver arrancar. 
- Debido a que el registro contiene casi toda la información del sistema operativo y del usuario, es fundamental asegurarse de que no se vea comprometido. Las aplicaciones potencialmente maliciosas pueden agregar claves de registro para que se inicien cuando se inicia la computadora. 
	- El registro también contiene la actividad que realiza un usuario durante el uso diario normal de la computadora. Esto incluye el historial de los dispositivos de hardware, incluidos todos los dispositivos que se han conectado a la computadora, incluido el nombre, el fabricante y el número de serie. Otra información, como qué documentos han abierto un usuario y un programa, dónde se encuentran y cuándo se accedió a ellos, se almacena en el registro.
- Existen claves llamadas "**Run Keys**" que son los objetivos principales de los atacantes con el fin de lograr persistencia. Cuando Windows inicia sesión, revisa esas **Keys** y ejecuta cualquier comando que encuentre en ellas. Los atacantes solo añaden un nuevo "**Value**" con la ruta de su malware en estas **Keys**. Las más comunes:
	- `HKEY_CURRENT_USER\Software\Microsoft\CurrentVersion\Run`: Ejecuta el programa cada vez que ese usuario específico inicie sesión. 
	- `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run`: Ejecuta el programa en todos los usuarios del sistema.
- Durante un arranque normal, el usuario no verá el inicio del programa porque la entrada está en el registro y la aplicación no muestra ventanas ni indicaciones de inicio cuando se inicia la computadora. 

![[Pasted image 20260124195759.jpg]]


