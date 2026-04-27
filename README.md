# 🤖 Automatizacion
 
## Español | [English](readme.en.md) | [Français](readme.fr.md) | [Português](readme.pr.md)
 
¡Bienvenido a **Automatizacion-Others**! 🚀  
Repositorio centralizado de scripts, flujos y recursos de automatización con distintas herramientas y tecnologías.

---


<img width="585" height="698" alt="image" src="https://github.com/user-attachments/assets/fe91ee8a-b963-49a1-b3e7-ff031105f765" />


---

## 📋 Tabla de Contenidos

1. [¿Qué contiene este repositorio?](#-qué-contiene-este-repositorio)
2. [Tecnologías y herramientas](#-tecnologías-y-herramientas)
3. [Cómo instalar n8n](#-cómo-instalar-n8n)
   - [Instalación local con Node.js](#1-instalación-local-con-nodejs)
   - [Instalación con Docker](#2-instalación-con-docker)
   - [Acceder a la interfaz](#3-acceder-a-la-interfaz)
   - [Persistencia de datos](#4-persistencia-de-datos)
   - [Solución de problemas](#5-solución-de-problemas-comunes)
4. [Recursos útiles](#-recursos-útiles)
5. [Canales de YouTube](#-canales-de-youtube)

---

## 📁 ¿Qué contiene este repositorio?

| Tipo | Descripción |
|------|-------------|
| 📜 Scripts | Automatizaciones en Python y Bash |
| 🔄 Workflows n8n | Flujos exportados listos para importar (`.json`) |
| 🔌 Integraciones | APIs, Webhooks, ETL, notificaciones, scraping |
| 🚀 CI/CD | Automatizaciones de despliegue |
| 🧩 Snippets | Ejemplos reutilizables |

---

## 🧰 Tecnologías y herramientas

| Tecnología | Uso |
|------------|-----|
| 🔄 n8n | Automatización de workflows e integraciones |
| 🐍 Python | Scripts de automatización |
| 🪄 Bash | Automatización en terminal |

---

## ⚙️ Cómo instalar n8n

### Requisitos previos

| Método | Requisitos |
|--------|------------|
| Local | Node.js >= 18, npm >= 8 |
| Docker | Docker Engine >= 20.x, Docker Compose |

**Sistemas operativos soportados:** Linux · macOS 10.15+ · Windows 10/11 (WSL2 recomendado)

---

### 1. Instalación local con Node.js

#### Instalar Node.js 20

**Ubuntu / Debian**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20 && nvm use 20
node -v && npm -v
```

**macOS**
```bash
brew install node@20
node -v && npm -v
```

**Windows** — Descargar [nvm-windows](https://github.com/coreybutler/nvm-windows/releases) y ejecutar:
```powershell
nvm install 20
nvm use 20
```

> 💡 En Windows se recomienda usar WSL2 con Ubuntu para mayor estabilidad.

#### Instalar y ejecutar n8n

```bash
npm install -g n8n   # Instalar
n8n --version        # Verificar
n8n start            # Ejecutar → http://localhost:5678
```

#### Ejecutar en background con pm2

```bash
npm install -g pm2
pm2 start n8n
pm2 startup && pm2 save
```

#### Variables de entorno útiles

```bash
export N8N_PORT=8080                        # Cambiar puerto (default: 5678)
export N8N_HOST=mi-dominio.com              # URL base para proxy inverso
export N8N_PROTOCOL=https
export N8N_USER_FOLDER=/ruta/a/datos        # Directorio de datos
n8n start
```

> Para hacerlas permanentes, agregá las líneas `export` a `~/.bashrc` o `~/.zshrc`.

---

### 2. Instalación con Docker

#### Instalar Docker

**Ubuntu / Debian**
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo usermod -aG docker $USER && newgrp docker
docker --version && docker compose version
```

**macOS / Windows** — Descargar [Docker Desktop](https://www.docker.com/products/docker-desktop/).

#### Modo simple (un solo comando)

```bash
docker run -d \
  --name n8n \
  --restart unless-stopped \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

#### Docker Compose (recomendado)

```bash
mkdir n8n-local && cd n8n-local
```

Crear `docker-compose.yml`:

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

```bash
docker compose up -d          # Levantar
docker compose logs -f        # Ver logs
docker compose down           # Detener
docker compose pull && docker compose up -d  # Actualizar
```

#### Docker Compose con PostgreSQL (entorno robusto)

<details>
<summary>Ver configuración completa</summary>

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

</details>

---

### 3. Acceder a la interfaz

Una vez que n8n esté corriendo, abrí tu navegador en:

```
http://localhost:5678
```

La primera vez se pedirá crear una cuenta de administrador local.

---

### 4. Persistencia de datos

**Local** — Los datos se guardan en `~/.n8n` por defecto. Para cambiar la ruta:
```bash
export N8N_USER_FOLDER=/ruta/personalizada/.n8n
```

**Docker** — Siempre usar volúmenes nombrados (no directorios temporales del contenedor):
```yaml
volumes:
  - n8n_data:/home/node/.n8n
```

---

### 5. Solución de problemas comunes

| Problema | Solución |
|----------|----------|
| Puerto 5678 en uso | `export N8N_PORT=5679 && n8n start` |
| Permisos en volumen Docker | `sudo chown -R 1000:1000 ~/.n8n` |
| Contenedor se detiene solo | `docker logs n8n` o `docker compose logs n8n` |
| Node.js incompatible | `nvm install 20 && nvm use 20` |
| Actualizar n8n (local) | `npm update -g n8n` |
| Actualizar n8n (Docker) | `docker compose pull && docker compose up -d` |

---

## 🔗 Recursos útiles

### 📂 Mis repositorios

| Repositorio | Descripción |
|-------------|-------------|
| [Automatizacion-Others](https://github.com/luchoxiii/Automatizacion-Others) | Este repositorio |
| [Airflow](https://github.com/luchoxiii/airflow) | Workflows y pipelines con Apache Airflow |
| [Snowflake](https://github.com/luchoxiii/snowflake) | Recursos y scripts para Snowflake |
| [Cyber_Securitys](https://github.com/luchoxiii/Cyber_Securitys/tree/main/n8n-workflows) | Workflows de n8n para ciberseguridad |

### 🌐 Links externos

| Recurso | Descripción |
|---------|-------------|
| [Documentación oficial n8n](https://docs.n8n.io/) | Guía completa y referencia de variables |
| [n8n en Docker Hub](https://hub.docker.com/r/n8nio/n8n) | Imagen oficial |
| [Repositorio n8n en GitHub](https://github.com/n8n-io/n8n) | Código fuente |
| [Awesome n8n Templates](https://github.com/enescingoz/awesome-n8n-templates) | Workflows listos para usar |
| [Costos de APIs IA](https://inworld.ai/models) | Comparativa de precios |
| [Agentes con LLMs — Nvidia](https://learn.nvidia.com/courses/course-detail?course_id=course-v1:DLI+S-FX-16+V1) | Curso gratuito |
| [DeepL](https://www.deepl.com/es/translator) | Traducción con IA |
| [Groq](https://groq.com/) | API de IA gratuita |
| [Documentación del repo](https://github.com/luchoxiii/Automatizacion-Others/tree/main/Books) | Books y docs internos |

---

## 📺 Canales de YouTube

**Español**
- [Imz Dev](https://www.youtube.com/@ImzoDev/videos)
- [Benjamin Cordero](https://www.youtube.com/@bencord/videos)
- [Aitor Wilzig](https://www.youtube.com/@AitorWilzig)


**Ingles**


---

## 📥 Clonar el repositorio

```bash
git clone https://github.com/luchoxiii/Automatizacion-Others.git
```
