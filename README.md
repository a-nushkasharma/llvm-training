#  LLVM Control Flow 

This project explores **Control Flow in LLVM IR**  involving branching, conditionals, loops, and CFG visualization. 
It demonstrates how C++ constructs like `if/else`, `for` loops, and `switch` statements are translated into LLVM Intermediate Representation (IR).

---

## 📁 Project Structure
```bash
llvm-training/
├── src/ # C++ source files
│ ├── condition.cpp # Contains 'check' function with if/else
│ ├── loop.cpp # Contains 'sum' function with loop
│ └── switch.cpp # Contains 'choose' function with switch
├── ir/ # LLVM IR output files
│ ├── condition.ll
│ ├── loop.ll
│ └── switch.ll
├── notes/ # Documentation deliverables
│ ├── control-flow.pdf # Final deliverable
├── loop_cfg.png # CFG diagram of the loop function
├── loop_cfg.dot # dot file for CFG diagram of the loop function
```
---
## Prerequisites

| Tool       | Purpose                                 |
|------------|------------------------------------------|
| `clang++`  | Compile C++ to LLVM IR                   |
| `opt`      | LLVM optimizer to extract CFG            |
| `llvm-dis` | Disassembler (optional)                  |
| `dot`      | From Graphviz, for CFG visualization     |

Make sure these are installed and available in your terminal:

```bash
clang++ --version
opt --version
dot -V
```
---
## Implementation

1. Compile C++ to LLVM IR (no optimization)
  ```bash
clang++ -O0 -S -emit-llvm src/condition.cpp -o ir/condition.ll
clang++ -O0 -S -emit-llvm src/loop.cpp -o ir/loop.ll
clang++ -O0 -S -emit-llvm src/switch.cpp -o ir/switch.ll
```
2. Analyze IR Files
 -Open .ll files in your preferred editor and observe:
* icmp → comparisons
* br → conditional/unconditional branches
* phi → value selection across control flow (seen with optimization)
* switch → for direct integer dispatch

3. Generate Control Flow Graph
  ```bash
cd ir/
opt -dot-cfg loop.ll
dot -Tpng cfg.?sum@@YAHH@Z.dot -o ../notes/loop_cfg.png
```
---
## 📋 Task Summary

| Part         | Task Description                                             | C++ File         | LLVM Concept Focused On          |
|--------------|--------------------------------------------------------------|------------------|----------------------------------|
| Part 1       | Conditional branching using `if (x > 5)`                     | `condition.cpp`  | `icmp`, `br`, basic blocks       |
| Part 2       | Loop using `for (int i = 0; i < n; ++i)`                     | `loop.cpp`       | Loop entry, `phi`, control flow  |
| Part 3       | Generate Control Flow Graph (CFG) from loop function         | `loop.ll`        | `opt -dot-cfg`, Graphviz         |
| Bonus Task   | Analyze `switch (x)` and how it compiles in LLVM IR          | `switch.cpp`     | `switch` instruction, jump table |

