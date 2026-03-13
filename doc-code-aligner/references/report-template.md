# Documentation-Code Alignment Report Template

Use this template when generating alignment reports. Customize sections based on the specific codebase and findings.

---

# Documentation-Code Alignment Report

**Generated**: [Date]
**Codebase**: [Project Name]
**Analyzer**: Claude (doc-code-aligner skill)

## Summary

Provide high-level statistics:

- **Total Code Elements**: X
  - Commands: X
  - Public Functions: X
  - Modules: X
  - Tests: X
- **Total Documentation Files**: X
- **Total Documentation Sections**: X

### Alignment Status

- ✅ **Documented**: X elements (X%)
- ⚠️ **Undocumented**: X elements (X%)
- ❌ **Outdated Documentation**: X references
- ℹ️ **Missing Examples**: X elements

### Issue Summary

- **Errors**: X
- **Warnings**: X
- **Info**: X

---

## Critical Issues

List high-priority issues that should be addressed immediately.

### Undocumented Public APIs

Commands and public functions that lack documentation:

#### [Function/Command Name]

- **Type**: [Command/Function/Module]
- **Location**: `file/path.ext:line_number`
- **Signature**: `pub fn example(param: Type) -> ReturnType`
- **Impact**: Users cannot discover this functionality
- **Suggestion**: Add documentation to [specific file] under [specific section]
- **Priority**: High

---

## Warnings

List medium-priority issues that affect documentation quality.

### Outdated Documentation

Documentation that references code elements that have changed or no longer exist:

#### [Reference Name]

- **Document**: `file/path.md:line_number`
- **Section**: "Section Name"
- **Issue**: [Description of what's outdated]
- **Current State**: [What the code actually does now]
- **Documented State**: [What the docs say]
- **Suggestion**: [How to fix it]
- **Priority**: Medium

---

## Informational Findings

List lower-priority issues and suggestions for improvement.

### Missing Examples

Code elements that would benefit from usage examples:

#### [Element Name]

- **Type**: [Function/Command/Feature]
- **Location**: `file/path.ext:line_number`
- **Current Documentation**: [Link to existing docs, if any]
- **Why Example Needed**: [Reason]
- **Suggestion**: [What kind of example would help]
- **Priority**: Low

### Documentation Coverage Opportunities

Areas where documentation could be expanded:

- [ ] Architecture overview
- [ ] Getting started guide
- [ ] API reference
- [ ] Configuration options
- [ ] Troubleshooting guide
- [ ] Contributing guidelines

---

## Detailed Analysis

### Code Elements Analyzed

<details>
<summary>Click to expand full list (X elements)</summary>

#### Commands (X)

- **`command_name`** in `src/main.rs:45` - [Brief description or "Undocumented"]
- ...

#### Public Functions (X)

- **`function_name`** in `src/module/file.rs:123`
  - Signature: `pub fn example(param: Type) -> ReturnType`
  - Documented: Yes/No
  - Location in docs: `docs/file.md#section`
- ...

#### Modules (X)

- **`module_name`** in `src/module/` - [Brief description]
- ...

#### Tests (X)

- **`test_name`** in `src/module/test.rs:45`
- ...

</details>

### Documentation Files Analyzed

<details>
<summary>Click to expand full list (X files)</summary>

#### README.md

- Sections: X
- Code references: X
- Last modified: [Date if available from git]

#### CLAUDE.md

- Sections: X
- Code references: X
- Topics covered: [List main topics]

#### docs/API.md

- Sections: X
- Code references: X
- Coverage: [What's documented]

</details>

---

## Recommendations

Provide prioritized action items:

### Immediate Actions (High Priority)

1. **Document [Command Name]**: Critical command missing from user documentation
   - Estimated effort: 15 minutes
   - Impact: High (users can't discover this feature)

2. **Update [Function Signature]**: Documentation shows outdated parameters
   - Estimated effort: 10 minutes
   - Impact: Medium (users might use wrong API)

### Short-term Improvements (Medium Priority)

1. **Add Examples for [Feature]**: Complex functionality lacks usage examples
   - Estimated effort: 30 minutes
   - Impact: Medium (improves user understanding)

2. **Create API Reference**: Public APIs scattered across multiple docs
   - Estimated effort: 2-3 hours
   - Impact: High (centralized reference)

### Long-term Enhancements (Low Priority)

1. **Add Architecture Documentation**: System design not documented
   - Estimated effort: 4-6 hours
   - Impact: High for new contributors

2. **Create Troubleshooting Guide**: Common issues not documented
   - Estimated effort: 2-3 hours
   - Impact: Medium (reduces support burden)

---

## Methodology

Brief description of how the analysis was performed:

- Code elements extracted from: [Source files analyzed]
- Documentation parsed from: [Doc files analyzed]
- Comparison method: [How alignment was checked]
- Severity assignment: [Criteria used]

---

## Appendix

### Full Issue List by Category

<details>
<summary>Undocumented Elements (X items)</summary>

1. `element_name` in `file:line` - [Brief description]
2. ...

</details>

<details>
<summary>Outdated References (X items)</summary>

1. Reference to `old_name` in `doc:line` - [Issue]
2. ...

</details>

<details>
<summary>Missing Examples (X items)</summary>

1. `complex_function` in `file:line` - [Why example needed]
2. ...

</details>

---

## Next Steps

Suggest what the user might want to do after reading this report:

- "Would you like me to help document the undocumented commands?"
- "Should I update the outdated function signatures?"
- "Do you want me to generate an API reference document?"
- "Can I help create usage examples for complex features?"

---

**Note**: This report was generated using the doc-code-aligner skill. Manual review is recommended for accuracy.
