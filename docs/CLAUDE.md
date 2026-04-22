# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development

Install the Mintlify CLI once globally:
```
npm i -g mintlify
```

Run the local dev server from the repo root (where `docs.json` lives):
```
mintlify dev
```

Deployment is automatic — pushing to the default branch triggers the Mintlify GitHub App.

## Architecture

This is a **Mintlify v4** documentation site for QuivaWorks, an AI assistant and workflow automation platform.

### Configuration

All site-level config — navigation structure, colors, logo, fonts, navbar, footer — lives in **`docs.json`**. The navigation is organized into three top-level tabs:

- **Guides** — User-facing documentation grouped into: Get Started, Assistants, Flows, Account Management, Advanced
- **API Reference** — Auto-generated from OpenAPI JSON specs located in `api-reference/endpoint/<group>/openapi.json`
- **Change Log** — Release notes in `changelog/`

Adding a new page requires both creating the `.mdx` file **and** registering its path in the `docs.json` navigation tree. The path in `docs.json` is relative to the repo root and omits the `.mdx` extension.

### Content Format

All content is `.mdx` (Markdown + JSX) with YAML frontmatter:

```mdx
---
title: "Page Title"
description: "Short description shown in cards and SEO."
icon: "icon-name"   # Font Awesome icon slug
---
```

Mintlify components used throughout: `<Card>`, `<CardGroup>`, `<Steps>`, `<Step>`, `<Tip>`, `<Info>`, `<Warning>`, `<Note>`.

Images are stored under `images/` and referenced with absolute paths (e.g. `/images/essentials/example.png`).

### Content Sections

| Directory | Product area |
|-----------|-------------|
| `get-started/` | Onboarding, core concepts, collaboration, plans |
| `assistants/` | AI Assistants — creation, configuration, learning, prompt engineering |
| `assistants/configuration/` | Information, provider, context settings, and knowledge |
| `flows/` | Workflow automation — triggers, steps, functions |
| `flows/triggers/` | HTTP, webhook, schedule, upload, email, embed, stream triggers |
| `flows/steps/` | Agent step, HITL, condition, map, rules, eval, nested flows, API integrations |
| `flows/functions/` | Utility, key-value, object storage, stream functions |
| `essentials/account/` | Account creation, settings, billing, closing |
| `essentials/users/` | User management, roles/permissions |
| `essentials/security/` | Auth, API keys, sessions, incident response |
| `advanced/variable-mapping/` | JSONPath-based variable mapping syntax |
| `advanced/rules/` | Rules engine — concepts, operations, patterns |
| `api-reference/endpoint/` | OpenAPI specs (accounts, secrets, hub-flows, gateway, storage, trigger, monitoring) |
| `changelog/` | Latest release and product updates |

# QuivaWorks — Complete Feature Summary

## Core Assistant Capabilities

### 1. Intelligent Collaboration
- Work with assistants in real-time conversations
- Team and personal sessions with shared collaboration
- @mentions to quickly add team members
- Smart notifications and unread badges
- Shared With Me view for sessions shared by others

### 2. Flexible Architecture

**Team vs. Personal Assistants**
- Team Assistants: Accessible to everyone in your account
- Personal Assistants: Private to the creator only

**Team vs. Personal Settings**
- Team Settings: Instructions, knowledge, integrations, context variables shared with entire team
- Personal Settings: Individual configurations that layer on top of team settings at runtime
- Both merge together when assistant executes

**Account-Level Configuration**
- Branding: Customise look and feel of interface
- Global Instructions: Default instructions passed into all assistant invocations
- Global Knowledge: Company-wide knowledge sources (enabled per-assistant)

### 3. Knowledge & Context Management

**Large Document Processing**
- High-accuracy document processing beyond normal context limits
- Works by loading documents into memory and using sub-agents
- Sub-agents break down document and store breakdown in memory
- Enables processing of entire documents despite token limitations

**Knowledge Integration**
- Add documentation, guidelines, and context to assistants
- Support for multiple knowledge sources
- Integration with account-level global knowledge

**Smart Context Management**
- Intelligent memory management across conversations
- Context variables for environment-specific configuration
- Token limit controls

### 4. System Integration

**Universal Connectivity via MCP Protocol**
- Native Model Context Protocol support
- Auto-generation of MCP servers and integrations from OpenAPI specs
- Enhanced OpenAPI specs with agent instructions supported
- Pre-built integrations for popular business tools
- Custom integration building via MCP

**Tooling Agents & Sub-Agents**
- Context window split across multiple tool calls via sub-agents
- Prevents context window explosion on tool-heavy workflows
- Default tools include: image generation, document generation, research, and all attached integrations

**Built-in Tool Capabilities (use_tools)**
- Web Search: Recent news and general web results
- Content Fetching: Retrieve and parse URLs as markdown
- Document Analysis: Search and analyse knowledge base documents
- Data Encoding/Decoding: Convert data using various schemes
- Math Evaluation: Solve mathematical expressions
- Cryptographic Hashing: Industry-standard hash generation
- Regular Expressions: Pattern matching using Go RE2 syntax
- Date/Time Parsing: Parse and format with timezone support
- JSON Extraction: Extract values using JSONPath
- Task Management: Create and manage structured task lists
- Escalation: Route to human supervisors when needed

**Image Analysis (analyze_image)**
- Describe visual content (photos, diagrams, screenshots)
- Extract text from images
- Analyse charts and graphs
- Identify objects, people, and scenes
- Examine technical diagrams
- Supported formats: PNG, JPG, JPEG, GIF, WEBP

### 5. Content Generation & Deployment

**File Generation**
- Image generation via Nano Banana Pro
- Document generation: DOCX, PPTX, XLSX, CSV
- Generated files stored in user account
- Assistant receives file links for rendering

**Simple App Deployment**
- Create HTML/JS/CSS applications
- "Deploy" command generates random subdomain.quiva.ai URL
- Assets uploaded to publicly accessible bucket
- Live web viewing of generated applications

### 6. Assistant-to-Assistant Communication

**Agent Systems**
- Any assistants in your account can be linked together
- Allows requests between different experts
- Each assistant has different available tools and knowledge
- Enable building sophisticated multi-agent systems

### 7. User Interface Features

**Multi-Tab Conversations**
- Switch between assistant conversations with ease
- Open history as new tab or start new chat in new tab
- Multiple tabs can run simultaneously
- Assistants continue working while switching tabs
- Smart notifications alert when assistants complete tasks

**Chat Enhancements**
- Voice input support
- Emoji support
- Better formatting options
- Redesigned chat interface

### 8. Continuous Learning & Improvement

**Learning System**
- Vote up/down on interactions to identify what works
- Feedback consolidation to surface actionable insights
- Review Learning tab to see patterns from successful interactions
- Intentionally refine assistant behaviour based on learnings
- No automatic improvement—intentional refinement by users

**Performance Insights**
- Consolidated feedback from interactions
- Pattern identification for what works well
- Actionable recommendations for refinement

### 9. Flows

A flow is a sequence of connected steps that execute in response to a trigger. Think of it as a recipe for automation:

- **Triggers** start your flow (webhooks, schedules, form submissions, etc.)
- **Steps** perform actions (run AI assistants, make decisions, transform data, call APIs)
- **Connections** pass data between steps using variable mappings

## Configuration Hierarchy

1. **Account Level** → Branding, Global Instructions, Global Knowledge
2. **Team Assistant** → Instructions, Knowledge, Integrations, Context Variables
3. **Personal Settings** → Personal Instructions, Knowledge, Integrations, Context Variables
4. **Runtime** → Team + Personal settings merge together

## Available AI Model

- **Default Model**: Claude Haiku 4.5 (fast, cost-effective, optimised for business workflows)
- **LLM Provider**: Anthropic Claude (Team and Enterprise can bring own keys)

## Billing Model

- **Credit-based per interaction**: Each assistant conversation consumes credits
- **Monthly refresh**: Included credits reset each month
- **Purchase additional**: Never expire, roll over to next month
- **Plan-based allocation**:
  - Free: 500 credits per account
  - Pro: 1,000 credits per user
  - Team: 1,500 credits per user

## Key Differentiators

✅ Collaboration built-in (not bolted-on)
✅ Document processing beyond context limits
✅ File and image generation with cloud storage
✅ One-click app deployment
✅ Multi-agent systems via assistant-to-assistant communication
✅ Sophisticated tooling via sub-agents
✅ Flexible team/personal/account-level configuration
✅ Intentional learning (not automatic)
✅ Multi-tab workflow with smart notifications

## Real links
Marketplace - https://quiva.ai/marketplace
Logged in Marketplace - https://app.quiva.ai/en/hub/marketplace
Community - https://quiva.ai/community
Help center - https://www.quiva.ai/help-center
Support Email - support@quiva.ai
Help email - help@quiva.ai
Register link - https://app.quiva.ai/en/signup
Login link - https://app.quiva.ai/en/login
Docs site - https://docs.quiva.ai


Missing images to create
                          
  You need to create these 17 images (15 unique paths):
                                                                            
  Image path: /images/agents/information-tab.png
  Used in: assistants/configuration/information-settings.mdx                
  Description: Screenshot of the Information configuration tab
  ────────────────────────────────────────
  Image path: /images/agents/context-tab.png                                
  Used in: assistants/configuration/context-settings.mdx                    
  Description: Screenshot of the Context configuration tab                  
  ────────────────────────────────────────                                  
  Image path: /images/agents/smart-context-diagram.png                      
  Used in: assistants/configuration/context-settings.mdx
  Description: Diagram of how Smart Context works                           
  ────────────────────────────────────────                  
  Image path: /images/agents/tools-diagram.png                              
  Used in: assistants/tools-and-connectors.mdx
  Description: Diagram of tools/MCP connector architecture                  
  ────────────────────────────────────────                  
  Image path: /images/agents/add-tool.png                                   
  Used in: assistants/tools-and-connectors.mdx
  Description: Screenshot of adding a tool/integration                      
  ────────────────────────────────────────                  
  Image path: /images/assistant-learning/rate-conversation.png              
  Used in: assistants/learning.mdx
  Description: Screenshot of thumbs up/down rating UI                       
  ────────────────────────────────────────                  
  Image path: /images/assistant-learning/learning-tab.png
  Used in: assistants/learning.mdx
  Description: Screenshot of the Learning tab with insights
  ────────────────────────────────────────
  Image path: /images/flows/flow-diagram.png                                
  Used in: flows/overview.mdx
  Description: Diagram of a flow with trigger → steps                       
  ────────────────────────────────────────                  
  Image path: /images/flows/trigger-diagram.png                             
  Used in: flows/triggers/overview.mdx
  Description: Diagram showing trigger types                                
  ────────────────────────────────────────                  
  Image path: /images/triggers/button-embed.png                             
  Used in: flows/triggers/embed-triggers.mdx
  Description: Screenshot of button embed trigger                           
  ────────────────────────────────────────                  
  Image path: /images/triggers/form-embed.png
  Used in: flows/triggers/embed-triggers.mdx
  Description: Screenshot of form embed trigger
  ────────────────────────────────────────
  Image path: /images/triggers/chat-embed.png                               
  Used in: flows/triggers/embed-triggers.mdx
  Description: Screenshot of chat embed trigger                             
  ────────────────────────────────────────                  
  Image path: /images/essentials/user-sessions.png                          
  Used in: essentials/security/sessions.mdx,
    essentials/users/user-settings.mdx                                      
  Description: Screenshot of active sessions UI             
  ────────────────────────────────────────
  Image path: /images/global-admin-branding-panel.png                       
  Used in: essentials/account/global-admin-branding-settings.mdx
  Description: Screenshot of global branding settings panel                 
  ────────────────────────────────────────                  
  Image path: /images/rules-step-config.png                                 
  Used in: advanced/rules/getting-started.mdx
  Description: Screenshot of the rules step configuration