# Custom Claude Code Commands

## Overview

The `.claude/commands/` directory provides a powerful mechanism for creating and invoking custom commands within Claude Code. These commands allow users to streamline repetitive operations, standardize workflows, and create reusable templates for Claude Code interactions.

## Directory Structure

```
.claude/
└── commands/
    ├── COMMANDS.md  # This documentation file
    ├── prime.md     # Example command for project context initialization
    └── ...          # Additional custom commands
```

## Command File Format

Command files are Markdown (`.md`) documents that follow a specific format to provide structured instructions for Claude. Each command file represents a distinct operation that Claude can execute when invoked.

### Basic Structure

A typical command file includes:

1. **Title/Header**: Describes the command's purpose
2. **Description**: Explains what the command does
3. **Instructions**: Step-by-step directions for Claude to follow
4. **Optional Sections**: Context, parameters, examples, etc.

Example (`prime.md`):

```markdown
# Context Prime
> Follow the instructions to understand the context of the project.

## Run the following command

eza . --tree --git-ignore

## Read the following files
> Read the files below and nothing else.

README.md
```

## Command Invocation

Commands are invoked using the `/project:[Filename]` syntax within Claude Code conversations. This reference pattern tells Claude to locate and execute the specified command file.

### Syntax

```
/project:[Filename]
```

Example:

```
/project:prime
```

When this pattern is used, Claude Code will:

1. Locate the command file at the specified path
2. Parse the command instructions
3. Execute the steps defined in the command
4. Respond according to the command's directives

## Use Cases

### Project Context Initialization

The `prime.md` command demonstrates a common use case: initializing Claude with project context. When invoked, it directs Claude to:

1. Run a command to visualize the project structure
2. Read specific documentation files to understand the project

This ensures Claude has the necessary context before answering questions or performing tasks related to the project.

### Other Potential Uses

1. **Code Generation Templates**: Standardized approaches for generating specific types of code
2. **Documentation Workflows**: Templates for creating consistent documentation
3. **Analysis Routines**: Predefined steps for analyzing code or data
4. **Environment Setup**: Instructions for setting up development environments
5. **Testing Procedures**: Standardized testing protocols

## Command Design Best Practices

1. **Clear Purpose**: Each command should have a single, well-defined purpose
2. **Explicit Instructions**: Provide explicit, step-by-step instructions
3. **Self-Contained**: Commands should include all necessary context
4. **Parameterization**: Consider how commands might accept parameters or variables
5. **Documentation**: Include usage examples and expected outcomes
6. **Modularity**: Design commands to be composable where possible

## Technical Implementation Details

### Command Resolution

When a command is invoked using `@[path]`, Claude resolves the path relative to the project root. The path should be the complete relative path from the project root to the command file.

### Command Execution Context

Commands execute within the context of the current conversation. They have access to:

1. The conversation history up to the point of invocation
2. Any files or resources explicitly referenced in the command
3. The user's active workspace

Commands do not automatically have access to all project files unless specifically directed to read them.

### Command Limitations

1. Commands cannot directly modify files (Claude must be instructed to do so)
2. Commands cannot access external systems unless explicitly permitted
3. Commands are parsed as Markdown, so complex formatting may affect execution

## Advanced Usage

### Dynamic Content

Commands can include placeholder sections that Claude will dynamically replace based on the current context:

```markdown
# Generate Test

Create a unit test for the following function:

{FUNCTION_CODE}

The test should cover the following cases:
- Normal operation
- Edge cases
- Error handling
```

## Security Considerations

1. **Command Validation**: Claude should validate commands before execution
2. **Resource Access**: Commands should only access resources they explicitly need
3. **User Confirmation**: Consider requiring user confirmation for potentially destructive operations

## Extending the Command System

The command system can be extended by:

1. Creating new command files in the `.claude/commands/` directory
2. Organizing commands into subdirectories by category
3. Creating command templates that can be customized for specific use cases
4. Developing meta-commands that can generate or modify other commands
