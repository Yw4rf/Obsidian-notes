#### CMD
- La interfaz de linea de comandos de Windows conocida como **CMD** puede ser utilizada para ejecutar programas, navegar en el sistema y gestionar archivos y carpetas. A su vez, es posible crear archivos conocidos como archivos **batch** con el fin de automatizar tareas repetitivas ejecutando secuencias de comandos almacenados en un archivo de texto `.bat`  Se utilizan comúnmente para agilizar operaciones como copiar, cambiar el nombre o eliminar archivos, crear directorios, iniciar aplicaciones o realizar mantenimiento del sistema.
- Incluso el **CMD** de Windows con todas las características y comandos que tiene no ofrece mecanismos nativos para interactuar directamente con estructuras internas del sistema (objetos del kernel, memoria, hilos), y su modelo se basa casi exclusivamente en texto y ejecución de procesos externos.

#### PowerShell
- **PowerShell** es una solución de automatización de tareas de Microsoft que combina una **shell** de linea de comandos moderna, un **lenguaje de scripting** orientado a objetos y un marco de gestión de configuración.
- A diferencia del **CMD** tradicional (que solo procesa texto), **PowerShell** trabaja con **objetos**. Osea, cuando se pide información sobre un archivo, no solo se obtiene el nombre como una cadena de texto,, sino como un objeto completo con propiedades: tamaño, fecha de creación, permisos, etc. Estos pueden ser fácilmente manipulados.
- Se utiliza principalmente para administración de sistemas, nube, automatización, gestionar configuraciones, entre otras cosas.
- Es multiplataforma, aunque nació para Windows, existe **PowerShell Core** el cual funciona en Linux y MacOS. 
- **PowerShell** utiliza los archivos `.ps1` para ejecutar tareas automáticas, son archivos de texto que contienen **scripts** (secuencias de comandos).
- A diferencia de los archivos `.bat` que solo mueve carpetas o renombra archivos, los `.ps1` permiten interactuar con componentes del sistema a través de APIs de alto nivel, WMI/CIM y .NET, lo que habilita una administración mucho más profunda que CMD, aunque siempre desde espacio de usuario.
- Por seguridad, Windows bloquea la ejecución de scripts por defecto, por ello el comando: `Set-ExecutionPolicy RemoteSigned` permite ejecutar scripts locales.

#### Cmdlets and Pipelines 
- Para entender **PowerShell** es fundamental aprender conceptos claves como: **Cmdlets (command-lets)** y **The Pipeline (|)**
- **Cmdlets (Command-lets)**: Son los comandos integrados de **PowerShell**. Tienen una estructura muy intuitiva, como `Get-Service`,  `Stop-Process` o `New-Item`, etc.
- **The Pipeline (|)**: Permite pasar el objeto resultante de un comando directamente al siguiente para filtrarlo o transformarlo. El pipeline permite encadenar cmdlets sin perder estructura, ya que se transmiten objetos tipados y no strings.

~~~PowerShell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
Try the new cross-platform PowerShell https://aka.ms/pscore6
PS C:∖WINDOWS∖system32> help
TOPIC
   Windows PowerShell Help System
SHORT DESCRIPTION
   Displays help about Windows PowerShell cmdlets and concepts.
LONG DESCRIPTION
   Windows PowerShell Help describes Windows PowerShell cmdlets,
   functions, scripts, and modules, and explains concepts, including
   the elements of the Windows PowerShell language.
   Windows PowerShell does not include help files, but you can read the
   help topics online, or use the Update-Help cmdlet to download help files
   to your computer and then use the Get-Help cmdlet to display the help
   topics at the command line.
   You can also use the Update-Help cmdlet to download updated help files
   as they are released so that your local help content is never obsolete.
   Without help files, Get-Help displays auto-generated help for cmdlets,
   functions, and scripts.
ONLINE HELP
   You can find help for Windows PowerShell online in the TechNet Library
   beginning at http://go.microsoft.com/fwlink/?LinkID=108518.
   To open online help for any cmdlet or function, type:
   Get-Help -Online
UPDATE-HELP
   To download and install help files on your computer:
      1. Start Windows PowerShell with the "Run as administrator" option.
      2. Type:
         Update-Help
   After the help files are installed, you can use the Get-Help cmdlet to
   display the help topics. You can also use the Update-Help cmdlet to
   download updated help files so that your local help files are always
   up-to-date.
   For more information about the Update-Help cmdlet, type:
      Get-Help Update-Help -Online
-- More --
~~~

- Hay 4 niveles de ayuda en Windows **PowerShell**
	- **get-help** _PS command_ - Muestra ayuda básica del comando
	- **get-help** _PS command [-examples]_ - Muestra ayuda básica del comando con ejemplos
	- **get-help** _PS command [-detailed]_ - Muestra ayuda detallada para el comando con ejemplos.
	- **get-help** _PS command [-full]_ - Muestra toda la información acerca del comando con ejemplos detallados en gran profundidad. 