# ajc-study_exercises

A collection of coding exercises for ongoing programming practice and software engineering interview preparation.

## Purpose

This repository serves as a staging area for practicing coding exercises, primarily generated with the assistance of LLMs.

The main practice languages are **TypeScript** and **Rust**, with **PHP** as a possible future addition.

Exercises are organized by difficulty:

- **Easy** — Fundamental programming concepts and straightforward problems.
- **Medium** — More involved algorithms, data structures, and problem-solving.
- **Hard** — Challenging problems requiring more advanced reasoning.

The goal is to attempt each exercise independently, test the implementation, review alternative solutions, and improve programming skills over time.

## Repository Structure

```text
.
├── exercises/                  # blank worksheets — write your solutions here
│   ├── typescript/
│   │   ├── easy/
│   │   ├── medium/
│   │   └── hard/
│   └── rust/
│       ├── Cargo.toml          # worksheet workspace manifest
│       ├── Cargo.lock
│       ├── easy/
│       ├── medium/
│       └── hard/
├── solutions/                  # reference solutions (fully implemented, tested)
│   ├── typescript/
│   │   ├── easy/
│   │   ├── medium/
│   │   └── hard/
│   └── rust/
│       ├── Cargo.toml          # solutions workspace manifest
│       ├── Cargo.lock
│       ├── easy/
│       ├── medium/
│       └── hard/
├── problems/                   # problem/solution/syntax documents
│   ├── README.md               # catalog (indexed by difficulty and topic)
│   └── ...
├── learning/
│   └── problem-solving-guide.md
├── package.json
├── pnpm-lock.yaml
├── pnpm-workspace.yaml
├── tsconfig.json
├── .gitignore
└── README.md
```

Two directories do two different jobs:

- **`exercises/`** — blank **worksheets**. Each file is a stub (a function signature with a `TODO`). This is where you write your own solution.
- **`solutions/`** — **reference solutions**. Fully implemented, tested, and runnable. Compare your work against these after you attempt a problem.

Every problem is documented in [`problems/`](problems/README.md) with the statement, a reference solution, and a syntax explanation. The directory tree above is illustrative; it grows as problems are added.

## Problem Documents

Every documented exercise lives in [`problems/`](problems/README.md) as a self-contained markdown file with three sections:

- **Problem** — statement, examples, constraints, and prompts to think through before coding.
- **Solution** — approach, TypeScript and Rust implementations, and likely interviewer follow-ups.
- **Syntax Explanation** — the idea in plain steps, each language explained piece by piece, a worked trace, and a TypeScript↔Rust comparison table.

See the [problems catalog](problems/README.md) for the full, indexed list grouped by difficulty and topic.

For guidance on *how to think about and prepare for* these problems, see the [learning guide](learning/problem-solving-guide.md).

## Prerequisites

Install the following tools:

- [Node.js](https://nodejs.org/)
- [pnpm](https://pnpm.io/)
- [Rust and Cargo](https://www.rust-lang.org/tools/install)

Run commands from the repository root unless otherwise specified.

## TypeScript

TypeScript dependencies and configuration are managed from the repository root. Individual worksheets and solutions do not need their own `package.json` or TypeScript installation.

Each TypeScript worksheet is a standalone `.ts` stub; each TypeScript solution is a standalone `.ts` file with the completed implementation and quick checks.

### Initial setup

Install the project dependencies:

```powershell
pnpm install
```

If the TypeScript tooling has not yet been installed, run:

```powershell
pnpm add -D typescript tsx @types/node
```

If `tsconfig.json` does not exist, initialize it:

```powershell
pnpm exec tsc --init
```

These initialization commands only need to be run when setting up or repairing the project, not for each new exercise.

### Running a worksheet

Run your worksheet (from `exercises/`) using `tsx`:

```powershell
pnpm exec tsx exercises/typescript/easy/two_sum.ts
```

### Running a reference solution

Run the corresponding reference solution (from `solutions/`) the same way:

```powershell
pnpm exec tsx solutions/typescript/easy/two_sum.ts
```

Replace the path with the problem you are working on.

### Type-checking

Check the whole TypeScript project — worksheets and solutions alike — for type errors without generating JavaScript files:

```powershell
pnpm exec tsc --noEmit
```

Ensure `tsconfig.json` includes the exercise directories and appropriate compiler options.

## Rust

Rust code is split across two Cargo workspaces:

- **Worksheets:** `exercises/rust/Cargo.toml` — blank stubs you fill in.
- **Solutions:** `solutions/rust/Cargo.toml` — completed, tested reference implementations.

Each exercise is a separate Cargo package containing its own `Cargo.toml` and `src/main.rs`, so each can be compiled, run, and tested independently. The two workspaces share the same package names, so the same `-p` flag works for either.

### Workspace configuration

Each workspace manifest uses an **explicit list of members**. For example, `exercises/rust/Cargo.toml` may contain:

```toml
[workspace]
resolver = "3"
members = [
    "easy/valid-brackets",
    "easy/two-sum",
]
```

Each entry corresponds to a package directory relative to that workspace's root. The package name used with Cargo is defined by the package's own `Cargo.toml`.

When a new exercise is created, its worksheet directory must be added to `exercises/rust/Cargo.toml`, and its solution directory (once written) to `solutions/rust/Cargo.toml`.

### Creating a new exercise

Create a Cargo package inside the appropriate difficulty directory of each workspace. For example:

```powershell
cargo new exercises/rust/easy/reverse-string
```

This generates a package similar to:

```text
exercises/rust/easy/reverse-string/
├── Cargo.toml
└── src/
    └── main.rs
```

Next, add the package path to `exercises/rust/Cargo.toml` (and, when you write the solution, to `solutions/rust/Cargo.toml`):

```toml
[workspace]
resolver = "3"
members = [
    "easy/valid-brackets",
    "easy/two-sum",
    "easy/reverse-string",
]
```

Keep the existing members in the list when adding a new one. Do not replace them with only the newest exercise.

### Running a worksheet or solution

From the repository root, run a Rust package by specifying the workspace manifest and package name:

```powershell
# Your worksheet (blank stub):
cargo run --manifest-path exercises/rust/Cargo.toml -p valid-brackets

# The reference solution:
cargo run --manifest-path solutions/rust/Cargo.toml -p valid-brackets
```

The `-p` argument identifies the package by the `name` field in that exercise's `Cargo.toml`.

### Other useful Cargo commands

Compile a package without running it, and run its tests:

```powershell
cargo check --manifest-path solutions/rust/Cargo.toml -p valid-brackets
cargo test  --manifest-path solutions/rust/Cargo.toml -p valid-brackets
```

Run the full test suite for either workspace:

```powershell
cargo test --manifest-path exercises/rust/Cargo.toml
cargo test --manifest-path solutions/rust/Cargo.toml
```

Check that Cargo can load a workspace:

```powershell
cargo metadata --manifest-path solutions/rust/Cargo.toml --no-deps
```

Replace `valid-brackets` with the relevant package name when working on a different exercise.

## Working with Exercises

A typical practice session follows this workflow:

1. Select an exercise from the [problems catalog](problems/README.md) appropriate to the desired difficulty.
2. Read the **Problem** section and identify the expected inputs, outputs, and constraints.
3. Implement a solution independently in the matching blank worksheet under `exercises/`.
4. Run your worksheet against representative examples and edge cases.
5. Compare your work against the reference solution in `solutions/` and the doc's **Solution** and **Syntax Explanation** sections.
6. Review correctness, readability, and time and space complexity, and record useful observations.

## Conventions

- Organize worksheets and solutions by language and difficulty.
- Use descriptive, consistent names across languages (snake_case for docs and TypeScript files, kebab-case for Rust packages).
- Prefer one self-contained TypeScript file per exercise.
- Use one Cargo package per Rust exercise.
- Keep `exercises/` (worksheets) and `solutions/` (reference) in sync: same names, same signatures.
- Run commands from the repository root.
- Keep `package.json`, lockfiles, Cargo manifests, and other project configuration files under version control.
- Exclude generated output and dependency directories such as `node_modules/`, `dist/`, and Rust's `target/` from version control.

## Future Expansion

PHP or other languages may be added in the future using a similar language-and-difficulty organization.
