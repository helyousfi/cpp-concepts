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

**Example:** 
- parsing `int f(int a){ return a+1; }` → AST node `FunctionDecl(f)` with parameter and `ReturnStmt(BinaryOp(+, a, 1))`.
