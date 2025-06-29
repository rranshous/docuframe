# DocuFrame Design Document

## Overview

DocuFrame is a minimum viable collaborative frame designed to explore and experiment with the principles outlined in our collaborative-frame-context document. It focuses on human-AI collaboration for idea exploration and expression generation.

## Core Philosophy

This is **exploration and experimentation** - we are not aiming for production products. We want to create a living laboratory for testing collaborative intelligence concepts, particularly:

- **Unified Information Model**: Different representations as facets of the same underlying information
- **Boundary-Driven Development**: Focus on defining constraints and letting AI handle implementation details  
- **Context Preservation**: Maintain rich context about decisions, alternatives, and rationale
- **Collaborative Intelligence**: Human-AI partnership where humans guide direction and AI handles translation/implementation

## Technical Guidelines

- **TypeScript** throughout
- **No more than one backend server**
- **Most simple possible solutions**
- **Use local disk for now**
- **Single user system** (no WebSocket complexity initially)

## Core Domain Concepts

### **Idea** - Evolving Concepts
An **Idea** is the primary unit of exploration in our collaborative frame. It's a living, evolving understanding that grows through human-AI collaboration.

**Properties:**
- **Core Essence**: The fundamental concept being explored
- **Context & Understanding**: Built through exploration sessions
- **Version History**: Track how the idea evolves over time
- **No explicit states** - maturity emerges naturally through exploration depth

**Design Decisions:**
- Ideas exist in a global shared space
- No complex organization or categorization initially
- Version tracked through simple append-only logs

### **Expression** - Multi-Idea Manifestations
An **Expression** is a specific manifestation drawing from multiple ideas, tailored for a particular medium and audience.

**Properties:**
- **Source Ideas**: **Set of ideas** (not single idea) - could be all ideas, subset, or specific combination
- **Medium**: Blog post, technical doc, README, presentation, etc.
- **Audience**: Junior developer, product owner, general public, etc.
- **Purpose**: Inform, persuade, document, teach, etc.
- **Generated Content**: AI-created content drawing from the idea pool
- **Version History**: Track refinements and updates

**Design Decisions:**
- Always assume expressions draw from multiple ideas
- Let AI determine which ideas are relevant for each expression
- No explicit idea→expression relationship mapping initially
- Versioned through simple append-only logs

### **Exploration Session** - Collaborative Memory
The conversation and refinement process between human and AI that builds cumulative collaborative intelligence.

**Properties:**
- **Cross-Idea Learning**: Sessions build on each other regardless of which idea is being explored
- **Collaborative Patterns**: System learns how this human likes to think and explore
- **Accumulated Context**: Each session enriches the overall collaborative relationship
- **Global Memory**: Not scoped to individual ideas but spans all interactions
- **Conversation History**: Full dialogue preservation
- **Insights & Decisions**: Key realizations and choices made during exploration

**Design Decisions:**
- Single global session memory (not per-idea)
- System learns collaboration patterns across all interactions
- Previous insights inform new explorations automatically

## Conceptual Model

```
┌─────────────────────────────────────────────────────────────┐
│                    Collaborative Frame                      │
│                                                             │
│  ┌─────────────┐    ┌─────────────────┐    ┌─────────────┐  │
│  │    Ideas    │    │   Exploration   │    │ Expressions │  │
│  │             │◄──►│    Sessions     │◄──►│             │  │
│  │ (versioned) │    │   (builds       │    │(multi-idea, │  │
│  │             │    │ global memory)  │    │ versioned)  │  │
│  └─────────────┘    └─────────────────┘    └─────────────┘  │
│                                                             │
│              All connected through shared context           │
└─────────────────────────────────────────────────────────────┘
```

## The Collaborative Frame Workflow

1. **Idea Initiation**: Human introduces a seed idea or continues exploring existing idea
2. **Exploration**: Human-AI dialogue to develop understanding, leveraging cumulative collaborative memory
3. **Boundary Definition**: Establish what the idea is/isn't through natural conversation
4. **Expression Generation**: AI creates tailored expressions drawing from relevant ideas
5. **Refinement**: Iterative improvement of both ideas and expressions
6. **Evolution**: Ideas grow and inform future explorations

## Example Flow

```
Session 1: Explore "collaborative frames"
→ Creates/evolves Idea A
→ System learns: Human likes concrete examples, iterative refinement

Session 2: Explore "AI-human boundaries" 
→ Creates/evolves Idea B
→ System applies learned collaboration patterns
→ Naturally references insights from collaborative frames discussion

Expression Generation: "Blog post for developers"
→ AI draws from Ideas A, B, and any others in the pool
→ Creates cohesive narrative combining relevant concepts
→ Human refines → creates Expression v2

Session 3: Explore "system health cultivation"
→ Creates/evolves Idea C  
→ Benefits from accumulated collaborative understanding
→ Previous expressions inform how to articulate new concepts
```

## Key Design Principles

### **Idea-Centric but Multi-Idea Expressions**
- Everything revolves around ideas as the core unit
- Expressions always draw from multiple ideas in the shared pool
- No artificial boundaries between ideas initially

### **Context Preservation**
- The exploration process is as valuable as the final expressions
- Preserve the journey, not just the destination
- Rich conversation history and decision rationale capture

### **Cumulative Collaboration**
- Each session builds the human-AI collaborative relationship
- System learns patterns across all interactions
- Global memory that spans beyond individual ideas

### **Collaborative Intelligence**
- AI participates in idea development, not just content generation
- Boundary definition through conversation
- Expression refinement that updates underlying ideas

### **Versioned Everything**
- Ideas evolve and we track that evolution
- Expressions get refined and we keep the history
- Enables rollback, comparison, and understanding progression

## Future Considerations (Not Initial Implementation)

### **Idea Relationships**
- Graph of interconnected ideas
- Parent-child or network relationships
- Cross-pollination between idea clusters

### **Expression Relationships**
- Expressions building upon other expressions
- Reference networks between different expressions
- Audience progression (intro → intermediate → advanced)

### **Advanced Collaboration Memory**
- Domain-specific collaboration patterns
- Context-aware suggestion refinement
- Predictive idea exploration assistance

### **Multi-User Collaboration**
- Real-time collaborative exploration
- Different user roles and perspectives
- Conflict resolution in idea development

## Implementation Architecture (Initial)

```
src/
├── server/
│   ├── index.ts              # Express server
│   ├── routes/
│   │   ├── exploration.ts    # Conversation/exploration API
│   │   ├── ideas.ts          # Idea management API
│   │   └── expressions.ts    # Expression generation/management API
│   ├── services/
│   │   ├── ai.ts            # AI integration (OpenAI, etc.)
│   │   ├── context.ts       # Global collaborative memory
│   │   ├── ideaService.ts   # Idea management and versioning
│   │   └── expressionService.ts # Expression generation and versioning
│   └── storage/
│       └── fileStore.ts     # Simple file-based storage operations
├── client/
│   ├── index.html           # Simple conversation interface
│   ├── style.css
│   └── app.js               # Frontend logic
└── data/                    # File storage
    ├── ideas/               # Versioned idea files
    ├── expressions/         # Versioned expression files
    ├── sessions/            # Exploration session history
    └── context/             # Global collaborative memory
```

## Success Metrics

How will we know this collaborative frame is working?

1. **Idea Evolution Quality**: Are ideas becoming richer and more nuanced through exploration?
2. **Expression Relevance**: Do generated expressions effectively combine multiple ideas coherently?
3. **Collaborative Learning**: Does the system demonstrably improve at understanding how to work with this human?
4. **Context Preservation**: Can the system surface relevant historical context when needed?
5. **Boundary Effectiveness**: Do conversationally-defined boundaries effectively guide system behavior?

## Open Questions for Implementation

1. **AI Provider**: Start with OpenAI API or another provider?
2. **Expression Triggers**: Auto-generate after every significant exploration, or only when explicitly requested?
3. **Starting Expression Types**: Which formats should we implement first? (outlines, summaries, blog posts, technical docs?)
4. **Context Granularity**: How detailed should the global collaborative memory be initially?
5. **Version Storage**: Simple timestamped files or more sophisticated versioning?

---

*This document captures our design thinking as of June 29, 2025. It will evolve as we experiment and learn through building this collaborative frame.*
