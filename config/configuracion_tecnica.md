# Configuración Técnica del Sistema – Red, NVR y Firewall
 
**Proyecto:** Sistema Inteligente de Seguridad Electrónica con IoT y Redes Seguras  
**Ubicación:** Centro de Salud – Yopal, Casanare  
**Responsable técnico:** Miguel Alfonso López Sánchez  
**Proyecto de Grado UNAD 202016907 – Mayo 2026**
 
---
 
## 1. Segmentación de Red para Dispositivos IoT y Videovigilancia
 
### Infraestructura general
 
| Componente | Detalle |
|------------|---------|
| Router principal | Huawei Enterprise Router |
| Fabricante dispositivos | Dahua Technology |
| Tipo de segmentación | Segmentación lógica mediante firewall sobre infraestructura existente del centro de salud |
 
> La segmentación se implementó mediante políticas de firewall sobre la infraestructura de red existente del establecimiento. No se configuraron VLANs dedicadas desde el router principal dado que el centro de salud ya contaba con infraestructura empresarial Huawei con capacidades de segmentación propias. El resultado funcional es equivalente: los dispositivos de videovigilancia operan en un segmento completamente aislado de la red administrativa.
 
### Red asignada para dispositivos de seguridad
 
| Parámetro | Valor |
|-----------|-------|
| Segmento | 172.20.140.0/24 |
| Rango operativo | 172.20.140.1 – 172.20.140.254 |
| Máscara de subred | 255.255.255.0 |
| Gateway | 172.20.140.1 |
| Uso | Exclusivo para NVR, cámaras IP y dispositivos IoT |
 
### Direccionamiento implementado
 
| Dispositivo | IP asignada | Ubicación |
|-------------|------------|-----------|
| NVR Principal | 172.20.140.205 | Cuarto técnico |
| Cámara 1 | 172.20.140.21 | Entrada principal |
| Cámara 2 | 172.20.140.22 | Recepción |
| Cámara 3 | 172.20.140.23 | Pasillo principal |
| Cámara 4 | 172.20.140.24 | Parqueadero |
 
### Características de seguridad de red
 
- Segmentación lógica mediante firewall del router Huawei Enterprise
- Red independiente para dispositivos de videovigilancia
- Restricción de acceso desde red corporativa hacia red de seguridad
- Acceso remoto con autenticación obligatoria
- Comunicación cifrada HTTPS/TLS 1.2
- Arquitectura preparada para futura integración de sensores IoT
---
 
## 2. Configuración del NVR Dahua
 
### Información general del equipo
 
| Parámetro | Valor |
|-----------|-------|
| Fabricante | Dahua Technology |
| Tipo | NVR – Grabador de Video en Red |
| Ubicación física | Centro de Salud – Yopal |
 
### Configuración de red del NVR
 
| Parámetro | Valor |
|-----------|-------|
| IP asignada | 172.20.140.205 |
| Máscara de subred | 255.255.255.0 |
| Gateway | 172.20.140.1 |
| DNS Primario | 8.8.8.8 |
| DNS Secundario | 1.1.1.1 |
| HTTPS | Habilitado |
| Acceso remoto | Habilitado |
 
### Cámaras registradas en el NVR
 
| Canal | IP | Ubicación |
|-------|----|-----------|
| Canal 1 | 172.20.140.140 | Escalera |
| Canal 2 | 172.20.140.142 | Recepción |
| Canal 3 | 172.20.140.144 | Pasillo interno |
| Canal 4 | 172.20.140.145 | Mesón recepción |
 
### Parámetros de grabación
 
| Parámetro | Valor |
|-----------|-------|
| Resolución | 4MP |
| Compresión | H.265 |
| FPS | 20 |
| Modo de grabación | Continua + detección de movimiento |
| Capacidad de disco | 1 TB |
| Retención verificada | 12 días |
 
### Protocolos habilitados
 
| Protocolo | Estado |
|-----------|--------|
| ONVIF | Habilitado |
| RTSP | Habilitado |
| HTTPS | Habilitado |
| TLS | TLS 1.2 |
 
### Gestión y monitoreo remoto
 
| Componente | Detalle |
|------------|---------|
| Aplicación móvil | DMSS – Dahua Mobile Surveillance System |
| Visualización remota | Habilitada |
| Notificaciones push | Habilitadas |
| Plataformas | iOS y Android |
 
### Seguridad aplicada en el NVR
 
- Credenciales por defecto reemplazadas por contraseña segura
- Acceso autenticado obligatorio para toda conexión remota
- HTTPS habilitado en todas las comunicaciones
- TLS 1.2 activo en tráfico NVR – plataforma de monitoreo
- Segmentación de red mediante firewall
- Restricción de acceso desde red administrativa del centro de salud
---
 
## 3. Políticas de Firewall Aplicadas
 
### Infraestructura de firewall
 
| Componente | Detalle |
|------------|---------|
| Router | Huawei Enterprise Router |
| Firewall | Módulo de seguridad integrado en infraestructura existente |
| Red protegida | 172.20.140.0/24 |
 
### Política 1 – Comunicación interna del segmento de seguridad
 
| Parámetro | Valor |
|-----------|-------|
| Origen | 172.20.140.0/24 |
| Destino | 172.20.140.0/24 |
| Acción | Permitir |
| Estado | Habilitada |
 
Permite que los dispositivos de videovigilancia se comuniquen entre sí dentro del segmento dedicado.
 
### Política 2 – Restricción desde red administrativa hacia videovigilancia
 
| Parámetro | Valor |
|-----------|-------|
| Origen | Red administrativa del centro de salud |
| Destino | 172.20.140.0/24 |
| Acción | Denegar |
| Estado | Habilitada |
 
Impide que equipos de la red corporativa accedan directamente a los dispositivos de videovigilancia sin autenticación.
 
### Política 3 – Salida controlada hacia internet
 
| Parámetro | Valor |
|-----------|-------|
| Origen | 172.20.140.0/24 |
| Destino | Internet |
| Servicios permitidos | HTTPS, RTSP, servicios nube Dahua |
| Acción | Permitir |
| Estado | Habilitada |
 
Permite el monitoreo remoto y la sincronización con la plataforma DMSS de Dahua.
 
### Política 4 – Acceso remoto autenticado
 
| Parámetro | Valor |
|-----------|-------|
| Acceso permitido | Únicamente mediante plataforma DMSS con autenticación obligatoria |
| Acción | Permitir con autenticación |
| Estado | Habilitada |
 
### Resumen de controles implementados
 
| Control | Estado |
|---------|--------|
| Segmentación lógica por firewall | ✅ Aplicado |
| Restricción de acceso intersegmento | ✅ Aplicado |
| Autenticación obligatoria acceso remoto | ✅ Aplicado |
| Comunicación cifrada HTTPS/TLS 1.2 | ✅ Aplicado |
| Aislamiento dispositivos de videovigilancia | ✅ Aplicado |
| Credenciales por defecto reemplazadas | ✅ Aplicado |
 
---
 
*Miguel Alfonso López Sánchez – Scrum Master / Developer*  
*Proyecto de Grado UNAD 202016907 – Mayo 2026*
