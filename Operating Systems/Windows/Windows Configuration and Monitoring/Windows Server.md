#### Windows Server
- **Windows Server** es una familia de sistemas operativos de Microsoft diseñada específicamente para **entornos empresariales** y **data centers**. Está optimizado para: 
	- **Alta disponibilidad**, **Gestión centralizada**, **Servicios de red críticos**, **Seguridad y control de identidades**, **Virtualización y escalabilidad**.
- El sistema operativo es una **plataforma de roles**, en **Windows Server** el sistema operativo base es minimo, por defecto no hace **casi nada** hasta que se le instala **roles** y **features**: 

	- **Roles**: Define qué función cumple el servidor en la red. Un **role** instala servicios de Windows específicos, componentes de red, APIs, configuración automática, dependencias obligatorias. En resumen, un rol **expone servicios a otros equipos** en la red. Pueden ser: **Active Directory Domain Services (AD DS)**, **DNS Server**, **DHCP Server**, **File and Storage Services**, **Web Server (IIS)**.  E.g: 
		- Un servidor con el rol **AD DS** deja de ser "un Windows más" y pasa a ser un **DC (Domain Controller)**
	- Cuando se instala un role, el servidor cambia su comportamiento, pasa a ser una infraestructura crítica y otros sistemas dependen de él.

	- **Features**: Son las capacidades adicionales que apoyan esos roles. Apoyan a roles o tareas administrativas. Técnicamente son librerías, servicios auxiliares, frameworks o herramientas del sistema. E.g: **.NET Framework**, **Group Policy Management**, **Failover Clustering**, **Windows Backup**, **RSAT tools**, etc. 
		- Un feature le da capacidades al servidor.

| Concept                             | Role | Feature        |
| ----------------------------------- | ---- | -------------- |
| Define la función del servidor      | ✔    | ✘              |
| Expone servicios a la red           | ✔    | Normalmente no |
| Cambia la identidad del host        | ✔    | ✘              |
| Puede depender de otros componentes | ✔    | ✔              |
| Puede existir sin roles             | ✘    | ✔              |