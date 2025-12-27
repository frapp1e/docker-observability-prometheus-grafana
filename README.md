# Docker Observability Stack (Prometheus + Grafana)

Proyecto de **observabilidad en entorno de producción simulado** basado en Docker Compose, orientado a la monitorización de **host y contenedores** con Prometheus y Grafana.

Este proyecto no es una demo básica: incluye **resolución de problemas reales**, compatibilidad de métricas y validación completa de targets.

---

## 🧱 Arquitectura

* **Docker Compose** como orquestador
* **Prometheus** como sistema de métricas
* **Grafana** para visualización
* **Node Exporter** para métricas del host
* **cAdvisor** para métricas de contenedores

Todos los servicios se comunican mediante una red bridge dedicada (`observability`).

---

## 📊 Qué se monitoriza

### Host (Node Exporter)

* CPU usage
* RAM
* Disk I/O y filesystem
* Network traffic

### Contenedores (cAdvisor)

* CPU por contenedor
* Memoria por contenedor
* Network RX/TX
* Estado de contenedores

---

## 📈 Dashboards usados (compatibles)

> ⚠️ Se descartaron dashboards antiguos por incompatibilidad de métricas (*NO DATA*).

* **Node Exporter Full** → ID **1860**
* **Docker / cAdvisor** → ID **19792**

Ambos dashboards funcionan correctamente con las versiones actuales de Prometheus y cAdvisor.

---

## ✅ Validaciones realizadas

* Todos los **targets en Prometheus aparecen UP**
* Scraping correcto de:

  * `prometheus:9090`
  * `node-exporter:9100`
  * `cadvisor:8080`
* Datasource de Grafana validado contra Prometheus en red Docker

---

## 🛠️ Problemas reales resueltos

* Conflicto de puertos con otro Prometheus activo
* Dashboards obsoletos mostrando *NO DATA*
* Datasource apuntando erróneamente a `localhost` en lugar de red Docker
* Falta de utilidades en contenedor Prometheus (debug de red)

Este troubleshooting forma parte clave del proyecto.

---

## 🚀 Puesta en marcha

```bash
# Levantar el stack
docker compose up -d

# Ver targets en Prometheus
http://localhost:9091/targets

# Acceder a Grafana
http://localhost:3001
```

Credenciales por defecto:

* **User:** admin
* **Password:** admin

---

## 📂 Estructura del proyecto

```text
.
├── docker-compose.yml
├── prometheus/
│   └── prometheus.yml
├── volumes/
│   ├── grafana_data/
│   └── prometheus_data/
└── README.md
```

---

## 🎯 Objetivo del proyecto

Simular un **entorno real de observabilidad en producción**, aplicando buenas prácticas de:

* Monitorización
* Networking en Docker
* Diagnóstico de errores
* Visualización de métricas

Proyecto orientado a perfiles **Sysadmin / Linux / DevOps / SRE**.

---

## 📌 Próximo paso

Integración de **Alertmanager** con alertas reales y automatización de respuesta mediante scripts Bash y systemd.
