# 1️⃣ Windows Internals (7th Edition – Part 1)

👉 **Este libro es para entender “qué hay debajo”, no para memorizar**

## 📌 Capítulos que SÍ debés leer

No todo el libro. Solo esto:

### 🔹 **Chapter 1 – Concepts and Tools**

**LEER COMPLETO (obligatorio)**

Cubre directamente:

- User Mode vs Kernel Mode ✅
    
- Qué es un proceso ✅
    
- Qué es un thread ✅
    
- Qué es un servicio (conceptual) ✅
    
- Qué es el Registry (visión interna) ✅
    
- Objetos, handles, seguridad básica ✅
    

Este capítulo **alimenta todo lo demás**. Sin él, lo demás pierde sentido.

Windows System Internals 7e Par…

---

### 🔹 **Chapter 2 – System Architecture**

**Leer selectivamente**

Enfocate en:

- Architecture overview
    
- User mode vs Kernel mode (refuerzo)
    
- Executive / Kernel / HAL
    
- System processes
    

📌 Objetivo:  
Entender **qué componentes existen**, no cómo programarlos.

---

### 🔹 **Chapter 3 – Processes and Jobs**

**Leer hasta “Process Internals”**

Con esto cubrís:

- Qué es un proceso vs thread (a nivel real) ✅
    
- Relación proceso–servicios
    
- Cómo Windows crea procesos
    
- Qué ves reflejado luego en Task Manager
    

❌ No necesitás:

- Pico processes
    
- Jobs avanzados
    
- Containers
    

---

### 🔹 **Chapter 4 – Threads**

**Lectura ligera**

Solo para:

- Proceso vs thread (definitivo)
    
- Scheduling básico
    
- Estados de threads
    

📌 Esto te ayuda a:

- Entender cuelgues
    
- Entender consumo de CPU
    
- Interpretar Task Manager / Resource Monitor
    

---

### ⛔ Capítulos que NO necesitás ahora

- Chapter 5 (Memory) → demasiado bajo nivel
    
- Chapter 6 (I/O system)
    
- Chapter 7 (Security) → esto vuelve después, con AD
    

---

## 🎯 Resumen Windows Internals

Con estos capítulos cubrís **el 100 % de esta parte de tu checklist**:

- User vs Kernel Mode ✅
    
- Proceso vs thread ✅
    
- Servicios (qué son realmente) ✅
    
- Flujo mental del arranque (a alto nivel) ✅
    

---

# 2️⃣ Windows 10 Inside Out (o equivalente de administración)

Este es el libro **operativo**, el que te forma como IT Support.

---

## 📌 Capítulos clave que debés leer

### 🔹 **Sistema de archivos**

Leer capítulos sobre:

- NTFS
    
- Permisos
    
- Seguridad avanzada
    

Cubre:

- NTFS vs FAT ✅
    
- Allow / Deny ✅
    
- Herencia ✅
    
- Permisos efectivos ✅
    
- Ownership y problemas reales de soporte ✅
    

---

### 🔹 **Registry**

Leer capítulos de:

- Windows Registry
    
- Configuración del sistema
    

Cubre:

- HKLM vs HKCU ✅
    
- Para qué lo usa el sistema ✅
    
- Riesgos desde seguridad ✅
    
- Casos reales de roturas por registry ✅
    

---

### 🔹 **Herramientas administrativas**

Leer secciones de:

- Task Manager
    
- Services
    
- Event Viewer
    
- MMC
    

Cubre:

- Task Manager (qué mirar y por qué) ✅
    
- Services.msc (dependencias, estados) ✅
    
- Event Viewer (estructura de logs) ✅
    
- MMC (concepto, no memorizar) ✅
    

---

### 🔹 **Windows Defender**

Solo:

- Visión general
    
- Qué protege
    
- Dónde loguea
    

📌 No es EDR avanzado, solo **entender qué es y qué no es**.

---

## 🎯 Resumen Inside Out

Este libro te cubre:

- Sistema de archivos completo
    
- Registry completo
    
- Herramientas de soporte
    
- Defender a nivel soporte
    

Es **perfecto para IT Support**.

---

# 3️⃣ Tu checklist: ¿está bien? ¿agregar algo?

Tu checklist es **correcta y bien acotada**.  
Solo agregaría **3 ítems muy pequeños**, nada grande.

---

## ✅ Agregaría SOLO esto

### 🔹 **Windows Boot (un poco más explícito)**

Agregá:

- Boot Manager
    
- Winload
    
- Qué pasa si falla el arranque
    

No para reparar, sino para **diagnóstico básico**.

---

### 🔹 **Event Logs – estructura**

Ya tenés eventos, pero agregá:

- Qué genera un evento
    
- Diferencia entre error, warning, info
    

Esto te ayuda muchísimo en SOC después.

---

### 🔹 **Sysinternals (conceptual)**

No usarlos aún, solo:

- Process Explorer (qué mejora vs Task Manager)
    
- Autoruns (qué te muestra)