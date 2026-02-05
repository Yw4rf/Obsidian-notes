#### Event Viewer
- El Windows **Event Viewer** es el **sistema central de logging** de Windows. Registra **eventos generados por el sistema operativo, servicios, aplicaciones y mecanismos de seguridad.** 
- Un **evento** es la materialización de un comportamiento real: 
	- Un proceso que arranca, un servicio que falla, un usuario que inicia sesión, una política que se aplica, un driver que crashea, etc. 
- Su función principal es el **diagnóstico**. Los **eventos** sirven para **Troubleshooting**, **Detección de incidentes**, **Investigación forense**, **Auditoria y cumplimiento**, **Correlación con alertas EDR / SIEM**, etc. El **Event Viewer** es el punto de partida para toda investigación en Windows.
- El **Event Viewer no registra eventos por sí mismo**, solo expone los eventos producidos según las políticas de **auditing** ([[Local Security Policy]])
- Arquitectura de Windows Event Viewer y términos clave: 
	- **Provider**: el emisor del evento (E.g: `Microsoft-Windows-Security-Auditing`, `Sysmon` o un programa/aplicación) 
	- **Channel / LogName**: donde se escribe el evento, E.g: 
		- `Application`: Eventos generados por aplicaciones y servicios de usuario, incluyendo errores, crashes y logs propios de la app. (E.g: Chrome, Office, Games, etc).
		- `Security`: Intentos de inicio de sesión, cambios de permisos y auditorias. Depende completamente del auditing habilitado.
		- `System`: eventos de Windows, drivers y hardware.  
	- **EventID**:  identificador númerico de tipo de evento (E.g: `4624`, `4688`)
	- **EventRecordID**: identificador único secuencial en el archivo de log (diferente al EventID) 
	- **Level**: gravedad del evento (E.g: `Information`, `Warning`, `Error`, `Critical`)
	- **Task / Opcode / Keywords**: metadatos que dan contexto sobre la categoría y fase de la operación
	- **Event XML / EventData**: cada evento tiene una representación XML con campos como `TimeCreated`, `Provider`, `EventID`, `Computer`, `UserID`, `EventData` (campos específicos como `NewProcessName`, `CommandLine`, `SubjectUserName`, etc)
- Campos útiles para observar dentro de un evento: 
	- `TimeCreated`: timestamp (siempre usar UTC/convertir)
	- `ProviderName`: permite saber quién generó el evento
	- `EventID`: saber el ID del evento permite identificar qué tipo de evento se generó
	- `Level / Task`: gravedad y categoría del evento
	- `UserID / Account Domain`: correlación por identidad
	- `NewProcessId`, `CreatorProcessId`, `ProcessId`: correlación por proceso
	- `CommandLine`: si está disponible es esencial para detección (hay que habilitarlo)
- Los eventos **no se analizan de forma aislada**. La investigación se basa en **correlación**, principalmente por:
    - **Tiempo**
    - **Usuario**
    - **PID (Process ID)**
    - **Host**
- Un solo evento rara vez indica un incidente. E.g de correlación típica:
    - `4624` → Logon exitoso
    - `4672` → Privilegios elevados asignados
    - `4688` → Ejecución de proceso sospechoso
- El valor real del Event Viewer está en:
    - reconstruir secuencias, entender el contexto, detectar patrones anómalos.

#### Auditing
- **Auditing** es el mecanismo que define **qué acciones del sistema se registran como eventos**. 
- El **Event Viewer no decide qué se registra**: solo muestra los eventos que fueron generados según las **políticas de auditoría** configuradas.
- Si una acción **no está auditada**, el evento **no existe**, aunque la acción haya ocurrido.
- El **Security Log depende completamente del auditing**. Sin auditing habilitado, no hay visibilidad de seguridad.
- El auditing se configura mediante:
    - **Local Security Policy**
    - **Group Policy (GPO)**
    - **`auditpol`** (línea de comandos)
- Las políticas de auditoría se organizan en **categorías y subcategorías**, y cada una puede registrar:
    - Success
    - Failure
    - Ambas
    - Ninguna (deshabilitada)
- Comando para ver el estado del auditing: `auditpol /get /category:*`
- Comando para habilitar auditoria de creación de procesos: `auditpol /set /subcategory:"Process Creation" /success:enable`

#### Event IDs 
- `4624` - **Logon exitoso (subcategoria: Audit Logon)**. Útil para ver sesiones creadas.
- `4625` - **Logon fallido**. Buen indicador de bruteforce o intentos externos.
- `4688` - **Nuevo proceso creado**. Fundamental para ver ejecución y padres (al incluir `CommandLine` su utilidad sube mucho). 
- `4672` - **Privilegios especiales asignados a un logon (admin-equivalent)**. Detectar escalado/uso de cuentas privilegiadas. 
- `1102` - **Auditing: el log de seguridad fue borrado**. Un indicador de intento de ocultamiento.
- `7045 / 4697` - **Servicio instalado** (7045 es un evento del Service Control Manager; 4697/others aparecen en Security cuando Auditing está habilitado) Nuevos servicios = persistencia.
- `4698 / 4702` - **Scheduled task creado / modificado**. Otro método de persistencia ampliamente usado.

#### Event Viewer GUI Tips
- **Administrative Events (Custom View preconfigurada)**: buen triage inicial (muestra Critical / Error / Warning)
- **Filter Current Log...**: filtrar por Event IDs, nivel, fuente, rango horario. 
- **Attach Task To This Event**: automatizar respuestas locales (E.g: ejecutar script cuando aparece X). Útil en laboratorio, raramente usado en producción.
- **Save / Export**: `.evtx` para análisis forense (file --> Save All Events As...).
- **View --> Show Analytics and Debug Logs**: para ver canales adicionales (útil con Sysmon).

#### CLI / PowerShell
- **wevtutil (CLI Windows)**
	- listar canales: `wevtutil el`
	- exportar log: `wevtutil epl Security C:\temp\Security.evtx`
	- limpiar log: `wevtutil cl Security` solo si corresponde (audit trail)
- **PowerShell (Lo más moderno)**
filtrar por hashtable (rápido y preciso):
~~~PowerShell
# últimos 500 eventos 4688 en Security
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4688} -MaxEvents 500 |
  Select-Object TimeCreated, Id, @{n='Message';e={$_.Message -replace "`r`n"," "}} | Format-Table -AutoSize
~~~

Buscar 4624 en última hora:
~~~PowerShell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4624; StartTime=(Get-Date).AddHours(-1)} | ft TimeCreated, Id, @{n='Account';e={$_.Properties[5].Value}}
~~~
(la indexación de `Properties` varía según evento; usar `-ExpandProperty` o parsear XML cuando sea necesario).

- `Get-EventLog` = legacy / lento
- `Get-WinEvent` = moderno / recomendado

#### Event Viewer Limitations
- No todo el comportamiento del sistema se registra por defecto.
- La visibilidad depende del nivel de auditing configurado.
- Los logs pueden ser:
    - borrados (`Event ID 1102`), sobrescritos por retención insuficiente, etc.
- Malware avanzado puede:
    - evadir generación de eventos, ejecutar código en memoria, operar en kernel mode
- Por estas razones, el Event Viewer:
    - **no es suficiente por sí solo**, debe complementarse con:
        - **Sysmon**, **EDR**, **SIEM**, **Windows Event Forwarding (WEF)**