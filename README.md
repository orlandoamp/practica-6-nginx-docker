# Práctica 6: Ejecutar Servidor Web Nginx con Docker Compose

Este repositorio contiene la solución completa para la **Práctica 6: Ejecutar servidor web Nginx con Docker**, en la cual se despliega un servidor web local utilizando **Docker Compose** y montando un volumen persistente hacia el directorio estático de Nginx.

---

## 📋 Requisitos Previos

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) instalado y en ejecución.
- Soporte para `docker compose` (incluido en Docker Desktop v2+).
- Git instalado localmente.

---

## 📁 Estructura del Proyecto

```text
practica-6-nginx-docker/
├── src/
│   └── index.html          # Archivo HTML estático con mensaje 'Hola Mundo'
├── docker-compose.yml      # Configuración del servicio Nginx y mapeo de volúmenes
├── .gitignore              # Archivos y carpetas ignorados por Git
└── README.md               # Documentación detallada del proyecto
```

---

## ⚙️ Configuración (`docker-compose.yml`)

El archivo `docker-compose.yml` define el servicio web basado en la imagen ligera `nginx:alpine`:

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    container_name: nginx-servidor-web
    restart: always
    ports:
      - "80:80"
    volumes:
      - ./src:/usr/share/nginx/html
```

### Explicación de los parámetros:
- **`image: nginx:alpine`**: Utiliza la distribución oficial de Nginx sobre Alpine Linux, optimizada para un consumo mínimo de memoria y almacenamiento.
- **`container_name: nginx-servidor-web`**: Asigna un nombre identificable al contenedor.
- **`ports: ["80:80"]`**: Mapea el puerto local `80` del host al puerto `80` dentro del contenedor.
- **`volumes: ["./src:/usr/share/nginx/html"]`**: Monta la carpeta local `./src` directamente en la ruta `/usr/share/nginx/html` de Nginx. De este modo, cualquier cambio en los archivos de `src/` se refleja de inmediato sin necesidad de reconstruir la imagen ni reiniciar el contenedor.
- **`restart: always`**: Asegura que el servicio se reinicie automáticamente si se detiene de forma imprevista o al iniciar el sistema.

---

## 🚀 Instrucciones de Ejecución

### 1. Iniciar el servidor

Desde la raíz del repositorio, ejecuta el siguiente comando para levantar el contenedor en segundo plano (detached mode):

```bash
docker compose up -d
```

### 2. Verificar el estado del contenedor

Para comprobar que el contenedor se encuentra activo y escuchando en el puerto 80:

```bash
docker compose ps
```

También puedes visualizar los logs de acceso en tiempo real con:

```bash
docker compose logs -f
```

### 3. Visualizar la página web

Abre cualquier navegador web y accede a:

👉 **[http://localhost](http://localhost)** o **[http://127.0.0.1](http://127.0.0.1)**

Verás la página con el mensaje *"¡Hola Mundo!"* servida directamente por Nginx desde la carpeta `src/`.

---

## 🛑 Comandos Útiles

- **Detener los contenedores:**
  ```bash
  docker compose stop
  ```

- **Detener y remover contenedores y redes:**
  ```bash
  docker compose down
  ```

- **Reiniciar el servicio:**
  ```bash
  docker compose restart
  ```

---

## 👤 Autor

- **Nombre:** Orlando Amparo
- **Materia:** Programación Web
- **Institución:** ITLA
