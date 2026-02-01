#### net Command
- El comando `net` es utilizado para la administración der redes, usuarios, grupos y recursos compartidos. Está disponible en Windows 10, Windows 11 y en todas las versiones de Windows Server.

~~~cmd
C:∖> net help
The syntax of this command is:
NET HELP
command
          -or-
NET command /HELP
   Commands available are:
   NET ACCOUNTS            NET HELPMSG               NET STATISTICS
   NET COMPUTER            NET LOCALGROUP            NET STOP
   NET CONFIG              NET PAUSE                 NET TIME
   NET CONTINUE            SESSION                   NET USE
   NET FILE                NET SHARE                 NET USER
   NET GROUP               NET START                 NET VIEW
   NET HELP
   NET HELP NAMES explains different types of names in NET HELP syntax lines
   NET HELP SERVICES lists some of the services you can start.
   NET HELP SYNTAX explains how to read NET HELP syntax lines.
   NET HELP command | MORE displays Help one screen at a time.
C:∖>
~~~

- `net use`: Para conectar o desconectar unidades de red compartidas. 
- `net view`: Para listar equipos o recursos compartidos en una red. 
- `net user`: Para gestionar cuentas de usuario locales o dominio. 
- `net config`: Para ver configuraciones de servidor o grupo de trabajo. 
- `net share`: Para crear o gestionar compartidos locales.
- `net accounts`: Configura contraseñas y requerimientos de logon para usuarios.
- `net start / net stop:`: Inicia un servicio de red o lista los servicios de red ejecutandose / detiene servicios de red.
-  `net session`: lista o desconecta sesiones entre el computador y otras computadoras en la red.
- `net use`: muestra, conecta o desconecta información sobre los recursos compartidos en la red.