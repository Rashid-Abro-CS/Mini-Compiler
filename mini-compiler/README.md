# Mini Compiler

Interactive, step-by-step compiler visualizer for C, C++, Java and Python (subset).
Everything runs in the browser: no install, no backend.

## Run in VS Code

1. Unzip and open the folder in VS Code (File > Open Folder).
2. Install the **Live Server** extension (Ritwick Dey).
3. Right-click `index.html` > **Open with Live Server**.
   (Double-clicking `index.html` to open it in a browser also works.)

Internet is only needed for the Sora / JetBrains Mono fonts; the app falls back to system fonts offline.

## What is implemented

- Lexer with character-by-character scan events, token classification
- Recursive-descent parser producing a parse tree and an AST, with grammar-rule events
- Semantic analysis: scopes, type checks, undeclared / redeclared / mismatch errors, warnings
- Symbol table with insert, lookup and update events (type, scope, value, bytes@offset, line)
- Three-Address Code generation with temporaries and labels
- Optimizer: constant propagation, constant folding, copy elimination, dead-code elimination
- Event-driven playback: play, pause, step forward/back, replay, speed, timeline slider
  (keyboard: Space, Left, Right). Every view is rebuilt from stored events, so stepping back restores state.
- `.msa` project files (JSON): save, open, validation, recent projects (localStorage)
- Export report, sample library, error examples, My Code / Sample Learning modes

## Supported language subset

Statement sequences only: declarations, assignments, `if`/`else`, `while`, print calls
(`printf`, `cout <<`, `System.out.println`, `print`). No functions, classes or `main` wrapper yet.

## `.msa` format

```json
{
  "format": "msa",
  "version": 1,
  "name": "Untitled",
  "language": "c | cpp | java | py",
  "source": "...",
  "settings": { "mode": "my", "speed": 1 },
  "saved": "ISO timestamp",
  "result": { "status": "success | failed", "tac": [], "optimized": [], "stats": {} }
}
```

## Code layout (index.html, one script block)

`lex` > `parse` > `sema` > `gen` > `optimize` > `compile` (emits events) > UI renderers (`center`, `right`, `upd`).
Not yet done: Monaco editor, React/FastAPI split, SQLite, multi-language comparison.
