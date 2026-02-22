### Alias
- Los nombres de los comandos de PowerShell pueden ser consistentes e intuitivos, pero suelen ser largos. Para mejorar ello existen los **alias**, los cuales **son nick-names para los comandos**. 
	- Es posible ver todos los alias disponibles en la sesión con el comando `Get-Alias`
- Para obtener el **alias** de un comando en específico se utiliza el comando `Get-Alias -Definition [command]`. E.g: En el ejemplo se puede observar que el alias de `Get-Process` es `gps`.

~~~PowerShell
> Get-Alias -Definition Get-Process

CommandType     Name    Version    Source
-----------     ----    -------    ------
Alias           gps -> Get-Process
~~~

- Cuando se pide ayuda (`Get-Help` o `Help`) sobre un alias, este suele devolver toda la ayuda del comando, incluyendo el nombre completo del comando.

~~~PowerShell
> Get-Help gps

NAME
    Get-Process
    
SYNOPSIS
    Gets the processes that are running on the local computer.
    
    
SYNTAX
    Get-Process [-FileVersionInfo 
    <System.Management.Automation.SwitchParameter>] [-Module 
    <System.Management.Automation.SwitchParameter>] [[-Name] 
    <System.String[]>] [<CommonParameters>]
~~~

- Es posible crear alias propios utilizando el comando `New-Alias`, exportando una lista de aliases utilizando `Export-Alias`, o incluso importando una lista de aliases previamente creada utilizando `Import-Alias`. 
	- Cuando se crea un alias, esta misma **se mantiene hasta que la sesión actual de la shell cierre**, una vez que esa sesión se cierra esos alias ya no permanecen. Por ello es útil exportarlos, para poder utilizarlos nuevamente en otra sesión. 
- E.g de sintaxis para `New-Alias`: `New-Alias -Name mycmd -Value Get-Process`

#### Important 
- Los alias pueden no ser la mejor práctica en scripts compartidos o en producción, ya que pueden ser menos legibles para aquellos que no están familiarizados con ellos. Es por esta razón que los alias suelen ser por sesión principalmente.