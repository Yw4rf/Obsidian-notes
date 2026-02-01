#### Local Users
- Cuando se inicia la computadora por primera vez Windows necesita una cuenta para el primer logon interactivo, puede ser: **vinculada a Microsoft**, de **dominio** o **cuenta de usuario (User Account)**. Esta última se le conoce como **Local User** (esto siempre que el usuario no se una a un dominio). Esta cuenta contiene, ajustes de personalización, permisos de acceso, ubicaciones de archivos, y todo lo relacionado a datos del usuario. Ademas de la anterior, existen dos cuentas: **The Guest** y **The Administrator**. 
- Estas cuentas son **built-in accounts (cuentas integradas)** con **SIDs (Security Identifiers)** conocidos: 
	- **Administator**: SID `...-500` 
	- **Guest**: SID `...-501`
- Ambas se encuentran deshabilitadas por defecto. 
#### Groups and SIDs (Security Identifiers)
- Windows implementa un modelo de control de acceso basado en grupos para simplificar la administración de permisos. Mediante esto, se le asigna permisos a los grupos y los usuarios heredan los permisos de los grupos a los que pertenecen. 
- Cada usuario tiene un **SID** único el cual identifica al usuario en el sistema, no el nombre. Cada grupo también tiene un **SID**, un grupo es una colección lógica de **SIDs (Security Identifiers)**. 
- En Windows los permisos **NO** se suelen asignar directamente a un **Local User** en específico, sino a un **SID (Security Identifier)** de grupo o usuario. 
- Cuando un usuario inicia sesión en Windows: 
	1. Windows autentica al usuario.
	2. Crea un **Access Token**. 
	3. Ese token contiene: 
		- **SID** del user
		- **SID** de **todos los grupos** al que pertenece.
		- Privilegios (SeDebugPrivilege, SeShutdownPrivilege, etc).
	 Ese **Access Token** es el que usa Windows para **TODAS las decisiones de acceso**.
- Un usuario puede pertenecer a múltiples grupos: 
	- Grupos locales.
	- Grupos integrados (built-in). 
	- (En dominio) grupos globales/universales.
- Por ende, el **Access Token** del usuario contiene todos esos **SIDs**. A su vez, el usuario obtiene la unión de permisos, excepto donde haya Deny (Windows Permissions). La seguridad de Windows sigue una jerarquía. Si el Grupo A permite leer un archivo, pero el Grupo B tiene un "Deny" (Denegar) explícito, el **Deny siempre gana**. El sistema busca primero cualquier restricción antes de conceder el acceso.

#### Built-in Groups (Grupos Integrados)
- Windows trae grupos predefinidos, con permisos específicos ya asignados en el sistema, algunos ejemplos: 
	- `Administrators`: **control total del sistema**
	- `Users`: **permisos básicos**
	- `Guests`: **acceso extremadamente limitado**
	- `Remote Desktop Users`: **login por RDP**
	- `Performance Log Users`: **recolección de contadores de rendimiento**
	- `Backup Operators`: **backup sin ser admin**

#### Local Users and Groups (lusrmgr.msc)
- `lusrmgr.msc` es un **MMC (Microsoft Management Console) snap-in** que permite administrar: 
	- **Local Users**, **Local Groups**, **Memberships**
- Aunque solo existe en Windows Pro, Education y Enterprise, NO en Home.
- `lusrmgr.msc` modifica la **SAM local (Security Account Manager)**, ubicada internamente en el registro `HKLM\SAM` (protegida por Kernel). 
- **Security Account Manager (SAM)** es una base de datos fundamental que almacena información de cuentas de usuario locales, incluidos nombres de usuario y contraseñas en hash.  Es responsable de almacenar la información de cuentas locales durante los intentos de inicio de sesión en computadoras independientes o entornos de grupos de trabajo que no forman parte de un dominio. 
- Se encuentra en `%SystemRoot%\System32\config\SAM`. La misma interactua con **LSASS (Local Security Authority Subsystem Service)** el cual es un proceso que gestiona la autenticación, interactuando con la **SAM** para validar credenciales durante el inicio de sesión local. Cuando un usuario se autentica, **LSASS** consulta la base de datos **SAM** para verificar el hash de la contraseña ingresada contra el almacenado, permitiendo o denegando el acceso. Además, **LSASS** también gestiona credenciales en caché, secretos LSA y tokens de acceso, protegiendo estos datos en memoria durante la sesión

#### Domains 
- Un **Dominio en Windows** es una **colección lógica de objetos** (como usuarios, grupos, equipos, impresoras) que se administran de forma centralizada dentro de una red. 
- Esto se realiza mediante **Windows Active Directory (AD)**. Ya no se depende de una base local (**SAM o Security Accounts Manager**), sino de una base de datos replicada entre **Domain Controllers**.
- **Active Directory (AD)** es un servicio de directorio que actúa como una base de datos centralizada para gestionar usuarios, equipos, grupos y otros recursos en una red de dominio Windows.
- Los **Domain Controllers (DC)** son servidores que ejecutan el rol de **Active Directory**, administran la autenticación, autorización y políticas de seguridad de los usuarios dentro de un dominio de red, verifican las credenciales de los usuarios y controlan el acceso a recursos de red como archivos, aplicaciones e impresoras. Utilizan protocolos como **Kerberos** para la autenticación y **LDAP** para consultar a la base de datos de objetos.
- Al estar en el dominio el usuario se autentica una vez ante el **DC** y este le otorga un **"ticket"** para acceder a impresoras, archivos o programas en toda la red sin pedir la contraseña nuevamente, a esto se le conoce como **Single Sign-On (SSO)**. 
- Las configuraciones enviadas por el **DC** se conocen como **GPO (Group Policy Objects)**. Estas políticas pueden definir desde el fondo de pantalla hasta restricciones críticas de seguridad en miles de computadoras a la vez.
- Cuando un usuario en el **Domain** inicia sesión:
	1. Se autentica contra el **DC**.
	2. El **DC** valida la identidad y determina las membresías de dominio; el sistema local construye el **Access Token** combinando **SIDs** de dominio y locales. 
	3. El **Access Token** incluye: 
		- User **SID**. 
		- Domain Groups **SIDs**
		- Local Groups **SIDs** (si es que hay)
	4. El **Access Token** se utiliza en la sesión local. 
- Si el **DC** define una configuración, **esa configuración se aplica aunque exista una local distinta**. A su vez, si el **DC** no define una configuración en específico, Windows toma la del usuario local. 
- `NTDS.dit` es la base de datos central donde reside toda la información del dominio. Físicamente suele encontrarse en `%SystemRoot%\NTDS\Ntds.dit` en los **DC**.   
#### Local Users and Groups vs Domains

| **Característica**      | **Local (SAM-based)**                                                                                                      | **Domain (AD-based)**                                                                                       |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Arquitectura**        | Descentralizada (Workgroup). Cada máquina es una isla de seguridad.                                                        | Centralizada (Cliente-Servidor). Estructura jerárquica de confianza.                                        |
| **Base de Datos**       | `%SystemRoot%\System32\config\SAM` (Registro HKLM).                                                                        | `%SystemRoot%\NTDS\ntds.dit` (Motor ESE/Jet Blue).                                                          |
| **Identidad**           | El usuario `Admin` en PC1 es **distinto** al usuario `Admin` en PC2, aunque tengan la misma clave. Tienen SIDs diferentes. | El usuario `jdoe@empresa.com` es el mismo objeto con el mismo SID en cualquier equipo del dominio.          |
| **Límite de Confianza** | El núcleo del SO local. No hay confianza inherente entre máquinas.                                                         | El **Forest (Bosque)**. Se pueden establecer relaciones de confianza entre diferentes dominios.             |
| **Autenticación**       | **Challenge-Response (NTLM)**: La PC comprueba el hash contra su propia SAM.                                               | **Tickets (Kerberos)**: El DC emite un TGT (Ticket Granting Ticket) que el usuario presenta a los recursos. |
| **Escalabilidad**       | Muy baja. Cambiar una política en 50 PCs requiere entrar a las 50 (o usar herramientas de terceros).                       | Alta. Un cambio en una GPO en el DC se replica a miles de objetos mediante el servicio **DFSR**.            |
