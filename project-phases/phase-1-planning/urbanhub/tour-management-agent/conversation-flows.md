# Tour Management Agent - Conversation Flows

## Overview
This document outlines the detailed conversation flows for the UrbanHub Tour Management Agent, including happy paths, edge cases, and error handling scenarios.

## Primary Flows

### 1. New Tour Booking Flow

#### Flow Diagram
```
Start → Greeting → Property Interest → Availability Check → 
Time Selection → Lead Info Collection → Confirmation → End
```

#### Detailed Conversation

**Initial Contact**
```
User: Hi, I'd like to schedule a tour
Agent: Hello! I'd be happy to help you schedule a property tour with UrbanHub. 

Which property are you interested in viewing? I can:
📍 Show you available properties in a specific area
🏢 Provide information about a specific property
📋 Show you all available properties

[Button 1: Search by area]
[Button 2: Specific property] 
[Button 3: Show all properties]
```

**Property Selection - Specific Property**
```
User: [Clicks: Specific property]
Agent: Great! Please tell me the property name or address you'd like to tour.

User: Urban Lofts on Main Street
Agent: Perfect! I found Urban Lofts at 123 Main Street. This property features:
- Studio, 1BR, and 2BR units available
- Starting at $1,800/month
- Rooftop amenities and gym
- Pet-friendly community

Would you like to schedule a tour of Urban Lofts?
[Button: Yes, schedule tour]
[Button: See other properties]
[Button: More information]
```

**Property Selection - Search by Area**
```
User: [Clicks: Search by area]
Agent: Which neighborhood are you interested in?

Popular areas:
📍 Downtown (15 properties)
📍 Midtown (8 properties)
📍 Riverside (12 properties)
📍 University District (10 properties)

Or type any neighborhood name.

User: Downtown
Agent: Here are available properties in Downtown:

1️⃣ Urban Lofts - From $1,800/mo
   • Studio to 2BR available
   • Rooftop pool & gym
   
2️⃣ City Center Apartments - From $2,200/mo
   • 1BR to 3BR available
   • Concierge service
   
3️⃣ Metro Heights - From $1,600/mo
   • Studio to 1BR available
   • Near transit hub

[List continues with up to 5 properties]

Which property would you like to tour?
```

**Availability Check**
```
Agent: Let me check tour availability for Urban Lofts. 

When would you prefer to visit?
[Button: Today]
[Button: Tomorrow]
[Button: This week]
[Button: Next week]

User: [Clicks: This week]
Agent: Here are available tour times this week:

📅 Thursday, Jan 4
⏰ 10:00 AM | 2:00 PM | 4:00 PM

📅 Friday, Jan 5  
⏰ 11:00 AM | 1:00 PM | 3:00 PM | 5:00 PM

📅 Saturday, Jan 6
⏰ 10:00 AM | 12:00 PM | 2:00 PM

Please select your preferred date and time.
```

**Lead Information Collection**
```
User: Friday at 3:00 PM
Agent: Excellent! I've reserved Friday, January 5 at 3:00 PM for your tour.

To complete your booking, I'll need a few details:

What's your full name?

User: Sarah Johnson
Agent: Thank you, Sarah. What's the best phone number to reach you?

User: 555-123-4567
Agent: Perfect! And your email address?

User: sarah.j@email.com
Agent: Great! Just a few quick questions to help our leasing agent prepare for your tour:

1. When are you looking to move in?
[Button: ASAP]
[Button: Within 30 days]
[Button: Within 60 days]
[Button: Just browsing]

User: [Clicks: Within 30 days]
Agent: 2. How many people will be living in the unit?
[Button: Just me]
[Button: 2 people]
[Button: 3 people]
[Button: 4+ people]

User: [Clicks: 2 people]
Agent: 3. Do you have any pets?
[Button: No pets]
[Button: Dog]
[Button: Cat]
[Button: Other]

User: [Clicks: Dog]
Agent: 4. What's your preferred monthly budget range?
[Button: $1,500-$2,000]
[Button: $2,000-$2,500]
[Button: $2,500-$3,000]
[Button: $3,000+]

User: [Clicks: $2,000-$2,500]
```

**Confirmation**
```
Agent: Perfect! Your tour is confirmed ✅

📍 Property: Urban Lofts (123 Main Street)
📅 Date: Friday, January 5
⏰ Time: 3:00 PM
👤 Agent: Jessica Martinez
📱 Your info: Sarah Johnson (555-123-4567)

I've sent a confirmation to sarah.j@email.com with:
- Directions and parking information
- What to bring
- Jessica's direct contact

You'll receive a reminder 24 hours before your tour. 

Is there anything specific you'd like to see during your tour?

User: I'd like to see the 2 bedroom units and the gym
Agent: Noted! I've added that to your tour preferences. Jessica will make sure to show you the 2BR units and the fitness facilities.

You're all set! If you need to reschedule or have questions, just message me anytime. Looking forward to showing you Urban Lofts!

[Button: Schedule another tour]
[Button: Get directions]
[Button: Done]
```

### 2. Rescheduling Flow

**Initiation**
```
User: I need to reschedule my tour
Agent: I'll help you reschedule your tour. Can you provide either:
- Your confirmation number
- The phone number used for booking
- The email address used for booking

User: 555-123-4567
Agent: I found your upcoming tour:

📍 Urban Lofts - 123 Main Street
📅 Friday, January 5 at 3:00 PM
👤 With agent Jessica Martinez

Is this the tour you'd like to reschedule?
[Button: Yes, reschedule this]
[Button: No, different tour]
```

**New Time Selection**
```
User: [Clicks: Yes, reschedule this]
Agent: When would you like to reschedule your tour?

[Button: Today]
[Button: Tomorrow]  
[Button: This week]
[Button: Next week]
[Button: Specific date]

User: [Clicks: Tomorrow]
Agent: Here are available times for tomorrow (Saturday, Jan 6):

⏰ 10:00 AM
⏰ 12:00 PM  
⏰ 2:00 PM
⏰ 4:00 PM

Which time works best for you?

User: 2:00 PM
Agent: Perfect! I've rescheduled your tour to:

📅 New date: Saturday, January 6
⏰ New time: 2:00 PM
✅ Same property: Urban Lofts
✅ Same agent: Jessica Martinez

You'll receive an updated confirmation email shortly. Your previous time slot has been released.

[Button: Done]
[Button: Cancel tour instead]
```

### 3. Cancellation Flow

```
User: I need to cancel my tour
Agent: I can help you cancel your tour. To locate your booking, please provide:
- Confirmation number, phone number, or email

User: My confirmation is UH-1234
Agent: I found your tour:

📍 Urban Lofts
📅 Saturday, January 6 at 2:00 PM

Would you like to cancel this tour?
[Button: Yes, cancel it]
[Button: No, keep it]
[Button: Reschedule instead]

User: [Clicks: Yes, cancel it]
Agent: Your tour has been cancelled. Would you mind sharing why you're canceling? This helps us improve our service.

[Button: Found another place]
[Button: Schedule doesn't work]
[Button: Not ready to move]
[Button: Other reason]
[Button: Prefer not to say]

User: [Clicks: Schedule doesn't work]
Agent: Thank you for letting us know. Your tour has been cancelled and you'll receive a confirmation email.

When you're ready, I'd be happy to help you schedule a new tour at a more convenient time. Just message me anytime!

[Button: Schedule new tour]
[Button: Done]
```

### 4. Property Information Flow

```
User: Tell me about the amenities at Urban Lofts
Agent: Urban Lofts offers fantastic amenities! Here's what's included:

🏊 Rooftop Features:
- Heated pool & spa
- BBQ grills & dining areas
- Panoramic city views

🏋️ Fitness & Wellness:
- 24/7 fitness center
- Yoga studio
- Sauna

🏠 Building Amenities:
- Concierge service
- Package lockers
- Bike storage
- EV charging stations

🐕 Pet-Friendly:
- Dog park on-site
- Pet washing station
- No weight restrictions

Would you like to:
[Button: Schedule a tour]
[Button: See floor plans]
[Button: View photos]
[Button: Ask about pricing]
```

## Edge Cases & Error Handling

### 1. No Availability
```
Agent: I'm checking availability for Urban Lofts this week...

Unfortunately, all tour slots are booked for this week. Here are the next available times:

📅 Monday, Jan 8: 10 AM, 2 PM, 4 PM
📅 Tuesday, Jan 9: 11 AM, 3 PM, 5 PM

Would any of these work for you?
[Button: Show more dates]
[Button: Join waitlist]
[Button: Try another property]
```

### 2. Invalid Input Handling
```
User: I want to tour tomorrow at midnight
Agent: Tours are available Monday-Saturday from 9 AM to 6 PM. 

For tomorrow, I have these times available:
⏰ 10:00 AM
⏰ 2:00 PM
⏰ 4:00 PM

Which would work best for you?
```

### 3. Multiple Property Interest
```
User: I want to tour Urban Lofts and Metro Heights
Agent: Excellent! I can help you schedule tours for both properties. Would you prefer to:

[Button: Same day back-to-back]
[Button: Different days]

User: [Clicks: Same day back-to-back]
Agent: I'll find times where you can tour both properties on the same day. The properties are 15 minutes apart.

Available for both properties:
📅 Friday, Jan 5
⏰ Option 1: Urban Lofts at 2:00 PM, Metro Heights at 3:30 PM
⏰ Option 2: Metro Heights at 11:00 AM, Urban Lofts at 12:30 PM

Which option works better?
```

### 4. Incomplete Information
```
Agent: What's your phone number?
User: Actually, can I just give my email?
Agent: Of course! I'll need either a phone number or email to complete your booking. Your email address will work perfectly.

User: sarah@email
Agent: The email appears incomplete. Please provide your full email address (example: name@email.com)

User: sarah@email.com
Agent: Perfect! I have sarah@email.com. We'll send your confirmation there.
```

## Handoff Scenarios

### 1. Complex Requirements
```
User: I need a wheelchair accessible unit with roll-in shower
Agent: I understand you need specific accessibility features. Let me connect you with a specialist who can ensure we find the perfect unit for your needs.

I'm transferring you to Jessica Martinez, our senior leasing agent who specializes in accessibility requirements. She'll be with you in just a moment.

[Handoff initiated - Context passed: Accessibility needs, Property interest: Urban Lofts]
```

### 2. Technical Issues
```
Agent: I'm having trouble accessing the calendar system right now. Let me connect you with someone who can help you immediately.

[Handoff initiated - Context: Calendar system error, Attempting to book Urban Lofts tour]
```

### 3. Upset Customer
```
User: This is ridiculous! I've been trying to book for 20 minutes!
Agent: I sincerely apologize for the frustration. Let me immediately connect you with a manager who can assist you personally and ensure your tour is scheduled right away.

[Handoff initiated - Priority: High, Context: Frustrated customer, booking difficulties]
```

## Multi-Language Support (Future)

### Spanish Language Detection
```
User: Hola, quiero programar un tour
Agent: ¡Hola! Estaré encantado de ayudarte a programar un tour. 

(Switching to Spanish conversation flow...)
```

## Performance Optimizations

### Quick Actions
For returning users or those with confirmation numbers:
```
User: UH-1234
Agent: Welcome back! I see you have a tour scheduled:
📍 Urban Lofts - Friday at 3 PM

How can I help you?
[Button: Confirm I'm coming]
[Button: Reschedule]
[Button: Add special requests]
[Button: Get directions]
```

### Smart Suggestions
Based on conversation context:
```
Agent: Since you're interested in 2BR units at Urban Lofts ($2,400-$2,800), you might also like:
- City Center Apartments: 2BR from $2,500 (luxury amenities)
- Riverside Commons: 2BR from $2,200 (waterfront views)

Would you like to tour any of these as well?
```

---

**Document Version**: 1.0  
**Created Date**: January 3, 2025  
**Author**: BMAD PM Agent  
**Next Steps**: Implement in Bird.com platform with personality configuration