---
title: Left rotate
slug: WebAssembly/Reference/Numeric/Left_rotate
l10n:
  sourceCommit: df9d06402163f77fc3e2d327ab63f9dd4af15b38
---

Die **`rotl`**-Anweisungen, kurz für _rotate-left_, werden verwendet, um eine bitweise Linksdrehung durchzuführen.

{{EmbedInteractiveExample("pages/wat/rotl.html", "tabbed-taller")}}

## Syntax

```wasm
;; load two numbers onto the stack
i32.const 3758096384 ;; 11100000_00000000_00000000_00000000
i32.const 1          ;; left rotate one spot

;; perform a bitwise left-rotate
i32.rotl

;; the top item on the stack will now be 3221225473
;; (11000000_00000000_00000000_00000001)
```

| Anweisung  | Binärer Opcode |
| ---------- | -------------- |
| `i32.rotl` | `0x77`         |
| `i64.rotl` | `0x89`         |
