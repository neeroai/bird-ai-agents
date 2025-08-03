# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a documentation-based template repository for implementing AI employees on the Bird.com platform using the BMAD (Breakthrough Method for Agile AI-Driven Development) methodology. It is NOT a traditional software project with executable code.

## Key Context

- **Project Type**: Documentation and methodology framework (no executable code)
- **Purpose**: Templates for WhatsApp Business API integration via Bird.com
- **Target Users**: Businesses implementing AI customer service/sales agents
- **Platform Constraints**: Bird.com requires manual configuration (no API/automation)

## Repository Structure

```
bmad-agents/              # 6 specialized AI agent methodologies
project-phases/           # 3-phase implementation workflow
knowledge-base-templates/ # Industry-specific templates (e-commerce, real-estate)
personality-templates/    # AI personality configurations
whatsapp-integration/     # WhatsApp Business API implementation guides
ai-actions-library/       # Reusable AI action patterns
```

## Development Guidelines

Since this is a documentation repository:
- No build/test/lint commands exist
- All content is in Markdown format
- Changes involve updating documentation and templates
- Focus on clarity, completeness, and practical implementation guidance

## Key Files

1. `BMAD-BIRD-METHOD.md` - Core methodology (479 lines)
2. `README.md` - Project overview and quick start guide
3. `bmad-agents/01-analyst-agent.md` - Business analysis methodology (295 lines)

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

## File Organization Rules

### Where to place specific file types:

1. **Business Analysis Documents**
   - Location: `project-phases/phase-1-planning/{client}/`
   - Naming: `{client}-brd.md`, `{client}-prd.md`, `{client}-architecture.md`
   - Example: `project-phases/phase-1-planning/urbanhub/urbanhub-brd.md`

2. **Configuration Guides**
   - Location: `project-phases/phase-2-configuration/{client}/`
   - Naming: `step-{number}-{description}.md`
   - Example: `project-phases/phase-2-configuration/koaj/step-01-profile-setup.md`

3. **Testing Documentation**
   - Location: `project-phases/phase-3-testing/{client}/`
   - Naming: `{client}-test-plan.md`, `{client}-test-results.md`
   - Example: `project-phases/phase-3-testing/urbanhub/urbanhub-test-results.md`

4. **Personality Templates**
   - Location: `personality-templates/{industry}/`
   - Naming: `{brand}-personality.md`
   - Example: `personality-templates/e-commerce/koaj-personality.md`

5. **Knowledge Base Content**
   - Location: `knowledge-base-templates/{industry}/{category}/`
   - Structure: Follow Bird.com's folder hierarchy exactly
   - Example: `knowledge-base-templates/real-estate/properties/listings.md`

6. **WhatsApp Templates**
   - Location: `whatsapp-integration/templates/{use-case}/`
   - Naming: `{purpose}-template.md`
   - Example: `whatsapp-integration/templates/sales/welcome-message.md`

7. **AI Actions Library**
   - Location: `ai-actions-library/{action-type}/`
   - Naming: `{action-name}-config.md`
   - Example: `ai-actions-library/handover/escalate-to-human.md`

8. **Case Studies**
   - Location: `case-studies/{client}/`
   - Structure: Include all relevant documentation for the case
   - Example: `case-studies/koaj/implementation-summary.md`

### File Creation Guidelines:

- **NEVER** create files in the root directory (except for README.md updates)
- **ALWAYS** create a client-specific subfolder when starting a new implementation
- **MAINTAIN** industry separation (e-commerce vs real-estate) in template folders
- **FOLLOW** the naming conventions strictly for consistency
- **USE** lowercase with hyphens for file names (kebab-case)
- **CREATE** README.md files in each directory to explain its purpose

### Directory Structure Example:

```
project-phases/
└── phase-1-planning/
    ├── README.md (explains phase 1 process)
    └── koaj/
        ├── koaj-brd.md
        ├── koaj-prd.md
        └── koaj-architecture.md
```

## When Making Changes

- Maintain consistency with BMAD methodology
- Ensure templates are complete and self-contained
- Include practical examples and step-by-step instructions
- Consider Bird.com's manual configuration limitations
- Focus on WhatsApp-specific implementation details
- **CRITICAL**: Always follow the file organization rules above