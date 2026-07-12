# Source Code vs Bytecode vs Binary Code

## Example: `01_HelloWorld.js`

```js
console.log("Hello, World!");
```

---

## Comparison Table

| Aspect | Source Code | Bytecode | Binary Code (Machine Code) |
|--------|-------------|----------|----------------------------|
| **What it is** | Human-readable instructions written in a programming language | Intermediate representation between source code and machine code | Lowest-level instructions directly executed by the CPU |
| **Readability** | Readable by humans | Partially readable, mostly cryptic | Not readable by humans (raw 0s and 1s) |
| **Example with this code** | `console.log("Hello, World!");` | `0xL0AD_CONST "Hello, World!"`, `0xCALL console.log` (pseudo) | `10101000 00001111 ...` (CPU-specific) |
| **Who executes it** | Developers write it | Interpreter / Virtual Machine (e.g., V8, JVM, CPython) | The physical CPU directly |
| **Portability** | Portable across platforms | Portable if VM exists on target platform | **Not portable** — tied to a specific CPU architecture (x86, ARM, etc.) |
| **How this file runs** | You write this in a `.js` file | V8 (Node.js) parses JS → compiles to bytecode (Ignition interpreter) | Bytecode is further compiled (TurboFan JIT) into machine code for your CPU |
| **Speed** | Not executed directly | Faster than source, slower than binary | Fastest possible execution |
| **Examples by language** | `.js`, `.py`, `.java`, `.c`, `.ts` | `.class` (Java), `.pyc` (Python), V8 bytecode (JS) | `.exe`, `.o`, `.out` (compiled binaries) |

---

## How It Flows for This JavaScript File

```
Source Code (01_HelloWorld.js)
      │
      ▼
Parsing (Tokenizer → AST)
      │
      ▼
Ignition Interpreter generates Bytecode
      │
      ▼
(If hot code detected) TurboFan JIT compiles to Binary Code
      │
      ▼
CPU executes Binary Code natively
```

- **Source code**: `console.log("Hello, World!");` — you wrote this.
- **Bytecode**: After Node.js parses the file, V8's Ignition interpreter turns it into internal bytecode instructions (e.g., `LoadUndefined`, `CallRuntime`). This is an intermediate format V8 uses internally.
- **Binary code**: If that line runs often enough, V8's TurboFan JIT compiler converts the bytecode into native x86/ARM machine instructions that the CPU executes directly.

You can inspect the **bytecode** V8 generates by running:

```
node --print-bytecode 01_HelloWorld.js
```
