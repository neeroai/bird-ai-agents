# 🤖 AI Actions Library

> **Purpose**: Reusable AI Action configurations for common automation patterns in Bird.com

## 🎯 Overview

AI Actions are the automation building blocks that define what your AI Employee can do beyond just answering questions. This library provides tested configurations for common actions that can be adapted to your specific needs.

## 🔧 What Are AI Actions?

AI Actions in Bird.com are triggered automations that allow your AI Employee to:
- Perform specific tasks based on conversation context
- Hand over conversations to human agents
- Send structured messages
- Update systems or trigger workflows
- Mark conversations as resolved

## 📁 Library Structure

```
ai-actions-library/
├── README.md (this file)
├── core-actions/
│   ├── main-task.md         # Primary conversation handler
│   ├── handover-human.md    # Escalation to human agent
│   ├── send-message.md      # Custom message sending
│   └── resolve-chat.md      # Conversation completion
├── sales-actions/
│   ├── product-recommendation.md
│   ├── order-creation.md
│   ├── discount-offer.md
│   └── cart-abandonment.md
├── support-actions/
│   ├── ticket-creation.md
│   ├── status-check.md
│   ├── faq-redirect.md
│   └── feedback-collection.md
└── booking-actions/
    ├── appointment-scheduling.md
    ├── availability-check.md
    ├── reminder-setup.md
    └── cancellation-handling.md
```

## 🎯 Core Actions (Required)

### 1. Main Task Action
**Purpose**: Primary conversation handler that processes all messages
```yaml
Action Name: Main Task
Trigger: Every incoming message
Configuration:
  - Enable knowledge base search
  - Set confidence threshold
  - Define fallback behavior
```

### 2. Handover to Human
**Purpose**: Escalate to human agent when needed
```yaml
Action Name: Handover to Human
Triggers:
  - "I want to speak to a human"
  - "Talk to agent"
  - Sentiment: Very negative
  - Confidence: Below threshold
Configuration:
  - Preserve conversation context
  - Set routing rules
  - Add handover message
```

### 3. Send Custom Message
**Purpose**: Send specific messages based on triggers
```yaml
Action Name: Send Message
Use Cases:
  - Welcome messages
  - Business hours notification
  - Follow-up messages
  - Promotional content
```

### 4. Resolve Conversation
**Purpose**: Mark conversation as completed
```yaml
Action Name: Resolve Chat
Triggers:
  - "Thank you, bye"
  - Inactivity timeout
  - Task completed
  - Customer confirms resolution
```

## 💼 Sales Actions

### Product Recommendation
```markdown
# Product Recommendation Action

## Trigger Conditions
- Keywords: "recommend", "suggest", "what should I buy"
- Context: User has mentioned preferences
- Timing: After initial greeting

## Configuration
1. Analyze user preferences from conversation
2. Search knowledge base for matching products
3. Present 3-5 relevant options
4. Include product links/images

## Example Flow
User: "I need a dress for a wedding"
AI: *Triggers product recommendation*
AI: "Based on your needs, I recommend these elegant options..."
```

### Order Creation
```markdown
# Order Creation Action

## Trigger Conditions
- Keywords: "I want to buy", "place order", "purchase"
- Context: Product selected
- Requirements: Customer details collected

## Configuration
1. Confirm product selection
2. Collect necessary information
3. Create order in system
4. Send confirmation

## Integration Points
- E-commerce platform API
- Payment gateway
- Inventory system
```

## 🛠️ Support Actions

### Ticket Creation
```markdown
# Support Ticket Creation

## Trigger Conditions
- Keywords: "problem", "issue", "not working", "broken"
- Sentiment: Negative
- Context: Technical issue described

## Configuration
1. Categorize issue type
2. Collect relevant details
3. Create ticket in support system
4. Provide ticket number

## Data Collection
- Issue description
- Product/service affected
- Customer contact info
- Priority level
```

### Status Check
```markdown
# Order/Ticket Status Check

## Trigger Conditions
- Keywords: "status", "where is", "track", "update on"
- Context: Reference number provided

## Configuration
1. Extract reference number
2. Query status system
3. Format status update
4. Provide next steps

## Response Template
"Your [order/ticket] #[number] is currently [status]. 
Expected [resolution/delivery]: [date]"
```

## 📅 Booking Actions

### Appointment Scheduling
```markdown
# Appointment Scheduling Action

## Trigger Conditions
- Keywords: "book", "schedule", "appointment", "viewing"
- Context: Service type identified

## Configuration
1. Check availability
2. Offer time slots
3. Collect contact details
4. Confirm booking
5. Send calendar invite

## Integration Requirements
- Calendar system API
- Availability database
- Notification system
```

## 🔨 Implementation Guide

### Step 1: Identify Needed Actions
1. Review your use cases from Phase 1
2. Select relevant actions from library
3. Identify any custom actions needed

### Step 2: Configure in Bird.com
1. Navigate to AI Actions section
2. Create new action
3. Set trigger conditions
4. Configure action behavior
5. Test thoroughly

### Step 3: Action Configuration Template
```yaml
Action Name: [Descriptive Name]
Type: [Main Task/Handover/Send Message/Resolve/Custom]

Triggers:
  Keywords:
    - keyword1
    - keyword2
  Phrases:
    - "exact phrase match"
  Sentiment: [Positive/Negative/Neutral]
  Confidence: [Below X%]
  Context: [Specific conditions]

Configuration:
  Primary Action: [What it does]
  Data Collection: [What info to gather]
  Integration: [External systems]
  Success Message: [Confirmation to user]
  Fallback: [If action fails]

Testing Scenarios:
  1. [Test case 1]
  2. [Test case 2]
  3. [Edge case]
```

## 💡 Best Practices

### 1. Trigger Design
- **Specific over Generic**: Better to have multiple specific triggers
- **Context Awareness**: Consider conversation state
- **Language Variations**: Include synonyms and variations
- **False Positive Prevention**: Test for unintended triggers

### 2. Action Flow
- **Confirm Before Acting**: Especially for irreversible actions
- **Collect Progressively**: Don't overwhelm with questions
- **Provide Feedback**: Always confirm action completion
- **Handle Errors Gracefully**: Have fallback plans

### 3. Integration Planning
- **API Reliability**: Plan for external system failures
- **Data Validation**: Verify before sending to systems
- **Security**: Never expose sensitive data
- **Logging**: Track all actions for debugging

## 📊 Action Performance Metrics

Track these for each action:

| Metric | Description | Target |
|--------|-------------|--------|
| Trigger Accuracy | % correctly triggered | > 95% |
| Completion Rate | % successfully completed | > 90% |
| User Satisfaction | Rating after action | > 4.0/5 |
| Error Rate | % failed executions | < 5% |
| Processing Time | Average duration | < 3 sec |

## 🚧 Common Pitfalls

### 1. Over-Triggering
**Problem**: Action triggers too frequently
**Solution**: Add more specific conditions

### 2. Under-Triggering
**Problem**: Users can't activate needed actions
**Solution**: Add trigger variations and test

### 3. Complex Flows
**Problem**: Too many steps frustrate users
**Solution**: Simplify and break into smaller actions

### 4. Poor Error Handling
**Problem**: Failed actions leave users stuck
**Solution**: Always provide fallback options

## 🧪 Testing Checklist

Before deploying any action:

- [ ] Test all trigger phrases
- [ ] Verify data collection works
- [ ] Check integration connections
- [ ] Test error scenarios
- [ ] Validate success messages
- [ ] Confirm fallback behavior
- [ ] Test with real users
- [ ] Monitor for false triggers
- [ ] Measure completion rates
- [ ] Gather user feedback

## 🔄 Action Optimization

### Monthly Review Process
1. Analyze trigger logs
2. Review completion rates
3. Identify failure patterns
4. Update trigger conditions
5. Refine action flows
6. Test improvements

### Optimization Opportunities
- Combine frequently sequential actions
- Remove rarely used actions
- Improve unclear trigger phrases
- Streamline data collection
- Enhance error messages

---

*Remember: AI Actions transform your AI Employee from a question-answerer to a task-completer. Design them thoughtfully for maximum impact.*