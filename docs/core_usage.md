# Uso del Repositorio Core (GitHub)

> [Repositorio en GitHub](https://github.com/UIS-IoT-Smart-Campus/smart_campus_core)

Esta guía te ayudará a configurar y ejecutar el core del proyecto **Smart Campus** utilizando contenedores Docker.

## **Requisitos previos**

Antes de comenzar, asegúrate de tener instalados los siguientes programas:

- **Docker**: Se utiliza para correr los contenedores que componen el proyecto. Puedes instalarlo siguiendo las instrucciones de la siguiente guía: [Instalación Docker](https://www.notion.so/Instalaci-n-Docker-11f6aa8e4194800ab2f4e11fe68f2ccb?pvs=21).
- **Docker Compose**: Es la herramienta que orquestará el despliegue de todos los contenedores.
- **Git**: Para clonar el repositorio. Si no lo tienes instalado, sigue las instrucciones [aquí](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## **Clonar el repositorio**

Primero, clona el repositorio principal del proyecto en tu máquina local:

```sh
git clone https://github.com/UIS-IoT-Smart-Campus/smart_campus_core.git
cd smart_campus_core
```
## **Estructura del Proyecto**

El proyecto está organizado en varios servicios, cada uno con su propio rol dentro de la arquitectura:

- **Base de Datos (MongoDB & PostgreSQL)**: Almacenan datos relacionados con los dispositivos IoT y la administración del sistema.
- **Microservicios**: Servicios REST que gestionan datos IoT y la administración de la infraestructura.
- **MQTT Broker (Mosquitto)**: Se encarga de la comunicación entre los dispositivos y los microservicios.
- **Frontend (React)**: Interfaz gráfica para administrar y visualizar la infraestructura.

## **Despliegue de los servicios**

Con todo configurado, puedes desplegar la infraestructura con Docker Compose. Desde la carpeta raíz del proyecto, ejecuta:
docker-compose up -d

Esto desplegará los siguientes contenedores:

1. **PostgreSQL**: Base de datos relacional para la administración del sistema.
2. **MongoDB**: Base de datos documental para almacenar mensajes de los dispositivos.
3. **Mosquitto**: Broker MQTT para gestionar la comunicación entre dispositivos.
4. **Admin Microservice**: Servicio que gestiona la infraestructura IoT.
5. **Data Microservice**: Servicio encargado de recibir y almacenar los datos de los dispositivos IoT.
6. **GoGateway**: Un Gateway liviano para la comunicación con los microservicios.
7. **Frontend**: Interfaz de administración basada en React.

## **Verificación del despliegue**

Para comprobar que los servicios están corriendo correctamente, puedes ejecutar:

```bash
docker ps
```

Esto te mostrará una lista de los contenedores en ejecución.

- El **Frontend** estará disponible en `http://localhost:4000`
- El **Gateway** estará disponible en `http://localhost:8080`
- Los servicios REST expuestos por los microservicios estarán disponibles en los puertos configurados.

## **Interacción con el sistema**

Para enviar datos desde un dispositivo IoT simulado, puedes usar un cliente MQTT y publicar mensajes en el tópico `device_messages`. El formato del mensaje debe ser un JSON con los siguientes atributos:

```json
{
  "userUUID": "123e4567-e89b-12d3-a456-426614174000",
  "deviceId": "DEVICE123",
  "topic": "temperatura",
  "timeStamp": "14-03-2023 12:42:57",
  "values": {
    "temperatura": 25
  }
}
```

Asegúrate de respetar los nombres de los atributos para que los microservicios puedan procesar los datos correctamente.

## **Consideraciones adicionales**

- **Logs**: Si necesitas revisar los logs de algún servicio para solucionar errores, puedes utilizar el comando:

```bash
docker-compose logs <nombre-del-servicio>
```

- **Apagar los servicios**: Para detener todos los contenedores:

```bash
docker-compose down
```

> **Expansión futura**: Si planeas añadir nuevos microservicios o mejorar la arquitectura, asegúrate de seguir las convenciones existentes en este repositorio para mantener la coherencia en el proyecto.
>
