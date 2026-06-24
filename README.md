# Relay8CH ETH/16Z - Firmware 🚀

Este repositorio contiene el firmware profesional desarrollado para la plataforma **Raspberry Pi Pico** (RP2040/RP2350), diseñado para el control robusto de una placa de **8 canales de relés** con conectividad **Ethernet** y bus industrial **LAN485**.

El sistema está gobernado por el sistema operativo en tiempo real **FreeRTOS**, garantizando determinismo y confiabilidad en entornos de automatización industrial.

---

## 📌 Características del Sistema
* **Control de Actuadores:** Gestión de 8 canales de relés independientes con lógica de pulsos y temporización adaptativa.
* **Núcleo RTOS:** Arquitectura basada en tareas de **FreeRTOS** (administración de memoria con `heap_4.c`, colas de mensajes y semáforos binarios).
* **Conectividad Red:** Interfaz Ethernet integrada para telemetría y comandos remotos (arquitectura MQTT/Sockets).
* **Bus Industrial:** Driver de comunicación **LAN485** con conmutación automática de dirección (Tx/Rx) para distancias largas.
* **Almacenamiento Persistente:** Administrador de memoria para EEPROM externa **24Cxxx** a través del bus I2C (resguardo de estados ante fallas de energía).
* **Conversión A/D:** Monitoreo analógico de precisión mediante el ADC secuencial **TLA2528** por bus I2C.

---

## 📂 Estructura del Código Fuente

* `ProjectFiles/` -> Código fuente principal en C.
  * `main.c` -> Inicialización de hardware y lanzamiento del planificador de FreeRTOS.
  * `commrtos.c` -> Tareas principales de comunicación y sincronización de hilos.
  * `lan485.c` -> Driver de bajo nivel para el bus diferencial RS485.
  * `i2c_Manager.c` -> Administrador de colas y bloqueos para el bus I2C compartido.
  * `eeprom_24c.c` / `tla2528.c` -> Drivers para la memoria no volátil y el ADC externo.
  * `pulsed_devices.c` / `fsm_zonas.c` -> Lógica de disparo de relés y máquina de estados de zonas.

---

## 🛠️ Entorno de Desarrollo y Compilación

El proyecto está estructurado de forma nativa para compilarse con el **Raspberry Pi Pico SDK** utilizando **CMake**.

### Prerrequisitos en el sistema (ej. Debian/Ubuntu)
Asegúrate de contar con el binal de Git y el toolchain de ARM:
```bash
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
```

### Flujo de Compilación Limpio
1. Descargar o clonar el proyecto.
2. Generar el directorio y compilar:
   ```bash
   mkdir build && cd build
   cmake .. -DCMAKE_BUILD_TYPE=Debug
   make -j\$(nproc)
   ```
*Nota: El archivo `.gitignore` está configurado para excluir automáticamente los binarios generados (`.elf`, `.bin`, `.uf2`) y las dependencias de CMake.*

---

## 🔗 Proyectos Relacionados
* **Hardware/PCB (KiCad):** El diseño de la placa de circuito impreso, ruteado de potencia y esquemáticos se encuentra en el repositorio hermano: **[placa_pcb](https://github.com)**.

---

## 👥 Autor
* **Eduardo Damian Granzella** - *Desarrollo de Firmware / Embedded Systems* - [edgranzella](https://github.com)

