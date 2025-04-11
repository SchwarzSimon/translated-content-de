---
title: Ceil
slug: WebAssembly/Reference/Numeric/Ceil
l10n:
  sourceCommit: c0fc8c988385a0ce8ff63887f9a3263caf55a1f9
---

Die **`ceil`**-Anweisungen werden verwendet, um den Wert einer Zahl zu erhalten, die auf die nächste ganze Zahl aufgerundet wird.

{{InteractiveExample("Wat Demo: ceil", "tabbed-standard")}}

```wat interactive-example
(module
  (import "console" "log" (func $log (param f32)))
  (func $main

    f32.const 2.7 ;; load a number onto the stack
    f32.ceil ;; round up
    call $log ;; log the result

  )
  (start $main)
)
```

```js interactive-example
const url = "{%wasm-url%}";
await WebAssembly.instantiateStreaming(fetch(url), { console });
```

## Syntax

```wat
;; load a number onto the stack
f32.const 2.7

;; round up
f32.ceil

;; the top item on the stack will now be 3
```

| Anweisung  | Binärer Opcode |
| ---------- | -------------- |
| `f32.ceil` | `0x8d`         |
| `f64.ceil` | `0x9b`         |
