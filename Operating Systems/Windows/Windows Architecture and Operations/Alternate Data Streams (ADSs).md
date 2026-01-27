##### Data Streams
- Caracteristica del file system NTFS que permite almacenar múltiples flujos de datos (data streams) dentro de un solo archivo o carpeta.
- NTFS almacena archivos como serie de atributos, como el nombre del archivo o las marcas de tiempo (timestamp). Estos datos los cuales el archivo contiene se almacenan en el atributo **$DATA** la cual es conocida como un flujo de datos (Data Stream). 
- Cada archivo en NTFS tiene al menos un flujo de datos principal, conocido como el **flujo de datos predeterminado**.
- **$DATA** seria el Default Stream (flujo de datos predeterminado). Por ejemplo cuando un archivo de texto se abre y se escribe algo se guarda en $DATA. Es lo que Windows suma al tamaño del archivo (bytes).
##### Alternate Data Streams or ADSss
- Es posible crear flujos de datos alternativos (Alternate Data Streams) que permiten almacenar información adicional como metadatos, comentarios o incluso archivos completos, sin que el tamaño del archivo principal cambie ni sea visible a través de Windows Explorer. 
- Windows lo utiliza de forma legitima. Por ejemplo cuando se descarga un archivo de internet, Windows le pega un ADS llamado `:Zone.Identifier` ADS por el cual Windows identifica que el archivo viene de internet. 
- No están disponibles directamente desde el entorno gráfico, pero pueden accederse mediante líneas de comandos (como `streams.exe`), PowerShell, o herramientas de análisis forense.

##### ADS Malicious Usage
- Son aprovechados por malware para ocultar código, exfiltrar datos o mantener persistencia sin ser detectados. Ejemplo: 

~~~CMD
C:∖ADS> echo "Alternate Data Here" > Testfile.txt:ADS
C:∖ADS> dir
  Volume in drive C is Windows
  Volume Serial Number is A606-CB1B
  Directory of C:∖ADS
2020-04-28 04:01 PM   <DIR>            .
2020-04-28 04:01 PM   <DIR>            ..
2020-04-28 04:01 PM            0 Testfile.txt
                 1 File(s)                 0 bytes
                 2 Dir(s) 43,509,571,584 bytes free
C:∖ADS> more < Testfile.txt:ADS
"Alternate Data Here"
C:∖ADS> dir /r
   Volume in drive C is Windows
   Volume Serial Number is A606-CB1B
   Directory of C:∖ADS
2020-04-28 04:01 PM   <DIR>
2020-04-28 04:01 PM   <DIR>
2020-04-28 04:01 PM            0 Testfile.txt
                            24 Testfile.txt:ADS:$DATA
            1 File(s)            0 bytes
            2 Dir(s) 43,509,624,832 bytes free
C:∖ADS>
~~~

**OUTPUT**: El comando `dir` detalla el tamaño del archivo `Testfile.txt` el cual pesa **0 bytes**, aunque dentro del ADS `Testfile.txt:ADS` hay texto guardado. 

- Un atacante podría esconder el código de un virus dentro de un archivo de texto totalmente inofensivo. El usuario ve un archivo `.txt` vacío, pero el atacante puede ejecutar el flujo oculto usando comandos. 