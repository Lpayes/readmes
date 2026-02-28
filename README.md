1️⃣ Librería de Estructura de Datos
umg.edu.gt.data-structure.queue
📌 Compilar la librería
mvn clean compile
📌 Instalar en el repositorio local (.m2)
mvn clean install

⚠️ Nota crítica:
Este paso es indispensable para generar el archivo .jar dentro del repositorio local (.m2) del usuario.
Sin esta instalación, el proyecto queueHandler no podrá reconocer la dependencia.

2️⃣ Proyecto Aplicación
queueHandler
📌 Compilar y empaquetar
mvn clean package

🔎 Nota técnica:
Este proceso ejecuta la compilación completa y activa el plugin ProGuard, encargado de ofuscar el código.

📌 Ejecutar desde consola
mvn exec:java -Dexec.mainClass="queueHandler.handler.App"
🧠 Explicación del Diseño y Decisiones Técnicas

El diseño del sistema se fundamenta en:

Arquitectura Modular

Principio de Responsabilidad Única (SRP)

El objetivo fue garantizar separación de responsabilidades, mantenibilidad y protección de la lógica crítica.

📦 Estructura de Datos Manual

Se implementó una clase genérica:

QueueLinked<T>
Características clave:

Implementación basada en nodos enlazados

Uso de referencias privadas:

head

tail

Complejidad temporal:

enqueue() → O(1)

dequeue() → O(1)

Esto asegura eficiencia constante en inserciones y extracciones.

🔐 Encapsulamiento

Los nodos internos no se exponen

Toda interacción se realiza mediante métodos públicos genéricos

Se protege la integridad estructural de la cola

🛡️ Ofuscación

Se integró ProGuard dentro del ciclo de vida de Maven para:

Proteger la lógica de prioridad del PlaylistManager

Mantener visibles únicamente los puntos de entrada obligatorios

Dificultar ingeniería inversa

En términos estratégicos: propiedad intelectual blindada.

🔥 Sistema de Prioridad (Parte C)

Para cumplir con el requerimiento de no utilizar estructuras del JDK, se diseñó una solución basada en dos colas internas dentro del PlaylistManager.

🎵 Estructura Interna

highPriority → Canciones con priority = 1

normalPriority → Canciones con priority = 2

⚙️ Lógica de Reproducción

El sistema verifica primero la cola VIP.

Mientras existan elementos en highPriority, se reproducen exclusivamente estos.

Solo cuando esté vacía, comienza la reproducción de normalPriority.

Dentro de cada categoría se respeta el orden FIFO.

Resultado: prioridad garantizada sin romper el orden natural.

⏱️ Simulación de Duración y Complejidad (Parte D)
🎬 Simulación Realista

La reproducción no es instantánea; se implementó un flujo que simula tiempo real:

Thread.sleep(1000);
Funcionalidad:

Detiene la ejecución 1 segundo por ciclo

Muestra progreso segundo a segundo

Ejemplo de log:

1s / 12s
2s / 12s
...

Esto permite validar visualmente el comportamiento del sistema.

🚀 Extensiones de Complejidad Implementadas
📊 Barra de Progreso Visual

Se desarrolló el método:

drawBar()

Ejemplo visual:

[#####-----]

Proporciona retroalimentación gráfica en consola.

📈 Contador Total

Al finalizar la ejecución se muestra:

Total de canciones reproducidas durante la sesión

Log final de resumen operativo

Indicador clave de ejecución exitosa.

📸 Evidencias de Funcionamiento

Ubicadas en la carpeta:

/evidencias
✔️ Librería instalada en .m2

Captura del archivo .jar generado correctamente.

✔️ Compilación del Handler

Evidencia de ejecución de:

mvn package
✔️ Logs de Simulación

Capturas mostrando:

Reproducción segundo a segundo

Barra de progreso activa

✔️ Prioridad Musical

Evidencia de que las canciones VIP se procesan antes que las normales.

👤 Autor

Lester

Carnet: [TU_CARNET]
Universidad: UMG – Ingeniería en Sistemas
