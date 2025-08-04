# Technical Architecture Document - AI Tour Management Agent for UrbanHub

## Executive Summary

Este documento define la arquitectura técnica para la implementación del AI Tour Management Agent de UrbanHub en la plataforma Bird.com. La solución utiliza un patrón Single Agent optimizado para la gestión de tours de propiedades residenciales, integrándose con Google Calendar y Salesforce CRM. La arquitectura está diseñada para operar dentro de las limitaciones de configuración manual de Bird.com mientras maximiza la eficiencia operacional y la experiencia del usuario en español mexicano.

## Architecture Overview

### Selected Pattern
**Pattern**: Single Agent Pattern
**Rationale**: 
- Dominio específico y bien definido (agendamiento de tours)
- Flujos de conversación lineales y predecibles
- Integración principal única (Google Calendar)
- Simplifica mantenimiento y optimización
- Reduce complejidad de handovers innecesarios

**Scalability Considerations**:
- Arquitectura permite expansión futura a multi-agent
- Knowledge base modular para agregar nuevos dominios
- APIs diseñadas para soportar múltiples agentes
- Monitoreo centralizado para identificar necesidades de especialización

### Agent Architecture

#### Agent 1: Alex - Tour Management Specialist
- **Function**: Gestión completa del proceso de agendamiento de tours para propiedades residenciales
- **Model Configuration**: 
  - Model: GPT-4
  - Temperature: 0.7
  - Max Tokens: 500
  - Top P: 0.95
  - Frequency Penalty: 0.2
- **Knowledge Base**: 
  - `/properties/` - Catálogo de propiedades disponibles
  - `/processes/` - Procedimientos de agendamiento
  - `/policies/` - Políticas de tours y requisitos
  - `/faqs/` - Preguntas frecuentes
- **Integrations**: 
  - Google Calendar API (lectura/escritura)
  - Salesforce CRM (creación/actualización de leads)
  - WhatsApp Business API (mensajería rica)
- **Performance Targets**: 
  - Response time: <2 segundos
  - Scheduling accuracy: >95%
  - User satisfaction: >4.0/5.0

### System Flow Architecture

```
Usuario WhatsApp → Bird.com Platform → AI Agent (Alex)
                                           ↓
                                    Knowledge Base
                                           ↓
                                    Decision Engine
                                           ↓
                            ┌──────────────┴──────────────┐
                            ↓                             ↓
                    Google Calendar API            Salesforce CRM
                            ↓                             ↓
                    Schedule Confirmation          Lead Registration
                            ↓                             ↓
                            └──────────────┬──────────────┘
                                           ↓
                                  WhatsApp Response → Usuario
```

## Bird.com Configuration Specifications

### Profile Configuration

#### Alex - Tour Management Specialist
```
Profile Setup:
- Name: Alex de UrbanHub
- Avatar: Professional, friendly, gender-neutral avatar
- Description: Especialista en agendamiento de tours para propiedades UrbanHub
- Model: GPT-4
- Temperature: 0.7
- Max Tokens: 500
- System Message: "Eres Alex, el especialista en tours de UrbanHub. Ayudas a prospectos a agendar tours de propiedades usando un tono cálido y profesional en español mexicano. Tienes acceso al calendario de disponibilidad y conoces todas las propiedades. Tu objetivo es hacer el proceso de agendamiento rápido, fácil y agradable."

Personality Configuration:
- Purpose: "Especialista en agendamiento de tours para propiedades residenciales UrbanHub, disponible 24/7 vía WhatsApp para hacer el proceso rápido y sencillo"
- Tasks: 
  1. Agendar nuevos tours verificando disponibilidad en tiempo real
  2. Modificar o cancelar tours existentes
  3. Proporcionar información sobre propiedades y proceso de renta
  4. Hacer seguimiento post-tour para mantener interés
  5. Calificar leads básicamente antes de transferir a ventas
- Audience: "Prospectos mexicanos de 25-45 años buscando rentar departamentos premium en zonas urbanas, que valoran respuesta rápida y servicio personalizado"
- Tone: "Cálido, profesional, entusiasta sin ser excesivo. Usa español mexicano neutro CDMX con expresiones como 'claro que sí', 'con mucho gusto', '¿te parece bien?'. Transmite confianza y conocimiento del mercado inmobiliario."
- Custom Instructions: "
  1. Siempre verifica disponibilidad en calendario antes de confirmar
  2. Recolecta información completa: nombre, propiedad de interés, fecha/hora preferida, número de asistentes
  3. Ofrece mínimo 3 opciones de horarios cuando sea posible
  4. Envía confirmación detallada con dirección y mapa
  5. Programa recordatorio automático 24 horas antes
  6. Si no hay disponibilidad, ofrece lista de espera
  7. Para cambios <24 horas, explica política y ofrece alternativas
  8. Mantén entusiasmo por las propiedades sin presionar
  9. Si detectas alto interés, ofrece agendar aplicación post-tour
  10. Escala a humano para: negociación de precios, temas legales, problemas técnicos no resueltos"

AI Actions Configuration:
- Main Task: Tour Scheduling Process
  - Trigger: Automatic on conversation start
  - Steps:
    1. Identificar intención de tour
    2. Recolectar información necesaria
    3. Verificar disponibilidad en calendario
    4. Ofrecer opciones disponibles
    5. Confirmar selección
    6. Crear evento en calendario
    7. Registrar lead en CRM
    8. Enviar confirmación por WhatsApp
- Handover Action:
  - Triggers: 
    - Keywords: "hablar con alguien", "agente humano", "necesito ayuda"
    - Situations: Negociación de precio, problemas legales, quejas graves
    - Complexity: Más de 10 intercambios sin resolución
  - Context Transfer: Resumen de conversación, información recolectada, motivo de escalación
  - Message: "Con gusto te voy a conectar con uno de nuestros asesores especializados que podrá ayudarte mejor con este tema. Un momento por favor..."
- Send Message Action:
  - Tour Reminder: 24 horas antes del tour
  - Follow-up: 2 horas después del tour
  - Re-engagement: 3 días después si no hubo respuesta
- Resolve Conversation:
  - Success: Tour agendado exitosamente
  - Completion: Usuario indica no necesitar más ayuda
  - Timeout: 30 minutos sin actividad
```

### Knowledge Base Architecture

#### Folder Structure
```
knowledge-base/
├── properties/
│   ├── available-units.md (1,500 words)
│   │   - Lista actualizada de unidades disponibles
│   │   - Características principales por propiedad
│   │   - Rangos de precio y promociones
│   ├── property-features.md (1,200 words)
│   │   - Amenidades por desarrollo
│   │   - Especificaciones técnicas
│   │   - Ventajas competitivas
│   ├── neighborhood-guide.md (1,800 words)
│   │   - Información por colonia
│   │   - Servicios cercanos
│   │   - Transporte y conectividad
│   └── virtual-tours.md (800 words)
│       - Links a tours 360°
│       - Videos de propiedades
│       - Galerías fotográficas
├── processes/
│   ├── tour-scheduling-steps.md (1,000 words)
│   │   - Proceso paso a paso
│   │   - Información requerida
│   │   - Confirmación y seguimiento
│   ├── tour-requirements.md (600 words)
│   │   - Documentos necesarios
│   │   - Políticas de asistencia
│   │   - Protocolo COVID-19
│   ├── application-process.md (900 words)
│   │   - Requisitos post-tour
│   │   - Proceso de aplicación
│   │   - Tiempos y costos
│   └── move-in-checklist.md (700 words)
│       - Pasos para mudanza
│       - Servicios incluidos
│       - Contactos importantes
├── policies/
│   ├── touring-policies.md (800 words)
│   │   - Horarios disponibles
│   │   - Política de cancelación
│   │   - Número máximo de asistentes
│   ├── pet-policy.md (500 words)
│   │   - Mascotas permitidas
│   │   - Restricciones y costos
│   │   - Áreas pet-friendly
│   ├── pricing-deposits.md (1,100 words)
│   │   - Estructura de precios
│   │   - Depósitos requeridos
│   │   - Formas de pago
│   └── terms-conditions.md (1,400 words)
│       - Términos de servicio
│       - Privacidad de datos
│       - Derechos y obligaciones
├── faqs/
│   ├── general-questions.md (1,300 words)
│   │   - Top 20 preguntas frecuentes
│   │   - Respuestas estándar
│   │   - Enlaces a más información
│   ├── amenities-services.md (900 words)
│   │   - Servicios incluidos
│   │   - Costos adicionales
│   │   - Horarios y acceso
│   └── maintenance-support.md (700 words)
│       - Proceso de reportes
│       - Tiempos de respuesta
│       - Contactos de emergencia
└── scripts/
    ├── greeting-variations.md (500 words)
    │   - Saludos por hora del día
    │   - Respuestas a diferentes intenciones
    │   - Personalización por contexto
    ├── objection-handling.md (1,000 words)
    │   - Objeciones comunes
    │   - Respuestas recomendadas
    │   - Cuándo escalar
    └── closing-statements.md (600 words)
        - Despedidas exitosas
        - Seguimientos programados
        - Llamadas a acción
```

#### Content Optimization Specifications
- **File Size**: 500-1,800 palabras por archivo para balance óptimo
- **Header Structure**: 
  - H1: Tema principal alineado con intención del usuario
  - H2: Subtemas específicos (variaciones comunes)
  - H3: Información detallada (respuestas específicas)
- **Keyword Optimization**: 
  - Términos naturales en español mexicano
  - Sinónimos y variaciones (depa/departamento, renta/alquiler)
  - Densidad 2-3% sin forzar
- **Cross-References**: Links internos entre temas relacionados usando formato `[texto](../carpeta/archivo.md)`
- **Update Protocol**: 
  - Diario: Disponibilidad de unidades
  - Semanal: Promociones y eventos
  - Mensual: Políticas y procedimientos
  - Trimestral: Revisión completa de contenido

### Integration Architecture

#### WhatsApp Business API Integration
```
Setup Configuration:
- Business Account: UrbanHub Oficial (Verificado ✓)
- Phone Number: +52 55 1234 5678 (Dedicado para tours)
- Display Name: "UrbanHub Tours 🏢"
- Category: Real Estate
- Description: "Agenda tu tour 24/7 📱 Tu nuevo hogar te espera"

Message Capabilities:
- Text Messages: ✓ Conversaciones completas
- Images: ✓ Fotos de propiedades (máx 5MB)
- Location: ✓ Mapas de ubicación
- Documents: ✓ PDFs informativos (máx 100MB)
- Quick Replies: ✓ Hasta 3 opciones
- List Messages: ✓ Hasta 10 elementos

Template Messages (Pre-aprobados):
1. tour_confirmation_es
   "¡Hola {{1}}! Tu tour está confirmado ✅
   📅 Fecha: {{2}}
   🕐 Hora: {{3}}
   📍 Propiedad: {{4}}
   👤 Te atenderá: {{5}}
   
   📍 Ver ubicación: {{6}}
   
   Te enviaremos un recordatorio 24h antes. ¡Nos vemos pronto!"

2. tour_reminder_24h_es
   "¡Hola {{1}}! 🔔 Te recordamos tu tour mañana:
   📅 {{2}} a las {{3}}
   📍 {{4}}
   
   ¿Necesitas cambiar la hora? Responde CAMBIAR
   ¿Todo bien? Responde CONFIRMO
   
   ¡Te esperamos! 🏠"

3. tour_followup_es
   "¡Hola {{1}}! 👋 ¿Qué tal tu tour en {{2}}?
   
   Nos encantaría saber tu opinión:
   ⭐⭐⭐⭐⭐ ¿Cómo fue tu experiencia?
   
   ¿Te gustó la propiedad? Podemos ayudarte con el siguiente paso 🏡"

Rate Limiting Strategy:
- Business Initiated: 1,000 mensajes/día
- User Initiated: Sin límite en ventana 24h
- Template Messages: 100,000/mes
- Media Messages: Optimización de caché para imágenes frecuentes

Session Management:
- 24-hour window tracking automático
- Contexto preservado durante toda la sesión
- Handoff mantiene historial completo
- Resumen automático en reinicios
```

#### Google Calendar API Integration
```
API Configuration:
- Service: Google Calendar API v3
- Auth Method: Service Account con dominio delegado
- Scopes: 
  - calendar.events.read
  - calendar.events.write
  - calendar.settings.readonly
- Calendar ID: tours@urbanhub.mx

Availability Logic:
- Business Hours: Lun-Vie 9AM-7PM, Sáb 10AM-5PM
- Tour Duration: 45 minutos por defecto
- Buffer Time: 15 minutos entre tours
- Max Tours per Slot: 3 (diferentes agentes)
- Timezone: America/Mexico_City (GMT-6)

Booking Process:
1. Check Availability:
   GET /calendars/{calendarId}/events
   timeMin: {current_time}
   timeMax: {current_time + 14 days}
   
2. Create Event:
   POST /calendars/{calendarId}/events
   {
     "summary": "Tour - {nombre_prospecto} - {propiedad}",
     "location": "{direccion_propiedad}",
     "description": "Prospecto: {nombre}\nTeléfono: {whatsapp}\nPersonas: {num_asistentes}\nNotas: {comentarios}",
     "start": {"dateTime": "{fecha_hora}", "timeZone": "America/Mexico_City"},
     "end": {"dateTime": "{fecha_hora + 45min}", "timeZone": "America/Mexico_City"},
     "attendees": [
       {"email": "{prospecto_email}", "responseStatus": "accepted"},
       {"email": "{agente_email}", "responseStatus": "accepted"}
     ],
     "reminders": {
       "useDefault": false,
       "overrides": [
         {"method": "email", "minutes": 1440},
         {"method": "popup", "minutes": 60}
       ]
     }
   }

3. Update Event (Reschedule/Cancel):
   PUT/DELETE /calendars/{calendarId}/events/{eventId}

Error Handling:
- API Timeout: Retry con exponential backoff (3 intentos)
- Calendar Unavailable: Mensaje explicativo + escalación humana
- Conflicto de Horario: Ofrecer alternativas automáticamente
- Quota Exceeded: Failover a calendario secundario
```

#### Salesforce CRM Integration
```
API Configuration:
- Instance: https://urbanhub.my.salesforce.com
- Auth: OAuth 2.0 con refresh token
- API Version: v59.0
- Integration User: birdai@urbanhub.mx

Lead Creation:
POST /sobjects/Lead
{
  "FirstName": "{nombre}",
  "LastName": "{apellido}",
  "Company": "Individual",
  "Phone": "{whatsapp_number}",
  "LeadSource": "WhatsApp Bot",
  "Status": "New",
  "Rating": "Warm",
  "Property_Interest__c": "{propiedad_id}",
  "Tour_Date__c": "{fecha_tour}",
  "Number_of_Occupants__c": {num_personas},
  "Preferred_Move_Date__c": "{fecha_mudanza}",
  "Budget_Range__c": "{rango_precio}",
  "Has_Pets__c": {boolean},
  "Additional_Notes__c": "{notas_conversacion}"
}

Lead Update (Post-Tour):
PATCH /sobjects/Lead/{leadId}
{
  "Status": "Toured",
  "Tour_Completed__c": true,
  "Tour_Feedback_Score__c": {score_1_5},
  "Tour_Comments__c": "{feedback_text}",
  "Next_Step__c": "{siguiente_accion}",
  "Follow_Up_Date__c": "{fecha_seguimiento}"
}

Activity Logging:
POST /sobjects/Task
{
  "Subject": "WhatsApp Conversation - {tipo_interaccion}",
  "WhoId": "{leadId}",
  "Status": "Completed",
  "Priority": "Normal",
  "ActivityDate": "{fecha}",
  "Description": "{resumen_conversacion}",
  "Type": "WhatsApp Message"
}

Custom Fields Mapping:
- Property_Interest__c → ID de propiedad UrbanHub
- Tour_Date__c → Fecha y hora del tour agendado
- Conversation_Transcript__c → Historial completo de WhatsApp
- AI_Qualification_Score__c → Score automático de calificación
- Preferred_Contact_Method__c → "WhatsApp" por defecto
```

## Performance and Monitoring

### Key Performance Indicators
| Metric | Target | Measurement Method | Alert Threshold |
|--------|--------|--------------------|-----------------|
| Response Time | <2 seconds | Bird.com Analytics | >5 seconds |
| Scheduling Accuracy | >95% | Calendar audit | <90% |
| Conversation Completion | >80% | Resolution tracking | <75% |
| User Satisfaction | >4.0/5.0 | Post-tour survey | <3.5/5.0 |
| API Success Rate | >99% | Integration monitoring | <95% |
| No-Show Rate | <15% | Calendar analysis | >20% |
| Lead Conversion | >25% | CRM reporting | <20% |

### Monitoring Strategy
```
Real-time Monitoring:
- Bird.com Dashboard:
  - Active conversations
  - Response times
  - Error rates
  - Message volumes
  
- Custom Dashboards:
  - API health status
  - Calendar availability
  - Lead creation rate
  - Conversion funnel

Daily Reviews:
- Conversation quality sampling (10%)
- Failed interaction analysis
- Integration error logs
- User feedback compilation

Weekly Analysis:
- Performance trend analysis
- Knowledge base effectiveness
- Integration reliability metrics
- Cost per conversation

Monthly Reports:
- Business impact metrics
- ROI calculation
- Optimization recommendations
- Capacity planning
```

### Optimization Framework
```
Continuous Improvement Cycle:

1. Data Collection (Real-time)
   - Conversation logs
   - User feedback
   - Performance metrics
   - Error patterns
   ↓
2. Analysis (Daily)
   - Intent recognition accuracy
   - Knowledge base gaps
   - Integration bottlenecks
   - User satisfaction drivers
   ↓
3. Optimization Planning (Weekly)
   - Priority improvements
   - A/B test designs
   - Configuration adjustments
   - Content updates
   ↓
4. Implementation (Bi-weekly)
   - Configuration changes
   - Knowledge base updates
   - Integration optimizations
   - New feature rollouts
   ↓
5. Validation (Monthly)
   - Performance impact measurement
   - User satisfaction surveys
   - Business metric correlation
   - ROI validation
```

## Risk Management and Mitigation

### Technical Risks

1. **Google Calendar API Outage**
   - Impact: No puede verificar disponibilidad ni agendar tours
   - Mitigation: 
     - Cache de disponibilidad local (actualizado cada 5 min)
     - Modo manual: Captura info y procesamiento posterior
     - Mensaje transparente al usuario sobre demora
   - Contingency: Escalación automática a agente humano

2. **WhatsApp Rate Limiting**
   - Impact: Mensajes no entregados o demorados
   - Mitigation:
     - Gestión proactiva de rate limits
     - Distribución de carga entre múltiples números
     - Priorización de mensajes críticos
   - Contingency: SMS backup para confirmaciones críticas

3. **Knowledge Base Inconsistencies**
   - Impact: Información incorrecta o desactualizada
   - Mitigation:
     - Validación automática de cambios
     - Versionado con rollback capability
     - Revisión humana de actualizaciones críticas
   - Contingency: Disclaimers automáticos para info sensible

4. **CRM Sync Failures**
   - Impact: Leads no registrados o duplicados
   - Mitigation:
     - Cola de reintentos con persistencia
     - Deduplicación por número de WhatsApp
     - Logs detallados para reconciliación
   - Contingency: Export manual diario como backup

### Operational Risks

1. **Peak Hour Overload**
   - Impact: Respuestas lentas o timeouts
   - Mitigation:
     - Auto-scaling de recursos
     - Gestión de cola inteligente
     - Respuestas de espera transparentes
   - Contingency: Modo de capacidad reducida

2. **Language Model Hallucinations**
   - Impact: Información incorrecta sobre propiedades
   - Mitigation:
     - Prompts estrictos con boundaries
     - Validación contra knowledge base
     - Confidence thresholds para escalación
   - Contingency: Verificación humana para datos críticos

3. **Integration Dependencies**
   - Impact: Funcionalidad degradada sin APIs
   - Mitigation:
     - Graceful degradation patterns
     - Funcionalidad offline básica
     - Status page para transparencia
   - Contingency: Procesos manuales documentados

## Implementation Roadmap

### Phase 1: Foundation (Week 1-2)
- [x] Bird.com account setup
- [ ] WhatsApp Business configuration
- [ ] Basic agent profile creation
- [ ] Core knowledge base upload
  - [ ] Properties folder complete
  - [ ] Processes documented
  - [ ] Policies uploaded
  - [ ] FAQs structured
- [ ] Initial personality configuration
- [ ] Basic conversation flows

### Phase 2: Integration Development (Week 3-4)
- [ ] Google Calendar API integration
  - [ ] Authentication setup
  - [ ] Availability checking logic
  - [ ] Event creation/modification
  - [ ] Error handling
- [ ] Salesforce CRM integration
  - [ ] OAuth configuration
  - [ ] Lead creation mapping
  - [ ] Activity logging
  - [ ] Sync verification
- [ ] WhatsApp template approval
- [ ] Integration testing suite

### Phase 3: Optimization & Testing (Week 5-6)
- [ ] Performance tuning
  - [ ] Response time optimization
  - [ ] Knowledge base indexing
  - [ ] API call optimization
- [ ] User acceptance testing
  - [ ] Internal team testing
  - [ ] Pilot group (20 users)
  - [ ] Feedback incorporation
- [ ] Monitoring setup
  - [ ] Dashboards configuration
  - [ ] Alert rules
  - [ ] Reporting automation
- [ ] Go-live preparation
  - [ ] Team training
  - [ ] Escalation procedures
  - [ ] Launch communication

## Change Management Process

### Configuration Change Protocol
1. **Change Request Form**
   - Requestor information
   - Change description and justification
   - Expected impact (users, performance, cost)
   - Testing requirements
   
2. **Impact Assessment**
   - Technical feasibility review
   - Risk analysis
   - Resource requirements
   - Timeline estimation
   
3. **Testing Plan**
   - Test scenarios definition
   - Success criteria
   - Rollback procedures
   - Performance benchmarks
   
4. **Implementation Steps**
   - Pre-implementation backup
   - Staged rollout plan
   - Monitoring during deployment
   - Validation checkpoints
   
5. **Post-Implementation**
   - Performance validation
   - User feedback collection
   - Documentation update
   - Lessons learned

### Version Control Strategy
```
Configuration Versioning:
- Git repository for all configurations
- Semantic versioning (MAJOR.MINOR.PATCH)
- Tagged releases with changelogs
- Automated backup before changes

Documentation Standards:
- Markdown format for all docs
- Change history in each file
- Review process for updates
- Publishing to team wiki

Knowledge Base Versioning:
- Date stamps on all content
- Change tracking enabled
- Approval workflow for updates
- Automated quality checks
```

## Security and Compliance

### Data Protection
- **Encryption**: TLS 1.3 for all API communications
- **Authentication**: OAuth 2.0 for integrations, API keys in secure vault
- **PII Handling**: Minimal data retention, automatic purging after 90 days
- **Access Control**: Role-based permissions, audit logging

### Compliance Requirements
- **LFPDPPP**: Mexican data protection law compliance
- **WhatsApp Business Policy**: Message templates, 24-hour window
- **Fair Housing**: No discriminatory language or practices
- **TCPA**: Opt-in consent management

### Security Monitoring
- **API Security**: Rate limiting, IP whitelisting where possible
- **Conversation Security**: No storage of sensitive financial data
- **Access Logs**: All configuration changes tracked
- **Incident Response**: 24/7 security team contact

---

**Document Version**: 1.0  
**Created Date**: January 3, 2025  
**Last Updated**: January 3, 2025  
**Status**: Ready for Scrum Master Review

**Prepared by**: BMAD Architect Agent  
**For**: UrbanHub AI Tour Management Implementation  
**Next Step**: Configuration Story Creation (Scrum Master Agent)