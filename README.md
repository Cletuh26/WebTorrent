# 🌊 TorrentFlow v4.0 (Mobile Ready)

![Python](https://img.shields.io/badge/Python-3.10-3776AB?style=flat&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-Live_App-000000?style=flat&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=flat&logo=docker&logoColor=white)
![Responsive](https://img.shields.io/badge/Mobile-Responsive-orange)

**TorrentFlow** es un gestor de descargas moderno, auto-hospedado y ahora **totalmente responsive** para qBittorrent. 
Gestiona tus descargas desde el móvil, personaliza tu perfil y controla exactamente quién puede descargar y dónde.

---

## 🔥 Novedades de la v4.0
* 📱 **Diseño Mobile-First:** Nueva interfaz adaptativa con menú hamburguesa y tablas deslizables para gestionar todo desde tu teléfono.
* 📸 **Perfiles Personalizados:** Los usuarios pueden subir su propia **foto de perfil**, cambiar su email y contraseña.
* 🔐 **Permisos Granulares:** El administrador puede asignar **rutas específicas** a cada usuario (ej: Pepe solo descarga en `/Pelis`, María en `/Series`).
* ⚡ **Live Dashboard:** Actualización en tiempo real sin recargar la página (AJAX).

## ✨ Características Principales
* **Interfaz Stitch:** Diseño oscuro moderno con TailwindCSS.
* **Gestión de Usuarios (RBAC):** Sistema completo de Administradores y Usuarios.
* **Auto-Sync:** Detecta enlaces Magnet sin hash y sincroniza metadatos automáticamente.
* **Smart OS Detection:** Oculta botones de "Abrir carpeta" si el servidor no tiene interfaz gráfica (Docker/Headless).

---

## 📸 Vista Previa

| **Dashboard (Móvil)** | **Gestión de Perfil** |
|:---:|:---:|
| ![Mobile Dash](https://via.placeholder.com/250x500/101922/FFFFFF?text=Mobile+View) | ![Profile](https://via.placeholder.com/400x250/101922/FFFFFF?text=Profile+Editor) |

---

## 🚀 Despliegue con Docker Compose (Recomendado)

Para persistir la base de datos **y las fotos de perfil**, usa esta configuración.

```yaml
version: '3.8'
services:
  torrentflow:
    image: basilioag/webtorrent:latest # O 'build: .' si usas el código local
    container_name: torrentflow
    restart: unless-stopped
    ports:
      - "5000:5000"
    volumes:
      - ./torrents.db:/app/torrents.db          # Base de datos
      - ./profile_pics:/app/static/profile_pics  # <--- NUEVO: Persistencia de fotos
    environment:
      - QBIT_HOST=192.168.1.XX  # Tu IP de qBittorrent
      - QBIT_PORT=8080
      - QBIT_USER=admin
      - QBIT_PASS=adminadmin
      - SECRET_KEY=cambia_esta_clave_por_seguridad