# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation-based template repository for implementing AI employees on the Bird.com platform using the BMAD (Breakthrough Method for Agile AI-Driven Development) methodology. It is NOT a traditional software project with executable code.

## Key Context

- **Project Type**: Documentation and methodology framework (no executable code)
- **Purpose**: Templates for WhatsApp Business API integration via Bird.com
- **Target Users**: Businesses implementing AI customer service/sales agents
- **Platform Constraints**: Bird.com requires manual configuration (no API/automation)

## Repository Structure (Updated 2025-08-03)

```
templates/              # Ready-to-use configuration templates
guides/                 # Step-by-step implementation guides (3 phases)
examples/               # Real-world case studies (e-commerce, real-estate)
docs/                   # Technical documentation
bmad-agents/            # 6 specialized BMAD agent guides (reference)
```

**Note**: Structure was simplified from 27 directories to 8 for better usability.

## Development Guidelines

Since this is a documentation repository:
- No build/test/lint commands exist
- All content is in Markdown format
- Changes involve updating documentation and templates
- Focus on clarity, completeness, and practical implementation guidance

## Key Files

1. `BMAD-METHOD.md` - Core methodology (simplified and updated)
2. `README.md` - Project overview and quick start guide (compact)
3. `guides/quick-start.md` - 5-minute getting started guide
4. `examples/real-estate/urbanhub-example.md` - Complete implementation case study

## BMAD Agent Roles

When working with this repository, understand the 6 agent roles:
1. **Analyst Agent**: Business requirements and WhatsApp use cases
2. **Product Manager Agent**: Feature prioritization and project phases
3. **Architect Agent**: Technical design and platform constraints
4. **Scrum Master Agent**: Sprint planning and workflow management
5. **Configuration Agent**: Bird.com implementation details
6. **QA Agent**: Testing and validation strategies

## Implementation Phases

All AI employee implementations follow these phases:
1. **Planning Phase**: Requirements, design, and architecture
2. **Configuration Phase**: Bird.com setup and integration
3. **Testing Phase**: QA and refinement

## Important Constraints

- Bird.com platform requires manual configuration (no automation possible)
- All implementations must use WhatsApp Business API
- Focus on e-commerce and real estate verticals
- Templates should be complete and production-ready

## Language and Localization Standards

### UrbanHub Project Language Requirements

**Default Language**: Mexican Spanish (Neutral CDMX/Guadalajara tone)
- All UrbanHub AI agents must communicate in Mexican Spanish by default
- Use conversational, friendly, and authentically Mexican expressions
- Natural phrases: "claro que sí", "oye", "¿va?", "ándale", "la neta", "no te preocupes"
- Tone: Like a helpful real estate advisor with good vibes
- Transmit warmth, closeness, and security
- Avoid overly formal or technical language

**Multilingual Capability**: Future expansion ready
- Agents should be designed with multilingual architecture in mind
- Primary focus: Mexican Spanish
- Secondary consideration: English for international clients
- Template structure should support easy language expansion

**Cultural Context**:
- Mexican real estate terminology (departamento, recámara, cochera, etc.)
- Local business communication norms
- CDMX/Guadalajara neutral Mexican Spanish
- Professional yet warm and approachable tone

**Fallback Language Behavior**:
- When uncertain: "Déjame checarlo y te aviso en un momentito, ¿va?"
- Maintain Mexican Spanish throughout all interactions
- Escalate to human agents only when language barriers occur

## File Organization Rules (Simplified Structure)

### Where to place specific file types:

1. **Templates** (`templates/`)
   - `personality.md` - AI personality template
   - `knowledge-base.md` - KB structure template
   - `whatsapp-messages.md` - Message templates
   - `ai-actions.md` - Actions configuration

2. **Guides** (`guides/`)
   - `quick-start.md` - 5-minute overview
   - `01-planning.md` - Phase 1 guide
   - `02-configuration.md` - Phase 2 guide
   - `03-testing.md` - Phase 3 guide

3. **Examples** (`examples/`)
   - `e-commerce/` - E-commerce implementations
   - `real-estate/` - Real estate implementations
   - Each example should be self-contained

4. **Documentation** (`docs/`)
   - `bird-platform.md` - Platform overview
   - `best-practices.md` - Proven patterns

5. **BMAD Agents** (`bmad-agents/`)
   - Keep as reference for detailed methodology
   - 6 agent files remain unchanged

### File Creation Guidelines:

- **PREFER** using existing templates over creating new files
- **KEEP** structure flat and simple (max 2 levels deep)
- **FOCUS** on reusable templates rather than client-specific files
- **USE** lowercase with hyphens for file names (kebab-case)
- **AVOID** creating unnecessary subdirectories

## When Making Changes

- Maintain consistency with BMAD methodology
- Ensure templates are complete and self-contained
- Include practical examples and step-by-step instructions
- Consider Bird.com's manual configuration limitations
- Focus on WhatsApp-specific implementation details
- **CRITICAL**: Always follow the file organization rules above