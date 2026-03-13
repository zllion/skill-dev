---
name: doc-code-aligner
description: >
  Analyze alignment between documentation and code to find inconsistencies,
  missing documentation, and outdated references. Use when user asks to check
  documentation accuracy, verify docs match code, find undocumented code,
  detect outdated docs, or analyze documentation completeness. Triggers on:
  align docs with code, check documentation, verify documentation accuracy,
  find missing documentation, detect outdated docs, documentation code alignment.
---

# Documentation-Code Alignment Analyzer

This skill helps you systematically analyze and report on the alignment between a codebase's documentation and its actual implementation.

## When to Use This Skill

Use this skill when users request:
- "Check if my documentation is up to date"
- "Find undocumented functions"
- "Align docs with code"
- "Detect outdated documentation"
- "Validate documentation completeness"
- "Generate documentation coverage report"

## Analysis Process

Follow these steps in order to perform a comprehensive alignment analysis.

### Step 1: Understand the Codebase Structure

First, understand what you're analyzing:

1. **Identify the project type**: Look for clues about language and framework
   - Check for `Cargo.toml` (Rust), `package.json` (Node.js), `requirements.txt` (Python)
   - Identify the main entry points (main.rs, index.js, etc.)

2. **Identify documentation files**: Use Glob to find all documentation
   ```
   Use Glob with patterns: README*, *.md, CLAUDE.md, DESIGN.md, docs/**
   ```

3. **Understand the scope**: Ask the user if they want to analyze:
   - All code and documentation, or
   - Specific modules/features only

### Step 2: Extract Code Elements

Systematically extract code elements that should be documented:

#### CLI Commands and Flags

For **Rust projects using clap**:
```
Use Grep to search for:
- Pattern: "Commands::" (finds command enum variants)
- Pattern: "#\[arg\]" or "#\[clap\]" (finds flags and arguments)
- Read main.rs and command handler files
```

For **Node.js projects**:
```
Use Grep to search for:
- Pattern: "\.command\(" (finds command definitions)
- Pattern: "\.option\(" (finds option definitions)
- Read CLI entry point files
```

Extract:
- Command names
- Command descriptions/Help text
- Flags and their descriptions

#### Function Signatures

```
Use Grep to find public functions:
- Rust: Pattern "pub fn" with type "rust"
- Python: Pattern "^def |^async def " with type "py"
- JavaScript: Pattern "^function |export function|export const" with type "js"
```

For each function:
- Extract function name
- Extract signature (parameters and return types)
- Note the file and line number
- Check if it has doc comments (/// for Rust, """ for Python, /** */ for JS)

#### Module Structure

```
Use Glob to find module files:
- Rust: **/*.rs (exclude target/)
- Python: **/*.py (exclude __pycache__/)
- JavaScript: **/*.js or **/*.ts (exclude node_modules/)
```

Map out:
- Module hierarchy
- File organization
- Public vs private modules

#### Tests

```
Use Grep to find test functions:
- Rust: Pattern "#\[test\]" with type "rust"
- Python: Pattern "def test_|async def test_" with type "py"
- JavaScript: Pattern "it\(|test\(|describe\(" with type "js"
```

### Step 3: Analyze Documentation

#### Types of Documentation to Analyze

Common documentation files and directories you may encounter:

**Project Documentation:**
- `README.md` - Main project documentation and getting started guide
- `DESIGN.md` - Architecture and design documentation
- `CLAUDE.md` - AI assistant instructions (Claude Code specific)
- `AGENT.md` - AI agent instructions
- `GEMINI.md` - Gemini CLI instructions
- `CONTRIBUTING.md` - Contribution guidelines
- `CHANGELOG.md` - Version history and changes
- `LICENSE.md` - License information

**API Documentation:**
- `docs/` - Documentation directory
- `doc/` - Alternative documentation directory
- `api/` - API documentation
- `API.md` - API reference documentation

**Technical Documentation:**
- `INSTALLATION.md` - Installation instructions
- `DEVELOPMENT.md` - Development setup guide
- `DEPLOYMENT.md` - Deployment procedures
- `TESTING.md` - Testing guide
- `ARCHITECTURE.md` - System architecture documentation

**User Documentation:**
- `USAGE.md` - Usage examples and patterns
- `EXAMPLES.md` - Code examples and tutorials
- `FAQ.md` - Frequently asked questions
- `TROUBLESHOOTING.md` - Common issues and solutions

**Inline Documentation:**
- Doc comments in code (`///`, `/** */`, `"""`)
- Inline comments explaining complex logic
- Type definitions with documentation

#### Analysis Process

For each documentation file:

1. **Parse the structure**:
   - Use Read to get the full content
   - Extract all headers (lines starting with #)
   - Note the hierarchy and organization

2. **Extract code references**:
   - Find all inline code references (text in backticks)
   - Identify function names, command names, module names mentioned
   - Note which sections discuss which code elements

3. **Check for examples**:
   - Find code blocks (``` marked sections)
   - Note which APIs/commands are demonstrated
   - Check if examples are current vs potentially outdated

### Step 4: Compare and Find Issues

Systematically compare code and documentation to identify:

#### Undocumented Code Elements

For each code element (especially public ones):
1. Search for its name in documentation files using Grep
2. If not found, flag as undocumented
3. Prioritize: commands > public functions > modules > tests

**Severity**: Warning for public APIs, Info for internal code

#### Outdated Documentation

For each code reference in documentation:
1. Check if that element still exists in code
2. Verify the name matches exactly (case-sensitive)
3. For function signatures, check if parameters match

**Severity**: Warning if element doesn't exist, Info if might be renamed

#### Incomplete Documentation

Check for:
- Missing examples for key features
- Outdated examples (check imports, function signatures)
- Missing documentation for new features (compare git history if available)

**Severity**: Info

#### Inconsistent Descriptions

For code elements with doc comments:
1. Extract the doc comment
2. Find corresponding documentation section
3. Compare descriptions for consistency

**Severity**: Info

### Step 5: Generate Alignment Report

Create a comprehensive report following the template in [references/report-template.md](references/report-template.md).

**Report structure**:
1. **Summary**: High-level statistics and counts
2. **Issues by Severity**: Group by error/warning/info
3. **Issues by Category**: Group by undocumented/outdated/inconsistent
4. **Detailed Findings**: Each issue with file locations and suggestions
5. **Coverage Metrics**: What percentage is documented
6. **Recommendations**: Prioritized action items

**Important**: For each issue, provide:
- Exact file path and line number
- Clear description of the problem
- Actionable suggestion for fixing it
- Severity level

### Step 6: Present Findings to User

After generating the report:

1. **Write the report to a file**:
   - Default: `documentation-alignment-report.md`
   - Ask user for preferred location if needed

2. **Summarize key findings**:
   - Start with most critical issues
   - Mention quick wins (easy fixes)
   - Highlight any systematic patterns

3. **Offer next steps**:
   - "Would you like me to help fix any of these issues?"
   - "Should I update the documentation for [specific element]?"
   - "Do you want me to generate documentation for undocumented items?"

## Best Practices

### Be Thorough but Focused

- Start with public APIs and user-facing features
- Don't get bogged down in internal implementation details
- Balance completeness with practicality

### Provide Actionable Feedback

- Don't just say "undocumented" - suggest where to document
- Don't just say "outdated" - explain what changed
- Provide specific file paths and line numbers

### Respect Project Conventions

- Check existing documentation style before suggesting changes
- Match the tone and format of existing docs
- Consider the audience (users vs developers)

### Handle Uncertainty Gracefully

- Use severity levels appropriately
- When unsure if something is an issue, mark as "Info" not "Warning"
- Provide context so users can make informed decisions

## Common Patterns

### Pattern 1: Undocumented CLI Commands

**Detection**: Command exists in main.rs but not in README.md

**Report**:
```
- **Type**: Undocumented Command
- **Element**: `add`
- **Location**: src/main.rs:45
- **Suggestion**: Add documentation in README.md under "Commands" section
- **Example**: See documentation for `list` command for format
```

### Pattern 2: Outdated Function Signature

**Detection**: Doc shows `fn add_task(description: String)` but code has `fn add_task(workspace: &Workspace, description: String)`

**Report**:
```
- **Type**: Outdated Signature
- **Element**: `add_task`
- **Location**: docs/API.md:23
- **Current Signature**: `pub fn add_task(workspace: &Workspace, description: String) -> Result<TaskId>`
- **Documented As**: `fn add_task(description: String)`
- **Suggestion**: Update documentation to include workspace parameter
```

### Pattern 3: Missing Examples

**Detection**: Complex function documented but no usage example

**Report**:
```
- **Type**: Missing Example
- **Element**: `resolve_workspace`
- **Location**: CLAUDE.md:89
- **Suggestion**: Add usage example showing common scenarios
- **Note**: Function has complex logic that would benefit from example
```

## Tips for Effective Analysis

1. **Use grep efficiently**: Combine patterns when searching
2. **Read strategically**: Don't read every file completely - use grep to find relevant sections first
3. **Track what you've checked**: Keep mental notes of what's been analyzed
4. **Prioritize user-facing**: Focus on what users/developers will reference
5. **Be constructive**: Frame issues as opportunities for improvement

## Reference Files

- **[report-template.md](references/report-template.md)**: Template for alignment reports
- **[examples.md](references/examples.md)**: Example reports from real projects
