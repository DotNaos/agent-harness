# Iteration 1 Scope

## Goal

Establish the product foundation:

- multi-project support
- fast project switching
- branch/worktree-based feature runtimes
- isolated agent runtimes
- runtime provider support for Codex and Copilot

This iteration exists to make the product operational at its core.

---

## In Scope

### Multi-project foundation
- register/open multiple local repositories as projects
- persist known projects
- switch between projects quickly
- preserve per-project runtime state while switching

### Project workspace basics
- show active project
- show project branches
- show project feature runtimes
- allow selecting and opening a runtime

### Workspace engine
- inspect repository metadata
- list branches
- create or attach worktrees
- allocate isolated runtime paths and runtime metadata
- manage runtime lifecycle

### Feature runtime model
- create a runtime from a branch
- optionally create a new feature branch
- bind runtime to a worktree
- attach runtime-level env overrides
- track runtime status

### Agent runtime provider abstraction
- shared internal provider interface
- Codex runtime provider
- GitHub Copilot runtime provider
- bind provider session to one feature runtime

### Runtime isolation
- isolate cwd
- isolate env overrides
- isolate runtime temp data
- isolate terminal session
- isolate provider session state

---

## Out of Scope

- advanced code quality enforcement
- design-doc adherence automation
- two-layer planning workflow enforcement
- comment-based context overlays
- README injection hooks
- background steering subagents
- advanced browser automation
- release channel enforcement details
- complete git UX polish

---

## Constraints

- multi-project support is first-class, not optional
- the app must treat feature runtime as the main working unit
- the runtime layer must not hardcode a single provider
- parallel runtimes must not share mutable runtime state by default

---

## Deliverable at End of Iteration

A working desktop foundation where:

- multiple projects are known to the app
- the user can switch between projects quickly
- runtimes can be created from branches/worktrees
- agents can run in isolated contexts
- Codex and Copilot are both supported through one runtime abstraction

---

## Acceptance Criteria

- user can add at least two projects and switch between them without losing state
- user can see branches for a selected project
- user can create a feature runtime for a project branch
- each feature runtime has an isolated working directory and runtime metadata
- user can choose Codex or Copilot for a runtime
- provider session is attached to exactly one runtime
- at least two runtimes can exist concurrently without shared runtime collisions

---

## Dependencies

This iteration is the base for all later work.

Later workflow UX and enforcement layers depend on this iteration being stable first.
