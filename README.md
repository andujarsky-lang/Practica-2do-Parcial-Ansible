# 🚀 Automatización y Gestión de Servidores Linux con Docker y Ansible

## 📌 Descripción del proyecto y objetivo de la práctica

Este proyecto corresponde a una práctica integral de laboratorio enfocada en la implementación de infraestructura automatizada, gestión de configuraciones y orquestación de sistemas.

**Objetivo principal:**
Crear y aprovisionar un entorno de laboratorio compuesto por dos servidores virtuales basados en Ubuntu 24.04 utilizando contenedores de Docker, para posteriormente administrarlos de manera centralizada, eficiente y sin intervención manual mediante Ansible.

**Alcance técnico:**

- **Orquestación:** Despliegue de dos contenedores con Docker Compose, corriendo en segundo plano.
- **Conexión sin agentes:** Ansible se conecta directo a los contenedores (`ansible_connection=docker`), sin necesidad de SSH.
- **Aprovisionamiento (Playbook):** Un playbook en YAML que recopila datos del sistema (*facts*), crea directorios y archivos, usa *loops* y una condicional (`when: ansible_distribution == 'Ubuntu'`).

---

## 📖 Glosario de Conceptos Fundamentales

- **Ansible:** Herramienta que automatiza la configuración y administración de varios servidores, sin necesidad de instalar agentes en ellos.
- **Docker:** Plataforma que empaqueta aplicaciones y sus dependencias en contenedores ligeros y aislados.
- **Docker Compose:** Herramienta para levantar varios contenedores a la vez usando un solo archivo YAML.
- **Playbook:** Archivo YAML con la lista de tareas que Ansible ejecuta en los servidores.
- **Inventario:** Archivo que lista los servidores administrados por Ansible y cómo conectarse a ellos.
- **Módulo de Ansible:** Pieza de código que ejecuta una acción específica (crear archivos, instalar paquetes, etc.).

---

## 🛠️ Tecnologías y Herramientas Utilizadas

- **Ansible:** Motor principal de automatización y orquestación utilizado para configurar y administrar los servidores.
- **Docker & Docker Compose:** Plataforma y herramienta de contenedores empleadas para simular el parque de servidores virtuales de prueba.
- **Ubuntu 24.04:** Distribución de Linux utilizada como imagen base para los contenedores del laboratorio.
- **Git & GitHub:** Sistema de control de versiones y plataforma en la nube utilizados para almacenar, versionar y entregar el repositorio del proyecto.

---

## 📂 Estructura del Proyecto

```text
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

---

## 🚀 Instrucciones de Instalación y Ejecución del Laboratorio

### Paso 1: Iniciar los servidores Docker

Sitúate en la carpeta raíz del proyecto (`ansible-lab`) y levanta la infraestructura definida en `docker-compose.yml`:

```bash
docker compose up -d
```

### Paso 2: Verificar que los contenedores están en ejecución

```bash
docker ps
```

Deberías ver `server1` y `server2` listados con estado `Up`.

### Paso 3: Instalar Python en cada contenedor

Ansible necesita un intérprete de Python en los nodos administrados para poder ejecutar sus módulos, por lo que se instala manualmente en cada contenedor:

```bash
docker exec -it server1 bash
apt update
apt install -y python3
exit
```

```bash
docker exec -it server2 bash
apt update
apt install -y python3
exit
```

### Paso 4: Comprobar la conectividad con Ansible

Con el archivo `inventory.ini` ya configurado, se valida que Ansible pueda comunicarse con ambos nodos:

```bash
ansible docker -i inventory.ini -m ping
```

Una respuesta `pong` en ambos servidores confirma que la conexión fue exitosa.

### Paso 5: Ejecutar el Playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

---

## 📋 Tareas Automatizadas por el Playbook

El archivo `playbook.yml` ejecuta, sobre ambos servidores, la siguiente secuencia de tareas:

1. **Mostrar el nombre del host** de cada servidor mediante los *facts* recopilados por Ansible.
2. **Mostrar el sistema operativo** y su versión (`ansible_distribution`, `ansible_distribution_version`).
3. **Crear el directorio** `/tmp/ansible-demo` en cada nodo.
4. **Crear el archivo** `info.txt` dentro de dicho directorio.
5. **Escribir en el archivo** el nombre del servidor y el sistema operativo detectado.
6. **Crear, mediante un loop**, los subdirectorios `logs`, `backup` y `config` dentro de `/tmp/ansible-demo`.
7. **Mostrar un mensaje condicional**, únicamente cuando el sistema operativo detectado sea Ubuntu (`when: ansible_distribution == 'Ubuntu'`).

---

## 📸 Evidencia de Ejecución

A continuación se presenta una captura de pantalla que evidencia la ejecución exitosa del playbook sobre ambos servidores, mostrando el resultado `ok` / `changed` de cada tarea y la ausencia de errores (`failed=0`) al finalizar el `PLAY RECAP`.

<!-- Inserta aquí la captura de pantalla de la ejecución del playbook -->


<img width="1600" height="844" alt="playbook_success" src="https://github.com/user-attachments/assets/bc10a1c3-65c3-4915-bc77-b5d5c7ba57f4" />

---

## 🎯 Resultados y Aprendizajes

- Se logró levantar un entorno de laboratorio reproducible utilizando Docker Compose, sin necesidad de máquinas virtuales completas.
- Se comprobó la viabilidad de administrar contenedores como si fueran servidores remotos, usando el conector nativo `ansible_connection=docker`, sin configurar SSH.
- Se aplicaron conceptos clave de Ansible como *facts*, *loops*, módulos de archivos (`file`, `copy`/`lineinfile`) y condicionales (`when`), reforzando el flujo de trabajo declarativo característico de la automatización de infraestructura (IaC).

---

## 👤 Autor

Sky Luisahania Andujar Victorino
