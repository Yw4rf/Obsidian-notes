#### Network Resources
- El acceso a los recursos de la red es un componente central del sistema operativo. Muchos programas dependen de la red: web, correos, impresiones, y en especial, **compartición de archivos**. Para esto ultimo, Windows utiliza principalmente **SMB (Server Message Block)**. 

#### SMB (Server Message Block)
- **SMB** es un protocolo de nivel de aplicación originalmente desarrollado por IBM y luego ampliado por Microsoft. Su función principal es permitir:
	- **Compartición de archivos**
	- **Compartición de impresoras**
	- **Acceso remoto a recursos del sistema**
	- **Comunicación cliente-servidor dentro de redes Windows**
- Hoy en dia se utilizan versiones modernas como **SMBv2**, **SMBv3**, ya que **SMBv1** es inseguro (E.g: vulnerabilidades como **Eternal Blue**).
- **SMB** es de los protocolos más atacados en redes corporativas.
- Windows accede a recursos **SMB** utilizando el formato **UNC (Universal Naming Convention)**, permite identificar de manera única un recurso de red. Formato:  `\\servername\sharename\file`
	- **servername**: puede ser un nombre **DNS** (`fileserver.empresa.local`), nombre de **NetBIOS** (`FILESERVER`) o una **IP Address** (`192.168.1.10`)
	- **sharename**: es el punto **raíz compartido** en el sistema de archivos remoto. 
	- **file**: es el archivo o subdirectorio dentro del recurso compartido.  (E.g: `\\192.168.1.10\Documents\reports\10-02-25.pdf`)
- Cuando se comparte una carpeta en Windows se define qué parte del **file system** será accesible. Se aplican permisos a nivel: **Share permissions**, **NTFS permissions**. Los permisos pueden permitir o denegar: Lectura (Read), Escritura (Write), Modificación y Control total.
- Windows crea automáticamente **shares administrativos**, identificados por `$`. Estos no aparecen al enumerar **shares** comunes, son únicamente **accesibles por usuarios administradores**. Muy utilizados por administradores de sistemas, herramientas de gestión remota, atacantes post-explotación. E.g:
	- `C$, D$, E$`: raíz de cada volumen.
	- `ADMIN$`: carpeta de instalación de Windows (`C:\Windows`)
	- `PRINT$`: recursos de impresión
- El acceso a **shares** desde Windows más sencillo es conectarse desde **File Explorer**, ingresando la ruta **UNC (Universal Naming Convention)** en la barra superior. E.g: `\\fileserver\C$` 
	- Cuando el acceso al recurso es de manera remota Windows solicita **credenciales del equipo remoto**. No sirven las credenciales locales si no existe en el host destino. En dominio se usan credenciales **Active Directory**
- **SMB (Server Message Block)** se ejecuta comúnmente en el puerto **TCP/445** que permite la comunicación directa sobre **TCP/IP** **sin necesidad de NetBIOS**. También puede usar el puerto **TCP/139** en versiones antiguas que dependen de **NetBIOS**

#### RDP (Remote Desktop Protocol)
- Windows permite controlar un sistema remoto usando **RDP (Remote Desktop Protocol)**. Permite usar el escritorio remoto como si fuera local, configurar el sistema, instalar software, realizar tareas de troubleshooting. 
- **RDP** es un objetivo natural para atacantes debido a que da control interactivo total, suele estar mal protegido, muchas veces está expuesto a Internet. 
- **RDP** generalmente suele ejecutarse en el puerto **TCP/3389**, es el puerto estándar para conexiones de escritorio remoto en sistemas Windows.