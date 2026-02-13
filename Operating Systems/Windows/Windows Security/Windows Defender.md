#### Windows Defender
- Es el **Antivirus/Antimalware integrado** en Windows. Su función principal es detectar y eliminar software malicioso. No protege la red, protege el **endpoint**. 
- Tiene tres funciones principales: 
		1.**Protección en tiempo real**: cuando se descarga un archivo, cuando se copia algo desde un USB, cuando se ejecuta un `.exe` o cuando se crea un proceso nuevo Windows Defender lo inspecciona automáticamente.
		2.**Detección de malware**: detecta amenazas usando firmas conocidas (virus ya catalogados), heurística (cosas "raras" en el comportamiento), análisis en la nube (consulta contra la base de datos de Microsoft en la nube, Block at First Sight). E.g: si un programa intenta modificar claves de inicio automático, inyectarse en otro proceso o desactivar el antivirus, esto levanta alerta. 
		3.**Protección contra scripts**: protege contra PowerShell malicioso, macros de Office y scripts descargados.  
- Windows Defender trabaja sobre archivos, procesos, memoria y scripts. No analiza paquetes de red.
- Componentes principales: 
	- **Protección contra Malware**: utiliza firmas (definiciones de virus conocidos) y análisis de comportamiento (detecta acciones sospechosas aunque el virus sea nuevo). 
	- **Protección contra Ransomware**: incluye "Acceso controlado a carpetas". Impide programas no autorizados a que modifiquen carpetas sensibles como Documents, Images, etc. 
	- **Protección basada en Reputación (SmartScreen)**:evalúa apps y páginas web descargadas. Si un archivo tiene mala reputación o es desconocido, te avisa antes de ejecutarlo. 
	- **Aislamiento de núcleo (Core Isolation)**: usa virtualización del hardware para aislar procesos críticos del sistema. La función más importante es Memory Integrity que protege el kernel contra inyecciones de código malicioso.
	- **Exploit Protection**: protege contra técnicas de explotación de vulnerabilidades (buffer overflow, heap spray, etc).
- Cuando detecta algo puede bloquearlo automáticamente, ponerlo en cuarentena (un área cifrada y aislada donde el archivo no puede ejecutarse), eliminarlo o notificar en el centro de seguridad.