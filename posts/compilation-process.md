# Big picture (one-line)
Source code → preprocessing → lexing/tokenizing → parsing → semantic analysis & type checking → IR generation → optimizations → code generation (assembly) → assembler (.o) → linker → executable (→ loader/runtime).

# Preprocessing
**What it does :**
- Handles `#include`, `#define macros`, conditional compilation `#if/#ifdef`.
- Produces a translation unit (single big source text) fed to the lexer.
```bash
gcc -E main.c -o main.i   # or g++ -E for C++
```

# Lexical analysis (tokenization)
**What it does :**
- Converts preprocessed source characters into tokens: identifiers, keywords, literals, operators, punctuators.
- Detects simple lexing errors (unterminated string, invalid numeric literal).

**Example:**
- Source: `int x = 42;`
- Tokens: `int identifier(x) = numeric-literal(42) ;`

# Parsing → AST (Abstract Syntax Tree)
**What it does :**
- Consumes tokens according to grammar, produces a parse tree / AST.
- In C++ this is complex (templates, elaborate grammar, ambiguity resolution).

**Example :** 
- parsing `int f(int a){ return a+1; }` → AST node `FunctionDecl(f)` with parameter and `ReturnStmt(BinaryOp(+, a, 1))`.

# Semantic analysis & name resolution
**What it does :**
- Builds symbol table, resolves identifiers to declarations, performs type checking, checks scoping rules.
- In C++: overload resolution, template instantiation, name mangling, conversion rules, access control (private/protected), ADL (argument-dependent lookup).
- Reports errors/warnings.

**Examples of semantic checks :**
- Type mismatch: `int x = "hello"`; → error.
- Use-before-declaration when not allowed.
- For C++: choose which overload of `f()` to call; instantiate template `vector<int>`.

# Intermediate representation (IR) generation / translation
**What it does :**
- Translates AST into an intermediate form that’s easier for analyses and optimizations.
- Classic compilers: generate an IR per function (e.g., LLVM IR, GCC GIMPLE/RTL).

**Why IR?**
- Easier to implement language-independent optimizations.
- IR often uses a form like three-address code or SSA (Static Single Assignment).
- Simple IR example (pseudo-IR) for int add(int a,int b){return a+b;}:
```bash
t1 = a + b
return t1
```
