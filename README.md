# Automatizacion

## Español | [English](readme.en.md) | [Français](readme.fr.md) | [Português](readme.pr.md)

¡Bienvenido a **Automatizacion-Others**! 🚀

Este repositorio agrupa **scripts, flujos y recursos de automatización** utilizando distintas herramientas y tecnologías.  
La idea es centralizar soluciones prácticas para automatizar tareas repetitivas, integraciones y procesos.

---

## 🧠 ¿Qué contiene este repositorio?

Este repo está pensado como un espacio flexible para organizar automatizaciones de distintos tipos, por ejemplo:

- 📜 Scripts de automatización
- 🔄 Flujos de trabajo con **n8n**
- 🔌 Integraciones entre servicios (APIs, Webhooks, etc.)
- 🚀 Automatizaciones para CI/CD
- 🧩 Snippets y ejemplos reutilizables

---

## 🔄 Automatización con n8n

[n8n](https://n8n.io/) es una de las herramientas principales contempladas en este repositorio.

Acá vas a poder encontrar (o agregar):

- Workflows exportados de n8n (`.json`)
- Automatizaciones con Webhooks
- Integraciones con APIs externas
- Flujos para notificaciones, ETL, scraping, etc.
- Ejemplos listos para importar en n8n

> 💡 Los workflows de n8n pueden importarse directamente desde la interfaz usando el archivo `.json`.

---

## 🧰 Tecnologías y herramientas

| Tecnología / Tool | Uso |
|------------------|-----|
| 🔄 n8n           | Automatización de workflows e integraciones |
| 🐍 Python        | Scripts de automatización |
| 🪄 Bash          | Automatización en terminal |
| 🧪 Otros         | Según necesidades futuras |

---

## 📥 Cómo usar este repositorio

### 1️⃣ Clonar el proyecto

```bash
git clone https://github.com/luchoxiii/Automatizacion-Others.git

```

<img width="585" height="698" alt="image" src="https://github.com/user-attachments/assets/fe91ee8a-b963-49a1-b3e7-ff031105f765" />


---
### Diferentes IAs para hacer cosas

#### Traduccion:
  - [DeepL](https://www.deepl.com/es/translator)

#### IA API gratuita 
  - [Groq](https://groq.com/)


---

### Canales de YouTube

  #### Español

  - [Imz Dev](https://www.youtube.com/@ImzoDev/videos)
  - [Benjamin Cordero](https://www.youtube.com/@bencord/videos)
  - [Aitor Wilzig](https://www.youtube.com/@AitorWilzig)

  #### Ingles

---



### Otros recursos importantes

- [Documentacion](https://github.com/luchoxiii/Automatizacion-Others/tree/main/Books)
- [N8N Workflows de Cybersecurity Ideas](https://github.com/luchoxiii/Cyber_Securitys/tree/main/n8n-workflows)
- [Costos de APIs IA](https://inworld.ai/models)
- [Agentes con LLMs by Nvidia](https://learn.nvidia.com/courses/course-detail?course_id=course-v1:DLI+S-FX-16+V1)

---

### Como instalar N8N

### Tabla de Contenidos
 
1. [Requisitos Previos Generales](#1-requisitos-previos-generales)
2. [Instalación Local con Node.js](#2-instalación-local-con-nodejs)
   - [Instalar Node.js y npm](#21-instalar-nodejs-y-npm)
   - [Instalar n8n globalmente](#22-instalar-n8n-globalmente)
   - [Ejecutar n8n](#23-ejecutar-n8n)
   - [Variables de entorno útiles](#24-variables-de-entorno-útiles)
3. [Instalación con Docker](#3-instalación-con-docker)
   - [Instalar Docker](#31-instalar-docker)
   - [Ejecutar n8n con Docker (modo simple)](#32-ejecutar-n8n-con-docker-modo-simple)
   - [Ejecutar n8n con Docker Compose](#33-ejecutar-n8n-con-docker-compose)
4. [Acceder a la interfaz](#4-acceder-a-la-interfaz)
5. [Configuración de persistencia de datos](#5-configuración-de-persistencia-de-datos)
6. [Solución de problemas comunes](#6-solución-de-problemas-comunes)
---
 
### 1. Requisitos Previos Generales
 
Antes de instalar n8n, asegurate de contar con lo siguiente según el método que elijas:
 
| Método        | Requisitos                              |
|---------------|-----------------------------------------|
| Local         | Node.js >= 18, npm >= 8                 |
| Docker        | Docker Engine >= 20.x, Docker Compose   |
 
### Sistema operativo soportado
 
- **Linux** (Ubuntu, Debian, CentOS, Fedora, etc.)
- **macOS** (10.15 Catalina o superior)
- **Windows** (10/11 con WSL2 recomendado)
---
 
### 2. Instalación Local con Node.js
 
#### 2.1 Instalar Node.js y npm
 
n8n requiere **Node.js versión 18 o superior**.
 
##### En Ubuntu / Debian
 
```bash
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y
 
# Instalar curl si no está disponible
sudo apt install -y curl
 
# Instalar Node.js 20 LTS con nvm (recomendado)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
 
# Recargar el terminal
source ~/.bashrc
 
# Instalar Node.js 20
nvm install 20
nvm use 20
 
# Verificar versiones
node -v
npm -v
```
 
##### En macOS (con Homebrew)
 
```bash
# Instalar Homebrew si no está disponible
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
 
# Instalar Node.js
brew install node@20
 
# Verificar versiones
node -v
npm -v
```
 
##### En Windows (con nvm-windows)
 
1. Descargar el instalador de [nvm-windows](https://github.com/coreybutler/nvm-windows/releases).
2. Ejecutar el instalador `.exe` y seguir los pasos.
3. Abrir una terminal (PowerShell o CMD) como administrador:
```powershell
nvm install 20
nvm use 20
node -v
npm -v
```
 
> **Recomendación para Windows**: Se sugiere usar WSL2 (Windows Subsystem for Linux) para una experiencia más estable. Instalá Ubuntu desde la Microsoft Store y seguí los pasos de Linux.
 
---
 
#### 2.2 Instalar n8n globalmente
 
Con Node.js instalado, ejecutá el siguiente comando para instalar n8n de forma global:
 
```bash
npm install -g n8n
```
 
Para verificar que la instalación fue exitosa:
 
```bash
n8n --version
```
 
---
 
#### 2.3 Ejecutar n8n
 
Para iniciar n8n en modo local:
 
```bash
n8n start
```
 
Por defecto, n8n corre en el puerto **5678**. Podés acceder desde el navegador en:
 
```
http://localhost:5678
```
 
##### Ejecutar en segundo plano (background) con `pm2`
 
Si querés que n8n corra como un servicio persistente:
 
```bash
# Instalar pm2
npm install -g pm2
 
# Iniciar n8n con pm2
pm2 start n8n
 
# Configurar pm2 para que inicie al arrancar el sistema
pm2 startup
pm2 save
```
 
---
 
#### 2.4 Variables de entorno útiles
 
Podés personalizar el comportamiento de n8n definiendo variables de entorno antes de ejecutarlo:
 
```bash
# Cambiar el puerto (por defecto es 5678)
export N8N_PORT=8080
 
# Definir la URL base (útil si usás un proxy inverso)
export N8N_HOST=mi-dominio.com
export N8N_PROTOCOL=https
 
# Definir el directorio de datos
export N8N_USER_FOLDER=/ruta/a/datos
 
# Iniciar con las variables aplicadas
n8n start
```
 
Para hacerlas permanentes, agregá las líneas `export ...` al archivo `~/.bashrc` o `~/.zshrc`.
 
---
 
### 3. Instalación con Docker
 
#### 3.1 Instalar Docker
 
##### En Ubuntu / Debian
 
```bash
# Actualizar paquetes
sudo apt update
 
# Instalar dependencias
sudo apt install -y ca-certificates curl gnupg lsb-release
 
# Agregar la clave GPG oficial de Docker
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 
# Agregar el repositorio de Docker
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
 
# Instalar Docker Engine
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
 
# Permitir usar Docker sin sudo (opcional)
sudo usermod -aG docker $USER
newgrp docker
 
# Verificar instalación
docker --version
docker compose version
```
 
##### En macOS
 
Descargá e instalá [Docker Desktop para Mac](https://www.docker.com/products/docker-desktop/). Incluye Docker Engine y Docker Compose.
 
```bash
# Verificar instalación
docker --version
docker compose version
```
 
##### En Windows
 
Descargá e instalá [Docker Desktop para Windows](https://www.docker.com/products/docker-desktop/). Se recomienda tener habilitado **WSL2** como backend.
 
---
 
### 3.2 Ejecutar n8n con Docker (modo simple)
 
Este comando descarga la imagen oficial de n8n y la ejecuta:
 
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```
 
**Descripción de los parámetros:**
 
| Parámetro                          | Descripción                                               |
|------------------------------------|-----------------------------------------------------------|
| `-p 5678:5678`                     | Expone el puerto 5678 del contenedor al host              |
| `-v ~/.n8n:/home/node/.n8n`        | Monta un volumen para persistir los datos localmente      |
| `--rm`                             | Elimina el contenedor al detenerlo                        |
| `--name n8n`                       | Le asigna un nombre al contenedor                         |
 
Para correrlo en segundo plano (modo detached):
 
```bash
docker run -d \
  --name n8n \
  --restart unless-stopped \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```
 
---
 
#### 3.3 Ejecutar n8n con Docker Compose
 
Docker Compose es el método recomendado para entornos más organizados y con configuraciones adicionales.
 
#### Paso 1: Crear el directorio del proyecto
 
```bash
mkdir n8n-local && cd n8n-local
```
 
##### Paso 2: Crear el archivo `docker-compose.yml`
 
```yaml
version: "3.8"
 
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_HOST=localhost
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - NODE_ENV=production
      - WEBHOOK_URL=http://localhost:5678/
      - GENERIC_TIMEZONE=America/Argentina/Buenos_Aires
    volumes:
      - n8n_data:/home/node/.n8n
 
volumes:
  n8n_data:
    driver: local
```
 
##### Paso 3: Levantar el servicio
 
```bash
docker compose up -d
```
 
##### Otros comandos útiles de Docker Compose
 
```bash
# Ver los logs en tiempo real
docker compose logs -f
 
# Detener el servicio
docker compose down
 
# Detener y eliminar los volúmenes (¡borra los datos!)
docker compose down -v
 
# Actualizar la imagen de n8n
docker compose pull
docker compose up -d
```
 
---
 
##### Docker Compose con PostgreSQL (base de datos externa)
 
Para un entorno más robusto, podés usar PostgreSQL como base de datos en lugar de SQLite:
 
```yaml
version: "3.8"
 
services:
  postgres:
    image: postgres:15
    container_name: n8n_postgres
    restart: unless-stopped
    environment:
      POSTGRES_USER: n8n
      POSTGRES_PASSWORD: n8n_password
      POSTGRES_DB: n8n
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U n8n"]
      interval: 10s
      timeout: 5s
      retries: 5
 
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_HOST=localhost
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - NODE_ENV=production
      - WEBHOOK_URL=http://localhost:5678/
      - GENERIC_TIMEZONE=America/Argentina/Buenos_Aires
      - DB_TYPE=postgresdb
      - DB_POSTGRESDB_HOST=postgres
      - DB_POSTGRESDB_PORT=5432
      - DB_POSTGRESDB_DATABASE=n8n
      - DB_POSTGRESDB_USER=n8n
      - DB_POSTGRESDB_PASSWORD=n8n_password
    volumes:
      - n8n_data:/home/node/.n8n
    depends_on:
      postgres:
        condition: service_healthy
 
volumes:
  postgres_data:
  n8n_data:
```
 
---
 
### 4. Acceder a la interfaz
 
Una vez que n8n esté corriendo (por cualquiera de los métodos), abrí tu navegador y accedé a:
 
```
http://localhost:5678
```
 
La primera vez, n8n te pedirá que crees una cuenta de administrador local con un correo electrónico y contraseña.
 
---
 
### 5. Configuración de persistencia de datos
 
Es importante asegurarse de que los datos (workflows, credenciales, ejecuciones) no se pierdan al reiniciar el servicio.
 
#### Local
 
Por defecto, n8n guarda los datos en `~/.n8n`. Podés cambiar esta ruta con la variable de entorno:
 
```bash
export N8N_USER_FOLDER=/ruta/personalizada/.n8n
```
 
#### Docker
 
Usá **volúmenes de Docker** (como en los ejemplos anteriores) en lugar de directorios temporales del contenedor. Los volúmenes nombrados son más seguros y portables:
 
```yaml
volumes:
  - n8n_data:/home/node/.n8n
```
 
---
 
### 6. Solución de problemas comunes
 
#### Puerto 5678 en uso
 
```bash
# Ver qué proceso usa el puerto
sudo lsof -i :5678
 
# Cambiar el puerto de n8n
export N8N_PORT=5679
n8n start
```
 
#### Permisos en el volumen de Docker
 
```bash
# Asignar permisos correctos al directorio de datos
sudo chown -R 1000:1000 ~/.n8n
```
 
#### El contenedor Docker se detiene solo
 
Revisá los logs del contenedor:
 
```bash
docker logs n8n
# o con Docker Compose:
docker compose logs n8n
```
 
#### Versión de Node.js incompatible
 
```bash
# Verificar versión actual
node -v
 
# Debe ser >= 18. Si no, actualizarla con nvm:
nvm install 20
nvm use 20
```
 
#### Actualizar n8n (instalación local)
 
```bash
npm update -g n8n
```
 
#### Actualizar n8n (Docker)
 
```bash
docker pull docker.n8n.io/n8nio/n8n
docker stop n8n && docker rm n8n
# Volver a ejecutar el comando docker run o docker compose up -d
```
 
---
 
### Referencias
 
- [Documentación oficial de n8n](https://docs.n8n.io/)
- [n8n en Docker Hub](https://hub.docker.com/r/n8nio/n8n)
- [Repositorio de n8n en GitHub](https://github.com/n8n-io/n8n)
- [Variables de entorno de n8n](https://docs.n8n.io/hosting/configuration/environment-variables/)

