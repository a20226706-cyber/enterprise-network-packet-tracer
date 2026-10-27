# Red Empresarial Segmentada en Cisco Packet Tracer

Proyecto personal orientado a practicar fundamentos de redes mediante el diseño y configuración de una red empresarial segmentada utilizando Cisco Packet Tracer.

La red fue dividida en diferentes áreas mediante VLANs y se implementó routing inter-VLAN, DHCP y una ACL para controlar la comunicación entre segmentos.

## Tecnologías y conceptos

- Cisco Packet Tracer
- IPv4
- Subnetting
- VLANs
- Trunking 802.1Q
- Router-on-a-Stick
- Routing inter-VLAN
- DHCP
- ACL
- Troubleshooting de conectividad

## Topología

La red está compuesta por:

- 1 router
- 1 switch Cisco 2960
- 3 PCs
- 1 servidor

Las áreas fueron separadas de la siguiente manera:

```text
R1
 |
 | 802.1Q Trunk
 |
SW1
 |
 +-- VLAN 10 → Administración
 +-- VLAN 20 → Soporte
 +-- VLAN 30 → Ventas
 +-- VLAN 40 → Servidores
```

## Direccionamiento

| VLAN | Área | Red | Gateway |
|---|---|---|---|
| 10 | Administración | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Soporte | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Ventas | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Servidores | 192.168.40.0/24 | 192.168.40.1 |

El servidor utiliza una dirección IP estática:

```text
192.168.40.10
```

## VLANs

Se configuraron cuatro VLANs en el switch:

```text
VLAN 10 → ADMIN
VLAN 20 → SOPORTE
VLAN 30 → VENTAS
VLAN 40 → SERVIDORES
```

Cada dispositivo fue asignado a un puerto de acceso correspondiente a su área.

## Trunk 802.1Q

El enlace entre el switch y el router fue configurado como trunk para transportar tráfico perteneciente a múltiples VLANs.

```text
SW1 Gi0/1
     |
     | 802.1Q
     |
R1 Gi0/0
```

## Routing inter-VLAN

Se utilizó la técnica Router-on-a-Stick.

Sobre una única interfaz física del router se crearon diferentes subinterfaces:

```text
G0/0.10 → 192.168.10.1
G0/0.20 → 192.168.20.1
G0/0.30 → 192.168.30.1
G0/0.40 → 192.168.40.1
```

Esto permite que dispositivos pertenecientes a diferentes VLANs puedan comunicarse mediante el router.

## DHCP

El router fue configurado como servidor DHCP para las VLANs de usuarios.

Se crearon pools independientes para:

```text
ADMIN
SOPORTE
VENTAS
```

Las PCs reciben automáticamente:

- dirección IPv4
- máscara de subred
- gateway predeterminado
- servidor DNS

El servidor de la VLAN 40 mantiene una dirección IP estática.

## ACL

Se implementó una ACL extendida para controlar el tráfico entre las VLANs.

La política configurada restringe el tráfico originado desde la red de Ventas hacia la red de Administración:

```text
VENTAS
192.168.30.0/24
      |
      X
      |
ADMINISTRACIÓN
192.168.10.0/24
```

El resto del tráfico permitido por la política puede continuar circulando entre las redes.

## Pruebas realizadas

Se realizaron pruebas para comprobar:

- conectividad con los gateways
- comunicación entre VLANs
- acceso hacia la VLAN de servidores
- asignación automática mediante DHCP
- funcionamiento del trunk 802.1Q
- funcionamiento de la ACL
- restricción de tráfico entre Ventas y Administración

## Evidencias

Las capturas de configuración y pruebas se encuentran en:

```text
/screenshots
```

Incluyen:

- topología completa
- VLANs configuradas
- enlace trunk
- interfaces y gateways
- asignaciones DHCP
- ACL
- pruebas de conectividad

## Archivo de Packet Tracer

El laboratorio completo se encuentra en:

```text
/packet-tracer/enterprise-network.pkt
```

## Resultado

El proyecto permitió implementar una red empresarial segmentada utilizando conceptos fundamentales de switching, routing y control de acceso.

La arquitectura final integra:

```text
VLANs
  ↓
Trunk 802.1Q
  ↓
Router-on-a-Stick
  ↓
Routing inter-VLAN
  ↓
DHCP
  ↓
ACL
```
