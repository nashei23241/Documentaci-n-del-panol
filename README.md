
# Sistema de Gestión de Préstamos de Pañol Escolar 🛠️

Repositorio correspondiente al **Trabajo Integrador de Modelos y Sistemas** (7mo año, Escuela Técnica)[cite: 1]. 

## 📋 Introducción y Alcance
Un sistema puede estar muy bien programado, pero sin una documentación adecuada resulta incompleto[cite: 1]. Este proyecto documenta el funcionamiento, la arquitectura y los flujos operativos del **Sistema de Gestión de Préstamos para el Pañol Escolar**, enfocado en resolver problemas cotidianos como devoluciones tardías, roturas o faltantes de herramientas[cite: 1].

### Funcionalidades principales:
* Control de stock e inventario de herramientas e insumos[cite: 1].
* Registro de entregas y devoluciones a alumnos[cite: 1].
* Historial de estado y mantenimiento de los equipos[cite: 1].
* Reportes de herramientas dañadas e insumos agotados[cite: 1].
* **Tarea crítica documentada:** Registro de un préstamo con validación de disponibilidad y sanciones[cite: 1].

---

## 🏛️ Apartado 1: Marco Conceptual y Clasificación

El sistema diferencia claramente dos tipos de documentación según su audiencia y objetivo[cite: 2]:

| Aspecto | Documentación de Usuario | Documentación Técnica (de Sistema) |
| :--- | :--- | :--- |
| **Audiencia** | Pañoleros, docentes y alumnos[cite: 2]. | Programadores, administradores de BD y soporte IT[cite: 2]. |
| **Lenguaje** | Simple, sin tecnicismos, con pasos y ejemplos[cite: 2]. | Preciso, con términos técnicos, diagramas UML y esquemas SQL[cite: 2]. |
| **Objetivo** | Que la persona resuelva una tarea cotidiana sin ayuda[cite: 2]. | Configurar, desplegar, reparar y ampliar código y base de datos[cite: 2]. |

* **Ejemplo Técnico:** Manual de configuración de cadenas de conexión a la Base de Datos y despliegue del servidor[cite: 2].
* **Ejemplo de Usuario:** Guía rápida en PDF sobre cómo solicitar el préstamo de una herramienta desde la aplicación[cite: 2].

---

## 📝 Apartado 2: Instructivo Paso a Paso (Registro de Préstamo)

1. **Prerrequisitos:**
   * El pañolero debe haber iniciado sesión con su cuenta habilitada[cite: 2].
   * El alumno debe estar registrado y **sin sanciones activas** por mora o roturas[cite: 2].
   * La herramienta debe figurar como *"Disponible"*[cite: 2].

2. **Procedimiento:**
   1. En el panel principal, hacer clic en **"Nuevo Préstamo"**[cite: 2].
   2. Ingresar el **DNI del alumno** solicitante[cite: 2].
   3. Verificar que el sistema muestre el estado del alumno como **"Habilitado"**[cite: 2].
   4. Ingresar el nombre o código de la herramienta y validar que se encuentre en stock[cite: 2].
   5. Seleccionar el plazo de devolución (ej: *"Mismo turno"* o *"Préstamo 24 hs"*)[cite: 2, 5].
   6. Revisar el resumen en pantalla y presionar **"Confirmar Préstamo"**[cite: 2].

3. **Posibles Errores y Soluciones:**
   * **"Préstamo bloqueado: alumno con sanción activa"** $\rightarrow$ Regularizar la deuda o esperar el término de la sanción[cite: 3].
   * **"Herramienta no disponible o en reparación"** $\rightarrow$ Elegir una unidad equivalente libre o consultar fecha de retorno del service[cite: 3].
   * **"Sesión expirada"** $\rightarrow$ Volver a iniciar sesión y repetir el proceso[cite: 3].

---

## 🔀 Apartado 3: Diagrama de Flujo del Proceso

El flujo contempla las validaciones críticas antes de efectuar el registro en la Base de Datos[cite: 3]:

```text
[ Inicio ] 
    │
    ▼
[ Ingresar DNI y Herramienta ] ──( Datos incompletos? )──> [ Error: Inexistente ]
    │ (Sí)
    ▼
[ ¿Alumno sin sanción activa? ] ──( No )──> [ Error: Sanción activa ] ──> [ Fin ]
    │ (Sí)
    ▼
[ ¿Herramienta disponible? ] ──( No )──> [ Error: Prestada/Reparación ] ──> [ Fin ]
    │ (Sí)
    ▼
[ Registrar préstamo en BD ]
    │
    ▼
[ Descontar stock y emitir comprobante ]
    │
    ▼
[ Fin ]
