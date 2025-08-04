# Bird.com Configuration Template

Esta plantilla proporciona la configuración paso a paso para implementar un agente AI especializado en la plataforma Bird.com. Use este template como guía para configurar cualquier agente siguiendo la metodología BMAD.

## Profile Configuration

### Basic Information
```
Agent Name: [Nombre del Agente]
Avatar: [Descripción del avatar - profesional, amigable, neutral]
Description: [Breve descripción del rol del agente]
Model: GPT-4 (recomendado para agentes especializados)
Temperature: [0.3-0.9 según necesidad de creatividad]
Max Tokens: [300-800 según complejidad de respuestas]
```

### System Message Template
```
Eres [Nombre], [rol específico] de [empresa/proyecto]. [Descripción breve de la función principal].

Tu objetivo es [objetivo principal claro y específico].

Características de personalidad:
- [Rasgo 1]
- [Rasgo 2] 
- [Rasgo 3]

Instrucciones de comportamiento:
1. [Instrucción específica 1]
2. [Instrucción específica 2]
3. [Instrucción específica 3]
4. Si no sabes algo, sé honesto y ofrece conseguir la información
5. Mantén siempre un tono [descripción del tono deseado]
```

## Personality Configuration

### Purpose Statement
```
[Descripción detallada del propósito del agente - qué hace, por qué existe, qué valor aporta]
```

### Tasks List
```
1. [Tarea principal específica]
2. [Tarea secundaria específica]
3. [Tarea de apoyo específica] 
4. [Tarea de escalación específica]
5. [Tarea de seguimiento específica]
```

### Target Audience
```
[Descripción detallada del público objetivo - demografía, necesidades, contexto de interacción]
```

### Communication Tone
```
[Descripción específica del tono - formal/informal, características del lenguaje, expresiones permitidas/prohibidas]
```

### Custom Instructions
```
Instrucciones específicas para este agente:

Siempre:
- [Instrucción obligatoria 1]
- [Instrucción obligatoria 2]
- [Instrucción obligatoria 3]

Nunca:
- [Prohibición específica 1]
- [Prohibición específica 2]
- [Prohibición específica 3]

En caso de [situación específica]:
- [Acción recomendada]

Frases recomendadas:
- "[Frase común 1]"
- "[Frase común 2]"
- "[Frase común 3]"

Frases prohibidas:
- "[Frase a evitar 1]"
- "[Frase a evitar 2]"
```

## AI Actions Configuration

### Main Task Action
```
Action Name: [Nombre del proceso principal]
Trigger: [Cuándo se activa - automático/manual/palabras clave]

Steps:
1. [Paso específico 1]
2. [Paso específico 2]
3. [Paso específico 3]
4. [Paso específico 4]
5. [Paso específico 5]

Success Criteria:
- [Criterio de éxito 1]
- [Criterio de éxito 2]

Failure Handling:
- [Qué hacer si falla el paso X]
- [Cuándo escalar a humano]
```

### Handover Action
```
Handover Triggers:
- Keywords: "[palabra clave 1]", "[palabra clave 2]", "[palabra clave 3]"
- Situations: [Situación específica 1], [Situación específica 2]
- Complexity: [Descripción de cuándo es demasiado complejo]

Context Transfer Message:
"[Mensaje que proporciona contexto al agente humano sobre la conversación]"

Handover Message to User:
"[Mensaje explicando al usuario que será transferido y por qué]"
```

### Automated Actions
```
Send Message Actions:
1. [Tipo de mensaje automatizado 1]
   - Trigger: [Cuándo se envía]
   - Template: "[Contenido del mensaje]"
   
2. [Tipo de mensaje automatizado 2]
   - Trigger: [Cuándo se envía]
   - Template: "[Contenido del mensaje]"

Resolve Conversation Triggers:
- Success: [Cuándo se considera exitosa]
- Completion: [Cuándo se considera completa]
- Timeout: [Tiempo de inactividad para cerrar]
```

## Knowledge Base Structure

### Folder Organization
```
knowledge-base/
├── [categoria-1]/
│   ├── [subcategoria-1].md
│   ├── [subcategoria-2].md
│   └── [subcategoria-3].md
├── [categoria-2]/
│   ├── [subcategoria-1].md
│   └── [subcategoria-2].md
├── faqs/
│   ├── [tema-frecuente-1].md
│   └── [tema-frecuente-2].md
└── scripts/
    ├── greeting-variations.md
    ├── objection-handling.md
    └── closing-statements.md
```

### Content Guidelines
- **File Size**: 500-1,800 palabras por archivo
- **Header Structure**: H1 (tema principal), H2 (subtemas), H3 (detalles)
- **Keyword Optimization**: Incluir variaciones naturales de términos
- **Cross-References**: Links internos entre temas relacionados
- **Update Protocol**: Frecuencia y responsables de actualización

## WhatsApp Integration

### Business Profile
```
Business Name: [Nombre del negocio]
Phone Number: [Número dedicado]
Display Name: "[Nombre para mostrar] [emoji opcional]"
Category: [Categoría relevante]
Description: "[Descripción breve y atractiva]"
Website: [URL del sitio web]
Business Hours: [Horarios de atención]
```

### Message Templates (Para aprobación)
```
Template 1: [nombre_template]
"[Contenido del template con variables {{1}}, {{2}}, etc.]"

Template 2: [nombre_template_2]  
"[Contenido del template con variables]"

Template 3: [nombre_template_3]
"[Contenido del template con variables]"
```

### Media Capabilities
```
Images: ✓ [Tipos de imágenes que enviará]
Location: ✓ [Cuándo enviará ubicaciones]
Documents: ✓ [Tipos de documentos]
Quick Replies: ✓ [Opciones típicas]
List Messages: ✓ [Tipos de listas]
```

## Integration Requirements

### External APIs
```
Integration 1: [Nombre del sistema]
- Purpose: [Para qué se usa]
- Auth Method: [Tipo de autenticación]
- Endpoints Used: [APIs específicas]
- Error Handling: [Cómo manejar fallos]

Integration 2: [Nombre del sistema]
- Purpose: [Para qué se usa]
- Auth Method: [Tipo de autenticación]
- Endpoints Used: [APIs específicas]
- Error Handling: [Cómo manejar fallos]
```

### Data Flow
```
Input: [Usuario] → [Bird.com] → [AI Agent]
Processing: [AI Agent] → [Knowledge Base] → [External APIs]
Output: [Response] → [WhatsApp] → [Usuario]
Logging: [CRM/Analytics] ← [All interactions]
```

## Monitoring and Analytics

### Key Metrics
```
Performance Metrics:
- Response Time: [target] seconds
- Success Rate: [target]%
- User Satisfaction: [target]/5.0
- Completion Rate: [target]%

Business Metrics:
- [Métrica específica del negocio 1]: [target]
- [Métrica específica del negocio 2]: [target]
- [Métrica específica del negocio 3]: [target]
```

### Alert Thresholds
```
Critical Alerts:
- Response Time > [X] seconds
- Error Rate > [X]%
- User Satisfaction < [X]/5.0

Warning Alerts:
- Volume > [X] messages/hour
- Integration Latency > [X] seconds
- Knowledge Base Miss Rate > [X]%
```

## Testing Checklist

### Pre-Launch Testing
- [ ] All conversation flows tested
- [ ] Knowledge base responses verified
- [ ] Integration connections working
- [ ] WhatsApp templates approved
- [ ] Error handling tested
- [ ] Escalation procedures tested
- [ ] Performance benchmarks met

### Go-Live Checklist
- [ ] Team trained on agent capabilities
- [ ] Escalation contacts available
- [ ] Monitoring dashboards active
- [ ] Backup procedures documented
- [ ] Communication plan executed

---

**Instrucciones de Uso:**
1. Reemplaza todos los placeholders `[texto]` con información específica
2. Elimina secciones no aplicables a tu caso de uso
3. Personaliza templates según tu marca y audiencia
4. Valida toda la configuración antes de implementar
5. Documenta cualquier desviación de este template

**Versión:** 1.0
**Última Actualización:** Enero 2025
**Próxima Revisión:** Trimestral