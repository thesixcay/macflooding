# macflooding

# Ataque MAC Flooding

## Descripción

Este laboratorio demuestra cómo un atacante puede realizar un ataque de **MAC Flooding** contra un switch de capa 2 utilizando Scapy. El objetivo es saturar la tabla CAM (Content Addressable Memory) del switch enviando una gran cantidad de direcciones MAC falsas.

Cuando la tabla CAM se llena, el switch puede comenzar a comportarse como un hub, reenviando tráfico por múltiples puertos y permitiendo que un atacante capture información de otros dispositivos de la red.

> ⚠️ Este proyecto ha sido desarrollado únicamente con fines educativos y para prácticas autorizadas de ciberseguridad. :contentReference[oaicite:0]{index=0}

---

# Objetivo del Laboratorio

- Comprender el funcionamiento de las tablas CAM.
- Analizar el impacto de un ataque MAC Flooding.
- Observar el comportamiento de un switch bajo saturación.
- Implementar mecanismos de protección.
- Evaluar medidas de mitigación mediante Port Security.

---

# Topología de Red

<img width="480" height="416" alt="image" src="https://github.com/user-attachments/assets/7e251e49-187a-4a7b-af8c-b3cd2e088576" />

# Requisitos

## Software

- Python 3.x
- Scapy
- Kali Linux o Parrot OS
- Wireshark
- GNS3 o PNETLab

## Instalación de dependencias

```bash
pip install scapy
```

---

# Funcionamiento del Script

El script realiza las siguientes acciones:

1. Genera direcciones MAC aleatorias.
2. Genera direcciones IP aleatorias.
3. Construye paquetes Ethernet falsificados.
4. Envía los paquetes continuamente al switch.
5. Fuerza el aprendizaje de miles de direcciones MAC inexistentes.
6. Busca saturar la tabla CAM del dispositivo.

---

# Características

- Generación automática de MAC aleatorias.
- Generación automática de IP aleatorias.
- Ataque de Capa 2.
- Envío continuo de paquetes.
- Compatible con laboratorios virtuales.
- Monitoreo mediante contador de paquetes.

---

# Ejecución

Ejecutar el script con privilegios de administrador:

```bash
sudo python3 mac_flooding.py
```

# ¿Cómo funciona el ataque?

Los switches almacenan asociaciones entre:

```text
Dirección MAC ↔ Puerto
```

en una estructura denominada **tabla CAM**.

El atacante genera miles de direcciones MAC falsas y las envía al switch.

Cuando la tabla CAM alcanza su capacidad máxima:

- El switch deja de aprender nuevas MAC.
- Parte del tráfico se envía por múltiples puertos.
- El atacante puede observar tráfico ajeno.
- Se degrada el rendimiento de la red.

---

# Riesgos de Seguridad

Un ataque MAC Flooding puede provocar:

- Saturación de la tabla CAM.
- Degradación del rendimiento de la red.
- Pérdida de confidencialidad.
- Captura de tráfico de otros usuarios.
- Facilitar ataques Man-in-the-Middle.
- Incremento del tráfico broadcast.

# Contramedidas

## Configuración de Port Security

### 1. Entrar al modo de configuración

```cisco
configure terminal
```

### 2. Seleccionar la interfaz

```cisco
interface ethernet 0/0
```

### 3. Configurar el puerto en modo acceso

```cisco
switchport mode access
```

### 4. Habilitar Port Security

```cisco
switchport port-security
```

### 5. Limitar a una sola dirección MAC

```cisco
switchport port-security maximum 1
```

### 6. Aprendizaje automático permanente

```cisco
switchport port-security mac-address sticky
```

### 7. Acción ante una violación

```cisco
switchport port-security violation shutdown
```

### 8. Salir de la configuración

```cisco
exit
```

---
