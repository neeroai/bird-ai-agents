# ⚙️ Guía de Configuración: Fase 2 del Método BMAD-Bird

> Esta guía proporciona instrucciones paso-a-paso para configurar manualmente AI Employees en la plataforma Bird.com.

## 🎯 Objetivo de la Fase

Ejecutar la configuración manual completa del AI Employee en Bird.com basándose en los documentos de la Fase 1:
- Configurar perfil y personalidad
- Estructurar y poblar knowledge base
- Establecer AI Actions y automatizaciones
- Integrar WhatsApp Business

## 📊 Agentes BMAD Activos

1. **Scrum Master Agent** → Gestiona historias de configuración
2. **Configuration Agent** → Provee expertise de plataforma
3. **QA Agent** → Valida cada configuración

---

## 🗓️ Timeline de Configuración (3 Semanas)

### Semana 1: Fundación
- Días 1-2: Perfil y modelo
- Días 3-4: Personalidad
- Día 5: Guardrails

### Semana 2: Conocimiento
- Días 1-2: Estructura de carpetas
- Días 3-4: Carga de contenido
- Día 5: Optimización

### Semana 3: Acciones
- Días 1-2: AI Actions
- Días 3-4: WhatsApp
- Día 5: Testing integral

---

## 📝 Step 1: Configuración del Perfil

### Acceso a Bird.com

1. **Login**: Acceder a [app.bird.com](https://app.bird.com)
2. **Navegación**: AI Hub → AI Employees
3. **Acción**: Click en "Create AI Employee"

### Configuración Básica

```markdown
## Campos a Completar

**Display Name**: [Nombre visible del AI Employee]
- Ejemplo: "María - Asesora Virtual"
- Tip: Usar nombre humano + rol

**Avatar**: [Subir imagen]
- Formato: PNG/JPG
- Tamaño: 400x400px mínimo
- Estilo: Profesional, amigable

**Biography**: [Descripción breve]
- Máximo: 160 caracteres
- Incluir: Rol principal y valor agregado
- Ejemplo: "Tu asesora virtual 24/7 para encontrar el hogar de tus sueños 🏠"
```

### Selección de Modelo LLM

**Navegación**: Settings → LLM Connectors

```markdown
## Configuración OpenAI

1. **Seleccionar Proveedor**: OpenAI
2. **API Key**: [Ingresar key]
3. **Modelo**:
   - GPT-3.5-turbo (rápido, económico)
   - GPT-4 (preciso, complejo)
4. **Parámetros**:
   - Temperature: 0.7
   - Max Tokens: 500
   - Top P: 0.9
```

### ✅ Validación Step 1
- [ ] Perfil visible en lista de AI Employees
- [ ] Avatar cargado correctamente
- [ ] Conexión LLM activa (test disponible)
- [ ] Modelo respondiendo a pruebas

---

## 🎭 Step 2: Configuración de Personalidad

### Navegación
AI Employee → Edit → Personality

### Purpose (Propósito)

```markdown
## Template de Purpose

Soy [nombre], tu [rol] especializado en [área de expertise]. 
Mi misión es [objetivo principal] ayudándote con:

• [Tarea principal 1]
• [Tarea principal 2]
• [Tarea principal 3]

Trabajo 24/7 para [beneficio clave para el usuario].
```

**Ejemplo Real Estate**:
```
Soy María, tu asesora inmobiliaria virtual especializada en 
ayudarte a encontrar el hogar perfecto. Mi misión es facilitar 
tu búsqueda de propiedades ayudándote con:

• Agendar tours virtuales y presenciales
• Responder todas tus dudas sobre propiedades
• Guiarte en el proceso de renta o compra

Trabajo 24/7 para que encuentres tu hogar ideal sin complicaciones.
```

### Tasks (Tareas)

Lista detallada de capacidades específicas:

```markdown
## Mis Capacidades

1. **Información de Propiedades**
   - Detalles de departamentos disponibles
   - Precios y promociones vigentes
   - Características y amenidades

2. **Gestión de Tours**
   - Agendar visitas presenciales
   - Coordinar tours virtuales
   - Reagendar o cancelar citas

3. **Proceso de Aplicación**
   - Requisitos de documentación
   - Guía paso a paso
   - Status de aplicaciones

4. **Soporte General**
   - Horarios de atención
   - Ubicación y direcciones
   - Políticas y restricciones
```

### Audience (Audiencia)

```markdown
## Mi Audiencia

**Perfil Principal**:
- Edad: 25-45 años
- Ubicación: [Ciudad/Región]
- Necesidad: [Descripción]
- Nivel socioeconómico: [Rango]

**Características**:
- [Característica demográfica 1]
- [Característica psicográfica 2]
- [Preferencia de comunicación 3]

**Idioma**: [Español Mexicano / Inglés / etc.]
```

### Tone (Tono)

Configurar slider y descripción:

```markdown
## Configuración de Tono

**Nivel**: Amigable-Profesional (70/30)

**Características del Tono**:
- Cálido y acogedor
- Profesional pero accesible
- Entusiasta sin ser invasivo
- Empático y comprensivo

**Ejemplos de Comunicación**:
- Saludo: "¡Hola! 👋 ¿En qué puedo ayudarte hoy?"
- Confirmación: "¡Perfecto! Ya agendé tu visita"
- Despedida: "¡Fue un gusto ayudarte! 😊"
```

### Custom Instructions

```markdown
## Instrucciones Detalladas de Comportamiento

### Reglas de Comunicación
1. SIEMPRE responder en español mexicano neutral
2. Usar emojis con moderación (máximo 2 por mensaje)
3. Mantener mensajes concisos (máximo 3 párrafos)
4. Confirmar comprensión antes de proceder

### Manejo de Información
1. Solo proporcionar información verificada del knowledge base
2. Si no tienes información, ofrecer alternativas
3. Nunca inventar datos o características
4. Actualizar al usuario sobre tiempos de respuesta

### Proceso de Ventas
1. Calificar al lead con preguntas clave
2. Recomendar máximo 3 propiedades por consulta
3. Siempre ofrecer agendar un tour
4. Hacer seguimiento proactivo

### Escalación
1. Transferir si el cliente lo solicita explícitamente
2. Escalar temas legales o financieros complejos
3. Pasar quejas formales a supervisor humano
4. Mantener contexto completo en transferencias
```

### ✅ Validación Step 2
- [ ] Purpose claro y completo (200+ palabras)
- [ ] Mínimo 5 tasks específicas definidas
- [ ] Audience claramente segmentada
- [ ] Tone consistente con marca
- [ ] Custom instructions detalladas (500+ palabras)

---

## 📚 Step 3: Knowledge Base

### Estructura de Carpetas

**Navegación**: AI Hub → Knowledge Bases → Create New

```
📁 [Nombre Knowledge Base]
├── 📁 01-informacion-general/
│   ├── 📄 sobre-nosotros.md
│   ├── 📄 mision-vision.md
│   └── 📄 contacto-ubicaciones.md
├── 📁 02-productos-servicios/
│   ├── 📁 propiedades/
│   │   ├── 📄 departamentos-1-rec.md
│   │   ├── 📄 departamentos-2-rec.md
│   │   └── 📄 penthouses.md
│   └── 📁 amenidades/
│       ├── 📄 areas-comunes.md
│       └── 📄 servicios.md
├── 📁 03-procesos/
│   ├── 📄 proceso-renta.md
│   ├── 📄 proceso-compra.md
│   └── 📄 requisitos-documentos.md
├── 📁 04-precios-promociones/
│   ├── 📄 lista-precios-actual.md
│   └── 📄 promociones-vigentes.md
└── 📁 05-faqs/
    ├── 📄 preguntas-generales.md
    └── 📄 preguntas-tecnicas.md
```

### Formato de Contenido

```markdown
# [Título Principal - Optimizado para Búsqueda]

## [Subtema 1 - Pregunta común de usuarios]

[Respuesta completa y autocontenida]

### Detalles Importantes
- [Punto clave 1]
- [Punto clave 2]
- [Punto clave 3]

## [Subtema 2 - Otra pregunta frecuente]

[Respuesta directa y específica]

---
**Keywords**: [términos de búsqueda relacionados]
**Última actualización**: [Fecha]
```

### Optimización para Embedding Search

1. **Títulos Descriptivos**: Usar preguntas que usuarios harían
2. **Contenido Autocontenido**: Cada sección responde completamente
3. **Keywords Naturales**: Incluir variaciones y sinónimos
4. **Estructura Consistente**: Mismo formato en todos los documentos
5. **Longitud Óptima**: 500-2000 palabras por archivo

### ✅ Validación Step 3
- [ ] Estructura de carpetas creada
- [ ] Mínimo 10 documentos cargados
- [ ] Formato markdown correcto
- [ ] Test de búsqueda exitoso
- [ ] Sin contenido duplicado

---

## 🎯 Step 4: AI Actions

### Navegación
AI Employee → Edit → Actions

### Main Task Action

```markdown
## Configuración Main Task

**Trigger**: Inicio de conversación
**Descripción**: Define la tarea principal del AI Employee

**Instrucciones**:
Cuando un usuario inicia conversación:
1. Saludar cordialmente
2. Identificar necesidad principal
3. Ofrecer opciones relevantes
4. Guiar hacia siguiente paso

**Variables disponibles**:
- {{contact.name}} - Nombre del contacto
- {{contact.phone}} - Teléfono
- {{conversation.channel}} - Canal (WhatsApp, etc)
```

### Handover Action

```markdown
## Configuración Handover

**Triggers**:
- Keywords: "agente humano", "supervisor", "queja"
- Intención: Escalación detectada
- Condición: Después de 3 intentos fallidos

**Configuración**:
1. Destino: [Equipo/Agente específico]
2. Mensaje de transición: "Te voy a transferir con un agente especializado"
3. Context preservation: Full conversation history
4. Prioridad: Alta/Media/Baja según trigger
```

### Send Message Action

```markdown
## Configuración Send Message

**Casos de Uso**:

1. **Recordatorio de Cita**
   - Trigger: 24 horas antes del tour
   - Mensaje: "¡Hola {{name}}! Te recordamos tu visita mañana a las {{time}}"
   
2. **Follow-up Post-Tour**
   - Trigger: 2 horas después del tour
   - Mensaje: "¿Qué te pareció la propiedad? ¿Tienes alguna pregunta?"

3. **Nutrición de Leads**
   - Trigger: 7 días sin interacción
   - Mensaje: "¡Tenemos nuevas propiedades que podrían interesarte!"
```

### Resolve Conversation Action

```markdown
## Configuración Resolve

**Condiciones de Resolución**:
1. Tour agendado exitosamente
2. Pregunta respondida + confirmación del usuario
3. 48 horas sin respuesta después de 2 follow-ups
4. Usuario indica "gracias" o "listo"

**Mensaje de Cierre**:
"¡Fue un placer ayudarte! Si necesitas algo más, 
no dudes en escribirme. ¡Que tengas excelente día! 😊"
```

### ✅ Validación Step 4
- [ ] Main Task configurada y activa
- [ ] Handover rules establecidas
- [ ] Al menos 2 Send Message actions
- [ ] Resolve criteria definidos
- [ ] Test de cada action exitoso

---

## 📱 Step 5: Integración WhatsApp

### Configuración de Canal

**Navegación**: Channels → WhatsApp → Connect

```markdown
## Proceso de Conexión

1. **Verificar Número**:
   - Ingresar número comercial
   - Recibir código de verificación
   - Confirmar verificación

2. **Business Profile**:
   - Nombre de empresa
   - Categoría de negocio
   - Descripción
   - Horario de atención
   - Website

3. **Display Info**:
   - Foto de perfil (igual que avatar AI)
   - About text
   - Dirección
```

### Message Templates

**Navegación**: WhatsApp → Message Templates

```markdown
## Templates Requeridos

1. **Bienvenida** (welcome_message)
   "Hola {{1}}! Soy {{2}}, tu asesora virtual. 
   ¿En qué puedo ayudarte hoy?"

2. **Confirmación Tour** (tour_confirmation)
   "✅ Tour confirmado para {{1}} a las {{2}}. 
   Dirección: {{3}}. ¡Te esperamos!"

3. **Recordatorio** (appointment_reminder)
   "Hola {{1}}, te recordamos tu cita mañana 
   a las {{2}}. Responde CONFIRMAR o CANCELAR."
```

### Configuración Avanzada

```markdown
## Features WhatsApp

**Habilitar**:
- [ ] Location sharing
- [ ] Media messages (images, documents)
- [ ] Contact cards
- [ ] Quick replies
- [ ] List messages

**Business Hours**:
- AI disponible: 24/7
- Agentes humanos: Lun-Vie 9-18
- Mensaje fuera de horario: Configurado

**Rate Limiting**:
- Máximo mensajes/día: 1000
- Throttling: Automático
- Queue management: Habilitado
```

### ✅ Validación Step 5
- [ ] WhatsApp conectado y verificado
- [ ] Templates aprobados por Meta
- [ ] Business info completa
- [ ] Features avanzadas activas
- [ ] Test de envío/recepción exitoso

---

## 🧪 Validación Integral

### Testing Funcional

```markdown
## Escenarios de Prueba

1. **Flujo Completo de Venta**
   - Saludo inicial
   - Calificación de lead
   - Mostrar propiedades
   - Agendar tour
   - Confirmación

2. **Manejo de Errores**
   - Pregunta no encontrada
   - Solicitud ambigua
   - Escalación a humano

3. **Integraciones**
   - Envío de ubicación
   - Compartir imágenes
   - Documentos PDF
```

### Checklist Final

- [ ] Todos los steps completados
- [ ] 10+ conversaciones de prueba
- [ ] Knowledge base respondiendo correctamente
- [ ] Actions ejecutándose según triggers
- [ ] WhatsApp fully funcional
- [ ] Métricas baseline establecidas

---

## 📊 Monitoreo Post-Configuración

### Dashboard Métricas

**Acceso**: Analytics → AI Employee Performance

**KPIs a Monitorear**:
- Response time (objetivo: <2 min)
- Resolution rate (objetivo: >80%)
- Handover rate (objetivo: <20%)
- User satisfaction (objetivo: >4.0)

### Optimización Continua

**Diario**:
- Revisar conversaciones problemáticas
- Actualizar knowledge base según gaps
- Ajustar personality si es necesario

**Semanal**:
- Análisis de métricas
- A/B testing de respuestas
- Reunión de mejora continua

---

## 🚀 Siguiente Paso

Con la configuración completa y validada, proceder a la [Fase 3: Testing y Optimización](./03-testing.md) →

---

**💡 Pro Tips**:
- Documentar cada configuración con screenshots
- Mantener log de cambios realizados
- Crear backup de knowledge base
- Establecer proceso de actualización regular