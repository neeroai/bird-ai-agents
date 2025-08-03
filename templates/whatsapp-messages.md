# 💬 Templates de Mensajes WhatsApp para AI Employees

> Biblioteca de templates pre-aprobados y mejores prácticas para comunicación vía WhatsApp Business API.

## 📱 Tipos de Mensajes en WhatsApp

### 1. Session Messages (Dentro de 24 horas)
- Respuestas libres a mensajes del usuario
- No requieren template pre-aprobado
- Pueden incluir rich media

### 2. Template Messages (Fuera de 24 horas)
- Requieren aprobación previa de Meta
- Deben seguir políticas estrictas
- Ideales para notificaciones proactivas

---

## 🎯 Templates Pre-Aprobados Esenciales

### 1. Mensaje de Bienvenida

```
Nombre: welcome_message
Categoría: UTILITY
Variables: {{1}} = nombre

¡Hola {{1}}! 👋

Soy [Nombre AI], tu asistente virtual de [Empresa].

Puedo ayudarte con:
• Información de productos/servicios
• Agendar citas o demos
• Resolver dudas frecuentes
• Conectarte con el equipo correcto

¿En qué puedo asistirte hoy?
```

### 2. Confirmación de Cita

```
Nombre: appointment_confirmation
Categoría: UTILITY
Variables: {{1}} = nombre, {{2}} = fecha, {{3}} = hora, {{4}} = ubicación

✅ Cita Confirmada

Hola {{1}}, tu cita ha sido agendada exitosamente:

📅 Fecha: {{2}}
🕐 Hora: {{3}}
📍 Lugar: {{4}}

Por favor llega 10 minutos antes. Si necesitas cancelar o reagendar, responde CAMBIAR.

¡Te esperamos!
```

### 3. Recordatorio de Cita

```
Nombre: appointment_reminder
Categoría: UTILITY
Variables: {{1}} = nombre, {{2}} = tiempo, {{3}} = ubicación

⏰ Recordatorio de Cita

Hola {{1}}, te recordamos que tienes una cita {{2}}.

📍 Lugar: {{3}}

Responde:
CONFIRMAR - Si asistirás
CANCELAR - Para cancelar
CAMBIAR - Para reagendar

¡Nos vemos pronto!
```

### 4. Seguimiento Post-Interacción

```
Nombre: follow_up_satisfaction
Categoría: MARKETING
Variables: {{1}} = nombre

Hola {{1}} 😊

Esperamos que hayas tenido una excelente experiencia con nosotros.

¿Cómo calificarías tu experiencia del 1 al 5?

1⭐ Muy mala
2⭐ Mala
3⭐ Regular
4⭐ Buena
5⭐ Excelente

Tu opinión nos ayuda a mejorar.
```

### 5. Notificación de Estado

```
Nombre: status_update
Categoría: UTILITY
Variables: {{1}} = nombre, {{2}} = tipo_solicitud, {{3}} = nuevo_estado

📊 Actualización de Estado

Hola {{1}}, tu {{2}} ha cambiado de estado:

Estado actual: {{3}}

Para más detalles o si tienes preguntas, no dudes en escribirnos.

Gracias por tu preferencia.
```

### 6. Oferta Personalizada

```
Nombre: personalized_offer
Categoría: MARKETING
Variables: {{1}} = nombre, {{2}} = producto/servicio, {{3}} = descuento

🎉 Oferta Especial para Ti

Hola {{1}}, tenemos una oferta exclusiva en {{2}}:

💰 {{3}} de descuento
⏰ Válido por 48 horas
🎯 Aplican restricciones

¿Te interesa conocer más detalles? Responde SÍ para más información.
```

### 7. Abandono de Carrito

```
Nombre: cart_abandonment
Categoría: MARKETING
Variables: {{1}} = nombre, {{2}} = productos

🛒 ¿Olvidaste algo?

Hola {{1}}, notamos que dejaste estos items en tu carrito:

{{2}}

¿Necesitas ayuda para completar tu compra? Estoy aquí para asistirte.

Responde COMPRAR para continuar o AYUDA si tienes dudas.
```

### 8. Confirmación de Pedido

```
Nombre: order_confirmation
Categoría: UTILITY
Variables: {{1}} = nombre, {{2}} = número_orden, {{3}} = total

✅ Pedido Confirmado

Hola {{1}}, tu pedido #{{2}} ha sido confirmado.

Total: ${{3}}

Recibirás actualizaciones sobre el envío. Para rastrear tu pedido, responde RASTREAR.

¡Gracias por tu compra!
```

---

## 💬 Respuestas Dentro de Sesión (24 horas)

### Saludo Inicial

```
¡Hola! 👋 Soy [Nombre AI], tu asistente virtual de [Empresa].

¿En qué puedo ayudarte hoy?

Algunas opciones populares:
📦 Ver productos
📅 Agendar cita
❓ Preguntas frecuentes
💬 Hablar con un agente
```

### Solicitud de Información

```
¡Por supuesto! Para brindarte la mejor información sobre [tema], necesito saber:

1. ¿[Pregunta calificadora 1]?
2. ¿[Pregunta calificadora 2]?

Esto me ayudará a darte opciones personalizadas 😊
```

### Presentación de Opciones

```
Basándome en lo que me comentas, estas son las mejores opciones para ti:

*Opción 1:* [Nombre]
💰 Precio: $[monto]
✨ Ideal para: [caso de uso]
📍 Disponible en: [ubicación]

*Opción 2:* [Nombre]
💰 Precio: $[monto]
✨ Ideal para: [caso de uso]
📍 Disponible en: [ubicación]

¿Cuál te interesa más? O si prefieres, puedo mostrarte otras alternativas.
```

### Manejo de Dudas

```
Entiendo tu pregunta sobre [tema]. Déjame explicarte:

[Respuesta clara y concisa en 2-3 puntos]

¿Esto resuelve tu duda? Si necesitas más detalles sobre algún punto específico, con gusto profundizo.
```

### Proceso de Agendamiento

```
¡Perfecto! Vamos a agendar tu [cita/demo/visita].

📅 ¿Qué día te conviene?
   • Lunes a Viernes: 9:00 - 18:00
   • Sábados: 10:00 - 14:00

Una vez que me indiques el día, te mostraré los horarios disponibles.
```

### Escalación a Humano

```
Entiendo que prefieres hablar con un miembro del equipo. 

Te voy a transferir con [nombre/departamento] quien podrá ayudarte mejor con [tema específico].

⏱️ Tiempo de espera estimado: [X minutos]

Mientras tanto, ¿hay algo más en lo que pueda asistirte?
```

### Cierre de Conversación

```
¡Ha sido un placer ayudarte! 😊

Resumen de lo que hicimos hoy:
✅ [Acción realizada 1]
✅ [Acción realizada 2]

Si necesitas algo más, no dudes en escribirme. Estoy disponible 24/7.

¡Que tengas un excelente día!
```

---

## 🎨 Elementos Interactivos de WhatsApp

### Quick Reply Buttons

```
¿Qué te gustaría hacer?

[🛍️ Ver Productos]
[📅 Agendar Cita]
[❓ Hacer Pregunta]
[💬 Hablar con Agente]
```

### List Messages

```
📋 *Selecciona una categoría:*

Tenemos las siguientes opciones disponibles:

[Ver Lista]
├── Productos
│   ├── Categoría A
│   ├── Categoría B
│   └── Categoría C
├── Servicios
│   ├── Servicio 1
│   ├── Servicio 2
│   └── Servicio 3
└── Soporte
    ├── Preguntas Frecuentes
    ├── Estado de Pedido
    └── Contacto
```

### Location Sharing

```
📍 *Nuestras Ubicaciones*

Te comparto la ubicación de nuestra sucursal más cercana:

[Compartir Ubicación]
Sucursal Norte
Av. Principal #123
Horario: Lun-Vie 9:00-18:00

¿Necesitas direcciones para otra sucursal?
```

### Media Messages

```
📸 *[Nombre Producto]*

[Imagen del producto]

✨ Características principales:
• [Característica 1]
• [Característica 2]
• [Característica 3]

💰 Precio: $[monto]
📦 Disponible para entrega inmediata

¿Te gustaría ver más fotos o necesitas información adicional?
```

---

## 📏 Mejores Prácticas

### 1. Longitud de Mensajes
- **Ideal**: 3-5 líneas por mensaje
- **Máximo**: 8 líneas (evitar scroll excesivo)
- **Párrafos**: Separar con líneas en blanco

### 2. Uso de Emojis
- **Recomendado**: 1-2 emojis por mensaje
- **Propósito**: Mejorar legibilidad, no decoración
- **Consistencia**: Usar los mismos emojis para conceptos similares

### 3. Formato de Texto
```
*Negrita* para destacar información importante
_Cursiva_ para énfasis sutil
~Tachado~ para mostrar cambios
```Código``` para referencias técnicas
```

### 4. Estructura de Información
```
🏷️ *Título Principal*

📝 Información clave:
• Punto importante 1
• Punto importante 2
• Punto importante 3

💡 _Nota adicional si es necesaria_
```

### 5. Call-to-Actions Claros
- Siempre indicar siguiente paso
- Usar verbos de acción
- Ofrecer opciones limitadas (2-4 máximo)

---

## 🚨 Errores Comunes a Evitar

### ❌ NO HACER:
1. **Mensajes muy largos**: Dificultan lectura en móvil
2. **Exceso de opciones**: Abruman al usuario
3. **Jerga técnica**: Confunde a usuarios no técnicos
4. **MAYÚSCULAS**: Se percibe como gritar
5. **Enlaces muy largos**: Usar acortadores si es necesario

### ✅ SÍ HACER:
1. **Mensajes concisos**: Ir al punto rápidamente
2. **Opciones claras**: 3-4 máximo por interacción
3. **Lenguaje simple**: Accesible para todos
4. **Formato amigable**: Uso estratégico de emojis y formato
5. **CTAs específicos**: Decir exactamente qué hacer

---

## 📊 Métricas de Efectividad

### KPIs de Mensajería
1. **Open Rate**: >95% (WhatsApp tiene alto engagement)
2. **Response Rate**: >70% para CTAs
3. **Resolution Rate**: >80% sin escalación
4. **Time to Resolution**: <5 minutos promedio

### A/B Testing Recomendado
- Tono formal vs casual
- Con emojis vs sin emojis
- CTAs directos vs opciones
- Mensajes largos vs múltiples cortos

---

## 🔄 Flujos Conversacionales

### Flujo de Venta
```
Usuario: "Hola"
    ↓
AI: Saludo + Opciones principales
    ↓
Usuario: "Ver productos"
    ↓
AI: Preguntas de calificación
    ↓
Usuario: Responde criterios
    ↓
AI: Muestra 3 opciones relevantes
    ↓
Usuario: Selecciona una
    ↓
AI: Detalles + CTA (comprar/agendar demo)
    ↓
[Cierre de venta o agendamiento]
```

### Flujo de Soporte
```
Usuario: "Tengo un problema"
    ↓
AI: Empatía + Solicitud de detalles
    ↓
Usuario: Explica problema
    ↓
AI: Intenta resolución con KB
    ↓
[Si resuelve → Confirmación + Cierre]
[Si no → Escalación a humano]
```

---

## 💡 Tips de Implementación

1. **Testear templates**: Antes de solicitar aprobación a Meta
2. **Documentar variables**: Mantener guía clara de qué va en cada {{variable}}
3. **Versionado**: Guardar historial de templates aprobados
4. **Monitoreo**: Revisar métricas semanalmente
5. **Actualización**: Refrescar templates según feedback

---

**Recuerde**: Los mensajes de WhatsApp son la voz de su marca. Mantenga consistencia, claridad y calidez en cada interacción.