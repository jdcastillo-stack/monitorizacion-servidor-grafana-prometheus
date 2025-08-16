# 📡 Monitorización de red con Raspberry Pi 4, Grafana y Prometheus

## 📋 Resumen del proyecto

Servidor de monitoreo en Raspberry Pi 4 para visualizar métricas de red y dispositivos conectados usando **Grafana** y **Prometheus**.
Permite recolectar, almacenar y visualizar métricas en tiempo real sobre el rendimiento de la red y los dispositivos, con paneles personalizados y alertas automáticas.

---

## 🎯 Objetivos

* Instalar y configurar software de monitoreo en Linux.
* Aprender a usar contenedores con Docker y Docker Compose.
* Configurar Prometheus para recolectar métricas desde tu Raspberry Pi y otros dispositivos de la red.
* Diseñar dashboards en Grafana para visualización y alertas.
* Configurar notificaciones automáticas (por correo o Telegram).

---

## 🛠 Requerimientos

### Hardware

* Raspberry Pi 4 (mínimo 2GB RAM recomendados)
* Tarjeta microSD (32 GB o más)
* Fuente de alimentación para Raspberry Pi
* Cable Ethernet o conexión WiFi

### Software

* Raspberry Pi OS (Lite o Desktop)
* Docker y Docker Compose
* Prometheus
* Grafana
* Exporters (Node Exporter, Blackbox Exporter, SNMP Exporter)

### Conexión de red

* Acceso a la red local para monitorear otros dispositivos.
* Conexión a Internet para recibir alertas externas.

---

## 🚀 Instalación paso a paso
📌 Fase 1 – Preparación del entorno

Objetivo:
Dejar el Raspberry Pi 4 listo para iniciar la instalación de las herramientas de monitoreo.

Pasos:

Verificar acceso por SSH

Confirmar que puedes conectarte al Raspberry Pi desde tu computadora mediante SSH.

Actualizar el sistema operativo

sudo apt update && sudo apt upgrade -y


Configurar una IP fija

Esto garantiza que Prometheus y Grafana siempre estén disponibles en la misma dirección IP.

Puedes hacerlo editando el archivo de configuración de red (dhcpcd.conf) o usando nmcli si usas NetworkManager.

Comprobar la conexión a Internet

Ejecuta un ping de prueba:

ping -c 4 google.com


Resultado esperado:
El Raspberry Pi queda actualizado, con IP fija y acceso SSH estable, listo para instalar el entorno de monitoreo.

1. **Instalar Docker y Docker Compose**

   ```bash
   sudo apt update && sudo apt upgrade -y
   curl -sSL https://get.docker.com | sh
   sudo usermod -aG docker $USER
   sudo apt install docker-compose -y
   ```

2. **Crear archivo `docker-compose.yml`**

   ```yaml
   version: '3'
   services:
     prometheus:
       image: prom/prometheus
       ports:
         - "9090:9090"
       volumes:
         - ./prometheus.yml:/etc/prometheus/prometheus.yml
     grafana:
       image: grafana/grafana
       ports:
         - "3000:3000"
   ```

3. **Configurar Prometheus**

   * Añadir `node_exporter`, `blackbox_exporter` y `snmp_exporter` en el archivo `prometheus.yml`.

4. **Levantar los servicios**

   ```bash
   docker-compose up -d
   ```

5. **Acceder a Grafana**

   * URL: `http://<IP_Raspberry>:3000`
   * Usuario y contraseña por defecto: `admin / admin`

---

## 📊 Configuración de métricas

* **Node Exporter**: Uso de CPU, memoria, disco, tráfico de red.
* **Blackbox Exporter**: Disponibilidad y latencia de dispositivos o sitios web.
* **SNMP Exporter**: Información de routers, switches y otros equipos compatibles.

---

## 📈 Creación de dashboards en Grafana

1. Añadir Prometheus como fuente de datos.
2. Crear paneles con:

   * Uso de CPU y RAM
   * Latencia y disponibilidad
   * Tráfico de red
3. Configurar alertas para:

   * CPU > 90%
   * Poco espacio en disco
   * Dispositivo desconectado

---

## 📷 Resultados

*(Añadir aquí capturas de pantalla y ejemplos reales)*

* Dashboard principal
* Ejemplo de alerta por CPU alta
* Gráfico de ancho de banda

---

## 📌 Conclusiones

* Aprendí a instalar y configurar Prometheus y Grafana en un entorno Linux (Raspberry Pi OS).
* Practiqué administración de servicios en contenedores con Docker y Docker Compose.
* Este sistema puede escalarse para empresas pequeñas y medianas.
* **Mejoras futuras**:

  * Integrar alertas vía Slack.
  * Añadir monitoreo de logs.
  * Automatizar backups de configuraciones.

---

## 👤 Autor

**Juan David Castillo Castillo**

📄 Licencia: [MIT](LICENSE)

---

