### Get-Command  
- El comando `Get-Command` (o su alias `gsm`) permite obtener información de todos los comandos en PowerShell (cutlets, funciones, aplicaciones, scripts, etc). Sirve para: 
	1. **Listar comandos**: muestra todos los comandos disponibles en la sesión actual.
	2. **Filtrado**: permite filtrar comandos específicos buscando por nombre, tipo y más.
	3. **Información de comandos**: Proporciona información detallada sobre un comando en particular, como sus parámetros y su uso.

#### Get-Command filters
- Es posible: 
	- **Listar todos los comandos**: `Get-Command`
	- **Filtrar por nombre**: `Get-Command -Name "command_name"`
	- **Filtrar por tipo de comando**: `Get-Commamd -CommandType Cmdlet` o `Get-Command -CommandType Function`
	- **Obtener info detallada de un comando**: `Get-Command -Name "command_name" | Format-List *` 
	- **Buscar comando que contiene una palabra**: `Get-Command -Name "*parte_del_nombre*"`
- Es posible y útil también filtar por `-Verb` (verbo) y `-Noun` (sustantivo). Esto es fundamental en el diseño de PowerShell debido a que todos los comandos utilizan tal estructura.
	- **Filtrar por verbo** (Get, Set, New, Remove, etc): `Get-Command -Verb "Get"`
	- **Filtar por sustantivo** (Process, Service, Item, etc): `Get-Command -Noun "Process"`
	- Es posible aplicar ambos parámetros en una misma linea: `Get-Command -Verb "Get" -Noun "Process"`
- Para obtener detalles adicionales sobre los comandos es posible usar pipelines y `Select-Object` mediante `Get-Command | Select-Object Name, CommandType, Module` 