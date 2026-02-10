##### File Systems 
- Antes de que un dispositivo de almacenamiento (HDD, SSD, etc) pueda ser utilizado como disco necesita ser formateado con un file system (sistema de archivo). A su vez, antes de que un sistema de archivos sea puesto en un dispositivo de almacenamiento necesita ser particionado. 
- El dispositivo de almacenamiento es dividido en areas llamadas particiones. Cada particion es una unidad lógica independiente que puede ser formateada para almacenar informacion. 
- Durante el proceso de instalación de un sistema operativo, la mayoria de los mismos automaticamente particionan y formatean el espacio disponible en el disco con un tipo de file system específico. 

##### File Systems Types
- **exFAT** - Sistema de archivos simple que soporta diferentes tipos de sistemas operativos. FAT tiene un numero limitado de particiones, tamaño de particiones y tamaño de archivos, por lo que usualmente no se usa como sistema de archivos _principal_ para el sistema operativo, pero es el estándar absoluto para **unidades externas** (pendrives, tarjetas SD de gran capacidad) porque elimina el límite de 4GB por archivo de FAT32 y es compatible con casi todo.
- **HFS+** - Sistema de archivos usado por computadoras con MAC OS X y permite nombres de archivos, tamaños de archivos y tamaños de particiones mucho más grandes que FAT. Es posible leer datos de particiones HFS+ con Windows.
- **EXT** - Sistema de archivos usado mayormente por sistemas operativos basados en Linux. Aunque no es soportado por Windows, este permite leer datos de particiones EXT con software especializado.
- **NTFS** - New Technologies File System o también conocido como NTFS es el más usado comunmente como sistema de archivos en Windows. Todas las versiones de Windows y Linux soportan NTFS. Aunque las computadoras con MAC-OS solo pueden leer datos de una partición NTFS, estas mismas pueden ser escritas si es que se instala drivers especializados.

##### NTFS - New Technologies File System
- NTFS es el sistema de archivos más usado por los sistemas Windows debido a varias razones, este mismo soporta gran cantidad de archivos y particiones y es compatible con otros sistemas operativos.
- Es confiable y tiene caracteristicas como la recuperación de archivos. Más importante aún, las caracteristicas de seguridad.
- El control de acceso a datos es logrado por Security Descriptors. A diferencia de sistemas viejos como FAT32, NFTS permite decir exactamente qué usuario puede leer, escribir o borrar un archivo específico. Estos Security Descriptors contienen propiedad y permisos de archivos hasta el nivel de archivo. 
- NTFS también tiene muchas marcas de tiempo (time stamps) para rastrear la actividad de archivos, también conocido como **MACE (Modify, Access, Create and Entry Modified)** las cuales son generalmente utilizadas en analisis forenses para determinar el historial de un archivo o carpeta. Siendo **M**odify: Última vez que se cambió el contenido. **A**ccess**: Última vez que se abrió. **C**reate: Cuándo se creó. **E**ntry Modified: Cuándo cambió la información del archivo en la tabla del sistema (metadatos).
- NTFS ademas soporta cifrado para garantizar la seguridad del dispositivo de almacenamiento.

##### NTFS Structures
- El formateo de NTFS crea una estructura específica dentro del disco, siendo estas las siguientes:
	- **Partition Boot Sector:** Son los primeros 16 sectores. Es como el "manual de inicio" que le dice a la computadora dónde está la **MFT**.
	- **Master File Table (MFT):** Este es el corazón de NTFS. Es una base de datos que dice: _"El archivo 'Tarea.docx' empieza en el sector X y termina en el Y, le pertenece a Juan y se creó el lunes"_. Si la MFT se daña, el sistema no sabe dónde están los archivos aunque sigan ahí.
	- **System Files:** Archivos invisibles que el usuario no toca, pero que NTFS usa para gestionarse a sí mismo.
	- **File Area:** El espacio libre donde realmente viven tus fotos, documentos y programas.

#### Formatting
- Formatear no es borrar.
- Cuando un archivo se borra o se formatea rápido, Windows solo borra "la entrada" en la **MFT o Master File Table** (el indice).
- Los datos siguen en el **File Area** solo que ahora ese espacio se marca como "disponible".
- Por lo cual, se recomienda usar un **Secure Wipe** (Limpieza segura) que escribe ceros o datos aleatorios sobre todo el disco varias veces para que nada sea recuperable.

Analogía para el **MFT (Master File Table)**: Si pensamos el MFT como el indice de un libro, al arrancar las hojas del índice (formateo rápido), los capítulos (tus datos) siguen ahí, pero no se sabe en qué página empieza cada uno.