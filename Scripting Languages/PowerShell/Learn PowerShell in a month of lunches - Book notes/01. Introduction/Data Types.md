#### Data Types
- PowerShell acepta cierto tipos de datos:
	- **String**: cadena (o string) es una serie de letras y/o números, pueden incluir espacios pero deben estar contenidas por comillas dobles o simples. E.g: `"This is a string 123123"`
	- **Int, Int32 or Int64**: Números enteros (integers), sin decimales. E.g: `123` 
		- **Int** es alias de **Int32**, por lo tanto son iguales.
	- **DateTime**: una cadena (o string) puede ser interpretada como una fecha. E.g: `14-09-2004` 
	- **Decimals**: PowerShell acepta dos tipos de decimales: 
		- **Double**: Es un tipo de punto flotante que ofrece precisión, entre 15-16 dígitos significativos. Tamaño de 64 bits, ideal para cálculos precisos.  
		- **Float**: Representa números decimales también, pero con menos precisión, aproximadamente 7 dígitos significativos. Tamaño de 32 bits, ideal para cálculos menos precisos.

#### Examples
- Para declarar un **String**:
~~~PowerShell
$MyString = "I'm a string"
~~~

- Para declarar un **Int**, **Int32** o **Int64**:
~~~PowerShell
$MyInt = 17 #Int32 == Int
$MyIntLong = [long] 17171717171717 #Int64
~~~

- Para declarar un número como **Double**:
~~~PowerShell
$DoubleNumber = [double] 3.14159
~~~

- Para declarar un número como **Float**
~~~PowerShell
$FloatNumber = [float] 3.14159 
~~~