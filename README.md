# Implementaci-n-de-VPN-Site-to-Site-IPsec-con-FortiGate-Next-Generation-Firewalls

## 👤 Información del Estudiante
* **Nombre:** Martin Alexander Perez Moya
* **Matrícula:** 2024-2295
* **Institución:** Instituto Tecnológico de Las Américas (ITLA)
* Link del video: https://www.youtube.com/watch?v=MoywTaHWIso

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

<img width="844" height="399" alt="image" src="https://github.com/user-attachments/assets/34a2855b-6769-472b-a8bf-6ca1d35effc3" />


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

ip en Puertos:


<img width="790" height="180" alt="image" src="https://github.com/user-attachments/assets/fb568048-a954-43e8-88d0-11b750f21c72" />


Bash
tracert 10.22.95.70


<img width="346" height="114" alt="image" src="https://github.com/user-attachments/assets/b99e5064-dba2-4d87-a760-e51c86984386" />


Tunel hacia el fortigate A;


<img width="1080" height="349" alt="image" src="https://github.com/user-attachments/assets/cd8da352-a438-498a-98e2-0d9a32acd237" />



Tunel hacia el fortigate B:


<img width="1152" height="258" alt="image" src="https://github.com/user-attachments/assets/839a241e-c725-4331-889c-e147f5775089" />


