# AI Engineering Structure

A modern project structure optimized for efficient AI-assisted development using Claude Code and OpenAI Codex.

## Overview

This repository provides a standardized structure for AI-enhanced software development workflows. Rather than directly inputting commands, documentation, and feature requests into the CLI of Claude Code or OpenAI Codex, this structure offers a more organized, version-controlled, and collaborative approach to working with AI coding assistants.

## Directory Structure

```
ai_engineering_structure/
├── .claude/
│   └── commands/       # Custom Claude Code command definitions
│       ├── COMMANDS.md # Documentation for commands system
│       └── prime.md    # Context initialization command
├── ai_docs/            # AI-specific documentation
│   ├── AI_DOCS.md      # Documentation for AI docs system
│   ├── claude_thinking.md
│   └── openai_reasoning_models.md
├── specs/              # Feature specifications
│   ├── SPECS.md        # Documentation for specs system
│   └── openai_reasoning.md
└── README.md           
```

## Key Components

### 1. Claude Commands (`.claude/commands/`)

Custom reusable commands that streamline interactions with Claude Code:

- **Project Context Initialization**: The `prime.md` command quickly primes Claude with project structure and important documentation
- **Standardized Workflows**: Create commands for code generation, testing, analysis, and more
- **Invocation Syntax**: Use `/project:command_name` to execute commands

### 2. AI Documentation (`ai_docs/`)

Specialized documentation that enhances AI models' understanding of your project:

- **Domain-Specific Knowledge**: Terminology, architecture, and design patterns
- **Implementation Details**: System relationships and code examples
- **Enhanced Generation**: Helps Claude generate code aligned with your project's patterns
- **Invocation Syntax**: Use `@[path/to/document]` to reference docs in conversations

### 3. Feature Specifications (`specs/`)

Structured specifications for planned features:

- **Implementation Blueprint**: Detailed specs for types, methods, tests, and validation
- **Consistent Design**: Standardized format ensures all necessary details are included
- **AI-Ready Format**: Optimized for consumption by Claude Code
- **Invocation Syntax**: Use `@[path/to/spec.md]` to reference in conversations

## Advantages Over Direct CLI Usage

### 1. Enhanced Context Management

- **Persistent Context**: Documentation remains consistent across sessions
- **Focused Inputs**: Provide only relevant context for each task
- **Knowledge Reuse**: Share documentation across team members
- **Versioned Context**: Track changes to AI-specific documentation over time

### 2. Improved Development Workflow

- **Reduced Repetition**: Eliminate redundant explanations and setup commands
- **Standardized Patterns**: Ensure consistent AI-assisted development across projects
- **Collaborative Development**: Multiple developers can contribute to and review AI-specific artifacts
- **Version Control**: Track changes to AI commands, documentation, and specs

### 3. Higher Quality AI-Generated Code

- **Better Understanding**: AI models receive clear, structured information
- **Consistent Conventions**: Generated code follows established project patterns
- **Reduced Hallucinations**: Explicit documentation reduces AI "guessing"
- **Faster Results**: Well-documented context leads to faster, more accurate generations

### 4. Project Scalability

- **Organized Knowledge Base**: Scale AI interactions as project grows
- **Onboarding Efficiency**: New developers can quickly understand project context
- **Evolving Documentation**: Update AI docs alongside code changes
- **Modular Structure**: Add new commands, docs, and specs as needed

## Using the Prime Command

The `prime.md` command fills Claude's context window with essential project information:

1. Run `/project:prime` in Claude Code
2. Claude will:
   - Display the project structure
   - Read key documentation files
   - Build a comprehensive understanding of the project

This allows Claude to provide more accurate assistance with your project.

## Best Practices

1. **Keep Documentation Current**: Update AI docs as your codebase evolves
2. **Be Explicit**: Provide clear patterns and examples in documentation
3. **Standardize Commands**: Create consistent commands for common tasks
4. **Use Version Control**: Commit changes to AI artifacts alongside code changes
5. **Include Examples**: Add representative code snippets to aid AI understanding

## Getting Started

1. Clone this repository or use it as a template
2. Customize the structure for your project's needs
3. Add your project-specific documentation to each section
4. Commit changes to version control
5. Use the prime command in Claude Code to initialize context