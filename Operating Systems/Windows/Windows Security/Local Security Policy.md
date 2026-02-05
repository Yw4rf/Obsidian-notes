#### Local Security Policy 
- La **Local Security Policy** (`secpol.msc`) es el contenedor de las configuraciones de seguridad aplicables a un equipo local ( E.g: cuentas locales, derechos, opciones de seguridad, auditoria, firewall local, AppLocker, IPsec, etc.). 
- En entornos como **Active Directory**, las **Account Policies** se definen preferentemente a nivel de dominio y **sobrescriben** la política local para equipos unidos al dominio; Las políticas aplicadas vía **GPO (Group Policy Object)** de dominio (y GPOs vinculadas al OU) tienen precedencia sobre la local.
- Para administrar políticas locales se usan: `secpol.msc` y `gpedit.msc` (**Local Group Policy Editor**), pero en escala empresarial se usan **GPOs (Group Policy Objects)**

#### LSDOU (Local - Site - Domain - OU)
- Windows aplica las políticas en el orden **LSDOU**. La Directiva Local es la **base de la pirámide**, pero también la más débil en jerarquía: 
	1. **Local**: Local Policy  `secpol.msc` 
	2. **Site**: sitio de Active Directory `dssite.msc`
	3. **Domain**: dominio `domain.msc`
	4. **OU**: Organizational Unit (de padre a hijo) `gpmc.msc`
 - La **última política aplicada gana**, salvo una que otra excepción. Si una política de **Dominio (Domain)** entra en conflicto con la **Local**, **la de Dominio siempre gana**. 
 - Si por alguna razón un cambio en **Local** no surte efecto, revisar **Resultant Set of Policy** `rsop.msc`

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
- Se aplica según el **AD Site** (basado en subred IP). Es poco usado en la práctica. Normalmente se usa para: 
	- Configuración dependiente de ubicación, control de tráfico WAN, políticas de autenticación según región. 