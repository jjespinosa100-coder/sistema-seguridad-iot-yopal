Configuración Técnica del Sistema – Red, NVR y Firewall
Proyecto: Sistema Inteligente de Seguridad Electrónica con IoT y Redes Seguras
Ubicación: Centro de Salud – Yopal, Casanare
Responsable técnico: Miguel Alfonso López Sánchez
Proyecto de Grado UNAD 202016907 – Mayo 2026

1. Segmentación de Red para Dispositivos IoT y Videovigilancia
Infraestructura general
ComponenteDetalleRouter principalHuawei Enterprise RouterFabricante dispositivosDahua TechnologyTipo de segmentaciónSegmentación lógica mediante firewall sobre infraestructura existente del centro de salud

La segmentación se implementó mediante políticas de firewall sobre la infraestructura de red existente del establecimiento. No se configuraron VLANs dedicadas desde el router principal dado que el centro de salud ya contaba con infraestructura empresarial Huawei con capacidades de segmentación propias. El resultado funcional es equivalente: los dispositivos de videovigilancia operan en un segmento completamente aislado de la red administrativa.

Red asignada para dispositivos de seguridad
ParámetroValorSegmento172.20.140.0/24Rango operativo172.20.140.1 – 172.20.140.254Máscara de subred255.255.255.0Gateway172.20.140.1UsoExclusivo para NVR, cámaras IP y dispositivos IoT
Direccionamiento implementado
DispositivoIP asignadaUbicaciónNVR Principal172.20.140.205Cuarto técnicoCámara 1172.20.140.21Entrada principalCámara 2172.20.140.22RecepciónCámara 3172.20.140.23Pasillo principalCámara 4172.20.140.24Parqueadero
Características de seguridad de red

Segmentación lógica mediante firewall del router Huawei Enterprise
Red independiente para dispositivos de videovigilancia
Restricción de acceso desde red corporativa hacia red de seguridad
Acceso remoto con autenticación obligatoria
Comunicación cifrada HTTPS/TLS 1.2
Arquitectura preparada para futura integración de sensores IoT


2. Configuración del NVR Dahua
Información general del equipo
ParámetroValorFabricanteDahua TechnologyTipoNVR – Grabador de Video en RedUbicación físicaCentro de Salud – Yopal
Configuración de red del NVR
ParámetroValorIP asignada172.20.140.205Máscara de subred255.255.255.0Gateway172.20.140.1DNS Primario8.8.8.8DNS Secundario1.1.1.1HTTPSHabilitadoAcceso remotoHabilitado
Cámaras registradas en el NVR
CanalIPUbicaciónCanal 1172.20.140.140EscaleraCanal 2172.20.140.142RecepciónCanal 3172.20.140.144Pasillo internoCanal 4172.20.140.145Mesón recepción
Parámetros de grabación
ParámetroValorResolución4MPCompresiónH.265FPS20Modo de grabaciónContinua + detección de movimientoCapacidad de disco1 TBRetención verificada12 días
Protocolos habilitados
ProtocoloEstadoONVIFHabilitadoRTSPHabilitadoHTTPSHabilitadoTLSTLS 1.2
Gestión y monitoreo remoto
ComponenteDetalleAplicación móvilDMSS – Dahua Mobile Surveillance SystemVisualización remotaHabilitadaNotificaciones pushHabilitadasPlataformasiOS y Android
Seguridad aplicada en el NVR

Credenciales por defecto reemplazadas por contraseña segura
Acceso autenticado obligatorio para toda conexión remota
HTTPS habilitado en todas las comunicaciones
TLS 1.2 activo en tráfico NVR – plataforma de monitoreo
Segmentación de red mediante firewall
Restricción de acceso desde red administrativa del centro de salud


3. Políticas de Firewall Aplicadas
Infraestructura de firewall
ComponenteDetalleRouterHuawei Enterprise RouterFirewallMódulo de seguridad integrado en infraestructura existenteRed protegida172.20.140.0/24
Política 1 – Comunicación interna del segmento de seguridad
ParámetroValorOrigen172.20.140.0/24Destino172.20.140.0/24AcciónPermitirEstadoHabilitada
Permite que los dispositivos de videovigilancia se comuniquen entre sí dentro del segmento dedicado.
Política 2 – Restricción desde red administrativa hacia videovigilancia
ParámetroValorOrigenRed administrativa del centro de saludDestino172.20.140.0/24AcciónDenegarEstadoHabilitada
Impide que equipos de la red corporativa accedan directamente a los dispositivos de videovigilancia sin autenticación.
Política 3 – Salida controlada hacia internet
ParámetroValorOrigen172.20.140.0/24DestinoInternetServicios permitidosHTTPS, RTSP, servicios nube DahuaAcciónPermitirEstadoHabilitada
Permite el monitoreo remoto y la sincronización con la plataforma DMSS de Dahua.
Política 4 – Acceso remoto autenticado
ParámetroValorAcceso permitidoÚnicamente mediante plataforma DMSS con autenticación obligatoriaAcciónPermitir con autenticaciónEstadoHabilitada
Resumen de controles implementados
ControlEstadoSegmentación lógica por firewall✅ AplicadoRestricción de acceso intersegmento✅ AplicadoAutenticación obligatoria acceso remoto✅ AplicadoComunicación cifrada HTTPS/TLS 1.2✅ AplicadoAislamiento dispositivos de videovigilancia✅ AplicadoCredenciales por defecto reemplazadas✅ Aplicado

Miguel Alfonso López Sánchez – Scrum Master / Developer
Proyecto de Grado UNAD 202016907 – Mayo 2026
