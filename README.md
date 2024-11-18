# Trabajo Práctico Final: Mundose - DevOps - Grupo 13

## Descripción General

Este proyecto implementa un clúster local de Kubernetes con **Minikube**, integrado con herramientas de monitoreo y visualización como **Prometheus** y **Grafana**, y gestionado mediante un pipeline automatizado utilizando **Jenkins**. La configuración permite recolectar métricas de servicios y nodos para su análisis.

## Arquitectura del Proyecto

![Arquitectura del Proyecto](https://raw.githubusercontent.com/berellajuan/PIN-DevOps-Final-Grupo13/e176f6902b771a8a08b77fa62e10c4577cc85be6/arquitectura/arquitectura-pin-final-mundose.svg)

## Herramientas Utilizadas

- **Minikube:** Para ejecutar un clúster de Kubernetes local.
- **Docker:** Para crear y gestionar contenedores.
- **Jenkins:** Como servidor CI/CD, configurado para interactuar con Minikube y Docker.
- **GitHub:** Repositorio utilizado por Jenkins para obtener las definiciones de los pipelines y despliegues.
- **Prometheus:** Herramienta para la recolección de métricas.
    - **URL Interna**: http://prometheus.monitoreo.svc.cluster.local:9090/services/prometheus
    - **URL Externa**: http://dev-env.grupo13.com/services/prometheus
- **Grafana:** Plataforma para la visualización de métricas.
    - **Dashboard**: Node Exporter Full - ID **1860**
    - **URL Externa**: http://dev-env.grupo13.com/services/grafana

## Pasos Realizados

1. **Configuración del Clúster Local**
   - Levanté un clúster de Minikube local.
   - Configuré la IP del clúster para resolver el dominio `dev-env.grupo13.com`.

2. **Configuración de Jenkins**
   - Instalé y configuré Jenkins en mi máquina local.
   - Instalé los plugins necesarios para trabajar con Docker y Kubernetes.
   - Conecté Jenkins a:
     - El clúster local de Minikube.
     - Mi repositorio en GitHub, que contiene las definiciones de los pipelines.

3. **Ejecución de Pipelines**
   - **`deploy-nginx-exporter-cluster-pin-final-mundose`:**  
     Desplegó el contenedor **NGINX Exporter** en el clúster para recolectar métricas de NGINX.
   - **`prometheus-cluster-monitoreo-pin-final-mundose`:**  
     Desplegó Prometheus en el namespace `monitoreo` para recolectar métricas de los pods y servicios. Este pipeline también desplegó **Node Exporter** para obtener métricas del nodo.
   - **`grafana-cluster-monitoreo-pin-final-mundose`:**  
     Desplegó Grafana en el namespace `monitoreo` y configuró la conexión con Prometheus.

4. **Verificación de Prometheus**
   - Verifiqué que Prometheus recolectara métricas de los pods y servicios del clúster.

5. **Configuración de Grafana**
   - Configuré Grafana para exponer su interfaz en la URL `http://dev-env.grupo13.com/services/grafana`.
   - Importé los dashboards necesarios para visualizar las métricas recolectadas.
