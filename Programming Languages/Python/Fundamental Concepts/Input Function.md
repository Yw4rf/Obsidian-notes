## input() function
La función **input()** permite ingresar datos por el usuario y que esos datos pasen al programa en ejecución. El programa entonces puede manipular los datos haciendo el código interactivo. 

~~~Python
anything = input("Dime lo que sea...")
print("Hmm...", anything, "...¿en serio?")
~~~

## Data Type Convert 
La función **input()** **lee por defecto una cadena (string)**, por lo tanto es necesario cambiar el tipo de dato mediante conversión de tipos. **Es posible cambiar de tipo simplemente incluyendo el input dentro de otra función que indique el tipo de dato específico**:
- E.g: si quiero que lea tipo de dato entero (int), es necesario incluir el input dentro de int(), `int(input("Now i'am an integer"))`

~~~Python 
anything = float(input("Ingresa un número: "))
something = anything ** 2.0
print(anything, "a la potencia de 2 es", something)
~~~

## String Operator
Es posible concatenar cadenas al sumar ambas `string + string`, esto hace que se conviertan en un **operador de concatenación**: 

~~~Python
ftName = input("Escribe el primer nombre: ")
scName = input("Escribe el segundo nombre: ")
srName = input("Escribe tu apellido aqui: ")
print("Graciaaaaas! aqui abajo esta tus nombres y tu apellido juntos")
print("Tu nombre es " + firstName + " " + seconName + " " + srName + ".")
~~~

## Replication 
El signo `*` (asterisco)cuando es aplicado a una cadena y a un número (o a un número y cadena) se convierte en **operador de replicación** `string * number` o `number * string`: 

~~~Python
"James" * 3 # "JamesJamesJames"
3 * "an" # "ananan"
5 * "2" # "22222"
~~~



