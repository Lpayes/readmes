## 🛠️ Manual de Compilación e Instalación

Este documento describe el procedimiento técnico para compilar, instalar y ejecutar correctamente el proyecto en entorno Windows utilizando CMD.

---

## 1. Librería de Estructura de Datos (`umg.edu.gt.data-structure.queue`)

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
Este comando genera el archivo `.jar` dentro del repositorio local

```
C:\Users\MI_USUARIO\.m2
```

Sin este paso, el proyecto `queueHandler` no podrá reconocer la dependencia.

---

## 2. Proyecto Aplicación (`queueHandler`)

Este módulo consume la librería instalada previamente y ejecuta la lógica principal del sistema.

### Compilar y Empaquetar

```cmd
mvn clean package
```

Durante este proceso:

- Se compila todo el proyecto.
- Se genera el archivo `.jar` ejecutable.

---

## Ejecutar desde CMD

```cmd
mvn exec:java -Dexec.mainClass="queueHandler.handler.App"
```

Este comando inicia la aplicación principal desde la consola de Windows.

---

## 🧠 Explicación del Diseño y Decisiones Técnicas

El sistema fue diseñado bajo los siguientes principios:

- Arquitectura modular.
- Principio de Responsabilidad Única (SRP).
- Separación entre estructura de datos y lógica de negocio.

La librería contiene únicamente la implementación de la cola enlazada manual.  
El módulo `queueHandler` contiene la lógica de reproducción y prioridad.

---

## Implementación de la Estructura de Datos

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

## 🔥 Sistema de Prioridad

Para gestionar la prioridad sin utilizar estructuras del JDK, se implementaron **dos colas internas** dentro de `PlaylistManager`:

```java
private QueueLinked<Song> highPriority;
private QueueLinked<Song> normalPriority;
```

### Asignación de Prioridad

- Si `priority == 1` → La canción se encola en `highPriority`.
- Si `priority == 2` → La canción se encola en `normalPriority`.

La decisión se realiza en el método:

```java
public void addSong(Song song) {
    if (song.getPriority() == 1) {
        highPriority.enqueue(song);
    } else {
        normalPriority.enqueue(song);
    }
}
```

### Lógica de Reproducción

1. Se procesa completamente la cola de alta prioridad.
2. Cuando está vacía, se procesa la cola normal.
3. Dentro de cada cola se respeta el orden FIFO.

Esto garantiza prioridad estricta sin alterar el comportamiento natural de la estructura de datos.

---

## ⏱️ Simulación de Duración

La reproducción simula tiempo real utilizando:

```java
Thread.sleep(1000);
```

Esto produce:

- Pausa de 1 segundo por iteración.
- Visualización del progreso segundo a segundo.
- Ejecución secuencial visible en consola.

---

## 👤 Autor
Lester David Payes Méndez, carnet: 0509-24-22750
UMG – Ingeniería en Sistemas
