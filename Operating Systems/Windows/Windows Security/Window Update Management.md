#### Windows Update Management
- Es el conjunto de mecanismos que permiten **recibir**, **instalar**, **gestionar** y **auditar** las actualizaciones del sistema operativo Windows. Su objetivo principal es reducir la superficie de ataque manteniendo el sistema parcheado contra vulnerabilidades conocidas.
- ¿Por qué es crítico en seguridad?
	- La mayoria de ataques no usan **zero-days** (**Zero Day** se refiere a una vulnerabilidad de seguridad en software o hardware que **no es conocida ni por el fabricante ni por los usuarios**), usan vulnerabilidades conocidas y ya parcheadas. Un sistema sin updates es: más fácil de explotar, más ruidoso, más barato para el atacante. Siempre hay que preguntarse, ¿está el sistema actualizado? 
- Diferentes tipos de updates en Windows: 
	- **Security Updates**: Corrigen vulnerabilidades de seguridad, impactan: drivers, kernel, servicios, componentes críticos. 
	- **Critical Updates**: Corrigen fallos que afectan estabilidad/funcionalidad. Pueden tener un impacto indirecto en la seguridad del sistema.
	- **Feature Update**: Nuevas versiones de Windows (E.g: 22H2 -> 22H3), cambian funcionalidades, más riesgo operativo, en empresas suelen retrasarse.

#### How it Works?
- Windows consulta los servidores de Microsoft, descarga las actualizaciones relevantes y las instala según la política configurada. Puede: 
	- Instalarse automáticamente, notificar acerca de la actualización o esperar a la confirmación para efectuar la misma.
- Todo esto se gestiona desde: `Settings --> Windows Update`

#### Windows Update Security
- Cuando el zero-day está, el parche aun no ha sido lanzado. Después del parche, el exploit suele aparecer públicamente y el riesgo aumenta si no se actualiza el sistema.
- El **patch level** es el contexto del incidente, este cambia la hipótesis del ataque. Durante una investigación de un incidente de seguridad, un exploit puede ser: imposible (ya parcheado) o totalmente viable (sistema desactualizado). 
- El **update status** puede indicar el riesgo: 
	- Sistemas muy atrasados: mayor probabilidad de compromiso, mayor severidad del incidente.
- Un **host** sin parches es **high priority (alta prioridad)**
- **Windows Update es diferente a un Evento de seguridad**. Los updates no aparecen como "alertas" pero dejan trazas: 
	- En el historial de actualizaciones, en el log del sistema.
- Un fallo recurrente al actualizar pude indicar, interferencias, problemas de permisos o corrupción del sistema.

#### Windows Update for Business
- Las empresas **no dependen del usuario** para actualizar. Utilizan mecanismos centralizados: 
	- **WSUS (Windows Servers Update Services)**, **Microsoft Update for Business**, **Intune**.
	- Permiten: distribuir parches, controlar reinicios, auditar cumplimiento, etc. 
- **Si no hay gestión centralizada, el riesgo se multiplica**.