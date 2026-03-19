# Implementaci-n-de-VPN-Site-to-Site-IPsec-con-FortiGate-Next-Generation-Firewalls

## 👤 Información del Estudiante
* **Nombre:** Martin Alexander Perez Moya
* **Matrícula:** 2024-2295
* **Institución:** Instituto Tecnológico de Las Américas (ITLA)

---

## 🎯 Objetivo del Proyecto
Configurar y validar un túnel VPN Site-to-Site utilizando el protocolo IPsec (IKEv2) entre dos unidades FortiGate-VM. El propósito es permitir la comunicación cifrada y segura entre dos segmentos de red LAN distintos a través de una infraestructura de red simulada (ISP).

---

## 🗺️ Topología y Direccionamiento
La red consta de dos sedes conectadas a través de un router ISP central.

| Dispositivo | Interfaz | Dirección IP | Función |
| :--- | :--- | :--- | :--- |
| **FortiGate-A** | port3 (WAN) | 192.168.10.2/30 | Salida hacia ISP |
| **FortiGate-A** | port4 (LAN) | 10.22.95.1/26 | Gateway Oficina A |
| **FortiGate-B** | port3 (WAN) | 192.168.20.2/30 | Salida hacia ISP |
| **FortiGate-B** | port4 (LAN) | 10.22.95.65/26 | Gateway Oficina B |

---

## 🛠️ Detalles de la Configuración IPsec
Para garantizar la máxima seguridad y compatibilidad, se utilizaron los siguientes parámetros:
* **Protocolo:** IKEv2
* **Cifrado (Phase 1 & 2):** AES128 / SHA256
* **Diffie-Hellman Group:** 14 (2048-bit MODP Group)
* **PFS (Perfect Forward Secrecy):** Habilitado
* **Selectores de Tráfico:** * Local: 10.22.95.0/26 <--> Remoto: 10.22.95.64/26 (Espejo en el otro extremo)

---

## 🔍 Verificación y Pruebas de Diagnóstico
A continuación, se presentan los comandos utilizados para validar la integridad y el funcionamiento de la solución.

### 1. Validación de Identidad y Tiempo del Sistema
Se confirma la identidad del equipo y la marca de tiempo de la configuración.
```fortinet
get system status | grep -E "Hostname|Version|System time"

2. Estado de Interfaces Físicas
Verificación de que los puertos WAN y LAN se encuentran operativos (Up).

get system interface physical

3. Integridad del Túnel VPN (Phase 1 y Phase 2)
Este comando muestra los algoritmos negociados y el estado del túnel.


get vpn ipsec tunnel details

4. Verificación de la Tabla de Enrutamiento
Se valida que el tráfico hacia la sede remota está siendo dirigido correctamente a través de la interfaz virtual del túnel.

Fragmento de código
get router info routing-table all

5. Captura de Paquetes (Cifrado ESP)
Prueba fundamental para un Analista SOC: validar que el tráfico ICMP viaja encapsulado bajo el protocolo ESP (Encapsulating Security Payload), garantizando que los datos no son legibles en tránsito.

Fragmento de código
diag sniffer packet port3 'esp' 4

6. Prueba de Salto Invisible (Traceroute)
Desde el Host final, se realiza una traza de ruta para confirmar que el tráfico "salta" la infraestructura pública y llega directamente al segmento remoto.

Bash
tracert 10.22.95.70
```
