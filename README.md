# Bloqueo Inteligente de Negocios y Hogares con Edge Computing

## Visión del Proyecto

Este proyecto busca desarrollar un sistema de seguridad inteligente capaz de operar de forma autónoma en negocios pequeños y hogares, sin depender de conexión a Internet.

El problema principal es que muchos sistemas de seguridad actuales dependen completamente de la nube. Cuando la conexión falla, los usuarios quedan vulnerables ante accesos no autorizados o robos.

Los usuarios objetivo son:
- Dueños de negocios pequeños  
- Hogares  
- Administradores de locales  

La solución propone un sistema que funcione en tiempo real, de manera local, garantizando seguridad continua incluso sin conectividad.

---

## Justificación de Diseño (Edge vs Cloud)

Este sistema requiere **Computación en el Borde (Edge Computing)** por las siguientes razones:

- **Baja latencia:** Las decisiones (abrir/cerrar, activar alarma) deben ser inmediatas  
- **Independencia de Internet:** El sistema sigue funcionando sin conexión  
- **Privacidad:** Datos sensibles como rostros o accesos no salen del dispositivo  
- **Optimización de ancho de banda:** No se envían datos constantemente a la nube  

El uso de Edge permite un sistema más **rápido, confiable y seguro** en comparación con soluciones basadas únicamente en la nube.

---

##  Arquitectura del Sistema

### Diagrama de bloques




---

## Componentes del Sistema

### 🔹 Entrada de Datos
- Sensor de movimiento  
- Sensor de sonido  
- Cámara (detección de rostro)  

### 🔹 Procesamiento en el Edge
- Filtrado de datos de sensores  
- Detección de eventos sospechosos  
- Reconocimiento básico de rostros (autorizado / no autorizado)  
- Toma de decisiones en tiempo real  

### 🔹 Salida del Sistema
- Activación de alarma  
- Bloqueo o desbloqueo de cerradura  
- Notificación visual en pantalla local  
- (Opcional) Envío de logs a la nube  

---

## Dispositivos Edge Seleccionados

Se utilizará una **combinación de dispositivos**:

-  **Raspberry Pi 5**
  - Procesamiento principal (visión, lógica)
  - Ejecución de modelos ligeros de IA  

-  **ESP32**
  - Control de sensores y actuadores  
  - Comunicación con Raspberry  

---

##  Restricciones del Sistema

### Hardware
- Memoria limitada (especialmente en ESP32)  
- Capacidad de procesamiento restringida (IA ligera)  
- Almacenamiento reducido  
- Consumo energético controlado  

### Red
- Posible ausencia de conexión a Internet  
- Operación completamente local obligatoria  

---

## Presupuesto Estimado

| Componente             | Costo Aproximado |
|----------------------|------------------|
| Raspberry Pi 5       | $80 - $100 USD   |
| ESP32                | $5 - $10 USD     |
| Cámara               | $10 - $25 USD    |
| Sensores             | $5 - $15 USD     |
| Cerradura electrónica| $20 - $50 USD    |
| **Total estimado**   | **$120 - $200 USD** |

---


## 🎯 Valor Diferencial

Este sistema se diferencia porque:
- No depende de Internet  
- Responde en tiempo real  
- Protege la privacidad del usuario  
- Es accesible para pequeños negocios  
