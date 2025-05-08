# AI Documentation for Claude Code

## Overview

The `ai_docs` directory provides a structured repository for AI-specific documentation that enhances Claude's understanding of your project. These documents serve as specialized knowledge bases that Claude can reference for deeper context, domain-specific terminology, architectural patterns, and implementation details that might not be readily apparent from code inspection alone.

## Directory Structure

```
ai_engineering_structure/
└── ai_docs/
    ├── AI_DOCS.md           # This documentation file
    ├── architecture.md      # System architecture documentation
    ├── domain_concepts.md   # Domain-specific terminology and concepts
    ├── design_patterns.md   # Custom design patterns used in the project
    ├── ai_strategy.md       # AI implementation strategy
    ├── openai_reasoning_models.md  # External API & framework documentation
    └── subdirectories/      # Optional topic-specific documentation
        ├── apis/            # API-specific context documentation
        ├── models/          # ML/AI model documentation
        └── workflows/       # Workflow and process documentation
```

## Documentation File Format

AI documentation files are Markdown (`.md`) documents structured to provide Claude with specific context about various aspects of the system. While there's flexibility in formatting, effective AI documentation typically follows certain patterns to maximize Claude's comprehension.

### Recommended Structure

1. **Title/Header**: Clear identification of the document's purpose
2. **Executive Summary**: Brief overview of the document's content (2-3 sentences)
3. **Detailed Sections**: Organized hierarchically with H2/H3 headers
4. **Technical Terminology**: Definitions of domain-specific terms
5. **Relationships**: Explicit connections between components/concepts
6. **Code References**: References to important code patterns with examples
7. **Diagrams**: Textual or ASCII representations of system relationships (Claude can understand these)

Example skeleton:

```markdown
# Domain Model Documentation
> This document describes the core domain model for the system, including key entities, value objects, and their relationships.

## Core Entities

### User
Central entity representing system users with the following properties...

### Transaction
Represents financial transactions with the following characteristics...

## Relationships

- Users can initiate multiple Transactions (1:N)
- Transactions belong to exactly one Category (N:1)

## Implementation Patterns

The domain model follows a DDD (Domain-Driven Design) approach with these specific patterns:

### Entity Base Class
```python
class Entity:
    def __init__(self, id):
        self.id = id
```
```

## Document Types

### Architecture Documentation

Provides Claude with an understanding of your system's overall architecture, component relationships, and design decisions.

Key elements to include:
- System boundaries and external interfaces
- Component hierarchy and dependencies
- Communication patterns and data flow
- Technology stack and justifications
- Architectural constraints and principles

### Domain Concepts

Explains the domain-specific terminology and conceptual model of your system, helping Claude understand the problem space.

Key elements to include:
- Entity definitions and attributes
- Business rules and invariants
- Domain-specific terminology glossary
- Bounded contexts and their relationships
- Domain events and state transitions

### Design Patterns

Documents custom or standard design patterns used throughout the codebase, enabling Claude to recognize and apply these patterns consistently.

Key elements to include:
- Pattern name and general purpose
- Structure and participant components
- Code examples showing implementation
- Usage contexts and variations
- Benefits and trade-offs

### API & Framework Documentation

Documents covering external APIs, SDKs, and frameworks that your project integrates with. These files provide context on endpoint definitions, usage patterns, authentication mechanisms, versioning, and best practices.

Key elements to include:
- **API Overview**: Description of the API or framework purpose and scope
- **Endpoints/Interfaces**: Detailed list of relevant endpoints, parameters, and response schemas
- **Authentication & Security**: OAuth flows, API keys, token scopes, and permissions
- **Usage Examples**: Code snippets in supported languages (e.g., Python, JavaScript, curl)
- **Rate Limits & Quotas**: Information on usage constraints and backoff strategies
- **Versioning & Changelog**: API version details and links to change histories
- **Integration Guides**: SDK library references and integration workflows
- **Best Practices & Caveats**: Common pitfalls and recommended usage patterns

For example, `[openai_reasoning_models.md](./openai_reasoning_models.md)` documents OpenAI's reasoning models (o3, o4-mini), usage with the Responses API, reasoning parameters, and sample code.

### AI Strategy

Defines how AI/ML is integrated into the system, including model selection, training approaches, and evaluation criteria.

Key elements to include:
- Problem formulation and approach
- Model architecture and design decisions
- Data pipeline and preprocessing steps
- Evaluation metrics and performance targets
- Deployment strategy and monitoring

## Documentation Invocation

Documentation files in the `ai_docs` directory can be referenced in Claude conversations using the `@[path]` notation, which tells Claude to incorporate the specified document into its context.

### Syntax

```
@[path/to/document]
```

Example:

```
@[ai_engineering_structure/ai_docs/architecture.md]
```

When this pattern is used, Claude will:

1. Locate the document at the specified path
2. Read and incorporate its contents into the current context
3. Use the information to inform responses and code generation
4. Reference specific concepts from the document when relevant

## Use Cases

### Enhanced Code Generation

Providing domain and architectural context enables Claude to generate code that aligns with your project's specific patterns and requirements.

Example invocation:

```
@[ai_engineering_structure/ai_docs/design_patterns.md]

Please implement a new service for handling user authentication following our established patterns.
```

### Architectural Guidance

Architecture documentation helps Claude provide design recommendations that align with your system's existing structure.

Example invocation:

```
@[ai_engineering_structure/ai_docs/architecture.md]

What's the best way to add a new notification subsystem that aligns with our current architecture?
```

### Domain-Aware Analysis

Domain concept documentation enables Claude to correctly interpret domain-specific terminology and business logic.

Example invocation:

```
@[ai_engineering_structure/ai_docs/domain_concepts.md]

Review this implementation of our settlement process and identify any potential issues with the business rules.
```

### Other Potential Uses

1. **Knowledge Transfer**: Onboarding new developers with clear, AI-guided explanations of complex systems
2. **Consistency Enforcement**: Ensuring code generation follows established patterns and conventions
3. **Technical Debt Analysis**: Having Claude analyze code against documented architectural principles
4. **Documentation Generation**: Creating user-facing documentation that aligns with internal concepts
5. **API Design Assistance**: Developing APIs that follow domain naming and structural conventions
6. **Test Strategy Development**: Generating test plans that cover critical domain scenarios
7. **Refactoring Guidance**: Planning refactoring initiatives with architectural goals in mind
8. **Integration Design**: Planning new integrations that align with system boundaries and interfaces
9. **Schema Evolution**: Managing database schema changes consistent with domain model evolution
10. **Compliance Verification**: Checking implementations against documented regulatory requirements

## Documentation Best Practices

1. **Specificity Over Generality**: Provide concrete details rather than vague generalizations
2. **Explicit Relationships**: Clearly state how components and concepts relate to each other
3. **Code Examples**: Include representative code snippets illustrating key patterns
4. **Terminology Consistency**: Use consistent naming across all documentation
5. **Progressive Disclosure**: Organize information from high-level concepts to specific details
6. **Update Frequency**: Keep documentation synchronized with code changes
7. **Single Source of Truth**: Avoid duplicating information across multiple documents
8. **Visual Representations**: Use ASCII diagrams or text-based charts where appropriate

## Technical Implementation Details

### Document Resolution

When a document is referenced using `@[path]`, Claude resolves the path relative to the project root. The path should be the complete relative path from the project root to the document file.

### Context Integration

Claude reads and integrates documentation into its context model by:

1. Parsing the Markdown structure to understand document organization
2. Extracting key concepts, terminology, and relationships
3. Building an internal knowledge graph of system components
4. Referencing this knowledge when generating code or analysis

### Documentation Limitations

1. Documentation cannot replace actual code inspection for current implementation details
2. Excessively long documents may be truncated in Claude's context window
3. Highly technical diagrams (beyond ASCII/text) may not be fully interpreted

## Advanced Usage

### Layered Documentation

Organize documents in a hierarchical structure, from high-level architecture to specific implementation details:

```
ai_docs/
├── L1_system_overview.md       # Highest level overview
├── L2_subsystem_architecture/   # Mid-level architectural details
└── L3_component_design/         # Detailed component design
```

This allows referencing the appropriate level of detail based on the task at hand.

### Documentation Templates

Consider creating standardized templates for different documentation types to ensure consistency:

```markdown
# [Component Name] Design Document

## Purpose and Responsibilities
[Brief description of the component's purpose]

## Interfaces
[API definitions and interaction patterns]

## Internal Design
[Implementation details and patterns]

## Dependencies
[External systems and components relied upon]

## Constraints and Limitations
[Known constraints or limitations]
```

### Live Code References

Reference specific code files or functions that implement described patterns:

```markdown
The Repository pattern is implemented in `src/infrastructure/repositories/base_repository.py` with concrete implementations following this pattern:

```python
class BaseRepository:
    def get_by_id(self, id): ...
    def save(self, entity): ...
```
```

## Documentation Maintenance

To ensure AI documentation remains valuable over time:

1. **Review Cycle**: Establish regular reviews of AI documentation for accuracy
2. **Change Tracking**: Update documentation alongside significant code changes
3. **Documentation Tests**: Consider implementing tests that verify documentation accuracy
4. **Consistency Checking**: Periodically review for terminology consistency
5. **Feedback Loop**: Gather feedback on documentation effectiveness from team members

## Integration with Development Workflow

### During Design

Create or update AI documentation early in the design process to help Claude assist with implementation planning and code generation:

```
1. Update domain_concepts.md with new entities
2. Reference in conversation with Claude
3. Collaborate on implementation approach
```

### During Implementation

Reference relevant documentation while implementing features to ensure Claude's code suggestions align with architectural intent:

```
@[ai_engineering_structure/ai_docs/design_patterns.md]

I'm implementing the new payment processing service. Please help me structure it according to our standard service patterns.
```

### During Code Review

Use documentation as a reference point for evaluating implementation against design intent:

```
@[ai_engineering_structure/ai_docs/architecture.md]

Review this implementation for alignment with our architectural principles:
[code snippet]
```

## Example Documentation Excerpt

```markdown
# Event Sourcing Implementation

## Overview
This document describes our implementation of the Event Sourcing pattern for maintaining state in the core domain model.

## Core Concepts

### Events
Immutable records of state changes in the system. All events implement the following interface:

```python
class DomainEvent:
    event_id: UUID
    aggregate_id: UUID
    timestamp: datetime
    version: int
```

### Event Store
Persistence mechanism for events with the following characteristics:
- Append-only storage
- Retrieval by aggregate ID
- Optional snapshotting for performance

### Aggregates
Consistency boundaries that maintain their state through an event stream:
```python
class Aggregate:
    def apply_event(self, event):
        # Update internal state based on event
        pass
        
    def load_from_history(self, events):
        for event in events:
            self.apply_event(event)
```

## Implementation Details
Our event store is implemented using PostgreSQL with the following schema...
```

## Conclusion

The `ai_docs` directory serves as a critical resource for enhancing Claude's understanding of your project's domain, architecture, and implementation patterns. By maintaining comprehensive and accurate AI documentation, you enable Claude to provide more contextually appropriate code generation, analysis, and recommendations that align with your project's specific needs and constraints.