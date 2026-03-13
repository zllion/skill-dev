# Example Alignment Reports

This file contains examples of documentation-code alignment reports from real projects. Use these as references when generating your own reports.

## Example 1: Rust CLI Project (task-cli)

### Summary

- **Total Code Elements**: 47
  - Commands: 11 (add, list, update, done, cancel, tags, tag, memo, create, info, set-default)
  - Public Functions: 28
  - Modules: 8
- **Total Documentation Files**: 4 (README.md, CLAUDE.md, DESIGN.md, ralph/progress.txt)
- **Documentation Coverage**: 67% (32/47 elements documented)

### Critical Issues

#### Undocumented Command: `info`

- **Type**: Command
- **Location**: `src/main.rs:89`
- **Issue**: The `info` command is implemented but not documented in README.md
- **Impact**: Users cannot discover this command
- **Suggestion**: Add to README.md under "Commands" section with description: "Display detailed information about a workspace"
- **Priority**: High

#### Undocumented Command: `set-default`

- **Type**: Command
- **Location**: `src/main.rs:95`
- **Issue**: The `set-default` command is implemented but not documented
- **Impact**: Users cannot discover workspace management features
- **Suggestion**: Add to README.md under "Workspace Management" section
- **Priority**: High

### Warnings

#### Outdated Function Signature: `add_task`

- **Document**: `CLAUDE.md:145`
- **Section**: "Adding Tasks"
- **Issue**: Documentation shows outdated signature
- **Documented As**: `fn add_task(description: String)`
- **Current Signature**: `pub fn add_task(workspace: &Workspace, description: String) -> Result<TaskId>`
- **Suggestion**: Update CLAUDE.md to include the workspace parameter and explain the workspace context
- **Priority**: Medium

#### Missing Documentation: Workspace Resolver

- **Code**: `src/workspace_resolver.rs:15-67`
- **Function**: `resolve_workspace()`
- **Issue**: Complex workspace resolution logic not documented in CLAUDE.md
- **Impact**: Developers don't understand how workspace resolution works
- **Suggestion**: Add section to CLAUDE.md explaining the resolution algorithm:
  1. Check current directory for tasks.md
  2. Fall back to default workspace
  3. Error with helpful message if no workspace found
- **Priority**: Medium

### Informational Findings

#### Missing Example: Tag Filtering

- **Element**: `list` command with tag filtering
- **Location**: `README.md:34`
- **Issue**: Tag filtering feature mentioned but no usage example
- **Current Doc**: "Filter tasks by tag with `task-cli list #tag`"
- **Suggestion**: Add example showing hierarchical tag filtering:
  ```bash
  # List all work tasks
  task-cli list #work

  # List specific work subcategory
  task-cli list #work/backend
  ```
- **Priority**: Low

#### Missing Example: Workspace Auto-Discovery

- **Feature**: Automatic workspace registration
- **Location**: `CLAUDE.md:234`
- **Issue**: Auto-discovery behavior documented but not demonstrated
- **Suggestion**: Add step-by-step example of how auto-discovery works when navigating to a directory with tasks.md
- **Priority**: Low

### Recommendations

#### Immediate Actions

1. **Document `info` and `set-default` commands** (15 minutes, High impact)
2. **Update `add_task` signature in CLAUDE.md** (5 minutes, Medium impact)

#### Short-term Improvements

1. **Add workspace resolution flow diagram** (30 minutes, High impact for developers)
2. **Create comprehensive command reference** (1 hour, High impact for users)

#### Long-term Enhancements

1. **Add architecture decision records** for workspace system (2 hours, High impact for contributors)
2. **Create troubleshooting guide** for common workspace issues (1 hour, Medium impact)

---

## Example 2: Python Web API Project

### Summary

- **Total Code Elements**: 89
  - API Endpoints: 23
  - Public Functions: 45
  - Models: 12
  - Tests: 9 test suites
- **Total Documentation Files**: 6 (README.md, docs/API.md, docs/DEPLOYMENT.md, docs/CONTRIBUTING.md, docs/CHANGELOG.md)
- **Documentation Coverage**: 78% (69/89 elements documented)

### Critical Issues

#### Undocumented Endpoint: `DELETE /api/users/{id}/sessions`

- **Type**: API Endpoint
- **Location**: `src/api/routes/users.py:145`
- **Issue**: Endpoint implemented but not in API.md
- **Impact**: API consumers don't know this endpoint exists
- **Suggestion**: Add to docs/API.md under "User Management" section:
  ```
  ### DELETE /api/users/{id}/sessions
  Logout user from all sessions.
  **Requires**: Admin role
  **Returns**: 204 No Content
  ```
- **Priority**: High

#### Breaking Change Not Documented

- **Code**: `src/api/routes/auth.py:67`
- **Function**: `login()`
- **Issue**: v2.0 changed return format but CHANGELOG.md doesn't mention it
- **Current**: Returns `{token, user, expires_at}`
- **v1.x**: Returned `{token, user}`
- **Impact**: Breaking change for API consumers
- **Suggestion**: Add to CHANGELOG.md v2.0 section:
  ```
  ### Breaking Changes
  - `POST /api/auth/login` now returns `expires_at` field
  ```
- **Priority**: High

### Warnings

#### Outdated Parameter Documentation

- **Document**: `docs/API.md:89`
- **Endpoint**: `POST /api/posts`
- **Issue**: Documentation missing `tags` parameter
- **Documented Parameters**: `title`, `content`, `author_id`
- **Actual Parameters**: `title`, `content`, `author_id`, `tags` (array, optional)
- **Suggestion**: Update parameter list and add example with tags
- **Priority**: Medium

#### Missing Error Code Documentation

- **Code**: `src/api/errors.py`
- **Error Codes**: 15 custom error codes defined
- **Documentation**: Only 8 documented in API.md
- **Missing**: `USER_NOT_FOUND`, `SESSION_EXPIRED`, `INVALID_TOKEN`, etc.
- **Suggestion**: Create complete error code reference table
- **Priority**: Medium

### Informational Findings

#### Missing Request/Response Examples

- **Endpoints**: 23 total, only 9 have examples
- **Impact**: Developers struggle to integrate without examples
- **Suggestion**: Add request/response examples for all endpoints:
  ```markdown
  ### Example Request
  ```json
  {
    "title": "My Post",
    "content": "Post content",
    "tags": ["tech", "python"]
  }
  ```

  ### Example Response
  ```json
  {
    "id": 123,
    "title": "My Post",
    "created_at": "2024-02-28T10:00:00Z"
  }
  ```
  ```
- **Priority**: Low (but high value)

---

## Example 3: JavaScript Library

### Summary

- **Total Code Elements**: 156
  - Public Functions: 89
  - Classes: 12
  - Types/Interfaces: 34
  - Constants: 21
- **Total Documentation Files**: 3 (README.md, docs/API.md, docs/GUIDES.md)
- **Documentation Coverage**: 92% (143/156 elements documented)

### Critical Issues

None - this project has excellent documentation coverage.

### Warnings

#### Outdated Type Definition

- **Document**: `docs/API.md:234`
- **Interface**: `UserConfig`
- **Issue**: Documentation missing new optional fields
- **Documented Fields**: `name`, `email`
- **Actual Fields**: `name`, `email`, `preferences?`, `metadata?`
- **Suggestion**: Update interface documentation with optional fields and their types
- **Priority**: Medium

### Informational Findings

#### Missing Migration Guide

- **Feature**: v3.0 introduced breaking changes
- **Issue**: No migration guide for v2.x users
- **Impact**: Users struggle to upgrade
- **Suggestion**: Create `docs/MIGRATION_v2_to_v3.md` with:
  - List of breaking changes
  - Code examples showing before/after
  - Step-by-step migration instructions
- **Priority**: Low (but high user value)

#### Missing Performance Guide

- **Feature**: Library has performance optimization options
- **Issue**: No documentation on when to use which options
- **Suggestion**: Add "Performance Tuning" guide to docs/GUIDES.md
- **Priority**: Low

---

## Common Patterns Across Examples

### High-Priority Issues (Always Report)

1. **Undocumented public APIs**: Commands, endpoints, public functions
2. **Breaking changes not documented**: Critical for versioned projects
3. **Outdated signatures**: Parameters or return types don't match

### Medium-Priority Issues (Usually Report)

1. **Missing parameter documentation**: Incomplete API docs
2. **Outdated examples**: Code examples that don't work
3. **Missing error documentation**: Undocumented error states

### Low-Priority Issues (Report When Comprehensive)

1. **Missing usage examples**: Could improve but not critical
2. **Missing guides**: Migration, performance, troubleshooting
3. **Style inconsistencies**: Minor formatting or tone differences

### Severity Guidelines

- **Error**: Code is broken or unusable due to doc issue
- **Warning**: Documentation is misleading or significantly incomplete
- **Info**: Documentation could be improved but is functional

### Coverage Thresholds

- **Excellent**: >90% documented
- **Good**: 75-90% documented
- **Fair**: 50-75% documented
- **Poor**: <50% documented

Always report coverage percentage and compare to these thresholds.
