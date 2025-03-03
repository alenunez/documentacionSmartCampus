# Arquitectura

## Diagramas
![Diagrama de Arquitectura](Diagrama%20en%20blanco.png)

El diagrama representa la arquitectura del sistema, donde se incluyen los componentes principales y sus interacciones.

## Explicación de los Componentes de la Arquitectura

La arquitectura del sistema se compone de los siguientes elementos:

- **Admin Front (React):** Interfaz de usuario desarrollada en React para la administración del sistema.
- **Admin Service (Spring Boot):** Servicio backend que maneja la lógica de negocio y la comunicación con la base de datos PostgreSQL.
- **Base de Datos (PostgreSQL):** Almacena la información administrativa del sistema.
- **Broker MQTT (EMQX):** Sistema de mensajería basado en MQTT que facilita la comunicación entre los dispositivos y el backend.
- **Base de Datos de Series Temporales (InfluxDB):** Almacena datos de los sensores que se reciben a través de EMQX.
- **Telegraf:** Herramienta utilizada para la recopilación y procesamiento de métricas de los datos provenientes de los sensores.
- **Sensores y Gateway:** Sensores conectados a una Raspberry Pi con software en Python, que envían datos en formato JSON al broker MQTT.
- **Docker:** Contenedorización de los servicios para facilitar la implementación y escalabilidad del sistema.

## Ventajas y Desventajas

### Ventajas
- Modularidad: Los componentes están desacoplados, facilitando la escalabilidad.
- Uso de tecnologías modernas: React, Spring Boot y bases de datos optimizadas para cada propósito.
- Flexibilidad: Uso de contenedores Docker para la fácil implementación y mantenimiento.
- Comunicación eficiente: MQTT permite la transmisión de datos en tiempo real de manera eficiente.

### Desventajas
- Complejidad: La combinación de múltiples tecnologías puede aumentar la curva de aprendizaje.
- Dependencias externas: Requiere la correcta configuración de Docker y bases de datos específicas.
- Seguridad: MQTT debe ser adecuadamente asegurado para evitar vulnerabilidades en la comunicación de sensores.

