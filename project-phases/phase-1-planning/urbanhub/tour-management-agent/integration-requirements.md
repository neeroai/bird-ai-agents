# Tour Management Agent - Integration Requirements

## Overview
This document details the technical integration requirements for the UrbanHub Tour Management Agent, including API specifications, data flows, security requirements, and implementation guidelines.

## Integration Architecture

### High-Level Architecture
```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   WhatsApp      │────▶│   Bird.com       │────▶│    UrbanHub     │
│   Business API  │◀────│   AI Employee    │◀────│   Tour Agent    │
└─────────────────┘     └──────────────────┘     └─────────────────┘
                               │ │ │ │
                               ▼ ▼ ▼ ▼
                    ┌──────────────────────────┐
                    │   External Integrations   │
                    ├──────────────────────────┤
                    │ • Google Calendar API     │
                    │ • Salesforce CRM          │
                    │ • Yardi Property Mgmt     │
                    │ • ValueKeep (future)      │
                    └──────────────────────────┘
```

## 1. Google Calendar API Integration

### Purpose
Enable real-time tour scheduling by checking agent availability and creating calendar events.

### API Details
- **API Version**: Google Calendar API v3
- **Authentication**: OAuth 2.0 with service account
- **Scopes Required**:
  - `https://www.googleapis.com/auth/calendar.readonly`
  - `https://www.googleapis.com/auth/calendar.events`

### Required Endpoints

#### Check Availability
```
GET /calendars/{calendarId}/freebusy
```
**Request Body**:
```json
{
  "timeMin": "2025-01-03T09:00:00-05:00",
  "timeMax": "2025-01-10T18:00:00-05:00",
  "items": [
    {"id": "agent1@urbanhub.com"},
    {"id": "agent2@urbanhub.com"}
  ]
}
```

#### Create Tour Event
```
POST /calendars/{calendarId}/events
```
**Request Body**:
```json
{
  "summary": "Property Tour - Sarah Johnson",
  "description": "Tour for Urban Lofts\nContact: 555-123-4567\nUnit preference: 2BR\nNotes: Interested in gym facilities",
  "location": "123 Main Street, Downtown, ST 12345",
  "start": {
    "dateTime": "2025-01-05T15:00:00-05:00",
    "timeZone": "America/New_York"
  },
  "end": {
    "dateTime": "2025-01-05T16:00:00-05:00",
    "timeZone": "America/New_York"
  },
  "attendees": [
    {"email": "agent@urbanhub.com"},
    {"email": "sarah.j@email.com"}
  ],
  "reminders": {
    "useDefault": false,
    "overrides": [
      {"method": "email", "minutes": 1440},
      {"method": "popup", "minutes": 120}
    ]
  }
}
```

### Calendar Management Rules
1. **Business Hours**: Only book Monday-Saturday, 9 AM - 6 PM
2. **Tour Duration**: Default 45 minutes, with 15-minute buffer
3. **Agent Assignment**: Round-robin based on availability
4. **Conflict Resolution**: If time slot becomes unavailable, offer next 3 alternatives

### Error Handling
- **401 Unauthorized**: Re-authenticate with refresh token
- **403 Forbidden**: Check API quotas and permissions
- **409 Conflict**: Slot no longer available, offer alternatives
- **503 Service Unavailable**: Queue request for retry (max 3 attempts)

## 2. Salesforce CRM Integration

### Purpose
Create and update lead records, track tour outcomes, and trigger follow-up workflows.

### API Details
- **API Version**: Salesforce REST API v58.0
- **Authentication**: OAuth 2.0 JWT Bearer Flow
- **Instance URL**: `https://urbanhub.my.salesforce.com`

### Required Objects & Operations

#### Lead Object
**Create Lead on Tour Booking**:
```
POST /services/data/v58.0/sobjects/Lead
```
**Request Body**:
```json
{
  "FirstName": "Sarah",
  "LastName": "Johnson",
  "Email": "sarah.j@email.com",
  "Phone": "555-123-4567",
  "LeadSource": "WhatsApp Tour Bot",
  "Status": "Tour Scheduled",
  "Tour_Date__c": "2025-01-05T15:00:00",
  "Property_Interest__c": "Urban Lofts",
  "Budget_Range__c": "$2,000-$2,500",
  "Move_In_Timeline__c": "Within 30 days",
  "Number_of_Occupants__c": 2,
  "Has_Pets__c": true,
  "Pet_Type__c": "Dog",
  "Tour_Agent__c": "Jessica Martinez",
  "Bot_Conversation_ID__c": "WA_123456789"
}
```

#### Task Object
**Create Follow-up Task**:
```
POST /services/data/v58.0/sobjects/Task
```
**Request Body**:
```json
{
  "Subject": "Tour Follow-up - Sarah Johnson",
  "Description": "Follow up after Urban Lofts tour",
  "ActivityDate": "2025-01-06",
  "Priority": "High",
  "Status": "Not Started",
  "WhoId": "{LeadId}",
  "OwnerId": "{AgentId}"
}
```

### Custom Fields Required
- `Tour_Date__c` (DateTime)
- `Property_Interest__c` (Multi-select Picklist)
- `Budget_Range__c` (Picklist)
- `Move_In_Timeline__c` (Picklist)
- `Number_of_Occupants__c` (Number)
- `Has_Pets__c` (Checkbox)
- `Pet_Type__c` (Picklist)
- `Tour_Agent__c` (Lookup to User)
- `Bot_Conversation_ID__c` (Text)
- `Tour_Completed__c` (Checkbox)
- `Tour_Outcome__c` (Picklist)

### Workflow Triggers
1. **On Lead Creation**: Send welcome email
2. **24 Hours Before Tour**: Send reminder
3. **Post-Tour**: Update lead score, assign follow-up task
4. **No-Show**: Create re-engagement task

## 3. Yardi Property Management Integration

### Purpose
Access real-time property availability, pricing, and unit details.

### API Details
- **API Type**: REST API
- **Authentication**: API Key + Basic Auth
- **Base URL**: `https://api.yardi.com/urbanhub/v2`
- **Rate Limit**: 100 requests per minute

### Required Endpoints

#### Get Available Properties
```
GET /properties/available
```
**Query Parameters**:
- `neighborhood`: String (optional)
- `min_rent`: Number (optional)
- `max_rent`: Number (optional)
- `bedrooms`: Number (optional)
- `available_date`: Date (optional)

**Response**:
```json
{
  "properties": [
    {
      "property_id": "UL-001",
      "name": "Urban Lofts",
      "address": "123 Main Street",
      "units_available": 8,
      "rent_range": {
        "min": 1800,
        "max": 3200
      },
      "amenities": ["pool", "gym", "pet_friendly"],
      "images": [
        "https://cdn.urbanhub.com/ul-001-exterior.jpg"
      ]
    }
  ]
}
```

#### Get Property Details
```
GET /properties/{propertyId}/details
```
**Response**:
```json
{
  "property_id": "UL-001",
  "name": "Urban Lofts",
  "description": "Modern urban living in the heart of downtown",
  "total_units": 150,
  "available_units": [
    {
      "unit_id": "UL-001-204",
      "unit_number": "204",
      "bedrooms": 2,
      "bathrooms": 2,
      "sqft": 1100,
      "rent": 2400,
      "available_date": "2025-02-01",
      "floor_plan_url": "https://cdn.urbanhub.com/ul-2br-floorplan.pdf"
    }
  ],
  "amenities": {
    "building": ["concierge", "package_room", "bike_storage"],
    "unit": ["dishwasher", "in_unit_laundry", "balcony"],
    "community": ["pool", "gym", "rooftop_deck"]
  },
  "pet_policy": {
    "allowed": true,
    "restrictions": "No weight limit",
    "deposit": 500,
    "monthly_fee": 50
  }
}
```

### Data Sync Requirements
- **Frequency**: Every 30 minutes for availability
- **Full Sync**: Daily at 2 AM EST
- **Cache Duration**: 30 minutes for property details
- **Fallback**: Static data if API unavailable

## 4. WhatsApp Business API Configuration

### Message Templates Required

#### Tour Confirmation Template
**Name**: `tour_confirmation_v1`
**Language**: en_US
**Category**: UTILITY
```
Hello {{1}},

Your tour is confirmed! 📍

Property: {{2}}
Date: {{3}}
Time: {{4}}
Agent: {{5}}

Address: {{6}}

What to bring:
• Valid ID
• Proof of income (if ready to apply)
• List of questions

Reply CANCEL to cancel or RESCHEDULE to change time.

See you soon!
UrbanHub Tours
```

#### Tour Reminder Template
**Name**: `tour_reminder_24h`
**Language**: en_US
**Category**: UTILITY
```
Hi {{1}}, 

This is a reminder about your tour tomorrow:

📍 {{2}}
📅 {{3}} at {{4}}
👤 With {{5}}

Directions: {{6}}

Reply CONFIRM to confirm attendance or RESCHEDULE to change.

UrbanHub
```

### Interactive Message Components

#### Time Slot Selection List
```json
{
  "type": "list",
  "header": {
    "type": "text",
    "text": "Select Tour Time"
  },
  "body": {
    "text": "Choose your preferred time slot:"
  },
  "action": {
    "button": "View Times",
    "sections": [
      {
        "title": "Morning",
        "rows": [
          {
            "id": "slot_0900",
            "title": "9:00 AM",
            "description": "Available"
          },
          {
            "id": "slot_1000",
            "title": "10:00 AM",
            "description": "Available"
          }
        ]
      }
    ]
  }
}
```

#### Quick Reply Buttons
```json
{
  "type": "button",
  "body": {
    "text": "Would you like to schedule a tour of Urban Lofts?"
  },
  "action": {
    "buttons": [
      {
        "type": "reply",
        "reply": {
          "id": "schedule_yes",
          "title": "Yes, schedule tour"
        }
      },
      {
        "type": "reply",
        "reply": {
          "id": "more_info",
          "title": "More information"
        }
      }
    ]
  }
}
```

## 5. Security Requirements

### API Key Management
1. **Storage**: All API keys stored in Bird.com secure configuration
2. **Rotation**: Quarterly key rotation schedule
3. **Access**: Limited to production environment only
4. **Monitoring**: Log all API usage for audit

### Data Protection
1. **PII Handling**:
   - No SSN or financial data stored
   - Phone/email encrypted in transit
   - 90-day retention for conversation logs
2. **Compliance**:
   - CCPA compliant data handling
   - Fair Housing Act compliance in all interactions
   - TCPA compliance for messaging

### Authentication Flow
```
1. Bird.com → OAuth Provider: Request access token
2. OAuth Provider → Bird.com: Return access token
3. Bird.com → External API: Include token in header
4. External API → Bird.com: Return requested data
5. Bird.com: Cache response per TTL rules
```

## 6. Error Handling & Fallbacks

### Integration Failure Matrix

| Integration | Failure Type | Fallback Strategy | User Message |
|------------|--------------|-------------------|--------------|
| Google Calendar | API Down | Queue bookings for manual process | "I'll have an agent confirm your tour time within 2 hours" |
| Google Calendar | Auth Failed | Use backup service account | Standard booking flow |
| Salesforce | API Down | Store locally, sync when available | No user impact |
| Salesforce | Create Failed | Log error, notify admin | No user impact |
| Yardi | API Down | Use cached data (30 min old) | Show cached availability |
| Yardi | No Data | Show generic "Contact us" | "Please call us for current availability" |

### Monitoring & Alerts

#### Health Checks
- Google Calendar API: Every 5 minutes
- Salesforce API: Every 10 minutes  
- Yardi API: Every 5 minutes
- WhatsApp API: Continuous monitoring

#### Alert Thresholds
- API Response Time > 3 seconds: Warning
- API Error Rate > 5%: Alert
- Failed Bookings > 3 in 10 minutes: Critical
- Integration Down > 5 minutes: Page on-call

## 7. Testing Requirements

### Integration Testing Checklist
- [ ] Calendar booking with single agent
- [ ] Calendar booking with multiple agents
- [ ] Calendar conflict handling
- [ ] Salesforce lead creation
- [ ] Salesforce duplicate handling
- [ ] Yardi data accuracy
- [ ] Yardi cache behavior
- [ ] WhatsApp template rendering
- [ ] WhatsApp media delivery
- [ ] Full end-to-end tour booking
- [ ] Rescheduling flow
- [ ] Cancellation flow
- [ ] API failure scenarios
- [ ] Rate limiting behavior

### Performance Benchmarks
- Calendar API response: < 500ms
- Salesforce API response: < 1000ms
- Yardi API response: < 750ms
- End-to-end booking: < 10 seconds
- Message delivery: < 2 seconds

## 8. Implementation Timeline

### Week 1-2: Foundation
- Set up OAuth for Google Calendar
- Configure Salesforce connected app
- Obtain Yardi API credentials
- Create WhatsApp message templates

### Week 3-4: Core Integration
- Implement calendar availability check
- Build tour booking flow
- Create Salesforce lead sync
- Integrate Yardi property data

### Week 5-6: Polish & Testing
- Error handling implementation
- Performance optimization
- End-to-end testing
- Documentation completion

---

**Document Version**: 1.0  
**Created Date**: January 3, 2025  
**Author**: BMAD Architect Agent  
**Next Review**: After technical spike completion