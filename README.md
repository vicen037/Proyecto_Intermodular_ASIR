# NexusGuard: Infraestructura de Virtualización y Monitorización Automatizada para Pymes

[![Proxmox](https://img.shields.io/badge/Proxmox_VE-8.x-E57000?style=for-the-badge&logo=proxmox&logoColor=white)](https://www.proxmox.com/)
[![Debian](https://img.shields.io/badge/Debian-12_Bookworm-A81D33?style=for-the-badge&logo=debian&logoColor=white)](https://www.debian.org/)
[![VMware](https://img.shields.io/badge/VMware-Workstation_Pro-607078?style=for-the-badge&logo=vmware&logoColor=white)](https://www.vmware.com/)
[![Bash](https://img.shields.io/badge/GNU_Bash-5.2+-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Apache](https://img.shields.io/badge/Apache-2.4-D22128?style=for-the-badge&logo=apache&logoColor=white)](https://httpd.apache.org/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com/)

> **Memoria Técnica del Proyecto Intermodular — Ciclo Formativo de Grado Superior en ASIR**  
> **Centro Educativo:** I.E.S. Ribera del Tajo (Talavera de la Reina)  
> **Autor:** Vicente Caballero Gómez  
> **Curso Académico:** 2025–2026  

---

## 1. Introducción y Contexto del Proyecto

### 1.1. Justificación y Problemática

En el ecosistema tecnológico de las Pequeñas y Medianas Empresas (Pymes), la gestión de infraestructuras TI se enfrenta a dos dificultades recurrentes:

1. **Dispersión de Servidores (*Server Sprawl*):** Ineficiencia provocada por mantener servidores físicos independientes para cargas aisladas (servidores de ficheros, plataformas web, bases de datos), multiplicando el coste de hardware, el consumo eléctrico y las incidencias de mantenimiento.
2. **Opacidad y Carencia de Monitorización Proactiva:** Falta de telemetría en tiempo real sobre el estado de carga y salud de las máquinas, recurriendo comúnmente a soluciones privativas sobredimensionadas y complejas de licenciar.

### 1.2. Solución Propuesta: NexusGuard

NexusGuard soluciona estas deficiencias consolidando los servicios bajo una arquitectura de virtualización anidada (*Nested Virtualization*).

Mediante un único equipo anfitrión robusto, se despliega el hipervisor bare-metal de tipo 1 **Proxmox Virtual Environment (PVE)** sobre el que se orquestan **contenedores LXC de alta densidad y bajo consumo**. Para garantizar la supervisión autónoma del entorno sin instalar suites pesadas de terceros, el proyecto incorpora un motor nativo de telemetría y respaldos programados en **Bash**, complementado con un **panel web responsivo en Bootstrap 5** que muestra el estado operativo en tiempo real.

---

## 2. Marco Formativo e Integración Curricular (ASIR)

NexusGuard está diseñado como un proyecto transversal que integra de forma progresiva las competencias adquiridas en el ciclo formativo de Administración de Sistemas Informáticos en Red:

### 2.1. Fase 1: Módulos de 1.º Curso (Implementación Base)

- **Implantación de Sistemas Operativos (ISO):**
  - Desarrollo de automatismos en Bash para la extracción de métricas de rendimiento del sistema operativo.
  - Planificación desatendida mediante el demonio Cron (muestreo periódico y rotación de copias).
  - Gestión lógica de almacenamiento mediante volúmenes LVM y particionado dinámico.
  - Bastionado básico del servicio de administración remota SSH y políticas de privilegios.
- **Lenguajes de Marcas y Sistemas de Gestión de Información (LMSGI):**
  - Maquetación y estructura semántica del panel de telemetría mediante HTML5.
  - Implementación de hojas de estilo responsivas mediante el framework Bootstrap 5 en modo oscuro.
  - Inyección dinámica de variables de sistema en plantillas web mediante bloques *Here Document*.
- **Fundamentos de Hardware (FHW):**
  - Configuración y habilitación de extensiones de virtualización por hardware (Intel VT-x / AMD-V).
  - Dimensionamiento técnico del entorno (cálculo de vCPUs, distribución de memoria RAM y almacenamiento LVM-Thin).

### 2.2. Fase 2: Módulos de 2.º Curso (Expansión Avanzada)

- **Seguridad y Alta Disponibilidad (SAD):**
  - Bastionado exhaustivo de sistemas, auditoría de puertos y mitigación de vectores de ataque.
  - Creación de túneles VPN cifrados con WireGuard para administración remota segura de la infraestructura.
  - Configuración de clústeres de alta disponibilidad (HA) con Proxmox y políticas de recuperación ante desastres (*Disaster Recovery Plans*).
  - Monitorización de eventos de seguridad y prevención de intrusiones (IDS/IPS con Suricata/Fail2ban).
- **Servicios de Red e Internet (SRI):**
  - Despliegue de servicios perimetrales de resolución y filtrado DNS con Pi-Hole (*DNS Sinkhole*).
  - Configuración de servidores proxy inversos (Nginx/HAProxy) con balanceo de carga y terminación SSL/TLS segura (HTTPS).
  - Segmentación de redes mediante VLANs virtuales y zonas desmilitarizadas (DMZ) para aislar servicios públicos de datos internos.
- **Administración de Sistemas Gestores de Bases de Datos (ASGBD / GBD):**
  - Sustitución de los datos planos en ficheros estáticos por motores relacionales como MariaDB o PostgreSQL.
  - Modelado de bases de datos para registro histórico de telemetría, consultas agregadas y métricas cronológicas.
  - Automatización de respaldos lógicos de bases de datos y políticas de integridad referencial.
- **Implantación de Aplicaciones Web (IAW):**
  - Evolución del servidor Apache estático hacia una arquitectura LAMP/LEMP dinámica.
  - Desarrollo de una API REST de telemetría en backend (Python/PHP) para desacoplar datos de la capa visual.
  - Integración de paneles web dinámicos avanzados con gráficos interactivos temporales (Chart.js / Grafana).
- **Empresa e Iniciativa Emprendedora (EIE):**
  - Estudio de viabilidad técnica y financiera para la implantación de NexusGuard en empresas reales.
  - Análisis comparativo de costes totales de propiedad (TCO) y retorno de inversión (ROI) frente a servidores tradicionales.

---

## 3. Arquitectura y Topología del Sistema

### 3.1. Modelo Jerárquico de Virtualización Anidada

El diseño implementa una estructura en tres niveles técnicos:

1. **Capa Anfitrión (Host Físico):** Estación base ejecutando VMware Workstation Pro como hipervisor de Tipo 2, exponiendo directamente las instrucciones del procesador físico.
2. **Capa de Control (Hipervisor PVE):** Nodo virtualizado ejecutando Proxmox VE 8 (Debian 12 Bookworm) como hipervisor bare-metal de Tipo 1.
3. **Capa de Cargas de Trabajo (Contenedores LXC):** Entornos de ejecución aislados a nivel de kernel, proporcionando arranque instantáneo y un coste de memoria base inferior a 50 MB por servicio.

### 3.2. Topología de Red y Enrutamiento (Subred `192.168.100.0/24`)

El laboratorio se estructura en una subred privada Clase C bajo un esquema de direccionamiento estático:

| Nodo / Elemento | Interfaz Lógica | Dirección IPv4 | Máscara | Puerta de Enlace | Función en la Infraestructura |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VMware Virtual Switch** | `VMnet8 (NAT)` | `192.168.100.1` | `/24` | N/A | Conmutador de la red privada virtual |
| **Router Virtual VMware** | Interno NAT | `192.168.100.2` | `/24` | Red Externa | Enrutamiento e intercomunicación a Internet |
| **Proxmox VE (Host)** | `vmbr0` (Bridge) | `192.168.100.10` | `/24` | `192.168.100.2` | Panel Web de gestión PVE (HTTPS `:8006`) |
| **Servidor Web LXC (CT 100)** | `eth0` (veth) | `192.168.100.20` | `/24` | `192.168.100.2` | Dashboard HTTP (`:80`) y servicios locales |

El mecanismo de enlace interno se apoya en el **Linux Bridge (`vmbr0`)**, el cual actúa funcionalmente como un conmutador de capa 2 en el kernel de Linux. Al iniciar el contenedor LXC, Proxmox vincula un par de interfaces virtuales (`veth`) al puente, permitiendo que el tráfico del servidor web circule directamente por la red del laboratorio como si estuviese conectado físicamente.

---

## 4. Dimensionamiento y Parámetros de Hardware

### 4.1. Nodo Maestro (Proxmox Virtual Environment)

- **Hipervisor Host:** VMware Workstation Pro con asistente de instalación avanzada.
- **Sistema Operativo Guest:** Debian 12.x 64-bit (Debian Bookworm).
- **Procesador:** 1 Socket asignado con 6 núcleos dedicados, con aceleración anidada habilitada (`VT-x/EPT` o `AMD-V/RVI`) y contadores de rendimiento de CPU activos para peritaje de carga.
- **Memoria RAM:** 16 GB DDR4 asignados estáticamente para permitir la futura integración de servicios pesados en fases posteriores (VPN, Bases de Datos, DNS).
- **Almacenamiento:** Disco virtual SCSI/NVMe de 100 GB en aprovisionamiento fino (*Thin Provisioning*), distribuido bajo esquema LVM:
  - Volumen raíz (`pve/root`): Espacio ext4 para el sistema operativo Debian, librerías y utilidades base (~25 GB).
  - Área de intercambio (`swap`): Partición de 8 GB para absorción de picos de carga.
  - Almacenamiento dinámico (`pve/data`): LVM-Thin dedicado al almacenamiento de volúmenes virtuales y discos de contenedores (~42 GB).

### 4.2. Contenedor del Panel de Control (LXC CT 100)

- **Imagen Base:** Plantilla oficial mínima `debian-12-standard`.
- **Capacidad de Cómputo:** 1 núcleo de CPU.
- **Memoria Operativa:** 1024 MB de memoria RAM con 512 MB de swap adicional.
- **Volumen de Almacenamiento:** 8 GB aprovisionados en el grupo de volúmenes lógicos locales (`local-lvm`).

---

## 5. Diseño del Flujo de Automatización y Servicios

### 5.1. Repositorios y Preparación de Proxmox

Para adecuar el nodo a un entorno académico sin suscripción de pago comercial, el sistema se desacopla del repositorio empresarial restrictivo y se conecta a la rama comunitaria `pve-no-subscription`. Con ello se garantiza la recepción de parches de seguridad del kernel y paquetes actualizados del entorno de virtualización sin coste de licenciamiento.

### 5.2. Aprovisionamiento Web y Bastionado (Hardening)

- **Servidor Web:** El contenedor aloja una instancia de Apache2 optimizada para servir ficheros web estáticos de forma ultrarrápida.
- **Seguridad en Acceso Remoto:** Conforme a las normas de seguridad de administración de sistemas, se deshabilita el inicio de sesión directo para la cuenta de superusuario (`root`) a través de SSH, restringiendo el acceso exclusivamente a usuarios administradores autenticados con pertenencia al grupo `sudo`, al tiempo que se desactiva el reenvío de interfaces gráficas X11 para minimizar la superficie de exposición.

### 5.3. Motor de Telemetría Dinámica

El script de monitorización funciona como un motor extractivo autónomo:

1. **Recolección en tiempo real:** Inspecciona las estructuras de datos y comandos del sistema operativo (`top`, `free`, `df`, `uptime`) para cuantificar la carga porcentual del procesador, el desglose de memoria RAM utilizada y disponible, el espacio ocupado en la partición raíz y el tiempo transcurrido desde el último arranque.
2. **Generación de la Interfaz:** Transforma los valores recolectados inyectándolos directamente sobre una plantilla HTML5/CSS estructurada con componentes de Bootstrap 5 en modo oscuro y acentos neón, depositando el documento final en el directorio de publicación del servidor HTTP.
3. **Planificación:** El proceso es invocado de forma recurrente cada sesenta segundos a través del programador del sistema Cron, garantizando la actualización continua de la información.

### 5.4. Política de Copias de Seguridad y Resiliencia

La continuidad de servicio y la preservación del panel web se apoya en un sistema automatizado de respaldos:

- **Compresión y Empaquetado:** Rutina diaria que genera archivos comprimidos (tarballs `.tar.gz`) con la información íntegra del sitio web, etiquetados con marcas de tiempo cronológicas precisas.
- **Regla de Retención de 7 Días:** Depuración automática de cualquier archivo de respaldo que supere una semana de antigüedad, preservando la capacidad disponible en disco.
- **Auditoría:** Registro centralizado de cada operación completada en los ficheros de log del sistema.
- **Programación:** Ejecución desatendida programada diariamente durante la ventana horaria de menor actividad operativa (02:00 AM).

---

## 6. Validación Técnica y Pruebas de Contingencia

La estabilidad y el comportamiento de la infraestructura fueron evaluados mediante una batería de pruebas de campo:

### 6.1. Prueba de Enrutamiento y Latencia de Red

- **Objetivo:** Verificar la integridad de la conmutación entre el equipo físico anfitrión y el contenedor LXC a través del puente de red `vmbr0`.
- **Metodología:** Envío sostenido de paquetes de diagnóstico ICMP.
- **Resultado:** Ausencia absoluta de pérdida de paquetes y latencia constante por debajo de 1 milisegundo, confirmando la inexistencia de saturación o retardos en la capa de enlace virtualizada.

### 6.2. Prueba de Estrés de CPU y Validación de Telemetría

- **Objetivo:** Confirmar que el motor de recolección lee métricas reales y que el ciclo de actualización de Cron opera con precisión temporal.
- **Metodología:** Inyección artificial de carga forzada en el contenedor mediante software de estrés de cómputo durante noventa segundos.
- **Resultado:** El panel reflejó un incremento instantáneo de uso desde un valor en reposo (~2%) hasta un **99% de ocupación de procesador** al cumplirse la ventana del minuto programado, regresando de forma natural a valores mínimos una vez finalizada la simulación de carga.

### 6.3. Prueba de Restauración y Recuperación ante Desastres (*Disaster Recovery*)

- **Objetivo:** Medir el tiempo de recuperación del servicio ante un borrado accidental o sabotaje del servidor web.
- **Metodología:** Eliminación intencionada de todos los datos alojados en el directorio de Apache provocando la caída del servicio a error HTTP 404, seguida del despliegue del último respaldo empaquetado disponible.
- **Resultado:** Restablecimiento íntegro del portal y de los ficheros de servicio en un intervalo inferior a **3 segundos**, sin necesidad de reiniciar el contenedor ni reconfigurar el servidor web.

### 6.4. Contingencia de Infraestructura

- **Instantáneas (*Snapshots*) de VMware:** Punto de restauración integral del hipervisor Proxmox para revertir fallos derivados de cambios mayores de configuración o actualizaciones fallidas del núcleo.
- **Copias de Seguridad VZDump:** Herramienta nativa de Proxmox para salvaguardar la totalidad del contenedor LXC (incluyendo configuración lógica, interfaz de red y volúmenes LVM) para su reinstanciación inmediata.

---

## 7. Plan de Expansión y Líneas Futuras (Fase 2 - Segundo Curso ASIR)

La arquitectura modular de NexusGuard ha sido dimensionada técnicamente para incorporar de forma progresiva los servicios avanzados correspondientes a los módulos de segundo curso:

### 7.1. Seguridad y Alta Disponibilidad (SAD)

- **Túneles VPN Criptográficos con WireGuard:** Configuración de un servidor VPN en el hipervisor con cifrado simétrico/asimétrico ChaCha20-Poly1305. Permitirá la conexión externa cifrada de administradores móviles hacia la red `192.168.100.0/24` sin exponer puertos web a Internet.
- **Alta Disponibilidad y Clúster Proxmox (HA):** Proyección para añadir un segundo nodo de virtualización y un testigo de cuórum (*qdevice*), permitiendo la migración en caliente de contenedores y la conmutación automática ante caída de hardware.
- **Sistemas de Detección de Intrusos (IDS/IPS):** Despliegue de agentes de detección basados en firmas y comportamiento (Suricata y Fail2ban) para bloquear intentos de fuerza bruta y ataques perimetrales.

### 7.2. Servicios de Red e Internet (SRI)

- **Filtrado Perimetral y DNS Sinkhole con Pi-Hole:** Instanciación de un nuevo contenedor LXC que asuma la función de servidor DNS local corporativo, interceptando consultas maliciosas, bloqueando dominios de telemetría y reduciendo el consumo de ancho de banda.
- **Proxy Inverso con Terminación SSL/TLS:** Despliegue de un proxy inverso (Nginx o HAProxy) como punto de entrada único para cifrar el tráfico mediante HTTPS y balancear peticiones hacia los distintos servicios internos.
- **Segmentación de Red y Zonas Desmilitarizadas (DMZ):** Creación de bridges virtuales adicionales (`vmbr1`, `vmbr2`) para segmentar el tráfico entre la zona de servicios expuestos, la red de gestión administrativa y la zona de bases de datos.

### 7.3. Administración de Sistemas Gestores de Bases de Datos (ASGBD / GBD)

- **Migración a Base de Datos Relacional:** Despliegue de un contenedor específico con MariaDB o PostgreSQL dedicado al almacenamiento persistente.
- **Registro Histórico de Telemetría:** Sustitución de los datos planos volátiles por un esquema estructurado que archive muestras históricas de uso de CPU, RAM, almacenamiento y tiempos de actividad.
- **Planes de Copias de Seguridad Lógicas:** Rutinas automatizadas de volcado y exportación de esquemas con retención histórica y verificación de integridad.

### 7.4. Implantación de Aplicaciones Web (IAW)

- **Evolución a Arquitectura Dinámica:** Transformación del servidor web estático en una pila dinámica LAMP/LEMP.
- **Desarrollo de API de Telemetría:** Creación de endpoints que sirvan los datos de telemetría en formato estructurado (JSON) mediante un backend en Python o PHP.
- **Cuadros de Mando Interactivos:** Sustitución del panel HTML estático por un dashboard interactivo alimentado dinámicamente mediante bibliotecas gráficas (Chart.js) o paneles avanzados (Grafana).

### 7.5. Empresa e Iniciativa Emprendedora (EIE)

- **Estudio de Viabilidad para Pymes:** Elaboración del plan de empresa y análisis de costes para evaluar la comercialización de la solución NexusGuard como servicio gestionado (*Managed Service Provider - MSP*).
- **Cálculo de TCO y Ahorro Energético:** Cuantificación económica del ahorro en hardware físico, licencias de software propietario y consumo eléctrico frente a arquitecturas convencionales.

---

## 8. Organización del Repositorio

```text
.
├── .github/                # Configuración de integración y automatización
├── anexos/                 # Evidencias complementarias, diagramas y capturas
├── docs/                   # Estructura documental y capítulos técnicos (MkDocs)
│   ├── index.md            # Visión general del proyecto
│   ├── 01_introduccion.md  # Justificación y objetivos académicos
│   ├── 02_marco_tecnologico.md # Fundamentos de virtualización y análisis comparativo
│   ├── 03_desarrollo.md    # Especificaciones de hardware y despliegue del entorno
│   ├── 04_resultados.md    # Memoria de pruebas y validaciones
│   ├── 05_conclusiones.md  # Conclusiones finales y líneas de trabajo
│   ├── 06_bibliografia.md  # Fuentes bibliográficas y normativas
│   └── 07_anexos.md        # Glosario conceptual y tablas técnicas
├── scripts/                # Secuencias de comandos y automatismos operativos
├── src/                    # Recursos de maquetación y estilos
├── mkdocs.yml              # Fichero de configuración del portal de documentación
├── pimas.pdf               # Documento original de la memoria técnica del proyecto
└── README.md               # Memoria ejecutiva y descriptiva del repositorio
```
