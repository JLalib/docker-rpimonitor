# RPi-Monitor – Contenedor Docker

Este repositorio contiene la configuración necesaria para desplegar **RPi-Monitor** en Docker.  
RPi-Monitor es una herramienta de monitorización en tiempo real diseñada para Raspberry Pi que permite visualizar métricas del sistema como CPU, memoria, temperatura, red y almacenamiento.

---

## 🚀 Características

- Imagen: `ikaritw/rpi-monitor:latest`
- Monitorización en tiempo real
- Interfaz web ligera
- Acceso a métricas del sistema host
- Compatible con Raspberry Pi
- Reinicio automático (`unless-stopped`)

---

## 📁 docker-compose.yml

```yaml
services:

  rpi-monitor:
    image: ikaritw/rpi-monitor:latest
    container_name: rpi-monitor
    ports:
      - "8888:8888"
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /opt/vc:/opt/vc
      - /boot:/boot
      - /sys:/dockerhost/sys:ro
      - /etc:/dockerhost/etc:ro
      - /proc:/dockerhost/proc:ro
      - /usr/lib:/dockerhost/usr/lib:ro
      - /stat:/var/lib/rpimonitor/stat:rw
      - /lib/modules:/dockerhost/lib/modules:ro
    devices:
      - "/dev/vchiq:/dev/vchiq"
      - "/dev/vcio:/dev/vcio"
    restart: unless-stopped
```

---

## 🔧 Volúmenes y acceso al sistema

Este contenedor necesita acceso a múltiples rutas del sistema para obtener métricas reales:

| Ruta | Uso |
|-----|-----|
| `/proc` | Información de procesos |
| `/sys` | Información del kernel |
| `/boot` | Configuración del sistema |
| `/opt/vc` | Librerías GPU (Raspberry Pi) |
| `/lib/modules` | Información del kernel |
| `/stat` | Persistencia de estadísticas |

---

## 🔌 Dispositivos

| Dispositivo | Uso |
|------------|-----|
| `/dev/vchiq` | Acceso GPU |
| `/dev/vcio` | Información del sistema |

---

## 🌐 Acceso a la interfaz web

http://TU-IP:8888

---

## ▶️ Puesta en marcha

docker compose up -d

---

## 🛑 Detener el contenedor

docker compose down

---

## 🔄 Actualizar RPi-Monitor

docker compose pull
docker compose up -d

---

## ⚠️ Consideraciones

- Este contenedor requiere acceso profundo al sistema host
- No recomendado exponer directamente a Internet
- Ideal para uso en Raspberry Pi o entornos homelab
- Puede ejecutarse detrás de un reverse proxy para mayor seguridad

---

## 🏠 Uso recomendado

- Monitorización de Raspberry Pi
- Homelabs
- Servidores domésticos
- Diagnóstico de rendimiento

---

