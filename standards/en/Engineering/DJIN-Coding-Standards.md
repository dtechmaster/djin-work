# DJIN Tech — Coding Standards

> Clear structure. Functional paradigm. Simplicity through functions. Zod at the core. Human readable.

---

## Code Style

### Composition API & TypeScript Only

* Use `<script setup lang="ts">`
* Don't mix Options API unless explicitly justified.

### Function Declarations

* ❌ Avoid anonymous functions: `const x = () => {}`
* ✅ Use named functions: `function x() {}`

### #region Blocks

* Use `// #region` and `// #endregion` consistently
* Works in `.ts`, `.vue`, and template blocks

```vue
<template>
  <!--#region Feature A -->
  <div>{{ sayHello() }}</div>
  <!--#endregion Feature A -->
</template>

<script setup lang="ts">
//#region Imports
import nuxt from 'nuxt'
//#endregion

//#region Feature A
const greeting = 'Hello World!'
function say(str: string) { return str }
function sayHello() { return say(greeting) }
//#endregion
</script>
```

> 💡 VS Code: `[CTRL+K CTRL+8]` to collapse all regions

### Logger Use

* Create a `Logger` class composable to handle logging if not exists
* Loggers should always have `log`, `info`, `warn`, `error` methods
* Logs should be human-readable like `[INFO][YYYY-MM-DD HH:MM:SS][File:Line] Message`
* Replace all `console.log` with `Logger.log`

---

### Nullable Programming

* Assume all values can be null or undefined — especially nested ones
  → Trust nothing, not even your own code.
* Use optional chaining (`?.`) consistently to avoid runtime errors
  → `user?.profile?.address?.street`
* Provide fallback values using nullish coalescing (`??`) or default factories
  → `const name = user?.profile?.name ?? 'ゲスト'`
* Never throw exceptions in the UI — instead:

  * Use `v-if`, `v-else`, or skeleton/loading components
  * Disable buttons or inputs when data is missing
  * Show clear validation or warning messages
* Prefer defensive computed properties over optimistic ones
  → Wrap in safe fallbacks or try/catch guards where needed
* Avoid deeply trusting types, even in TypeScript — structure can still be broken at runtime (e.g., from API or localStorage)

---

## Architecture Patterns

### Black Box Paradigm

* Avoid global state or class-like structures unless absolutely necessary
* Prefer composition over class-based logic
* Everything is a function, object, component, or composable. No class inheritance
* Avoid global state or class-like structures unless absolutely necessary

### Utility Structure

Organize general-purpose logic into `utils/`:

* `arrays.ts`
* `objects.ts`
* `japanese.ts`
* etc.

Check before implementing new utilities to avoid duplication.

### Composables

Avoid the `useX()` convention. Use global `$`-prefixed composables:

```ts
export default const $myComposable = {
  foo() {
    return 'bar'
  }
} as const
```

* Must be declared as default-exported `const`
* Must start with `$`

---

## Zod as SST (Single Source of Truth)

### Principle

Zod defines every interface in the system:

* Validation
* Types
* Props
* Shape-based logic

### Types of Interfaces

| Type     | Use Case                                     | Example                   |
|----------|----------------------------------------------|---------------------------|
| System   | Pages, components, composables               | `z.system.pageSchema`     |
| Database | PostgreSQL structure, validation, migrations | `z.database.userSchema`   |

### Benefits

* Extract types and props from same schema
* Central place for consistent logic
* Eliminates interface duplication
* Can construct database structure from system interfaces and apply Steve Jobs' philosophy (`"Start development from the user perspective only then we develop the technology"`)

Store shared schemas in a globally accessible folder and reuse them across all layers.

### File Sizes

* We should keep files concise, small, and focused. If a file is too large, it should be split into smaller files. `Ideally`, each file should have a single purpose and less than 2000 lines. `Ideally`.

### Naming Conventions

* Use `I` for interfaces, `T` for types, and `P` for props
* Use `camelCase` for interfaces, types, and props
* Use `snake_case` for database columns, tables, and migrations
* Use `snake_case` for environment variables and config files
* Use `ENV_` prefix for environment variables and `CONFIG_` prefix for config files

---

## Execution Principles

> Planning always before coding
> "First, solve the problem. Then, write the code." — John Johnson
> "Bad programmers worry about code. Good programmers worry about data structures and their relationships." — Linus Torvalds

## CLI

* Always use Deno for CLI
* Use Deno's `npm specifiers` for CLI so we can avoid dependency management issues (https://deno.com/blog/not-using-npm-specifiers-doing-it-wrong)

## Testing

* **Always write tests** for CLI tools, utilities, and core functionality when they are concise and make sense
* Tests should be simple, focused, and cover the main use cases
* Use Deno's built-in testing framework with `Deno.test()`
* **Test Organization**:
  - Create a `tests/` folder in the project root
  - Test files should be named `*.test.ts` and placed in the `tests/` folder
  - Mirror the source structure: `src/foo.ts` → `tests/foo.test.ts`
  - For CLI projects, main tests go in `tests/main.test.ts`
* Focus on testing:
  - CLI argument parsing and validation
  - Error handling and edge cases
  - Environment variable loading
  - Core business logic functions
* Keep tests maintainable - if a test becomes complex, consider refactoring the code being tested
* Tests should be fast and independent - no external dependencies or file system modifications when possible

---

## Other Resources

* use `./DJIN-standards.md` for reference
* use `./SYSTEM_SPECS.md` for reference
* use `./EXECUTION_PLAN.md` for reference
