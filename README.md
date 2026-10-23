# ajc-study_exercises

A collection of coding exercises for ongoing programming practice and interview preparation.

## Purpose

This repository serves as a staging area for practicing coding exercises, primarily generated with the assistance of LLMs.

The main practice languages are **TypeScript** and **Rust**, with **PHP** as a possible additional language.

Exercises are organized by difficulty:

- `easy/` — Fundamental programming concepts and straightforward problems.
- `medium/` — More involved algorithms, data structures, and problem-solving.
- `hard/` — Challenging algorithms and problems requiring more advanced reasoning.

The goal is to attempt each exercise independently, review alternative solutions, and improve programming skills over time.

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
│       ├── easy/
│       │   ├── two-sum/
│       │   │   ├── Cargo.toml
│       │   │   └── src/
│       │   │       └── main.rs
│       │   └── palindrome/
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

Each TypeScript exercise is a standalone `.ts` file. Each Rust exercise is a separate Cargo package managed through a workspace.

## Setup

### Prerequisites

- [Node.js](https://nodejs.org/)
- [pnpm](https://pnpm.io/)
- [Rust](https://www.rust-lang.org/tools/install), including Cargo

TypeScript dependencies should be managed from the repository root so that exercises can share the same tooling and configuration.

### TypeScript

Install the dependencies from the repository root:

```bash
pnpm install
```

The root project should have TypeScript, `tsx`, and the Node.js type definitions installed as development dependencies:

```bash
pnpm add -D typescript tsx @types/node
```

If `tsconfig.json` has not yet been created, initialize it from the root:

```bash
pnpm exec tsc --init
```

These initialization commands only need to be run when setting up the project, not for each new exercise.

#### Running an exercise

From the repository root, run an exercise using `tsx`:

```bash
pnpm exec tsx exercises/typescript/easy/two-sum.ts
```

Replace the path with the exercise you want to run.

#### Type-checking

Check the TypeScript project for type errors without generating JavaScript files:

```bash
pnpm exec tsc --noEmit
```

Ensure `tsconfig.json` includes the appropriate files and compiler options for the exercise directory structure.

### Rust

Rust exercises use Cargo packages managed through a workspace under `exercises/rust/`.

Each exercise should have its own directory containing a `Cargo.toml` and a `src/main.rs` file. This allows each solution to be compiled and run independently.

The workspace root at `exercises/rust/Cargo.toml` should declare the exercise packages as workspace members.

#### Running an exercise

From the repository root, run an exercise by specifying the workspace manifest and package name:

```bash
cargo run --manifest-path exercises/rust/Cargo.toml -p two-sum
```

Replace `two-sum` with the package name of the exercise you want to run.

#### Creating a new Rust exercise

Create each exercise as a Cargo package inside the appropriate difficulty directory. For example:

```bash
cargo new exercises/rust/easy/reverse-string
```

Then add the new package to the workspace members in `exercises/rust/Cargo.toml` if the workspace is configured with an explicit member list.

Run the exercise using its package name:

```bash
cargo run --manifest-path exercises/rust/Cargo.toml -p reverse-string
```

## Working with Exercises

A typical practice session follows this workflow:

1. Select an exercise appropriate to the desired difficulty.
2. Read the problem statement and identify the expected inputs, outputs, and constraints.
3. Implement your own solution before reviewing reference solutions.
4. Run the solution and test it against representative cases, including edge cases.
5. Review alternative implementations and consider their correctness, readability, and time and space complexity.
6. Record useful observations or improvements when appropriate.

Keep exercise filenames and Rust package names descriptive and consistent across languages. For example, use `two-sum.ts` for TypeScript and `two-sum` as the Rust package name.

## Conventions

- Keep exercises grouped by difficulty.
- Prefer one self-contained TypeScript file per exercise.
- Use a separate Cargo package for each Rust exercise.
- Run commands from the repository root unless otherwise specified.
- Track project manifests and lockfiles in version control.
- Keep generated output and dependency directories, such as `node_modules/`, `dist/`, and Rust's `target/`, out of version control.

## Future Expansion

PHP and other languages may be added later using a similar organization by language and difficulty.

