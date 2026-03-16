# CLAUDE.md

This file provides guidance to AI assistants (Claude and others) working in this repository.

## Repository Overview

This repository is **Donjet2000/test-1**, currently in its initial state with no source files committed yet. This CLAUDE.md serves as a living document that should be updated as the codebase grows.

## Current State

- **Branch model**: Feature branches prefixed with `claude/` are used for AI-assisted development.
- **Active development branch**: `claude/add-claude-documentation-pLHmq`
- **No source code exists yet** — this file was the first commit.

## Git Conventions

### Branching
- AI-assisted work happens on branches named `claude/<description>-<session-id>`
- Never push directly to `main` or `master` without explicit permission
- Always use `git push -u origin <branch-name>` when pushing

### Commit Messages
- Use clear, descriptive commit messages in the imperative mood
- Example: `Add user authentication module` not `Added user auth`

### Signing
- Commits are signed with SSH keys; do not skip signing (`--no-gpg-sign`)
- Do not use `--no-verify` to bypass hooks

## Development Workflow

Since this repository has no code yet, follow these general principles when code is added:

1. **Read before editing** — always read existing files before modifying them
2. **Minimal changes** — only change what is necessary; avoid refactoring unrelated code
3. **No speculative additions** — don't add error handling, abstractions, or features that aren't explicitly needed
4. **Security** — avoid OWASP top-10 vulnerabilities (SQL injection, XSS, command injection, etc.)

## Adding Project Documentation

When source code is added to this repository, update this file with:

- **Project purpose**: What the application/library does
- **Tech stack**: Languages, frameworks, and major dependencies
- **Directory structure**: Where source, tests, and config live
- **Build commands**: How to build and run the project
- **Test commands**: How to run the test suite
- **Lint/format commands**: Code style tooling and how to run it
- **Environment setup**: Required env vars and how to configure them
- **CI/CD**: How automated pipelines work

## File Structure (to be updated)

```
/                   # repo root (currently empty)
└── CLAUDE.md       # this file
```

## Notes for AI Assistants

- This repo uses a local git proxy (`127.0.0.1:34399`) — network retries may be needed on push
- If push fails, retry up to 4 times with exponential backoff (2s, 4s, 8s, 16s)
- Confirm destructive operations (force-push, branch deletion, file deletion) with the user before proceeding
- Do not create unnecessary files — prefer editing existing ones
