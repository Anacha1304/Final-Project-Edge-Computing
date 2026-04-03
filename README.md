# Bloqueo Inteligente de Negocios y Hogares con Edge Computing

## Visión del Proyecto

El proyecto **Bloqueo inteligente de negocios y hogares con Computación en el Borde** busca resolver una problemática común en sistemas de seguridad actuales: la vulnerabilidad que se genera cuando estos dependen de una conexión a Internet para su funcionamiento. En muchos hogares y pequeños negocios, una caída de red puede impedir la detección de eventos, la validación de accesos o la activación de mecanismos de protección, dejando los espacios expuestos ante posibles robos o accesos no autorizados.

Este proyecto propone el desarrollo de un sistema de seguridad inteligente capaz de operar de forma autónoma a nivel local, garantizando la continuidad del servicio incluso en escenarios sin conectividad. La solución se enfoca en permitir la detección de situaciones sospechosas y la ejecución de acciones inmediatas, como el bloqueo de accesos o la activación de alarmas, sin interrupciones.

Los usuarios objetivo son principalmente dueños de pequeños negocios, propietarios de viviendas, familias y administradores de locales que requieren un sistema de seguridad confiable, accesible y que no dependa de infraestructura compleja. En este contexto, el proyecto busca ofrecer una alternativa que incremente la protección de los espacios, reduzca la dependencia tecnológica externa y mejore la capacidad de respuesta ante situaciones de riesgo.

---

## Justificación de Diseño (Edge vs Cloud)

El diseño de este sistema se fundamenta en el uso de **Computación en el Borde (Edge Computing)** debido a las exigencias de tiempo de respuesta, disponibilidad continua y manejo de datos sensibles propias de los sistemas de seguridad física.

En un enfoque basado únicamente en la nube, los datos capturados por sensores (movimiento, imagen) tendrían que ser enviados a servidores remotos para su procesamiento, lo que introduce latencias variables dependiendo de la calidad de la conexión. En un sistema de seguridad, incluso retrasos de pocos segundos pueden ser críticos, ya que decisiones como bloquear una cerradura o activar una alarma deben ejecutarse de manera inmediata. Al procesar estos eventos directamente en el dispositivo Edge, se elimina la dependencia del tiempo de ida y vuelta de la red (round-trip time), garantizando respuestas en tiempo real.

Adicionalmente, el uso de Edge Computing permite una **preservación significativa del ancho de banda**, ya que no es necesario transmitir continuamente flujos de datos como video o audio hacia la nube. En su lugar, el procesamiento local filtra y analiza la información, enviando únicamente eventos relevantes o registros cuando sea necesario, lo que reduce la carga sobre la red y mejora la eficiencia del sistema.

Otro aspecto clave es la **resiliencia operativa**. En escenarios donde la conexión a Internet es inestable o inexistente, un sistema basado en la nube pierde funcionalidad o queda completamente inoperante. En contraste, un sistema implementado en el borde mantiene su capacidad de detección, decisión y acción de manera autónoma, asegurando la continuidad del servicio en todo momento.

Finalmente, la **seguridad y privacidad de los datos** representan un factor determinante. Este sistema maneja información sensible, como patrones de acceso, posibles imágenes de usuarios o eventos internos del hogar o negocio. Al procesar estos datos localmente, se minimiza la exposición a riesgos asociados con la transmisión y almacenamiento en servidores externos, reduciendo la superficie de ataque y cumpliendo con principios de protección de datos.

En conjunto, la Computación en el Borde no solo mejora el rendimiento del sistema, sino que también garantiza mayor confiabilidad, eficiencia y protección de la información, características esenciales para una solución de seguridad en entornos reales.

---

## Arquitectura y Restricciones

### Arquitectura del sistema

El sistema se basa en una arquitectura de computación en el borde en la que se distribuyen las funciones entre un microcontrolador ESP32 y una Raspberry Pi 5. Esta distribución permite asignar las tareas según la capacidad de cada dispositivo, optimizando el rendimiento y garantizando la operación autónoma del sistema.

El ESP32 se encarga de la captura de datos provenientes de sensores como movimiento o mecanismos de acceso, además de ejecutar acciones inmediatas sobre actuadores como cerraduras o alarmas. Por otro lado, la Raspberry Pi 5 realiza el procesamiento local de mayor complejidad, incluyendo la detección de eventos sospechosos, la validación de usuarios autorizados y la toma de decisiones del sistema.

De manera opcional, el sistema puede conectarse a la nube para el almacenamiento de registros o monitoreo remoto, sin que esta conexión sea necesaria para su funcionamiento principal.

---

### Diagrama de bloques

<img width="1759" height="761" alt="image" src="https://github.com/user-attachments/assets/1e6b0373-4186-4fb3-b94d-f6fc23a0e124" />



#### Flujo de funcionamiento

1. **Captura de datos**
   - Sensores de movimiento detectan presencia o cambios en el entorno  
   - Cámara permite capturar imágenes o secuencias para validación de acceso  
   - Dispositivos de entrada (teclado, RFID u otros) permiten autenticación  

2. **Procesamiento principal en Raspberry Pi 5**
   - Recepción directa de datos provenientes de sensores o sistemas conectados  
   - Análisis de eventos en tiempo real  
   - Validación de usuarios (por ejemplo, rostro autorizado o patrón válido)  
   - Clasificación de eventos como normales o sospechosos  
   - Ejecución de la lógica de decisión del sistema  

3. **Ejecución de acciones a través del ESP32**
   - Recepción de órdenes desde la Raspberry Pi 5  
   - Control de cerraduras electrónicas  
   - Activación de alarmas  
   - Encendido de luces o señales de alerta  

4. **Salida de información**
   - Visualización de alertas en pantalla local  
   - Notificaciones del estado del sistema  

5. **Interacción con la nube (opcional)**
   - Registro de eventos para auditoría  
   - Monitoreo remoto  
   - Respaldo de información  

Esta organización permite que el sistema funcione de forma completamente autónoma en el borde, manteniendo la nube como un componente complementario y no crítico.
---

### Presupuesto estimado

| Componente              | Descripción                          | Costo Aproximado (USD) |
|------------------------|--------------------------------------|------------------------|
| Raspberry Pi 5         | Procesamiento principal              | 45 - 80               |
| ESP32                  | Control de sensores y actuadores     | 8 - 15                |
| Cámara                 | Captura de imagen/video              | 15 - 30               |
| Sensor de movimiento   | Detección de presencia               | 3 - 8                 |
| Cerradura electrónica  | Control de acceso físico             | 15 - 40               |
| Alarma / buzzer        | Señalización de eventos              | 2 - 6                 |
| Fuente y cableado      | Alimentación y conexión              | 10 - 20               |
| **Total estimado**     |                                      | **101 - 207**         |

El presupuesto fue definido considerando componentes accesibles en el mercado, buscando un balance entre costo y funcionalidad para entornos reales de pequeña escala.

---

### Restricciones del hardware

#### ESP32

El ESP32 es un microcontrolador optimizado para aplicaciones de bajo consumo y procesamiento ligero, lo que impone varias limitaciones:

### Restricciones del hardware

#### ESP32

- **Memoria limitada:** restringe el manejo de múltiples sensores y procesos simultáneos en el sistema  
- **Capacidad de procesamiento baja:** no permite ejecutar tareas como reconocimiento facial o análisis de video, por lo que estas deben delegarse a la Raspberry Pi 5  
- **Almacenamiento reducido:** solo permite guardar firmware y datos temporales, no registros históricos o imágenes del sistema  
- **Limitación en pines de conexión:** restringe la cantidad de sensores (movimiento, cerraduras) que se pueden conectar directamente  
- **Dependencia de comunicación inalámbrica:** puede presentar fallos o interferencias en la transmisión de datos hacia la Raspberry Pi  
- **Limitación en manejo de periféricos complejos:** no es adecuado para manejar directamente cámaras o dispositivos de alto consumo de datos  

#### Raspberry Pi 5

- **Consumo energético elevado:** requiere una fuente de alimentación estable para operar continuamente en el sistema de seguridad  
- **Generación de calor:** bajo cargas de procesamiento (por ejemplo, validación de accesos) puede requerir disipación térmica  
- **Dependencia de almacenamiento externo:** el rendimiento depende del uso de microSD o SSD, lo que puede afectar la velocidad del sistema  
- **Capacidad limitada frente a la nube:** no puede ejecutar modelos de inteligencia artificial complejos, por lo que se deben usar soluciones optimizadas  
- **Rendimiento variable bajo carga continua:** el procesamiento constante de eventos puede afectar la estabilidad del sistema  
- **Dependencia del sistema operativo:** introduce complejidad en configuración, mantenimiento y posibles fallos  
- **Riesgo de corrupción de datos:** si no se gestiona correctamente el apagado, pueden perderse registros del sistema  

#### Integración del sistema

- **Latencia en la comunicación entre ESP32 y Raspberry Pi:** puede afectar la sincronización de eventos en tiempo real  
- **Dependencia de protocolos de comunicación:** errores en la comunicación pueden impactar la detección y respuesta del sistema  
- **Complejidad de integración:** al combinar múltiples dispositivos, aumenta la probabilidad de fallos y la dificultad de mantenimiento  

---

### Restricciones del sistema

El sistema debe operar bajo condiciones de conectividad limitada o inexistente, lo que implica que todas las funciones críticas, como la detección de eventos y la toma de decisiones, deben ejecutarse localmente en el dispositivo. Además, requiere tiempos de respuesta inmediatos para garantizar la seguridad física del entorno, lo que limita el uso de procesos complejos o dependientes de servicios externos. También se deben manejar datos sensibles, como accesos o posibles registros visuales, que no pueden exponerse a riesgos de transmisión, lo que obliga a mantener el procesamiento y almacenamiento de información de forma local. Finalmente, el sistema debe ser eficiente en el consumo de recursos y energía, ya que está diseñado para operar de manera continua en entornos reales con infraestructura limitada.

---

### Decisiones de diseño

A partir de las restricciones anteriores, se definieron las siguientes decisiones arquitectónicas:

- Separar el sistema en dos niveles (ESP32 y Raspberry Pi) para distribuir la carga de trabajo  
- Mantener el procesamiento crítico en el borde para garantizar respuesta inmediata  
- Evitar el envío constante de datos a la nube para reducir consumo de red  
- Implementar lógica de decisión local para asegurar autonomía del sistema  
- Utilizar la nube únicamente como componente de apoyo para monitoreo y almacenamiento  

En conjunto, estas decisiones permiten construir un sistema eficiente, autónomo y alineado con las limitaciones reales del hardware embebido, cumpliendo con los principios fundamentales de la computación en el borde.


## Definición del MVP

El producto mínimo viable (MVP) está compuesto por las funcionalidades esenciales que permiten el funcionamiento básico del sistema de seguridad, incluyendo la detección de movimiento, la validación de accesos y la activación de mecanismos de respuesta como cerraduras y alarmas.

Las funcionalidades adicionales, como monitoreo remoto o almacenamiento en la nube, se consideran mejoras opcionales (nice-to-have) y no son necesarias para el funcionamiento inicial del sistema.

## Cronograma del Proyecto

El siguiente diagrama presenta el cronograma tentativo del proyecto, organizado en Sprints de una semana agrupados en Releases de dos semanas. Cada Release representa un avance funcional del sistema, iniciando con la validación de la viabilidad técnica (Spike) y finalizando con la entrega del sistema completo.

<img width="1045" height="1115" alt="image" src="https://github.com/user-attachments/assets/ea8d912f-07a8-4746-ba9e-40dcba4ec931" />


