# 🚀 TorrentFlow

![Python](https://img.shields.io/badge/Python-3.10-blue) ![Docker](https://img.shields.io/badge/Docker-Ready-green) ![Status](https://img.shields.io/badge/Status-Stable-success)

**TorrentFlow** es una interfaz web moderna y multi-usuario para gestionar descargas de **qBittorrent**. Diseñada para servidores caseros, permite controlar quién descarga y dónde se guardan los archivos, todo bajo una interfaz limpia con Modo Oscuro nativo.

---

## ✨ ¿Qué hace esta web?

* 🎨 **Dashboard Moderno:** Visualiza progreso, velocidad y estado de descargas en tiempo real (Diseño Stitch/TailwindCSS).
* 🛡️ **Roles de Usuario (RBAC):**
    * **Admins:** Gestionan usuarios, crean rutas de descarga y ven todo.
    * **Usuarios:** Solo pueden ver y borrar sus propias descargas.
* 📂 **Gestión de Rutas:** El Admin define carpetas específicas (ej: `/Pelis`, `/Juegos`) para mantener el servidor organizado.
* 🐳 **Docker Ready:** Despliegue inmediato con Docker Compose o Portainer.

---

## 📸 Vista Previa

*(Sube capturas a tu repo y enlázalas aquí para que la gente vea el diseño)*
| Dashboard | Gestión de Rutas |
|:---:|:---:|
| ![Dash](https://via.placeholder.com/400x200?text=Dashboard+Preview) | ![Rutas](https://via.placeholder.com/400x200?text=Path+Manager) |

---

## 🛠️ Instalación Rápida (Docker)

### 1. Requisitos
* Un servidor con **Docker** y **Docker Compose**.
* **qBittorrent** instalado y corriendo (con la WebUI activada en el puerto 8080).

### 2. Despliegue con Docker Compose
Crea un archivo `docker-compose.yml` con el siguiente contenido. **¡Importante!** Cambia la IP por la de tu servidor real.

version: '3.8'

services:
  torrentflow:
    image: basilioag/webtorrent:latest # O 'build: .' si clonas el repo
    container_name: torrentflow_app
    restart: unless-stopped
    ports:
      - "5000:5000"
    volumes:
      # Mapea tu carpeta local para persistir la base de datos
      - ./torrents.db:/app/torrents.db
    environment:
      - QBIT_HOST=192.168.1.XX  # <--- IP de tu servidor (NO usar localhost)
      - QBIT_PORT=8080
      - QBIT_USER=admin
      - QBIT_PASS=adminadmin
      - SECRET_KEY=pon_aqui_una_clave_aleatoria_larga

### 3. Ejecutar

docker-compose up -d

Accede a tu web en: http://TU-IP-SERVIDOR:5000

☁️ Despliegue en Portainer (Stack)
Ve a Stacks > Add Stack.

Selecciona Repository y usa la URL de este GitHub.

Copia el contenido del docker-compose.yml de arriba (o asegúrate de que el del repo tenga tus variables).

Pulsa Deploy the stack.

⚙️ Variables de Entorno
Variable,Descripción,Ejemplo
QBIT_HOST,IP donde corre qBittorrent,192.168.1.50
QBIT_PORT,Puerto de la WebUI,8080
SECRET_KEY,Firma de seguridad para sesiones,a1b2c3d4...

### Creado por BasilioAG.