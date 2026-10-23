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
├── exercises/
│   ├── typescript/
│   │   ├── easy/
│   │   │   ├── two-sum.ts
│   │   │   └── palindrome.ts
│   │   ├── medium/
│   │   └── hard/
│   └── rust/
│       ├── Cargo.toml
│       ├── Cargo.lock
│       ├── easy/
│       │   ├── valid-brackets/
│       │   │   ├── Cargo.toml
│       │   │   └── src/
│       │   │       └── main.rs
│       │   └── two-sum/
│       │       ├── Cargo.toml
│       │       └── src/
│       │           └── main.rs
│       ├── medium/
│       └── hard/
├── package.json
├── pnpm-lock.yaml
├── pnpm-workspace.yaml
├── tsconfig.json
├── .gitignore
└── README.md
```

Each TypeScript exercise is a standalone `.ts` file. Each Rust exercise is an independent Cargo package registered in the Rust workspace.

The directory tree above is illustrative; it will grow as exercises are added.

## Prerequisites

Install the following tools:

- [Node.js](https://nodejs.org/)
- [pnpm](https://pnpm.io/)
- [Rust and Cargo](https://www.rust-lang.org/tools/install)

Run commands from the repository root unless otherwise specified.

## TypeScript

TypeScript dependencies and configuration are managed from the repository root. Individual exercises do not need their own `package.json` or TypeScript installation.

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

### Running an exercise

Run a TypeScript exercise using `tsx` from the repository root:

```powershell
pnpm exec tsx exercises/typescript/easy/two-sum.ts
```

Replace the path with the exercise you want to run.

### Type-checking

Check the TypeScript project for type errors without generating JavaScript files:

```powershell
pnpm exec tsc --noEmit
```

Ensure `tsconfig.json` includes the exercise directories and appropriate compiler options.

## Rust

Rust exercises are managed through a Cargo workspace rooted at `exercises/rust/Cargo.toml`.

Each exercise is a separate Cargo package containing its own `Cargo.toml` and `src/main.rs`. This allows each solution to be compiled, run, and tested independently.

### Workspace configuration

The workspace manifest uses an **explicit list of members**. For example, `exercises/rust/Cargo.toml` may contain:

```toml
[workspace]
resolver = "3"
members = [
    "easy/valid-brackets",
    "easy/two-sum",
]
```

Each entry corresponds to a package directory relative to `exercises/rust/`. The package name used with Cargo is defined by the package's own `Cargo.toml`.

When a new exercise is created, its directory must be added to the workspace's `members` list.

### Creating a new exercise

Create a Cargo package inside the appropriate difficulty directory. For example:

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

Next, add the package path to `exercises/rust/Cargo.toml`:

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

### Running an exercise

From the repository root, run a Rust exercise by specifying the workspace manifest and package name:

```powershell
cargo run --manifest-path exercises/rust/Cargo.toml -p valid-brackets
```

The `-p` argument identifies the package by the `name` field in that exercise's `Cargo.toml`.

For example, to run the `reverse-string` package:

```powershell
cargo run --manifest-path exercises/rust/Cargo.toml -p reverse-string
```

### Other useful Cargo commands

Compile an exercise without running it:

```powershell
cargo check --manifest-path exercises/rust/Cargo.toml -p valid-brackets
```

Run its tests:

```powershell
cargo test --manifest-path exercises/rust/Cargo.toml -p valid-brackets
```

Check that Cargo can load the workspace:

```powershell
cargo metadata --manifest-path exercises/rust/Cargo.toml --no-deps
```

Replace `valid-brackets` with the relevant package name when working on a different exercise.

## Working with Exercises

A typical practice session follows this workflow:

1. Select an exercise appropriate to the desired difficulty.
2. Read the problem statement and identify the expected inputs, outputs, and constraints.
3. Implement a solution independently before reviewing reference implementations.
4. Run the solution against representative examples and edge cases.
5. Review alternative solutions for correctness, readability, and time and space complexity.
6. Record useful observations or improvements when appropriate.

## Conventions

- Organize exercises by language and difficulty.
- Use descriptive, consistent names across languages.
- Prefer one self-contained TypeScript file per exercise.
- Use one Cargo package per Rust exercise.
- Run commands from the repository root.
- Keep `package.json`, lockfiles, Cargo manifests, and other project configuration files under version control.
- Exclude generated output and dependency directories such as `node_modules/`, `dist/`, and Rust's `target/` from version control.

## Future Expansion

PHP or other languages may be added in the future using a similar language-and-difficulty organization.

