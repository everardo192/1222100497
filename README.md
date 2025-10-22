# 🐳 Guía Completa de Comandos Docker

## 📋 Información del Documento

**Autor:** Torres Tovar Everardo Guadalupe  
**Grupo:** GIDS5102-E  
**Materia:** Gestión del Proceso de Desarrollo de Software  

---

## 📑 Índice

1. [Comandos Básicos de Docker Engine](#comandos-básicos-de-docker-engine)
2. [Comandos de Redes en Docker](#comandos-de-redes-en-docker)
3. [Comandos de Volúmenes en Docker](#comandos-de-volúmenes-en-docker)
4. [Comandos de Docker Compose](#comandos-de-docker-compose)
5. [Comandos de Docker Swarm](#comandos-de-docker-swarm)
6. [Tips de Uso Práctico](#tips-de-uso-práctico)

---

## Comandos Básicos de Docker Engine

### `docker run`

**Descripción:** Crea y ejecuta un nuevo contenedor a partir de una imagen.

**Opciones disponibles:**
- `-d` - Ejecutar en segundo plano (detached mode)
- `-p` - Mapear puertos (host:container)
- `--name` - Asignar nombre al contenedor
- `-v` - Montar volúmenes
- `-e` - Establecer variables de entorno
- `--rm` - Eliminar contenedor automáticamente al salir
- `--network` - Conectar a una red específica

**Ejemplo:**
```bash
docker run -d -p 8080:80 --name mi-contenedor nginx
```

---

### `docker ps`

**Descripción:** Lista contenedores en ejecución.

**Opciones disponibles:**
- `-a` - Mostrar todos los contenedores (activos e inactivos)
- `-q` - Mostrar solo IDs de contenedores
- `--filter` - Filtrar contenedores por criterios específicos
- `--format` - Formatear la salida usando una plantilla Go

**Ejemplo:**
```bash
docker ps -a
```

---

### `docker images`

**Descripción:** Lista las imágenes disponibles localmente.

**Opciones disponibles:**
- `-a` - Mostrar todas las imágenes
- `-q` - Mostrar solo IDs de imágenes
- `--digests` - Mostrar digests de imágenes
- `--no-trunc` - No truncar la salida

**Ejemplo:**
```bash
docker images
```

---

### `docker build`

**Descripción:** Construye una imagen a partir de un Dockerfile.

**Opciones disponibles:**
- `-t` - Etiquetar la imagen (nombre:tag)
- `-f` - Especificar archivo Dockerfile
- `--no-cache` - Construir sin usar cache
- `--build-arg` - Establecer variables de construcción
- `--pull` - Siempre intentar descargar una versión más reciente de la imagen

**Ejemplo:**
```bash
docker build -t mi-app:1.0 .
```

---

### `docker stop`

**Descripción:** Detiene uno o más contenedores en ejecución.

**Opciones disponibles:**
- `-t` - Tiempo de espera antes de forzar la detención (default: 10 segundos)

**Ejemplo:**
```bash
docker stop mi-contenedor
```

---

### `docker start`

**Descripción:** Inicia uno o más contenedores detenidos.

**Opciones disponibles:**
- `-a` - Adjuntar STDOUT/STDERR y reenviar señales
- `-i` - Adjuntar STDIN del contenedor

**Ejemplo:**
```bash
docker start mi-contenedor
```

---

### `docker exec`

**Descripción:** Ejecuta un comando en un contenedor en ejecución.

**Opciones disponibles:**
- `-it` - Modo interactivo con TTY
- `-d` - Ejecutar en segundo plano
- `-u` - Usuario con el que ejecutar el comando
- `-w` - Directorio de trabajo dentro del contenedor
- `-e` - Establecer variables de entorno

**Ejemplo:**
```bash
docker exec -it mi-contenedor bash
docker exec mi-contenedor ls -la
```

---

### `docker rm`

**Descripción:** Elimina uno o más contenedores.

**Opciones disponibles:**
- `-f` - Forzar eliminación de contenedor en ejecución
- `-v` - Eliminar volúmenes asociados
- `-l` - Eliminar enlaces específicos

**Ejemplo:**
```bash
docker rm mi-contenedor
```

---

### `docker rmi`

**Descripción:** Elimina una o más imágenes.

**Opciones disponibles:**
- `-f` - Forzar eliminación

**Ejemplo:**
```bash
docker rmi mi-imagen:1.0
```

---

### `docker logs`

**Descripción:** Muestra los logs de un contenedor.

**Opciones disponibles:**
- `-f` - Seguir mostrando logs en tiempo real
- `--tail` - Mostrar últimas N líneas
- `-t` - Mostrar timestamps
- `--since` - Mostrar logs desde una fecha/hora específica

**Ejemplo:**
```bash
docker logs -f mi-contenedor
docker logs --tail 50 mi-contenedor
```

---

### `docker system prune`

**Descripción:** Elimina datos no utilizados del sistema Docker.

**Opciones disponibles:**
- `-a` - Eliminar todas las imágenes no utilizadas
- `--volumes` - Eliminar todos los volúmenes no utilizados
- `--force` - Forzar eliminación sin confirmación
- `--filter` - Proporcionar valores de filtro

**Ejemplo:**
```bash
docker system prune -a
```

---

## Comandos de Redes en Docker

### `docker network ls`

**Descripción:** Lista todas las redes Docker.

**Opciones disponibles:**
- `-q` - Mostrar solo IDs de red
- `--filter` - Filtrar redes basado en condiciones dadas
- `--no-trunc` - No truncar la salida

**Ejemplo:**
```bash
docker network ls
```

---

### `docker network create`

**Descripción:** Crea una nueva red Docker.

**Opciones disponibles:**
- `-d` - Controlador de red (bridge, overlay, etc.)
- `--subnet` - Especificar subred en CIDR formato
- `--gateway` - Dirección IPv4 o IPv6 para el gateway
- `--label` - Agregar metadatos a la red

**Ejemplo:**
```bash
docker network create -d bridge mi-red
docker network create --subnet=172.20.0.0/16 mi-red-personalizada
```

---

### `docker network inspect`

**Descripción:** Muestra información detallada de una o más redes.

**Opciones disponibles:**
- `-f` - Formatear la salida usando una plantilla Go
- `--verbose` - Mostrar información adicional

**Ejemplo:**
```bash
docker network inspect mi-red
```

---

### `docker network connect`

**Descripción:** Conecta un contenedor a una red.

**Opciones disponibles:**
- `--alias` - Agregar un alias de red para el contenedor
- `--ip` - Dirección IP IPv4
- `--ip6` - Dirección IP IPv6

**Ejemplo:**
```bash
docker network connect mi-red mi-contenedor
```

---

### `docker network disconnect`

**Descripción:** Desconecta un contenedor de una red.

**Opciones disponibles:**
- `-f` - Forzar la desconexión

**Ejemplo:**
```bash
docker network disconnect mi-red mi-contenedor
```

---

## Comandos de Volúmenes en Docker

### `docker volume ls`

**Descripción:** Lista todos los volúmenes Docker.

**Opciones disponibles:**
- `-q` - Mostrar solo nombres de volúmenes
- `--filter` - Filtrar volúmenes basado en condiciones
- `--format` - Formatear la salida usando una plantilla

**Ejemplo:**
```bash
docker volume ls
```

---

### `docker volume create`

**Descripción:** Crea un nuevo volumen.

**Opciones disponibles:**
- `-d` - Especificar el driver del volumen (por defecto: local)
- `--label` - Establecer metadatos para el volumen
- `--opt` - Establecer opciones específicas del driver

**Ejemplo:**
```bash
docker volume create mi-volumen
docker volume create --opt type=nfs --opt device=:/path/to/dir nfs-volumen
```

---

### `docker volume inspect`

**Descripción:** Muestra información detallada de uno o más volúmenes.

**Opciones disponibles:**
- `-f` - Formatear la salida usando una plantilla Go

**Ejemplo:**
```bash
docker volume inspect mi-volumen
```

---

### `docker volume rm`

**Descripción:** Elimina uno o más volúmenes.

**Opciones disponibles:**
- `-f` - Forzar la eliminación

**Ejemplo:**
```bash
docker volume rm mi-volumen
```

---

## Comandos de Docker Compose

### `docker compose up`

**Descripción:** Crea e inicia los servicios definidos en el archivo docker-compose.yml.

**Opciones disponibles:**
- `-d` - Ejecutar en segundo plano
- `--build` - Forzar reconstrucción de imágenes
- `--force-recreate` - Recrear contenedores incluso si no cambiaron
- `--scale` - Escalar servicios específicos
- `--remove-orphans` - Remover contenedores huérfanos

**Ejemplo:**
```bash
docker compose up -d
docker compose up --build
```

---

### `docker compose down`

**Descripción:** Detiene y elimina contenedores, redes y volúmenes definidos en el compose.

**Opciones disponibles:**
- `-v` - Eliminar volúmenes nombrados declarados en la sección volumes
- `--rmi` - Eliminar imágenes utilizadas por los servicios
- `--remove-orphans` - Remover contenedores huérfanos

**Ejemplo:**
```bash
docker compose down
docker compose down -v
```

---

### `docker compose logs`

**Descripción:** Muestra la salida de logs de los servicios.

**Opciones disponibles:**
- `-f` - Seguir mostrando logs
- `--tail` - Mostrar últimas N líneas por servicio
- `-t` - Mostrar timestamps
- `--no-color` - Producir salida monocrómica

**Ejemplo:**
```bash
docker compose logs -f mi-servicio
docker compose logs --tail=100
```

---

### `docker compose ps`

**Descripción:** Lista los contenedores de los servicios definidos en el compose.

**Opciones disponibles:**
- `-a` - Mostrar todos los contenedores (incluyendo detenidos)
- `-q` - Mostrar solo IDs
- `--services` - Mostrar servicios
- `--filter` - Filtrar salida por condiciones

**Ejemplo:**
```bash
docker compose ps
docker compose ps -a
```

---

## Comandos de Docker Swarm

### `docker swarm init`

**Descripción:** Inicializa un swarm Docker.

**Opciones disponibles:**
- `--advertise-addr` - Dirección para que otros nodos se conecten
- `--listen-addr` - Dirección de escucha para el swarm
- `--data-path-addr` - Dirección o interfaz usada para la ruta de datos

**Ejemplo:**
```bash
docker swarm init --advertise-addr 192.168.1.100
```

---

### `docker service create`

**Descripción:** Crea un nuevo servicio en el swarm.

**Opciones disponibles:**
- `--replicas` - Número de réplicas del servicio
- `--publish` - Publicar puertos
- `--mount` - Montar volúmenes
- `--env` - Establecer variables de entorno
- `--network` - Conectar a una red
- `--constraint` - Colocar restricciones

**Ejemplo:**
```bash
docker service create --replicas 3 --name web -p 80:80 nginx
```

---

### `docker service ls`

**Descripción:** Lista los servicios en el swarm.

**Opciones disponibles:**
- `-q` - Mostrar solo IDs de servicios
- `--filter` - Filtrar servicios basado en condiciones

**Ejemplo:**
```bash
docker service ls
```

---

### `docker service scale`

**Descripción:** Escala uno o más servicios replicados.

**Opciones disponibles:**
- `-d` - Escalar servicios en segundo plano

**Ejemplo:**
```bash
docker service scale web=5
docker service scale web=5 api=3
```

---

### `docker node ls`

**Descripción:** Lista los nodos en el swarm.

**Opciones disponibles:**
- `-q` - Mostrar solo IDs de nodos
- `--filter` - Filtrar nodos por criterios específicos

**Ejemplo:**
```bash
docker node ls
```

---

## Tips de Uso Práctico

### 🔧 Comandos Esenciales para Desarrollo

```bash
# Ejecutar comando interactivo en contenedor
docker exec -it contenedor bash

# Ver logs en tiempo real
docker logs -f contenedor

# Limpiar sistema completo
docker system prune -a --volumes

# Crear red personalizada
docker network create --driver bridge mi-red
```

### 🚀 Comandos para Producción

```bash
# Inicializar Swarm
docker swarm init

# Desplegar servicio con réplicas
docker service create --replicas 3 --name app mi-imagen:latest

# Escalar servicio
docker service scale app=5
```

### 📊 Comandos de Monitoreo y Diagnóstico

```bash
# Ver estadísticas de contenedores en tiempo real
docker stats

# Ver información detallada del sistema Docker
docker info

# Ver uso de disco
docker system df

# Inspeccionar contenedor específico
docker inspect nombre-contenedor
```

### 🖼️ Comandos para Manejo de Imágenes

```bash
# Descargar imagen sin ejecutarla
docker pull nombre-imagen:tag

# Etiquetar imagen
docker tag imagen-antigua nombre-nuevo:tag

# Guardar imagen como archivo tar
docker save -o imagen.tar nombre-imagen:tag

# Cargar imagen desde archivo tar
docker load -i imagen.tar
```

---

## 📝 Notas

Este documento fue creado como parte de la actividad de comandos Docker para la materia de Gestión del Proceso de Desarrollo de Software.

**Última actualización:** Octubre 2025

---

## 📄 Licencia

Documento educativo para uso académico.