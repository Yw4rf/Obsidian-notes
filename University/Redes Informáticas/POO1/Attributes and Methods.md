## What are Attributes?
Un atributo es una característica propia de un objeto. Todos los objetos de una misma clase tienen los mismos atributos, pero cada uno puede tener valores distintos. 
- E.g: Una clase `Persona`. Todos tienen el atributo `nombre`, pero cada persona tiene un nombre diferente. 

Los atributos también pueden hacer **referencia a otros objetos** (como `canasta: Canasta`) lo que representa la **asociación** entre clases.

## Instance/Class Attributes
- Los **Atributos de instancia** son los que pertenecen a **cada objeto individual** y se definen en el `__init__` 
- Los **Atributos de clase** pertenecen a **la clase en si**, y todos los objetos los comparten. 

~~~Python
class Naranja: 
	especie = "Citrus" # Class Attribute (compartido por todas)
	
	def __init__(self, peso): 
		self.peso = peso # Instance Attribute (único por objeto)
		
naranja1 = Naranja(0.3) # Instancia de la clase al nuevo objeto naranja1
naranja2 = Naranja(0.9) # Instancia de la clase al nuevo objeto naranja2

print(naraja1.especie) # "Citrus"
print(naranja2.especie) # "Citrus" Osea, el mismo valor lo comparten todos los objetos (naranja1, naranja2) debido a que "especie" es un atributo de clase.  

print(naranja1.peso) # 0.3 
print(naranja2.peso) # 0.9 Osea, cada uno tiene su propio valor debido a que "peso" es un atributo de instancia. 
~~~


## What are Methods? 
Los métodos son **acciones o comportamientos** que puede ejecutar o realizar un objeto. 
- Es como una función pero con una diferencia clave, **tiene acceso automático a todos los atributos del objeto**.

~~~Python
class Canasta:
    def __init__(self):
        self.naranjas = []   # Instance Attribute → lista vacía donde se guardarán las naranjas

class Naranja:
    def __init__(self, peso, huerto):
        self.peso = peso          # Instance Attribute (único por objeto)
        self.huerto = huerto      # Instance Attribute (único por objeto)
        self.canasta = None       # Instance Attribute → empieza vacío, se asigna al cosechar

    def cosechar(self, canasta):            # Método que recibe un objeto Canasta como parámetro
        self.canasta = canasta              # La naranja guarda en qué canasta está
        canasta.naranjas.append(self)       # La canasta agrega esta naranja (self) a su lista


canasta1 = Canasta()                # Instancia de la clase Canasta
naranja1 = Naranja(0.3, "Huerto 1") # Instancia de la clase Naranja
naranja2 = Naranja(0.9, "Huerto 2") # Instancia de la clase Naranja

print(canasta1.naranjas) # [] → la canasta está vacía todavía

naranja1.cosechar(canasta1) # naranja1 se agrega a canasta1, ambos objetos se actualizan
naranja2.cosechar(canasta1) # naranja2 se agrega a canasta1, ambos objetos se actualizan

print(canasta1.naranjas)  # [naranja1, naranja2] → la canasta ahora tiene las dos naranjas
print(naranja1.canasta)   # canasta1 → la naranja sabe en qué canasta está
~~~