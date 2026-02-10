#### NTFS Permissions
- Es el sistema de archivos de Windows, este implementa un sistema de seguridad basado en **Access Control Lists (ACLs)**, este sistema es una lista de entradas de control de acceso **(ACEs)** que define los permisos de acceso a objetos en el sistema de archivos NTFS, como archivos y carpetas. Cada **ACE** específica una identidad (usuario, grupo, o equipo) y los derechos de acceso **allow** y **deny**, como lectua, escritura, ejecución o eliminación. 
- Cada objeto (archivo o carpeta) tiene asociado un **Security Descriptor** que contiene dos tipos principales de **ACLs**: 
	- **DACL (Discretionary Access Control List)**: Es una lista ordenada de **ACEs** que controlan quién puede acceder. 
		- Cada **ACEs** contiene **SID** (usuario/grupo), **tipo de permiso** `allow` o `Deny`, **máscara de acceso** (qué bits/permiso es), **flags de herencia/propagación** (Object/Container, No-propagate, Inherit-only), **si es explicita o heredada**. 
	- **SACL (System Access Control List)**: Controla la **auditoría** ([[Windows Event Viewer#Auditing]])
		- Define que tipo de acceso, si se registra el **éxito, fracaso o ambos**, qué usuario o grupo está siendo auditado. Cuando se produce un acceso que coincide con una entrada en **SACL**, se genera un **evento de auditoría** en el **registro de seguridad** ([[The Windows Registry]]) del **Windows Event Viewer**. 
- **Standar Permissions**: Los seis permisos básicos son: 
	1. **Full Control** (control total del objeto incluyendo cambios de permisos y ownership)
	2. **Modify** (lectura, escritura, ejecución y eliminación) 
	3. **Read & Execute** (lectura y ejecución de archivos) 
	4. **Read** (visualización de contenido y propiedades) 
	5. **Write** (creación de archivos/carpetas y modificación de atributos)
	6. **List Folder Contents** (solo para carpetas, permite ver su contenido) 
- **Especial/Advanced Permissions**: 13-14 permisos granulares que incluyen: 
	- `FILE_READ_DATA` (0x00000001) — leer datos / listar carpeta
	- `FILE_WRITE_DATA` (0x00000002) — escribir datos / crear archivo
	- `FILE_APPEND_DATA` (0x00000004) — append (archivos)
	- `FILE_READ_EA` (0x00000008) — leer atributos extendidos
	- `FILE_WRITE_EA` (0x00000010) — escribir atributos extendidos
	- `FILE_EXECUTE` (0x00000020) — ejecutar archivo / traverse
	- `FILE_DELETE_CHILD` (0x00000040) — borrar hijos (importante)
	- `FILE_READ_ATTRIBUTES` (0x00000080)
	- `FILE_WRITE_ATTRIBUTES` (0x00000100)
	- `DELETE` (0x00010000) — delete principal
	- `READ_CONTROL` (0x00020000) — leer DACL
	- `WRITE_DAC` (0x00040000) — cambiar DACL (Change permissions)
	- `WRITE_OWNER` (0x00080000) — cambiar Owner (Take ownership)
	- `SYNCHRONIZE` (0x00100000)
- Cada uno de esos permisos puede configurarse como `Allow` o `Deny`. **Deny siempre le gana a Allow, sin excepciones**. 
	- Si un usuario tiene "**Deny Read**" por pertenecer a un grupo, pero "**Allow Read**" por pertenecer a otro, el resultado es `Deny`. En conclusión, un **Deny explícito**, corto-circuita la concesión de acceso aunque existan varios Allow.  
- **Especial privileges**: 
	- **SeBackupPrivilege / SeRestorePrivilege**: procesos con estos privilegios (E.g: cuentas de backup) pueden leer/renombrar/restaurar archivos **saltando** las restricciones habituales.
	- **Owner**: el propietario de un objeto puede cambiar permisos (WRITE_OWNER / WRITE_DAC). El propietario puede ser reasignado por quien tenga el privilegio `Take ownership` o siendo admin.

#### NTFS vs Share Permissions
- Cuando se accede a un recurso a través de la red (**SMB** vía **UNC path** E.g: `\server\share`) se enfrentan dos capas de seguridad distintas: **NTFS Permissions** y **Share Permissions**. 
- **Share Permissions**: Son únicamente 3. 
		1. **Full Control**
		2. **Change**
		3. **Read**
- Estos se aplican solo cuando se accede a un recurso de red, si se accede de manera local a un recurso (E.g: `C:\Data`) no se aplican los **Share Permissions**. Están diseñados para filtrar acceso **inbound (entrante) por red**. Son mucho más simples que los de **NTFS** y actúan como primera barrera. 
- Cuando se accede al recurso por red, el sistema evalúa **AMBOS** (**NTFS y Share Permissions**) y aplica el **más restrictivo**. E.g: 
	- Entre **Share Full Control** y **NTFS Read** el acceso más efectivo será **Read**. Por otro lado si se accede de manera local con **NTFS Full Control**, se obtiene **Full Control** debido a que **Share** no se aplica (solo se aplica cuando se accede por red). 
- Generalmente se configura **Share Permissions** en **Full Control** para **Everyone** y se gestiona toda la seguridad real mediante **NTFS Permissions**. Esto simplifica la administración y el troubleshooting porque solo se necesita revisar una capa de permisos para determinar accesos.

#### Inheritance and Propagation
- La herencia es el mecanismo mediante el cual los permisos fluyen desde **objetos padres** (carpetas superiores) hacia **objetos hijos** (subcarpetas y archivos). 
	- Cuando se crea un archivo o carpeta dentro de un contenedor, hereda automáticamente los permisos de su padre. Estos permisos heredades aparecen en gris (dimmed) en la GUI y no se pueden modificar directamente a ese nivel. Los permisos asignados directamente a un objeto se llaman "**explicity assigned**" y aparecen en negro. 
- Es posible bloquear la herencia. En propiedades avanzadas de seguridad se encuentra la opción "**Disable Inheritance**" donde es posible elegir entre:
	- **Convert inherited permissions into explicit permissions**: mantiene los permisos actuales pero ahora como explicitos y editables.
	- **Remove all inherited permissions**: elimina todo lo heredado dejando solo los permisos explícitos si los hay.
- Cuando se asignan permisos es posible controlar su scope de aplicación. Las opciones inlcuyen: 
	- **This folder, subfolders and files**: propagación completa. 
	- **This folder and subfolders**: carpetas pero no archivos.
	- **Subfolders and files**: archivos directos pero no subcarpetas.
	- **Subfolders and files only**: heredan las subcarpetas y archivos pero no el padre.
	- **Subfolders only**: heredan solo las subcarpetas.
	- **Files only**: heredan solo los archivos.

#### Effective Access
- Los **permisos efectivos (effective access)** son el resultado final luego de evaluar todas las fuentes de permisos para un usuario específico. El proceso de evaluación es este: 
	1. **Se recopilan todos los permisos Allow**: Se suman todos los permisos "Allow" de todos los grupos a los que pertenece el usuario, **más** los permisos directos del usuario.
	2. **Se recopilan todos los permisos Deny**: Se identifican todos los "Deny" de todos los grupos **y** del usuario.
	3. **Deny prevalece sobre Allow**: Los permisos "Deny" siempre ganan sobre "Allow" (Deny tiene prioridad absoluta).
	4. **Intersección con Share Permissions** (solo acceso de red): Si el acceso es por red (UNC path), se calcula la intersección entre los permisos NTFS efectivos y los Share Permissions. **El más restrictivo gana**.
- Es el cálculo final que determina si un usuario puede acceder a un recurso o no. Es la respuesta a la pregunta: "¿Qué permisos tiene este usuario para este archivo o carpeta en este momento?".
- Existe una **herramienta** en que incluye Windows en **Security → Advanced → Effective Access tab**. Permite introducir nombre de usuario y el sistema calcula automáticamente qué permisos tendrá ese usuario en ese objeto específico. Tiene como limitación que no considera **Share Permissions**, solo evalúa **NTFS**. 

#### Security and Auditing
- **Object Auditing (SACL)**: controla qué eventos se registran. Se configura en **Security → Advanced → Auditing tab.** Es posible auditar **Success (eventos exitosos)** y/o **Failure (intentos denegados)** de operaciones específicas como **Read**, **Write**, **Delete**, **Change Permissions**, **Take Ownership**. Los eventos se registran en el **Security Event Log con Event IDs específicos**.
- **Ownership and Privileges**: El **owner** de un objeto puede cambiar permisos incluso si no tiene **Change Permissions** en la **ACL** actual. **Take Owner Privilege** debe estar restringido debido a ello. Por defecto, solo **Administrators** pueden tomar ownership de cualquier archivo. 
- **Event IDs críticos para la seguridad**: 
~~~txt
Event ID 4663 (An attempt was made to access an object), 4656 (A handle to an object was requested), 4660 (An object was deleted), 4670 (Permissions on an object were changed), 4664 (An attempt was made to create a hard link), y 5145 (A network share object was checked to see whether client can be granted desired access). También Event ID 4907 (Auditing settings on object were changed) indica que alguien modificó la SACL misma, potencialmente para ocultar actividad.
~~~