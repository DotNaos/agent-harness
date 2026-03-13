# Project

## Purpose

Build a desktop app that acts as an agent harness for software engineering work.

The product must let multiple coding agents work in parallel across multiple projects and multiple feature branches, while keeping each runtime isolated.

The first focus is the runtime foundation and daily workflow surface. Enforcement, code quality automation, and steering come after the foundation is stable.

---

## Core Product Goal

The product is not primarily a chat interface.

The product is an enforced execution environment for coding agents.

It must allow a developer to:

- register and switch between multiple projects quickly
- create isolated feature runtimes per branch/worktree
- run multiple agents in parallel
- inspect and manage branch-level work
- use git, terminal, and browser surfaces from one desktop app
- later enforce project-toolkit and agent-toolkit rules consistently

---

## Product Priorities

### 1. Multi-project + multi-branch isolated runtime
This is the foundation.

The app must support:

- multiple projects from day one
- fast switching between projects
- isolated feature runtimes per project
- parallel agents across projects and branches

### 2. Workflow usability
Once the runtime model is stable, the app must expose it through practical developer surfaces:

- project switcher
- branch/worktree view
- git client
- terminal
- browser
- agent activity and runtime status

### 3. Enforcement and fine-tuning
After the runtime and workflow are stable, the app must support:

- code quality enforcement
- design-doc adherence checks
- encapsulation checks
- planning structure
- steering hooks
- project-toolkit and agent-toolkit enforcement

---

## Core Model

The main working unit is:

**Project -> Feature Runtime -> Agent Session**

### Project
A repository-level workspace known to the app.

### Feature Runtime
An isolated working context for one feature branch or worktree.

### Agent Session
A provider-backed coding session attached to one feature runtime.

---

## Runtime Requirements

Each feature runtime must isolate:

- working directory
- branch / worktree
- environment overrides
- temp/runtime files
- terminal session
- browser context when applicable
- agent session state

Parallel feature work must never rely on implicit shared mutable state.

---

## Supported Agent Providers

The runtime layer must support at least:

- Codex SDK
- GitHub Copilot SDK

These must be integrated through a shared provider abstraction.

The harness owns:

- project boundaries
- runtime boundaries
- workflow state
- approvals and policies
- future enforcement hooks

The provider only owns model/runtime execution.

---

## Workflow Surfaces

The app should converge toward these primary surfaces:

- Project switcher
- Branch / worktree view
- Active runtime list
- Git surface
- Terminal surface
- Browser surface
- Agent panel

---

## Planning Model

Project planning is managed under `.dev/`.

The structure is:

```text
.dev/
  Architecture.md
  Iterations/
    Iteration-1/
      Scope.md
      ...feature specs for the active iteration
    Iteration-2/
      Scope.md
    Iteration-3/
      Scope.md
```

Rules:

- `Architecture.md` is the stable high-level product and architecture anchor
- only the current iteration gets detailed feature specs
- future iterations are scoped only at a high level until they become active

---

## Workspace Folder Structure

The workspace uses a flat directory structure within each project to manage the source code and isolate concurrent feature development. 

```text
Projects/
  <project>/
    base/
    feature-<name>/
    feature-<name>/
```

- **`Projects/`**: The root directory containing all managed projects.
- **`<project>/`**: The container directory for a single project's entire workspace. All worktrees and environments for this project checkouts reside here.
- **`base/`**: The primary, long-running codebase. This is the foundation of the project repository (typically tracking `main` or `master`). 
- **`feature-<name>/`**: Isolated worktrees that serve as dedicated feature runtimes for parallel work. These environments prevent state or dependency conflicts between concurrent tasks. All feature folders live directly next to `base/` inside the project folder.

### Example

```text
Projects/
  agent-harness/
    base/
    feature-login-ui/
    feature-api-auth/
```

---

## Implementation Principle

Build the foundation in this order:

1. Multi-project support
2. Feature runtime isolation
3. Agent provider integration
4. Workflow usability surfaces
5. Enforcement and fine-tuning

---

## Non-goals for the first pass

Not required for the first implementation pass unless needed to unblock the runtime foundation:

- deep autonomous memory steering
- advanced semantic memory systems
- full automatic design-doc mutation
- full release automation
- advanced browser-agent orchestration
- complete code quality enforcement automation

---

## Success Condition

The first meaningful success state is:

- multiple projects can be opened
- the user can switch between them quickly
- feature runtimes can be created per branch/worktree
- multiple agents can run in parallel with isolated runtimes
- basic git, terminal, and browser workflow is available

Everything after that improves usability, consistency, and enforcement.
