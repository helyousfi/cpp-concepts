# Big picture (one-line)
Source code → preprocessing → lexing/tokenizing → parsing → semantic analysis & type checking → IR generation → optimizations → code generation (assembly) → assembler (.o) → linker → executable (→ loader/runtime).

# Preprocessing
What it does :
- Handles `#include`, `#define macros`, conditional compilation `#if/#ifdef`.
- Produces a translation unit (single big source text) fed to the lexer.
```bash
gcc -E main.c -o main.i   # or g++ -E for C++
```
# Lexical analysis (tokenization)
