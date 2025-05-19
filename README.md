# WebApplicationExample

Una API RESTful simple desarrollada con ASP.NET Core 8 y optimizada con Native AOT.

## Descripción

Esta aplicación es un ejemplo de una API RESTful que gestiona una lista de tareas pendientes (todos). La aplicación está construida con ASP.NET Core 8 y utiliza Native AOT (Ahead-of-Time) compilation para mejorar el rendimiento y reducir el consumo de recursos.

## Endpoints

La API expone los siguientes endpoints:

- `GET /todos`: Devuelve la lista completa de tareas pendientes.
- `GET /todos/{id}`: Devuelve una tarea específica por su ID.

## Requisitos

Para ejecutar esta aplicación necesitas:

- Docker

No se requiere tener instalado .NET SDK en la máquina host, ya que Docker se encargará de todo el proceso de compilación y ejecución.

## Ejecución con Docker

### Construir la imagen

Para construir la imagen Docker, ejecuta el siguiente comando desde el directorio raíz del proyecto:

```bash
docker build -t webapplicationexample .
```

Este comando construirá una imagen Docker optimizada para aplicaciones Native AOT.

### Ejecutar el contenedor

Para ejecutar la aplicación en un contenedor Docker, utiliza el siguiente comando:

```bash
docker run -d -p 8080:8080 -p 8081:8081 --name webapplication_container webapplicationexample
```

Esto iniciará un contenedor Docker con la aplicación y mapeará los puertos 8080 y 8081 del contenedor a los mismos puertos en tu máquina local.

### Verificar que la aplicación está funcionando

Para verificar que la aplicación está funcionando correctamente, puedes hacer una petición a uno de los endpoints:

```bash
curl http://localhost:8080/todos
```

Deberías recibir una respuesta JSON con la lista de tareas pendientes.

## Comandos Docker útiles

### Ver los logs del contenedor

```bash
docker logs webapplication_container
```

### Detener el contenedor

```bash
docker stop webapplication_container
```

### Eliminar el contenedor

```bash
docker rm webapplication_container
```

## Arquitectura

Esta aplicación utiliza:

- ASP.NET Core 8 con Minimal API
- Native AOT para compilación anticipada a código nativo
- Contenedorización con Docker optimizada para aplicaciones AOT

## Notas técnicas

- La aplicación utiliza Native AOT, lo que significa que se compila directamente a código nativo específico de la plataforma.
- La imagen Docker resultante es más pequeña y eficiente que las imágenes tradicionales de .NET, ya que no requiere el runtime completo de .NET.
- El tiempo de inicio de la aplicación es significativamente más rápido debido a la compilación AOT.
