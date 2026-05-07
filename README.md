Sistema Inteligente de Seguridad Electrónica con IoT y Redes Seguras
Universidad Nacional Abierta y a Distancia – UNAD  
Curso: Proyecto de Grado 202016907 | Grupo: 113  
Programa: Ingeniería de Sistemas  
Tutor: Orlando Gomez Barboza  
Mayo 2026 – Yopal, Casanare
---
Autores
Nombre	Rol
Jose Jhon Fredy Espinosa Cuevas	Product Owner
Miguel Alfonso López Sánchez	Scrum Master / Developer
---
Descripción
Este repositorio documenta el desarrollo del proyecto de grado: un sistema de seguridad electrónica basado en la integración de dispositivos IoT (cámaras IP, sensores de movimiento, sensores de apertura, control de acceso) sobre arquitecturas de red seguras con segmentación VLAN y cifrado TLS 1.2.
El proyecto no contempla desarrollo de software propio ni fabricación de hardware. Su propuesta consiste en la integración inteligente de tecnologías disponibles en el mercado, haciendo accesible y técnicamente segura la instalación para usuarios de ingresos medios en el municipio de Yopal, Casanare.
Nivel de madurez tecnológica alcanzado: TRL5 — validación en entorno real (centro de salud, Yopal)
---
Metodología
Marco / Metodología	Rol en el proyecto
Scrum	Metodología de desarrollo: cinco sprints iterativos de dos semanas
CDIO	Marco formativo educativo: Concebir – Diseñar – Implementar – Operar
Sprints ejecutados
Sprint	Período	Objetivo	TRL
Sprint 1	Semanas 1–2	Análisis de mercado y requerimientos	TRL3
Sprint 2	Semanas 3–4	Diseño de arquitectura de red	TRL3
Sprint 3	Semanas 5–8	Implementación y pruebas en laboratorio	TRL4
Sprint 4	Semanas 9–10	Validación en instalación real (centro de salud)	TRL5
Sprint 5	Semanas 11–12	Ajustes, documentación y presentación	TRL5
---
Arquitectura del sistema
El sistema opera en tres capas funcionales:
```
┌─────────────────────────────────────────────────────────────┐
│  CAPA 3 – GESTIÓN Y MONITOREO                               │
│  Plataforma escritorio · App móvil · Interfaz web NVR       │
└────────────────────────────┬────────────────────────────────┘
                             │ TLS 1.2
┌────────────────────────────▼────────────────────────────────┐
│  CAPA 2 – RED SEGURA                                        │
│  Router VLAN10 (IoT) | VLAN1 (datos) · Firewall · DDNS     │
└──────┬──────────────────────────────────────────────────────┘
       │ RTSP / Zigbee / MQTT
┌──────▼──────────────────────────────────────────────────────┐
│  CAPA 1 – PERCEPCIÓN (CAMPO)                                │
│  4× Cámaras IP · 2× Sensores PIR · 2× Sensores apertura    │
│  1× Panel alarma · 1× Videoportero IP                       │
└─────────────────────────────────────────────────────────────┘
```
---
Componentes del sistema
Componente	Especificación	Protocolo
Cámaras IP (×4)	4MP, IR nocturno, PoE, ONVIF	RTSP, ONVIF
NVR 4 canales	H.265, HDD 1TB, DDNS	RTSP, TCP/IP
Sensores PIR (×2)	Zigbee 3.0, alcance 8m	Zigbee
Sensores apertura (×2)	Magnético, Zigbee	Zigbee
Hub Zigbee	Coordinador USB/LAN	Zigbee
Panel alarma + sirena	Kit inalámbrico	RF/Zigbee
Videoportero IP	Audio/video bidireccional	SIP/RTSP
Router VLAN	802.1Q, firewall, DDNS	TCP/IP
Switch PoE	8 puertos, VLAN 802.1Q	Ethernet
---
Resultados de validación
TRL4 – Laboratorio
Parámetro	Criterio	Resultado	Estado
Latencia de video	≤ 3 s	1.8 s	✅ Aprobado
Notificación push	≤ 5 s	3.2 s	✅ Aprobado
Almacenamiento	≥ 7 días	12 días	✅ Aprobado
Acceso sin autenticación	Denegado	Denegado	✅ Aprobado
Cifrado TLS	TLS 1.2 activo	Verificado	✅ Aprobado
Aislamiento VLAN	Sin acceso VLAN1→VLAN10	Bloqueado	✅ Aprobado
TRL5 – Centro de salud, Yopal (fase de videovigilancia)
Parámetro	Criterio	Resultado	Estado
Disponibilidad operativa	≥ 99%	99.4%	✅ Aprobado
Latencia video en red real	≤ 3 s	2.1 s	✅ Aprobado
Notificación en campo	≤ 5 s	3.7 s	✅ Aprobado
Satisfacción del usuario	≥ 4.0 / 5	4.6 / 5	✅ Aprobado
Usabilidad sin capacitación	Acceso en ≤ 5 min	< 5 min	✅ Aprobado
Métricas sensores PIR	< 10% falsas alarmas	Pendiente siguiente fase	🔄 En progreso
---
Estructura del repositorio
```
sistema-seguridad-iot-yopal/
├── README.md
├── docs/
│   ├── Manual_Usuario.md
│   └── Manual_Instalacion.md
├── config/
│   ├── README.md               ← Índice de configuraciones
│   ├── vlan_config.md          ← Por agregar (Miguel López)
│   ├── nvr_setup.md            ← Por agregar (Miguel López)
│   ├── zigbee_hub.md           ← Por agregar (Miguel López)
│   └── firewall_rules.md       ← Por agregar (Miguel López)
├── diagrams/
│   ├── README.md               ← Índice de diagramas
│   └── [Archivos de imagen por agregar]
└── tests/
    ├── pruebas_TRL4.md
    ├── pruebas_TRL5.md
    └── checklist.md
```
---
Video del prototipo
▶️ Ver video de presentación del prototipo
Duración máxima: 10 minutos | Demo en tiempo real del sistema instalado
---
Marco legal
Ley 1581 de 2012 – Protección de Datos Personales
Decreto 1377 de 2013 – Avisos de privacidad
Ley 1801 de 2016 – Código Nacional de Seguridad y Convivencia Ciudadana
ISO/IEC 27001:2022 – Gestión de seguridad de la información
---
Referencias principales
Amaya Balaguera, Y. D. (2015). AEGIS-MD. Revista de Investigaciones UNAD.
Cárdenas, D. et al. (2021). Integración IoT en redes seguras. Revista Ingenierías U. de Medellín.
MinCiencias. (2022). Niveles de madurez tecnológica (TRL).
Miguel, H. B., & Luis Eduardo, B. R. (2020). Ciclo de vida de desarrollo ágil de software seguro.
Schwaber, K., & Sutherland, J. (2020). The Scrum Guide.
Tahir, H. et al. (2021). On the security of consumer IoT devices. Electronics.
---
Yopal, Casanare – Mayo 2026
