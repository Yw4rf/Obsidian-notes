#### Local Security Policy 
- La **Local Security Policy** o **LSP** (`secpol.msc`) es el contenedor de las configuraciones de seguridad aplicables a un equipo local ( E.g: cuentas locales, derechos, opciones de seguridad, auditoria, firewall local, AppLocker, IPsec, etc.). 
- Para administrar políticas locales se usan: `secpol.msc` (**Local Security Policy**) y `gpedit.msc` (**Local Group Policy Editor**), pero en escala empresarial se usan **GPOs (Group Policy Objects)**.
- En entornos como **Active Directory**, las **Account Policies** se definen preferentemente a nivel de dominio y **sobrescriben** la política local para equipos unidos al dominio; Las políticas aplicadas vía **GPO (Group Policy Object)** de dominio (y GPOs vinculadas al OU) tienen precedencia sobre la local.

#### LSDOU (Local / Site / Domain / OU)
- Windows aplica las políticas en el orden **LSDOU**. La Directiva Local es la **base de la pirámide**, pero también la más débil en jerarquía: 
	1. **Local**: Local Policy  `secpol.msc` 
	2. **Site**: sitio de Active Directory `dssite.msc`
	3. **Domain**: dominio `domain.msc`
	4. **OU**: Organizational Unit (de padre a hijo) `gpmc.msc`
 - La **última política aplicada gana**, salvo una que otra excepción. Si una política de **Dominio (Domain)** entra en conflicto con la **Local**, **la de Dominio siempre gana**. 
 - Si por alguna razón un cambio en **Local** no surte efecto, revisar **Resultant Set of Policy** `rsop.msc`
 - La **Local Security Policy** nunca vive aislada, siempre está subordinada al modelo **LSDOU**. 

#### Account Policies
- Controla la seguridad relacionada con las **contraseñas** y el **bloqueo de cuentas**. Estas políticas se dividen en dos categorías principales: 
	- **Password Policy**: Define requisitos como longitud mínima, complejidad, historial de contraseñas y duración máxima. Ayuda a prevenir el uso de contraseñas débiles y reutilizadas. 
	- **Account Lockout Policy**: Establece el número de intentos fallidos de inicio de sesión permitidos antes de bloquear una cuenta. Configura la duración del bloqueo y el tiempo para restablecer el contador de intentos.

	~~~
	-----------PASSWORD POLICY ---------------------------------------------------
	Minimum password length          → Barrera de entrada para brute force
	Maximum password age             → Rotación (compliance)
	Minimum password age             → Anti-bypass de password history
	Password must meet complexity    → Requiere uppercase, lowercase, digit, symbol
	Enforce password history         → Previene reuso (hasta 24 passwords)
	Store passwords using reversible encryption → NUNCA habilitar 
	~~~
	~~~
	-----------ACCOUNT LOCKOUT POLICY POLICY--------------------------------------
	Account lockout threshold         → Después de X intentos fallidos lockout
	Account lockout duration          → Cuánto dura el bloqueo (0 = manual unlock)
	Reset account lockout counter after  → Ventana donde se cuentan los intentos
	~~~~

- Account Policies en **LOCAL** solo aplica a **Local Accounts**. Si la máquina está en dominio, las Account Policies del **DOMAIN** **sobrescriben**.

#### User Rights Assignaments
- Controla qué acciones del sistema que puede realizar cada usuario o grupo. Son **capabilities** del sistema operativo. Quién puede loguear, quién puede ejecutar servicios, quién puede debuggear procesos, etc.
- Lista de los más importantes: 

~~~
Allow log on locally                 → Login físico / RDP
Access this computer from the network → SMB, WinRM, network logon
Deny log on locally                  → Override explícito (gana sobre allow)
Shut down the system                 → Usuarios normales lo tienen por default
Change the system time               → Usuarios NO deberían (afecta Kerberos)

---- MÁS IMPORTANTES PARA SOC (Privilege Escalation)----------------------------
SeDebugPrivilege          (Debug programs)              → Dump LSASS, inyección de procesos
SeBackupPrivilege         (Back up files and directories) → Leer CUALQUIER archivo (bypass ACLs)
SeRestorePrivilege        (Restore files and directories) → Escribir CUALQUIER archivo
SeTcbPrivilege            (Act as part of the OS)        → God mode (malware)
SeLoadDriverPrivilege     (Load/unload device drivers)   → Kernel rootkit
SeTakeOwnershipPrivilege  (Take ownership of files)      → Tomar control de objetos
SeImpersonatePrivilege    (Impersonate a client)         → Token manipulation, potato attacks
~~~

#### Security Options
- Controla opciones misceláneas de hardening del sistema. Son alrededor de 200 ajustes diferentes pero los más importantes son 10 o 15 más que nada. Los más críticos: 
	- **Interactive Logon**: Permite configurar políticas relacionadas al inicio de sesión, como la autenticación, mensajes personalizados, caché de credenciales y protección contra accesos no autorizados. 
	- **Network Security**: Políticas clave para reforzar la seguridad en la autenticación y comunicación de red, especialmente en entornos de **Domain**. 
	- **User Account Control (UAC)**: Permite configurar cómo se comporta el control de cuentas de usuario.

~~~~
-----------Interactive Logon --------------------------------------
Do not display last user name        → Seguridad: evita enumeration
Do not require CTRL+ALT+DEL          → Si disabled = seguridad física
Message text/title for users         → Warning banners (compliance)

-----------Network Security --------------------------------------
LAN Manager authentication level     → NTLM vs NTLMv2 vs Kerberos
Minimum session security (NTLM)      → Encryption + signing
Do not store LAN Manager hash        → Previene LM hash (muy débil)


-----------User Account Control (UAC) ----------------------------
Behavior of elevation prompt (Admin) → Cuándo pide UAC
Behavior of elevation prompt (User)  → Qué pasa si user intenta elevar
Run all administrators in Admin Approval Mode → Si disabled, no hay UAC (MAL)
~~~~


#### Audit Policy / Advanced Audit Policy 
- Permiten definir qué **eventos** de seguridad se registran en el sistema Windows. Sin auditoría no hay evidencia de actividades maliciosas, errores, o cambios críticos.  **Sin auditoría, no existió**.
- **Advanced Audit Policy** sobrescribe a **Audit Policy** (siempre y cuando Advanced este configurado).
- **Legact Audit Policy** cuenta con 9 categorías amplias. Por otro lado, **Advanced Audit Policy** cuenta con 53 **subcategorías granulares** (mucho mejor). 
- **Registry key** para forzar **Advanced**: `HKLM\System\CurrentControlSet\Control\Lsa\SCENoApplyLegacyAuditPolicy = 1`
 
~~~
-----------Audit Policy (Legacy) --------------------------------
Audit account logon events    → Autenticación (Kerberos/NTLM validation)
Audit logon events            → Sesiones (local/remote logons)
Audit account management      → Creación/modificación de cuentas
Audit policy change           → Cambios en audit policies (anti-forensics)
Audit privilege use           → Uso de privilegios sensibles
Audit object access           → Acceso a archivos (requiere SACL configurado)

----------Advanced Audit Policy --------------------------------
Account Logon
  └─ Credential Validation    → 4768 (Kerberos TGT), 4776 (NTLM)

Logon/Logoff
  ├─ Logon                    → 4624 (success), 4625 (failed)
  ├─ Logoff                   → 4634, 4647
  └─ Special Logon            → 4672 (admin logon)

Object Access
  ├─ File System              → 4656, 4663 (file access)
  ├─ SAM                      → Credential dumping detection
  └─ Registry                 → Persistence detection

Detailed Tracking
  └─ Process Creation         → 4688 (command line logging)

Privilege Use
  └─ Sensitive Privilege Use  → 4672, 4673, 4674

----------Events ID -------------------------------------------
4624 → Successful logon (ver Logon Type)
4625 → Failed logon (brute force)
4648 → Explicit credentials (RunAs, lateral movement)
4672 → Special privileges (admin logon indicator)
4688 → Process created (si command line enabled)
4720 → User created
4732 → User added to group (privilege escalation)
4740 → Account locked out (brute force victim)


----------Logon Types ------------------------------------------
Type 2  → Interactive (physical, console)
Type 3  → Network (SMB, RPC, network shares)
Type 4  → Batch (scheduled tasks)
Type 5  → Service (service accounts)
Type 7  → Unlock (screen unlock)
Type 10 → RemoteInteractive (RDP)
Type 11 → CachedInteractive (offline logon con cached creds)
~~~

#### Windows Firewall 
- Controla el tráfico de red entrante y saliente. Tiene 3 perfiles: **Domain**, **Private**, **Public**.
	- **Domain**: Cuando se está conectado a una **Domain Network**. 
	- **Private**: Redes caseras/confiables.
	- **Public**: Redes públicas (más restrictivo).
- Configuración crítica: 

~~~
Inbound connections  → Default: Block (excepto reglas explícitas)
Outbound connections → Default: Allow (casi siempre)

----------Reglas críticas para auditar --------------------------
Allow RDP (3389)     → ¿Desde dónde? ¿Cualquier IP?
Allow SMB (445)      → ¿Lateralmente accesible?
Allow WinRM (5985/6) → ¿PowerShell remoting abierto?
Allow RPC (135, dynamic) → ¿Quién puede?
~~~

#### AppLocker / Software Restriction Policies
- Controla qué aplicaciones/scripts pueden ejecutarse en el sistema. **Application whitelisting = prevención real de malware** debido a que el malware no puede ejecutarse.

~~~
----------Tipos de reglas ------------------------------------------
Executable rules  → .exe, .com
Script rules      → .ps1, .bat, .vbs, .js
MSI rules         → .msi, .msp (installers)
DLL rules         → .dll (alto overhead, usar con cuidado)

----------Modos de enforcement -------------------------------------
Not Configured → Sin control
Audit Only     → Loggea violaciones, no bloquea (testing)
Enforce        → Bloquea + loggea

----------Approach recomendado -------------------------------------
Default: Deny all
Allow:
  - C:\Windows\*
  - C:\Program Files\*
  - Signed by trusted publishers    

----------Event IDs (AppLocker log) --------------------------------
8002 → Allowed
8003 → Audited (would be blocked)
8004 → Blocked
~~~

#### RSOP / gpresult
- En producción, las policies vienen de múltiples fuentes (local, site GPO, domain GPO, OU GPOs). Se necesita **ver el resultado final** y **diagnosticar por qué algo no se aplicó**. Para ello es posible utilizar estas herramientas: 

- **Resultant Set of Policy** (`rsop.msc`): muestra qué **GPOs** se aplicaron y qué settings resultaron.
~~~
1. Win + R → rsop.msc
2. Navegar: Computer Config / User Config
3. Ver cada setting
4. Right-click → Properties → "Precedence" tab
   
Se busca: 
- ¿Qué GPO ganó? (última en aplicarse según LSDOU)
- ¿Hubo conflictos?
- ¿Alguna GPO fue filtrada? (Security Filtering, WMI Filter)
~~~

- **Group Policy Result** (`gpresult`): Se utiliza desde la linea de comandos. El comando básico es `gpresult /r` o el comando completo (HTML report):
~~~
gpresult /h C:\gpreport.html /f
~~~
- Secciones críticas del reporte: 
~~~
Applied Group Policy Objects     → Qué GPOs aplicaron
Denied Group Policy Objects      → Cuáles NO aplicaron (y por qué)
Security Group Membership        → Qué grupos tiene el user/computer
WMI Filters                      → Si hay filtros activos
~~~

- **Security Configuration Editor** `secedit`: Herramienta que permite a los administradores **crear**, **editar** y **aplicar** plantillas de seguridad para configurar políticas del sistema.

~~~cmd
-------------Export Policy Actual --------------------------------
secedit /export /cfg C:\current_policy.inf

-------------Analizar contra baseline ----------------------------
secedit /analyze /db secedit.sdb /cfg C:\baseline.inf /log analysis.log

-------------Ver diferencias -------------------------------------
Abrí analysis.log
Buscá discrepancias entre configuración actual y baseline
~~~