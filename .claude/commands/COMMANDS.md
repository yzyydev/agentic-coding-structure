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
6. **Code Reviews**: Automated checks for code quality, style conformance, and potential issues
7. **Dependency Analysis**: Scanning and reporting on project dependencies and potential vulnerabilities
8. **Onboarding Assistance**: Quick-start guides for new developers joining the project
9. **CI/CD Pipeline Integration**: Commands to test or update CI/CD configuration files
10. **Database Schema Exploration**: Commands to load and explain database schemas
11. **Performance Profiling**: Instructions to run profiling tools and interpret results
12. **API Documentation Generation**: Automatically generate API docs from code comments
13. **Localization Support**: Commands to extract strings for translation or manage localization files
14. **Code Refactoring Templates**: Standard patterns for common refactoring operations
15. **Architecture Visualization**: Generate architecture diagrams from codebase analysis

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

## Advanced Command Examples

### Automated Test Generator

```markdown
# Generate Tests
> Generate unit tests for a specified module or function

## Read the target file

{TARGET_FILE}

## Generate pytest tests with coverage for all public methods

1. Create appropriate test fixtures
2. Test normal usage patterns
3. Test edge cases and error conditions
4. Include docstrings explaining test purpose
```

### Dependency Analyzer

```markdown
# Analyze Dependencies
> Scan project dependencies and provide a security and compatibility report

## Run the following commands

pip list --outdated
npm audit (if package.json exists)

## Analyze key dependencies

1. Identify major frameworks and their versions
2. Flag deprecated or vulnerable packages
3. Suggest upgrade paths for outdated dependencies
```

### Performance Profiler

```markdown
# Profile Performance
> Run performance tests on specified module or endpoint

## Run the following command

python -m cProfile -o profile_results.pstat {TARGET_SCRIPT}
python -m pstats profile_results.pstat

## Analyze the results

1. Identify the top 10 bottlenecks
2. Suggest optimization strategies
3. Compare with previous profiling runs if available
```

### Architecture Diagram Generator

```markdown
# Generate Architecture Diagram
> Create visual representation of project architecture

## Analyze codebase structure

1. Identify key modules and their relationships
2. Map data flow between components
3. Document external service integrations

## Create diagram

Generate a PlantUML or Mermaid diagram representing the architecture
```

## Contextual Command Pattern

Commands can be designed to be contextually aware, adapting their behavior based on the current codebase state or conversation context:

```markdown
# Smart Linting
> Run appropriate linters based on detected file types

## Detect project language and frameworks

## Run appropriate linting tools

For Python: flake8, pylint
For JavaScript: eslint
For TypeScript: tslint
For Ruby: rubocop

## Summarize linting results

1. Group issues by severity
2. Provide specific file locations
3. Suggest automated fixes where applicable
```

## Command Customization

Commands can include customization options to adapt to different use cases:

```markdown
# Code Review
> Perform automated code review with customizable focus areas

## Parameters

- FOCUS: ["security", "performance", "maintainability", "all"]
- VERBOSITY: ["high", "medium", "low"]
- INCLUDE_SUGGESTIONS: [true, false]

## Run appropriate analysis tools based on parameters

## Generate review report
```

## Integration Patterns

### Development Workflow Integration

Commands can be integrated into standard development workflows:

1. **Pre-commit Checks**: Commands that run before committing code changes
2. **Post-merge Analysis**: Commands that analyze code after merging branches
3. **Sprint Review Preparation**: Commands that generate sprint review materials
4. **Release Preparation**: Commands that prepare documentation and notes for releases

### Team Collaboration

Commands can facilitate team collaboration:

1. **Knowledge Sharing**: Commands that extract and organize tribal knowledge from codebase
2. **Standards Enforcement**: Commands that check adherence to team coding standards
3. **Code Explanation**: Commands that generate explanations of complex code sections for team discussion
4. **Meeting Preparation**: Commands that prepare code-related materials for meetings
