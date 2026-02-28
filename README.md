### 🛠️ Manual de Compilación e Instalación

Este documento describe el procedimiento técnico para compilar, instalar y ejecutar correctamente el proyecto en entorno Windows utilizando CMD.

---

### 1. Librería de Estructura de Datos (`umg.edu.gt.data-structure.queue`)

Esta librería contiene la implementación personalizada de la estructura de datos tipo cola.

### Compilar la librería

```cmd
mvn clean compile
```

### Instalar en el repositorio local (.m2)

```cmd
mvn clean install
```

**Nota Importante:**  
Este comando genera el archivo `.jar` dentro del repositorio local del usuario (`C:\Users\TU_USUARIO\.m2`).  
Sin este paso, el proyecto `queueHandler` no podrá reconocer la dependencia.

---

### 2. Proyecto Aplicación (`queueHandler`)

Este módulo consume la librería instalada previamente y ejecuta la lógica principal del sistema.

### Compilar y Empaquetar

```cmd
mvn clean package
```

Durante este proceso:

- Se compila todo el proyecto.
- Se ejecuta el plugin **ProGuard**.
- Se genera el archivo empaquetado y ofuscado.

---

### Ejecutar desde CMD

```cmd
mvn exec:java -Dexec.mainClass="queueHandler.handler.App"
```

Este comando inicia la aplicación principal desde la consola de Windows.

---

### 🧠 Explicación del Diseño y Decisiones Técnicas

El sistema fue diseñado bajo los siguientes principios:

- Arquitectura Modular  
- Principio de Responsabilidad Única (SRP)  
- Separación entre estructura de datos y lógica de negocio  

El objetivo es garantizar mantenibilidad, claridad estructural y protección de la lógica crítica.

---

### Implementación de la Estructura de Datos

Se desarrolló una implementación manual:

```java
QueueLinked<T>
```

Características técnicas:

- Basada en nodos enlazados.
- Referencias privadas `head` y `tail`.
- Inserción en O(1).
- Extracción en O(1).
- Encapsulamiento completo de nodos internos.

No se utilizaron estructuras del JDK para cumplir con el requerimiento académico.

---

### Encapsulamiento

- Los nodos internos no son accesibles desde el exterior.
- Toda interacción se realiza mediante métodos públicos controlados.
- Se garantiza integridad estructural.

---

### Ofuscación con ProGuard

Se integró ProGuard dentro del ciclo de vida de Maven para:

- Proteger la lógica del `PlaylistManager`.
- Evitar ingeniería inversa.
- Mantener visibles únicamente los puntos de entrada necesarios.

---

### 🔥 Sistema de Prioridad (Parte C)

Para gestionar la prioridad sin estructuras del JDK, se implementaron dos colas internas:

### Cola VIP (`highPriority`)

- Almacena canciones con `priority = 1`.

### Cola Normal (`normalPriority`)

- Almacena canciones con `priority = 2`.

---

### Lógica de Reproducción

1. Se verifica primero la cola VIP.
2. Mientras tenga elementos, se reproducen en orden FIFO.
3. Solo cuando esté vacía se procesa la cola normal.
4. Se respeta el orden de llegada dentro de cada categoría.

Esto garantiza prioridad estricta sin alterar la lógica FIFO.

---

### ⏱️ Simulación de Duración (Parte D)

La reproducción simula tiempo real utilizando:

```java
Thread.sleep(1000);
```

Esto produce:

- Pausa de 1 segundo por iteración.
- Visualización del progreso segundo a segundo.
- Validación clara del flujo de ejecución.

Ejemplo de salida:

```
Reproduciendo: Canción X
1s / 12s
2s / 12s
...
```

---

### Extensiones Implementadas

### Barra de Progreso Visual

Método utilizado:

```java
drawBar()
```

Representación en consola:

```
[#####-----]
```

---

### Contador Total de Canciones

Al finalizar la ejecución se muestra:

- Total de canciones reproducidas.
- Resumen general de la sesión.

---

### 📸 Evidencias de Funcionamiento

Ubicación:  

```
/evidencias
```

Incluye:

- Captura del `.jar` en `.m2`.
- Evidencia de `mvn clean package`.
- Logs de simulación.
- Validación de prioridad VIP sobre normal.

---

### 👤 Autor

**Lester**  
**Carnet:** [TU_CARNET]  
**Universidad:** UMG – Ingeniería en Sistemas
