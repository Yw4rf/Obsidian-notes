#### Anatomy of a command

![Command-Anatomy](anatomy-of-a-command.png)

- En la imagen es posible observar que: 
	1. El **cmdlet** es `Get-Command`. Los cmdlets ([[Cmdlets]]) de PowerShell siempre tienen el formato **Verb-Noun** (Verbo-Sustantivo).
	2. El **primer parámetro (Parameter 1)** `-Verb` (indica: verbo) se le da el valor `Get` (debido a que el valor no contiene espacios ni puntuaciones, no necesita comillas).
	3. El **segundo parámetro (Parameter 2)** `-Module` (indica: modulo) se le da dos valores, el primero `PSReadLine` y el segundo luego de una coma `PowerShellGet`. 
	4. El **parámetro final (Parameter 3)** `-Syntax` es un parámetro **Switch (interruptor)** significa que no necesita un valor, específicar el parámetro es suficiente. 
- Los parámetros SIEMPRE empiezan con un **dash (-)**
- Hay un espacio obligatorio entre el nombre del parámetro y el valor del parámetro.
- los comandos **no son case sensitive** (no sensible a mayúsculas o minúsculas). 