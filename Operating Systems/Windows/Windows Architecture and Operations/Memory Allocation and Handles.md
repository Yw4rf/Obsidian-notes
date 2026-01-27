##### Physical Memory 
- La RAM es un recurso físico y limitado. 
- El CPU no trabaja directamente con direcciones fisicas en sistemas modernos; hacerlo asi haría imposible el aislamiento entre procesos y la multitarea segura.
##### Virtual Memory 
- Windows (y la mayoria de sistemas operativos hoy en dia) implementa **memoria virtual**. 
- Esta utiliza **abstracción** para crear una capa intermedia entre aplicaciones y la memoria fisica (RAM): 
	- Cada proceso vea su propio espacio de direcciones virtuales.
	- Esas direcciones no corresponden directamente a posiciones fisicas en RAM.
	- La traducción se realiza mediante **tablas de páginas (page tables)** gestionadas por el kernel y el **MMU (Memory Management Unit)** del CPU.
	- Dos procesos pueden usar la misma dirección virtual `0x00400000` y sin embargo mapear a páginas físicas completamente distintas.
##### Virtual Address Space (VAS)
- Es el conjunto de direcciones virtuales que un proceso puede usar. Cada proceso en modo usuario tiene su propio espacio de direcciones virtuales privado, lo que garantiza aislamiento entre procesos y seguridad, ya que un proceso no puede acceder ni modificar la memoria de otro proceso.
- Tamaños según arquitectura: 
	- **Windows 32-bit:** Espacio virtual total: 4GB (2^32). División típica: 2GB UserMode, 2GB KernelMode. Opcional: 3GB UserMode, 1GB KernelMode.
	- Limitación: Incluso con mucha ram física, un proceso de 32bits no puede direccionar más que su VAS.
	- **Windows 64-bit**: Espacio teórico: 16Exabytes. Windows Implementa: 8TB por proceso en UserMode. 128TB para Kernel Mode.
	- En la práctica esto elimina casi por completo los problemas de agotamiento de espacio virtual.
##### Private Address Space 
- Cada proceso en UserMode tiene: 
	- Su propio **VAS (Virtual Address Space)**.
	- Sus propias: DLLs mapedas, Heap, Stack, Código, Regiones reservadas/comprometidas.
- Por eso **un proceso no puede leer la memoria de otro**, salvo que **sea el kernel** o use mecanismos controlados. Esto garantiza aislamiento, seguridad, estabilidad.
##### Handles
- Un proceso en el UserMode no puede acceder directamente a **objetos del kernel**, **memoria del kernel**, **recursos globales** como por ejemplo: procesos, threads, archivos, tokens, claves de registro, secciones de memoria.
- La solución: **Handles**. Un Handle es un **identificador opaco** (no un puntero real), representa una referencia a un **objeto del kernel**. Es válido **solo en el contexto del proceso que lo posee**. 
- Un handle **no apunta directamente al objeto**, es un índice dentro de la **tabla de handles del proceso**, mantenida por el kernel.

























![[Pasted image 20260122191035.jpg]]