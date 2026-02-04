# 🌊 TorrentFlow v3.0

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Live_App-000000?style=flat&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat&logo=docker&logoColor=white)
![Status](https://img.shields.io/badge/Dashboard-Realtime-success)

**TorrentFlow** es un gestor de descargas auto-hospedado, moderno y potente para **qBittorrent**. 
Ahora con **actualizaciones en tiempo real**: observa cómo avanzan tus descargas sin recargar la página.

---

## 🔥 Novedades de la v3.0
* ⚡ **Live Dashboard:** El progreso y estado de las descargas se actualiza automáticamente cada 2 segundos (AJAX).
* 👤 **Gestión de Perfil:** Los usuarios ahora pueden cambiar su contraseña, email y foto de perfil.
* 🛡️ **Robustez:** Mejorado el sistema de captura de Magnet Links (soporte para enlaces sin hash explícito).
* 📱 **UI Unificada:** Navbar y Footer consistentes en todas las vistas con diseño responsivo.

## ✨ Características Principales
* 🎨 **Interfaz Stitch:** Diseño oscuro moderno con TailwindCSS.
* 👥 **Roles de Usuario (RBAC):** Admin (control total) vs Usuario Estándar (solo sus descargas).
* 📂 **Gestión de Rutas:** Define carpetas permitidas en el servidor para organizar el contenido.
* 🐳 **Docker Native:** Detecta si corre en contenedor para adaptar la interfaz (modo Headless).

---

## 📸 Vista Previa

| **Dashboard (Live)** | **Gestión de Usuarios** |
|:---:|:---:|
| ![Dash](https://via.placeholder.com/400x250/101922/FFFFFF?text=Live+Dashboard+Preview) | ![Users](https://via.placeholder.com/400x250/101922/FFFFFF?text=Admin+Panel) |

---

## 🚀 Despliegue Rápido (Docker Compose)

Crea un archivo `docker-compose.yml` y despliega en segundos.

```yaml
version: '3.8'
services:
  torrentflow:
    image: basilioag/webtorrent:latest # O usa 'build: .' si clonas el código
    container_name: torrentflow
    restart: unless-stopped
    ports:
      - "5000:5000"
    volumes:
      - ./torrents.db:/app/torrents.db
    environment:
      - QBIT_HOST=192.168.1.XX  # <--- IP de tu servidor qBittorrent
      - QBIT_PORT=8080          # <--- Puerto WebUI
      - QBIT_USER=admin
      - QBIT_PASS=adminadmin
      - SECRET_KEY=genera_una_clave_segura_aqui
