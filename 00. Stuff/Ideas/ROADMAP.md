### **CISCO NetAcad**
- [x] **Introduction to Cybersecurity**
- [x] **Networking Basics**
- [ ] **Networking Devices and Initial Configuration**
- [ ] **Endpoint Security**
- [ ] **Network Defense**
- [ ] **Cyber Threat Management**
- [ ] **Junior Cybersecurity Analyst**

---
#### **Windows OS**
- [x] **User Mode vs Kernel Mode**
- [x] **Processes vs Threads**
- [x] **Services**
- [x] WIndows Boot Process
- [x] **NTFS vs FAT**
- [ ] **NTFS permissions**
  - Allow vs Deny  
  - Inheritance
  - Permisos efectivos  
  - Ownership y su impacto en soporte y seguridad  
- [x] **Registry**  
- [ ] **Task Manager**
- [ ] **Services.msc**
- [ ] **Event Viewer**
  - Application / System / Security  
  - Niveles de eventos (Error, Warning, Information)  
  - Evento ↔ comportamiento real  
- [ ] **MMC (Microsoft Management Console)**  
- [ ] **Windows Defender Basics**
- [ ] **PowerShell para Analistas**:
    - [ ] Conceptos: Cmdlets, Pipelines (|), Variables y Privilegios
    - [ ] Gestión de procesos y servicios por CLI
    - [ ] Lectura y filtrado de eventos (logs) con PowerShell

### **Infraestructura - Active Directory Domain Services (AD DS)**
#### **Arquitectura y Fundamentos**
- [ ] Repaso de redes corporativas (IP, DNS, Gateway)
- [ ] Componentes: Domain Controller, Forest, Dominios y Global Catalog
- [ ] Relación crítica AD ↔ DNS
- [ ] Roles FSMO y Replicación (conceptos)
- [ ] Diferencia entre Autenticación y Autorización en dominio

#### **Administración de Objetos y GPO**
- [ ] **Usuarios y Grupos**: Atributos, estados de cuenta y tipos de grupos (Security/Distribution)
- [ ] **Estrategia de Grupos**: Domain Local, Global y Universal
- [ ] **Unidades Organizativas (OU)**: Organización lógica vs Grupos
- [ ] **Group Policy Objects (GPO)**:
    - [ ] Orden de aplicación (LSDOU) y herencia
    - [ ] User vs Computer Configuration
    - [ ] Directivas de Seguridad: Password Policy, Lockout, Firewall y Auditoría
    - [ ] Diagnóstico: `gpupdate` y `gpresult`

#### **Auditoría y Windows Logs (Event Viewer)**
- [ ] Categorías: Application, System y Security
- [ ] Niveles de severidad y filtrado de eventos
- [ ] **Eventos Críticos de Seguridad**:
    - [ ] Logons (4624 / 4625) y tipos de Logon
    - [ ] Privilegios especiales (4672)
    - [ ] Creación de procesos (4688)
    - [ ] Gestión de usuarios y grupos (4720, 4732)
    - [ ] Tráfico Kerberos (4768, 4769)

#### **AD Security & Offensive Concepts**
- [ ] Por qué el DC es el objetivo principal (Tier 0)
- [ ] Riesgos en cuentas de servicio y delegaciones
- [ ] Concepto de Movimiento Lateral
- [ ] **Vectores de Ataque Comunes**:
    - [ ] Password Spraying y Brute Force
    - [ ] Kerberoasting y AS-REP Roasting
    - [ ] Pass-the-Hash / Pass-the-Ticket (conceptos)

#### **AD Practical Lab**
- [ ] **LAB**: Montar Domain Controller (Server Core o GUI)
- [ ] **LAB**: Provisionamiento de OUs, usuarios y grupos
- [ ] **LAB**: Endurecimiento (Hardening) mediante GPOs
- [ ] **LAB**: Simulación de bloqueos de cuenta y análisis forense en Event Viewer

#### **Sistema Operativo - Linux**
- [ ] **[SI HICISTE NETACAD]**: Revisar Endpoint Security > Linux Security
- [ ] Instalación de Ubuntu Server y CentOS
- [ ] Comandos básicos: ls, cd, grep, find, ps, netstat, ss
- [ ] Logs en /var/log: auth.log, syslog, secure
- [ ] Bash scripting: 5 scripts básicos (backup, monitoreo)
- [ ] Permisos y usuarios: chmod, chown, sudo
- [ ] **LAB**: Servidor Linux con SSH hardening

#### **Networking Fundamentos**
- [ ] **[SI HICISTE NETACAD]**: Ya tienes esto dominado, hacer repaso rápido
- [ ] Modelo OSI: Memorizar las 7 capas y sus funciones
- [ ] TCP/IP: Three-way handshake, puertos comunes (80, 443, 22, 3389)
- [ ] Protocolos: HTTP/HTTPS, DNS, DHCP, SMTP, FTP
- [ ] Subnetting: Calcular 10 subnets diferentes
- [ ] Wireshark: Capturar y filtrar tráfico HTTP, DNS, SSH
- [ ] **LAB**: Analizar 3 PCAPs con tráfico malicioso

#### **Networking Avanzado**
- [ ] **[SI HICISTE NETACAD]**: Profundizar conceptos de Networking Devices course
- [ ] VLANs y segmentación de red
- [ ] Firewalls: Reglas básicas, stateful vs stateless
- [ ] NAT/PAT: Configuración y troubleshooting
- [ ] VPN: IPSec y SSL VPN conceptos
- [ ] Wireshark avanzado: Seguir TCP streams, exportar objetos
- [ ] **LAB**: Configurar firewall pfSense con 3 zonas

#### **Governance, Risk & Compliance (GRC) para el SOC**
- [ ] Frameworks de Control: NIST CSF, ISO 27001 (controles básicos), CIS Controls
- [ ] Regulaciones: GDPR, PCI-DSS, leyes locales de ciberseguridad
- [ ] SLA & SLO: Entender los tiempos de respuesta exigidos
- [ ] Vulnerability Management: Escaneo (Nessus/OpenVAS) vs. remediación
- [ ] **EJERCICIO**: Realizar un reporte de cumplimiento básico

#### **Email Security & Phishing Analysis**
- [ ] Email Headers: Return-Path, Received, Message-ID, X-Headers
- [ ] Protocolos de Autenticación: SPF, DKIM y DMARC (configuración y validación)
- [ ] Análisis de Cuerpo y Adjuntos: Defang de URLs y análisis de macros
- [ ] Herramientas: MXToolbox, PhishTool, URLScan.io
- [ ] **LAB**: Analizar 10 correos de phishing reales y extraer IOCs

#### **Bases de Datos**
- [ ] SQL básico: SELECT, WHERE, JOIN, GROUP BY
- [ ] Consultas para logs: Buscar eventos por fecha/usuario
- [ ] NoSQL básico: MongoDB queries
- [ ] Elasticsearch: Búsquedas simples con Kibana
- [ ] **LAB**: Base de datos con 1000 eventos, hacer 10 queries

---

### **SOC Structure & Operations**

#### **Estructura del SOC**
- [ ] **[CISCO NETACAD]**: Repasar Network Defense > SOC Overview
- [ ] Roles SOC: L1, L2, L3, Threat Hunter, Incident Responder
- [ ] Flujo de trabajo: Alerta → Triage → Investigación → Escalación
- [ ] Matriz RACI para incidentes
- [ ] Procedimientos de turno: Handover, escalación nocturna
- [ ] Métricas: MTTD, MTTR, False Positive Rate
- [ ] **EJERCICIO**: Crear SOP para 3 tipos de alertas

#### **Security Monitoring Básico**
- [ ] **[CISCO NETACAD]**: Aplicar conceptos de Network Defense > Security Alerts
- [ ] Fuentes de logs: Endpoint, network, cloud, application
- [ ] Tipos de eventos: Authentication, network, file, process
- [ ] Correlación básica: Mismo user + múltiples IPs
- [ ] Triaje de alertas: Priorización por criticidad
- [ ] False positives: Identificar 5 casos comunes
- [ ] **LAB**: Analizar 50 alertas y clasificarlas

#### **Herramientas del SOC**
- [ ] SIEM: Concepto y arquitectura básica
- [ ] Ticketing: Crear, actualizar, cerrar tickets
- [ ] Comunicación: Redactar 5 reportes de incidente
- [ ] Documentación: Crear runbook para phishing
- [ ] Remote access: RDP, SSH, VNC seguro
- [ ] **PRÁCTICA**: Simular día completo en SOC

#### **Clasificación de Incidentes**
- [ ] **[CISCO NETACAD]**: Aplicar Cyber Threat Management > Incident Response
- [ ] Taxonomía de incidentes: Malware, phishing, DDoS, data leak
- [ ] Severidad: Critical, High, Medium, Low, Informational
- [ ] Impacto vs Urgencia: Matriz de priorización
- [ ] Comunicación de incidentes: Técnica vs ejecutiva
- [ ] Chain of custody: Documentación de evidencia
- [ ] **EJERCICIO**: Clasificar 20 escenarios reales

---

### **Log Analysis & SIEM**

#### **Windows Event Logs**
- [ ] Security Log: 4624, 4625, 4648, 4672, 4688, 4697, 4720
- [ ] System Log: Eventos de servicio y errores críticos
- [ ] Application Log: Crashes y errores de apps
- [ ] PowerShell logs: Script Block Logging (4104)
- [ ] Sysmon: Event ID 1, 3, 7, 11, 22
- [ ] **LAB**: Detectar pass-the-hash en logs

#### **Linux & Web Server Logs**
- [ ] auth.log: SSH brute force, sudo usage
- [ ] syslog: Eventos del sistema
- [ ] Apache/Nginx: Access log analysis (200, 404, 500)
- [ ] Apache/Nginx: Error log analysis
- [ ] Logs de base de datos: MySQL/PostgreSQL
- [ ] **LAB**: Detectar web shell en access logs

#### **SIEM - Splunk Básico**
- [ ] Instalación de Splunk Free
- [ ] SPL básico: search, stats, timechart, table
- [ ] Filtros: source, sourcetype, host, index
- [ ] Campos: rex, eval, lookup
- [ ] Dashboards: Crear 3 dashboards de monitoreo
- [ ] **LAB**: Ingerir logs de Windows y Linux

#### **SIEM Avanzado & Correlación**
- [ ] SPL avanzado: subsearch, transaction, join
- [ ] Alertas: Configurar 10 reglas de detección
- [ ] Correlation: Detectar lateral movement
- [ ] Parsing: Extraer campos personalizados
- [ ] Performance: Optimizar búsquedas lentas
- [ ] **PROYECTO**: Crear 20 reglas Sigma convertidas a SPL

---

### **Network Security Monitoring**

#### **Network Traffic Analysis**
- [ ] NetFlow: Analizar flujos de red
- [ ] Packet analysis: Wireshark filters avanzados
- [ ] Protocolos: Analizar SMB, RDP, Kerberos
- [ ] Anomalías: Detectar beaconing, data exfil
- [ ] Bandwidth: Identificar uso anormal
- [ ] **LAB**: Analizar 5 PCAPs de ataques reales

#### **Intrusion Detection Systems**
- [ ] **[CISCO NETACAD]**: Profundizar Network Defense > IDS/IPS concepts
- [ ] Snort: Instalación y configuración
- [ ] Reglas Snort: Escribir 10 reglas custom
- [ ] Suricata: Configuración y diferencias con Snort
- [ ] NIDS vs HIDS: Casos de uso
- [ ] Tuning: Reducir falsos positivos en IDS
- [ ] **LAB**: Detectar Metasploit con Snort

#### **Security Onion**
- [ ] Instalación de Security Onion
- [ ] Componentes: Suricata, Zeek, Wazuh, Elasticsearch
- [ ] PCAP analysis con Security Onion
- [ ] Zeek logs: conn.log, dns.log, http.log
- [ ] Hunting en Security Onion
- [ ] **PROYECTO**: Montar lab completo con Security Onion

#### **Network Monitoring Tools**
- [ ] Zeek (Bro): Scripts básicos
- [ ] Ntopng: Traffic monitoring
- [ ] pfSense: Firewall rules y logs
- [ ] Cacti/Nagios: Infrastructure monitoring
- [ ] Flow analysis: Silk tools
- [ ] **LAB**: Detectar C2 traffic con Zeek

---

### **Threat Intelligence & IOCs**

#### **Threat Intelligence Fundamentos**
- [ ] **[CISCO NETACAD]**: Repasar Cyber Threat Management > Threat Intelligence
- [ ] Intelligence cycle: Requisitos, colección, análisis, diseminación
- [ ] Tipos: Strategic, Tactical, Operational
- [ ] Threat actors: APT groups, cybercrime, hacktivists
- [ ] TTPs vs IOCs: Diferencias y uso
- [ ] Pyramid of Pain: Entender el modelo
- [ ] **EJERCICIO**: Analizar 3 reportes de APT

#### **Indicators of Compromise**
- [ ] Tipos de IOCs: Hash, IP, Domain, URL, Email
- [ ] Formatos: STIX/TAXII, OpenIOC, YARA
- [ ] Lifecycle: Collection → Enrichment → Distribution
- [ ] Context: No usar IOCs sin contexto
- [ ] Aging: IOCs tienen fecha de vencimiento
- [ ] **LAB**: Crear base de 100 IOCs con contexto

#### **MITRE ATT&CK Framework**
- [ ] Tactics: Las 14 tácticas de la matriz
- [ ] Techniques: 20 técnicas más comunes
- [ ] Sub-techniques: Detalle de técnicas
- [ ] Navigator: Crear heat maps
- [ ] Detection: Mapear controles a técnicas
- [ ] **PROYECTO**: Mapear tu SOC a ATT&CK

#### **Threat Intelligence Platforms**
- [ ] MISP: Instalación y uso básico
- [ ] VirusTotal: API y búsquedas avanzadas
- [ ] AlienVault OTX: Uso de pulses
- [ ] Feeds comerciales: Integration
- [ ] Threat hunting con TI: IOC pivoting
- [ ] **LAB**: Integrar MISP con Splunk

---

### **Incident Response Básico**

#### **NIST Incident Response Lifecycle**
- [ ] Fase 1: Preparation (playbooks, tools, training)
- [ ] Fase 2: Detection & Analysis
- [ ] Fase 3: Containment (short-term y long-term)
- [ ] Fase 4: Eradication
- [ ] Fase 5: Recovery
- [ ] Fase 6: Post-Incident Activity
- [ ] **EJERCICIO**: Crear playbook para ransomware

#### **Evidence Handling**
- [ ] Chain of custody: Formularios y proceso
- [ ] Disk imaging: dd, FTK Imager, Autopsy
- [ ] Memory capture: DumpIt, WinPmem
- [ ] Hash verification: MD5, SHA256
- [ ] Legal: Admisibilidad de evidencia
- [ ] **LAB**: Adquirir evidencia de endpoint comprometido

#### Incident Analysis
- [ ] Timeline creation: Correlación de eventos
- [ ] Root cause analysis: 5 whys
- [ ] Scope determination: Lateral movement
- [ ] Artifact analysis: Prefetch, MFT, registry
- [ ] Malware triage: Identificación rápida
- [ ] **CASO PRÁCTICO**: Investigar brecha completa

#### **Reporting & Communication**
- [ ] Incident reports: Executive summary + technical details
- [ ] Stakeholder management: Quién necesita qué info
- [ ] Timeline: Cronología clara de eventos
- [ ] Lessons learned: Template y facilitación
- [ ] Métricas: Impacto, tiempo de respuesta
- [ ] **EJERCICIO**: Escribir 3 informes de incidente

---

## **INTERMEDIATE BLUE TEAM SKILLS**

### **SIEM & Advanced Analytics**

#### **Semana 1-2: SPL Avanzado**
- [ ] Statistical functions: avg, stdev, percentile
- [ ] Subsearches: Correlación compleja
- [ ] Macros y lookups avanzados
- [ ] Time-based analysis: trends y outliers
- [ ] Command chaining: Queries multi-etapa
- [ ] **LAB**: 15 queries avanzadas para detección

#### **Machine Learning en SIEM**
- [ ] Anomaly detection: Behavioral baselines
- [ ] Splunk ML Toolkit: Uso básico
- [ ] Clustering: Agrupar eventos similares
- [ ] Forecasting: Predecir volumetría
- [ ] Use cases: Login anomalies, data exfil
- [ ] **PROYECTO**: Modelo ML para detectar DGA domains

#### **SIEM Architecture**
- [ ] Distributed deployment: Indexers, search heads
- [ ] Data models: CIM (Common Information Model)
- [ ] Index design: Hot/warm/cold arquitectura
- [ ] Retention policies: Balancear storage/compliance
- [ ] Performance tuning: Acceleraciones y summaries
- [ ] **LAB**: Diseñar arquitectura para 1TB/día

#### **Custom Content Development**
- [ ] Apps de Splunk: Estructura y desarrollo
- [ ] Custom commands: Python scripts
- [ ] Dashboards avanzados: Drilldowns, tokens
- [ ] Saved searches: Schedule y alerting
- [ ] API integration: REST endpoints
- [ ] **PROYECTO**: App completa para phishing detection

---

### **Threat Hunting Fundamentos**

#### **Hunting Methodology**
- [ ] Hypothesis-driven hunting: Formular hipótesis
- [ ] Hunt missions: Planning y scoping
- [ ] Hunt matrix: ATT&CK-based hunting
- [ ] Success metrics: Tracking effectiveness
- [ ] Documentation: Hunt reports
- [ ] **EJERCICIO**: 5 hipótesis de hunting

#### **Hunting Techniques**
- [ ] Stacking: Frequency analysis
- [ ] Clustering: Group similar events
- [ ] Outlier detection: Find anomalies
- [ ] Pattern recognition: Behavioral patterns
- [ ] Statistical analysis: Z-score, chi-square
- [ ] **LAB**: Hunt en dataset real de 1M eventos

#### **MITRE ATT&CK Hunting**
- [ ] Technique-based hunting: T1059, T1053, T1003
- [ ] Data sources: Mapear logs a técnicas
- [ ] Hunt playbooks: 10 playbooks por técnica
- [ ] Coverage analysis: Gap identification
- [ ] Priority matrix: High-value techniques
- [ ] **PROYECTO**: 20 hunts basados en ATT&CK

#### **Hunting con ELK**
- [ ] Elasticsearch: Query DSL avanzado
- [ ] Kibana: Visualizations para hunting
- [ ] Logstash: Parsing personalizado
- [ ] Beats: Fleet management
- [ ] HELK: Hunting ELK setup
- [ ] **LAB**: Montar stack ELK para hunting

---

### **Malware Analysis Básico**

#### **Static Analysis**
- [ ] File format: PE structure, headers
- [ ] Strings: Extraer con strings.exe
- [ ] Metadata: ExifTool, PEiD
- [ ] Hashes: MD5, SHA1, SHA256, SSDEEP
- [ ] Packer detection: UPX, Themida, ASPack
- [ ] **LAB**: Analizar 10 malware samples (static)

#### **Dynamic Analysis**
- [ ] Sandbox: Cuckoo, ANY.RUN, Joe Sandbox
- [ ] Behavioral indicators: Registry, files, network
- [ ] Process monitoring: Process Monitor, Process Hacker
- [ ] Network traffic: Wireshark durante ejecución
- [ ] Memory strings: Detectar deobfuscation
- [ ] **LAB**: Ejecutar 10 malware en sandbox

#### **YARA Rules**
- [ ] Sintaxis YARA: strings, conditions
- [ ] Reglas para familias: Emotet, Trickbot, Cobalt Strike
- [ ] Testing: Falsos positivos/negativos
- [ ] Performance: Optimizar reglas lentas
- [ ] Distribution: YaraHub, YaraRules project
- [ ] **PROYECTO**: Crear 20 reglas YARA custom

#### **Reverse Engineering Básico**
- [ ] Ghidra: Setup y uso básico
- [ ] Assembly: x86/x64 instructions básicas
- [ ] Control flow: If, loops, functions
- [ ] API calls: WinAPI common functions
- [ ] Debugging: x64dbg paso a paso
- [ ] **LAB**: Reversear 5 crackmes simples

---
### **Digital Forensics**

#### **Disk Forensics**
- [ ] Imaging: E01, dd, AFF formats
- [ ] Autopsy: Análisis forense completo
- [ ] File systems: NTFS ($MFT, $LogFile), ext4
- [ ] Timeline: Plaso/Log2Timeline
- [ ] Deleted files: Recovery con Autopsy
- [ ] **CASO**: Analizar imagen forense de 100GB

#### **Windows Artifacts**
- [ ] Registry: SAM, NTUSER, SYSTEM, SOFTWARE
- [ ] Prefetch: Execution evidence
- [ ] LNK files: Recent documents
- [ ] Jump Lists: Application usage
- [ ] Event logs: Forense con Evtx
- [ ] **LAB**: Reconstruir actividad de usuario

#### **Memory Forensics**
- [ ] Memory acquisition: DumpIt, WinPmem, LIME
- [ ] Volatility: Profiles y plugins
- [ ] Process analysis: pslist, pstree, malfind
- [ ] Network: netscan, connections
- [ ] Malware detection: malfind, yarascan
- [ ] **LAB**: Analizar memory dump con Volatility

#### **Network Forensics**
- [ ] PCAP carving: NetworkMiner, Xplico
- [ ] Protocol reconstruction: HTTP, FTP, SMTP
- [ ] File extraction: Binarios de tráfico
- [ ] Encryption detection: TLS handshakes
- [ ] Timeline correlation: Network + endpoint
- [ ] **CASO**: Reconstruir ataque desde PCAPs

---
### **Endpoint Detection & Response (EDR)**

#### **EDR Fundamentals**
- [ ] EDR vs AV: Diferencias clave
- [ ] Arquitectura: Agent, cloud, console
- [ ] Telemetry: Qué recolecta un EDR
- [ ] Behavioral detection: Process chains, anomalies
- [ ] Response: Isolate, contain, remediate
- [ ] **LAB**: Configurar trial de EDR (CrowdStrike/SentinelOne)

#### **Endpoint Monitoring**
- [ ] Process monitoring: CreateProcess, injection
- [ ] File monitoring: Write, modify, delete
- [ ] Registry monitoring: Persistence locations
- [ ] Network monitoring: C2 detection
- [ ] PowerShell: Script Block Logging analysis
- [ ] **LAB**: Detectar 10 técnicas con EDR

#### **EDR Investigation**
- [ ] Alert triage: Prioritización en EDR
- [ ] Timeline analysis: Process tree
- [ ] IOC search: Hash, domain, IP hunting
- [ ] Host isolation: Cuando y cómo
- [ ] Evidence collection: Live response
- [ ] **CASO**: Investigar ransomware con EDR

#### **Response Automation**
- [ ] Playbooks: Automatizar respuestas comunes
- [ ] Scripts: PowerShell/Python para remediation
- [ ] API usage: Automatizar EDR con API
- [ ] Integration: EDR + SIEM + SOAR
- [ ] Orchestration: Workflows multi-tool
- [ ] **PROYECTO**: 5 playbooks automatizados

#### **SOAR & Workflow Automation**
- [ ] Conceptos SOAR: Orquestación y respuesta automatizada
- [ ] Playbooks: Automatización de bloqueos de IP y enriquecimiento de alertas
- [ ] Herramientas Open Source: Shuffle o TheHive/Cortex
- [ ] **LAB**: Crear un flujo automatizado que analice una IP en VirusTotal

---
### **Cloud Security Monitoring**

#### **Cloud Security Fundamentals**
- [ ] Shared responsibility: AWS/Azure/GCP
- [ ] IAM: Roles, policies, MFA
- [ ] Network: VPC, security groups, NACLs
- [ ] Data protection: Encryption, DLP
- [ ] Compliance: CIS Benchmarks
- [ ] **LAB**: Configurar AWS cuenta con security baseline

#### **AWS Security Monitoring**
- [ ] CloudTrail: Logs de API calls
- [ ] GuardDuty: Threat detection alerts
- [ ] Config: Compliance y drift detection
- [ ] VPC Flow Logs: Network traffic analysis
- [ ] Security Hub: Centralized findings
- [ ] **LAB**: Detectar 5 ataques en AWS

#### **Azure Security Monitoring**
- [ ] Azure Monitor: Logs y metrics
- [ ] Security Center: Posture management
- [ ] Azure AD: Sign-in logs, risky users
- [ ] Network Security Groups: Flow logs
- [ ] Sentinel: SIEM nativo de Azure
- [ ] **LAB**: Configurar Sentinel para Azure

#### **Cloud Detection Engineering**
- [ ] CloudTrail queries: Abuse de IAM
- [ ] S3 bucket attacks: Detección
- [ ] Crypto mining: EC2/Lambda abuse
- [ ] Data exfiltration: S3, RDS
- [ ] Privilege escalation: IAM changes
- [ ] **PROYECTO**: 20 detecciones cloud-native

---
## **PROYECTO FINAL: Purple Team Exercise**

### **Objetivo**
Simular ataque completo y detectarlo con todas las herramientas aprendidas

### **Scope**
- [ ] Red Team: Ejecutar 10 técnicas ATT&CK
- [ ] Blue Team: Detectar con SIEM, EDR, IDS
- [ ] Incident Response: Documentar y responder
- [ ] Report: Informe ejecutivo + técnico

### **Técnicas a Simular**
- [ ] T1566.001: Spearphishing Attachment
- [ ] T1059.001: PowerShell execution
- [ ] T1003.001: LSASS credential dumping
- [ ] T1021.001: RDP lateral movement
- [ ] T1053.005: Scheduled task persistence
- [ ] T1071.001: C2 over HTTP/HTTPS
- [ ] T1083: File and directory discovery
- [ ] T1005: Data from local system
- [ ] T1048.003: Exfiltration over unencrypted protocol
- [ ] T1490: Inhibit system recovery

### **Deliverables**
- [ ] Detection rules para cada técnica
- [ ] Hunting queries
- [ ] Incident response playbook
- [ ] Post-mortem report
- [ ] Lessons learned

---
### **Plataformas Hands-on**
- [ ] TryHackMe: SOC Level 1 & 2 paths
- [ ] LetsDefend: SOC Analyst challenges
- [ ] CyberDefenders: Blue Team labs
- [ ] Boss of the SOC (BOTS): Splunk datasets
- [ ] Blue Team Labs Online
 
---
## **Checklist de Validación Mensual**

Al final de cada mes, verificar:

- [ ] ¿Completé al menos 80% de los ítems?
- [ ] ¿Hice los labs prácticos?
- [ ] ¿Puedo explicar cada concepto en 2 minutos?
- [ ] ¿Documenté lo aprendido?
- [ ] ¿Actualicé mi LinkedIn/GitHub?

---

**Total: 24 meses | ~500 ítems | Tiempo estimado: 20-30 horas/semana**
