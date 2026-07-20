# 🚀 Automatización y Gestión de Servidores Linux con Docker y Ansible

## 📌 Descripción del proyecto y objetivo de la práctica

Este proyecto corresponde a una práctica integral de laboratorio enfocada en la implementación de infraestructura automatizada, gestión de configuraciones y orquestación de sistemas. 

### Objetivo principal:
Crear y aprovisionar un entorno de laboratorio compuesto por dos servidores virtuales basados en **Ubuntu 24.04** utilizando contenedores de **Docker**, para posteriormente administrarlos de manera centralizada, eficiente y sin intervención manual mediante **Ansible**.

### Alcance técnico detallado de la práctica:
* **Orquestación de Entornos:** Despliegue simultáneo de múltiples contenedores aislados mediante **Docker Compose**, asegurando su ejecución continua en segundo plano.
* **Conectividad sin agentes (Agentless):** Configuración del inventario de Ansible empleando el controlador de conexión directo a Docker (`ansible_connection=docker`), lo cual evita la complejidad de configurar demonios SSH o credenciales de acceso tradicionales en los nodos administrados.
* **Aprovisionamiento automatizado (Playbook):** Desarrollo de un flujo de tareas estructurado en YAML que recopila de forma dinámica los hechos del sistema (*facts*), despliega jerarquías de directorios mediante bucles (*loops*), manipula archivos de texto plano inyectando variables del sistema operativo y evalúa sentencias condicionales avanzadas basadas en el tipo de distribución (`when: ansible_distribution == 'Ubuntu'`).

---

## 📖 Glosario de Conceptos Fundamentales

* **Ansible:** Herramienta de automatización de TI de código abierto que maneja la gestión de configuraciones, el despliegue de aplicaciones y la orquestación de tareas en múltiples servidores de manera declarativa y sin necesidad de instalar agentes permanentes en los destinos.
* **Docker:** Plataforma de contenedores que permite empaquetar aplicaciones, entornos y sus dependencias en unidades aisladas llamadas contenedores, ejecutándose de forma ligera sobre el núcleo del sistema operativo host.
* **Docker Compose:** Herramienta de orquestación diseñada para definir, configurar y ejecutar aplicaciones Docker multi-contenedor utilizando un único archivo declarativo en formato YAML.
* **Playbook:** Archivo estructurado en formato YAML donde se define una serie de tareas secuenciales y declarativas que Ansible ejecutará en los servidores especificados en el inventario.
* **Inventario (Inventory):** Archivo de configuración centralizado que lista los servidores o nodos administrados por Ansible, permitiendo agruparlos y asignarles parámetros de conexión y variables personalizadas.
* **Módulo de Ansible:** Unidades de código reutilizables e independientes ejecutadas por Ansible en los nodos remotos para realizar acciones específicas (por ejemplo, gestión de archivos, control de paquetes o despliegue de contenido).

---

## 🛠️ Tecnologías y Herramientas Utilizadas

* **Ansible:** Motor principal de automatización y orquestación utilizado para configurar y administrar los servidores.
* **Docker & Docker Compose:** Plataforma y herramienta de contenedores empleadas para simular el parque de servidores virtuales de prueba.
* **Ubuntu (24.04):** Distribución avanzada de Linux utilizada como imagen base para los contenedores del laboratorio.
* **Git & GitHub:** Sistema de control de versiones y plataforma en la nube utilizados para almacenar, versionar y entregar el repositorio del proyecto.

---

## 📂 Estructura del Proyecto

ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md

---

## 🚀 Instrucciones de Instalación y Ejecución del Laboratorio

### Paso 1: Iniciar los servidores Docker
Para levantar la infraestructura de contenedores definida en el archivo de orquestación en segundo plano, sitúate en la carpeta raíz del proyecto (`ansible-lab`) y ejecuta el siguiente comando:

```bash
docker compose up -d
