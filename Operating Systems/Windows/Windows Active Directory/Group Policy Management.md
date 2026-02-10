#### LSDOU (Local / Site / Domain / OU)
- Windows aplica las políticas en el orden **LSDOU**. La Directiva Local es la **base de la pirámide**, pero también la más débil en jerarquía: 
	1. **Local**: Local Policy  `secpol.msc` 
	2. **Site**: sitio de Active Directory `dssite.msc`
	3. **Domain**: dominio `domain.msc`
	4. **OU**: Organizational Unit (de padre a hijo) `gpmc.msc`
 - La **última política aplicada gana**, salvo una que otra excepción. Si una política de **Dominio (Domain)** entra en conflicto con la **Local**, **la de Dominio siempre gana**. 
 - Si por alguna razón un cambio en **Local** no surte efecto, revisar **Resultant Set of Policy** `rsop.msc`
 - La **Local Security Policy** nunca vive aislada, siempre está subordinada al modelo **LSDOU**. 

#### Local Policy (L)
- Aplica **siempre** a todos los users y equipos del **host**. Se configura con: 
	- `secpol.msc` (Security Policy)
	- `gpedit.msc` (Local Group Policy)
- Incluye: 
	- Password policy local (solo efectiva en **stand-alone**, solo se aplican cuando el equipo **no está unido a un dominio**), User Rights Assignment, Security Options, Local Audit Policy, Firewall, AppLocker, etc.
- Las **Account Policies locales son ignoradas** y reemplazadas por la **Domain Policy** en equipos unidos a dominio. Aunque otras configuraciones se pueden aplicar si no hay conflicto. 
- Malware o atacante con **admin local** puede **modificar la política local** para: 
	- Desactivar auditoría, permitir ejecución de binarios, relajar UAC (User Accounts Control).

#### Site Policy (S)
- Se aplica según el **AD Site** (basado en subred IP). Es poco usado en la práctica, pero se procesan si existen. Normalmente se usa para: 
	- Configuración dependiente de ubicación, control de tráfico WAN, políticas de autenticación según región. 
- Un **Site GPO** mal configurado puede afectar **múltiples dominios/OU** sin que el equipo de IT lo note.

#### Domain Policy (D)
- Aplica a todos los **objetos del dominio**. Normalmente `Default Domain Policy` y **GPOs** adicionales linkeadas al dominio.
- Las siguientes son solo efectivas desde el dominio:
	- Password Policy, Account Lockout Policy, Kerberos Policy (ESTAS **NUNCA DEBERIAN CONFIGURARSE EN OU**)
- Cambios en **Domain Policy**, eventos de **alto impacto**: 
	- Event ID `4739` (**Domain Policy Changed**)
	- Event ID `5136` (**AD Object Modified**)

#### OU Policy (Organization Unit Policy)
- Las **OU Policy** se aplican en orden jerárquico. **OU padre → OU hijo → OU nieto...** 
	- La **GPO linkeada más abajo gana**. E.g:
~~~md
Domain
 └── Workstations
     └── SOC-Computers
~~~
La **GPO** en `SOC-Computers` **sobrescribe** a la de `Workstations`.
- Se usa generalmente para diferenciar políticas por:
	- **Tipo de equipo** (Servers vs Workstations), **Rol** (SOC, Developers, etc), **Nivel de hardening**.

#### Break the Flow
- Son excepciones y mecanismos de control: 
	- **Enforced (No Override)**: Una **GPO** marcada como **Enforced** **NO puede ser sobrescrita** por **OUs** inferiores. Se sigue aplicando incluso si no hay conflicto. 
		- Un enforced mal puesto puede romper la seguridad o **impedir hardening**. 
	- **Block Inheritance**: Una **OU** con **Block Inheritance** bloquea **GPOs** de **Site** y **Domain**. No bloquea **GPOs** de **Enforced**. 
		- Técnica común para **evadir controles** si el atacante tiene permisos **AD**.
	- **Security Filtering**: la **GPO** se aplica **solo** si el objeto tiene permiso **Read + Apply Group Policy**. No basta con estar en la **OU**. 
		- Los atacantes la utilizan para persistencia sigilosa, ataques modificando **ACLs** de **GPO**
	- **WMI Filtering**: Aplica la **GPO** solo si se cumple una condición **WMI** como: 
	- OS Version, RAM, Laptop vs Desktop, etc. E.g: 
	~~~
	SELECT * FROM Win32_OperatingSystem WHERE Version LIKE "10.%"
	~~~

#### How to Diagnostic LSDOU
- `gpresult` **(Group Policy Result)**: muestra todas las **GPOs** aplicadas, el **orden**, de donde vienen **(L/S/D/OU)**, filtradas por seguridad o **WMI**. E.g: 
~~~
gpresult /h result.html
~~~
- `rsop.msc` **(Resultant Set of Polify)**: muestra el conjunto final y efectivo de configuraciones de políticas de grupo aplicadas a un usuario o host. 
- **Group Policy Events**: Eventos importantes del **GPOs**. E.g:
	- `5312`: **GPO** aplicada correctamente
	- `7016`: error al aplicar **GPO**
	- `1129`: fallo de **DC** / **network**
	- Log:
~~~cmd
Micosoft-Windows-GroupPolicy/Operational
~~~
- `gpupdate` **(Group Policy Update)**: fuerza la aplicación de una **GPO**: 
~~~
gpupdate /force
~~~