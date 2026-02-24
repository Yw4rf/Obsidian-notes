#### Variables 
- Una variable es **un nombre que hace referencia a un objeto en la memoria**. E.g:

~~~Python
x = 10  # 'x' apunt a un objeto entero (integer) con el valor 10
b = "Site B" # 'b' apunta a un objeto cadena (string) "Site B"
~~~

- La misma variable puede apuntar a objetos de distinto tipo durante la ejecución. No hay declaración de tipado previa. Python es un lenguaje de tipado dinámico. 

#### Variable Scope
- Las variables tienen scope (alcance): 
	- **Local**: variables dentro de una función.
	- **Global/module**: variables del módulo. 
	- **Builtins**: nombres como `len`, `print`. 