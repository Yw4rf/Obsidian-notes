#### Windows Firewall
- El Firewall **controla qué tráfico de red puede entrar y salir** de la computadora. Este mismo funciona con reglas: 
	- **Dirección**: tráfico entrante (inbound) o saliente (outbound). 
	- **Protocolo**: TCP, UDP, ICMP, etc. 
	- **Puerto**: E.g: Port 443 para HTTP. 
	- **Programa**: qué aplicación genera/recibe ese tráfico.
	- **Acción**: permitir o bloquear.
- Cuando llega o sale un paquete de red, el firewall lo evalúa contra todas las reglas existentes. Si ninguna aplica, usa el **comportamiento por defecto** del perfil activo.
- El firewall de Windows define **tres perfiles independientes** (aplica uno según a que red se este conectado): 
	1. **Dominio**: cuando la PC está unida a un Domain de Active Directory. 
	2. **Privado**: cuando se marca la red como "de confianza" (casa, trabajo personal). Es más permisivo: permite el descubrimiento de red, compartir archivos, etc. 
	3. **Público**: cuando se conecta a una red desconocida (café, aeropuerto, hotel) es la más restrictiva debido a que bloquea casi todo el tráfico entrante por defecto. Es la protección al WiFi Público. 
- Tráfico entrante (inbound) vs saliente (outbound): 
	- **Inbound**: conexiones que se inician desde fuera hacia la PC del usuario. E.g: si alguien intenta conectarse a una PC se escritorio remoto (RDP) por defecto Windows bloquea casi todo el tráfico entrante a menos de que haya una regla explícita que lo permita. 
	- **Outbound**: conexiones que inicia la PC del usuario hacia afuera. E.g: el navegador cuando se conecta a un servidor web, por defecto Windows permite todo el tráfico saliente.
- El firewall por defecto **no bloquea programas que quieren conectarse a internet**. 

#### wf.msc
- La interfaz avanzada `wf.msc` da control total del Firewall. Este mismo permite: 
	1. Ver todas las reglas activas con sus detalles.
	2. Crear reglas personalizadas con criterios específicos. 
	3. Ver el registro (log) de conexiones bloqueadas/permitidas. 
	4. Configurar el comportamiento por defecto de cada perfil. 