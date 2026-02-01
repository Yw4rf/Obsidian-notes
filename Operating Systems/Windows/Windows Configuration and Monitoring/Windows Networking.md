#### Network and Sharing Center
- Es la herramienta Windows para visualizar, configurar y diagnosticar la conectividad de la red. Aunque en Windows 10/11 muchas opciones se duplicaron o migraron a **Settings**, este panel sigue siendo relevante desde una perspectiva técnica y operativa, especialmente en troubleshooting o redes empresariales. 
- Es un **applet del Panel de Control** que centraliza la administración de: 
	- Conectividad de red (LAN, Wi-Fi, VPN)
	- Tipo de red (Public / Private / Domain)
	- Recursos compartidos
	- Adaptadores de red
	- Diagnóstico de problemas
- Permitie ver el estado de la red y modificar su configuración de manera gráfica.
- Muestra: 
	- **Estado de Internet**: Internet access, No Internet access.
	- **Tipo de red**: Public (perfil restrictivo, firewall más estricto), Private (red confiable LAN doméstica/empresa), Domain (unido a un **Active Directory Domain**)
	- **Tipo de conexión**: Ethernet, Wi-Fi, etc. 
- **Network Sharing**, opciones disponibles: 
	- **Change Adapter Settings** (Cambiar ajustes del adaptador)
	- **Change Advanced Sharing Settings** (Cambiar ajustes avanzados del adaptador)
	- **Set up a new Connection or Network** (Configurar una nueva conección o red)
	- **Troubleshoot problems** (solucionar problemas)
- **Change Adaptere Settings (Configuración de Adaptadores)**, esta sección muestra todas las interfaces de red del sistema: 
	- Ethernet, Wi-Fi, VPN, Adaptadores virtuales (hyper-V, VirtualBox, etc.)
	- Es posible deshabilitar o habilitar adaptadores, ver estado, acceder a propiedades de cada interfaz, etc.
- **Adapter Properties (Propiedades del Adaptador)**, "This connection uses the following items", acá se listan los protocolos y servicios asociados al adaptador: 
	- Client for Microsoft Networks
	- File and Printer SHaring
	- Internet Protocol Version 4 (TCP/IPv4)
	- internet Protocol Version 5 (TCP/IPv6)
- **TCP/IPv4 and TCP/IPv6 Properties**, es posible definir cómo obtiene su configuración el host: 
	- **DHCP (automatic)**: IP Address, Subnet mask, Default gateway, DNS Server. Usado en: Redes corporativas, redes domésticas, etc. 
	- **Manual Configuration (static)**: IP fija, Gateway fijo, DNS específicos. Usado en Servidores, Equipos críticos, Segmentos controlados de red, Laboratarios y Troubleshooting. 

#### netsh.exe
- Ademas de la GUI, Windows permite administrar la red desde la consola con **netsh**. Permite ver y modificar interfaces, IP, rutas, Firewall, Wi-Fi.  Ejemplo: `netsh interface ip show config`

#### nslookup
- El comando **nslookup** sirve para probar **DNS resolution**. Ejemplo: `nslookup google.com`, si responde correctamente DNS está en funcionamiento y hay conectividad hacia el resolver.

#### netstat 
- El comando **netstat** muestra las conexiones de red actuales. Campos importantes: **Proto** (TCP/UDP), **Local Address** (IP:Puerto local), **Foreign Address** (IP:Puerto remoto), **State** (ESTABLISHED, TIME_WAIT, LISTENING). 

~~~cmd
netstat
Active Connections
  Proto     Local Address        Foreign Address     State
  TCP     127.0.0.1:3030        USER-VGFFA:58652   ESTABLISHED
  TCP     127.0.0.1:3030        USER-VGFFA:62114   ESTABLISHED
  TCP     &127.0.0.1:3030       USER-VGFFA:62480   TIME_WAIT
  TCP     127.0.0.1:3030        USER-VGFFA:62481   TIME_WAIT
  TCP     127.0.0.1:3030        USER-VGFFA:62484   TIME_WAIT
~~~