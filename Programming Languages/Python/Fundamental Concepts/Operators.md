
| Categoría             | Operador           | Nombre oficial                           |
| --------------------- | ------------------ | ---------------------------------------- |
| **Aritméticos**       | `+`                | Suma                                     |
|                       | `-`                | Resta                                    |
|                       | `*`                | Multiplicación                           |
|                       | `/`                | División                                 |
|                       | `//`               | División entera (floor division)         |
|                       | `%`                | Módulo (resto)                           |
|                       | `**`               | Exponenciación                           |
| **Asignación**        | `=`                | Asignación simple                        |
|                       | `+=`               | Asignación con suma                      |
|                       | `-=`               | Asignación con resta                     |
|                       | `*=`               | Asignación con multiplicación            |
|                       | `/=`               | Asignación con división                  |
|                       | `//=`              | Asignación con división entera           |
|                       | `%=`               | Asignación con módulo                    |
|                       | `**=`              | Asignación con exponenciación            |
|                       | `&=`               | Asignación AND bit a bit                 |
|                       | `\|=`              | Asignación OR bit a bit                  |
|                       | `^=`               | Asignación XOR bit a bit                 |
|                       | `>>=`              | Asignación desplazamiento a la derecha   |
|                       | `<<=`              | Asignación desplazamiento a la izquierda |
| **Comparación**       | `==`               | Igualdad                                 |
|                       | `!=`               | Desigualdad                              |
|                       | `<`                | Menor que                                |
|                       | `>`                | Mayor que                                |
|                       | `<=`               | Menor o igual que                        |
|                       | `>=`               | Mayor o igual que                        |
| **Identidad**         | `is`               | Identidad (mismo objeto)                 |
|                       | `is not`           | No identidad                             |
| **Membresía**         | `in`               | Membresía                                |
|                       | `not in`           | No membresía                             |
| **Lógicos**           | `and`              | Conjunción lógica                        |
|                       | `or`               | Disyunción lógica                        |
|                       | `not`              | Negación lógica                          |
| **Bit a bit**         | `&`                | AND bit a bit                            |
|                       | `\|`               | OR bit a bit                             |
|                       | `^`                | XOR bit a bit                            |
|                       | `~`                | NOT bit a bit (complemento)              |
|                       | `<<`               | Desplazamiento a la izquierda            |
|                       | `>>`               | Desplazamiento a la derecha              |
| **Operador ternario** | `x if cond else y` | Expresión condicional                    |
| **Suscripción**       | `[]`               | Acceso por índice                        |
| **Rebanado**          | `[:]`              | Slice                                    |
| **Llamada**           | `()`               | Invocación de función                    |
| **Acceso a atributo** | `.`                | Acceso a atributo                        |
| **Desempaquetado**    | `*` (en llamadas)  | Desempaquetado posicional                |
|                       | `**` (en llamadas) | Desempaquetado de palabras clave         |
| **Walrus**            | `:=`               | Asignación de expresión                  |