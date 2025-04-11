---
title: Greater than
slug: WebAssembly/Reference/Numeric/Greater_than
l10n:
  sourceCommit: c0fc8c988385a0ce8ff63887f9a3263caf55a1f9
---

Die **`gt`**-Anweisungen, kurz für _greater than_ (größer als), prüfen, ob eine Zahl größer als eine andere Zahl ist. Wenn die erste Zahl größer als die zweite Zahl ist, wird `1` auf den Stack geschoben, andernfalls wird `0` auf den Stack geschoben.

Die Ganzzahl-Typen haben separate Greater-Than-Anweisungen für vorzeichenbehaftete (**`gt_s`**) und vorzeichenlose (**`gt_u`**) Zahlen.

{{InteractiveExample("Wat Demo: gt", "tabbed-taller")}}

```wat interactive-example
(module
  (import "env" "log_bool" (func $log_bool (param i32)))
  (func $main
    ;; load `10` and `2` onto the stack
    i32.const 10
    i32.const 2

    i32.gt_u ;; check if `10` is greater than '2'
    call $log_bool ;; log the result
  )
  (start $main)
)
```

```js interactive-example
const url = "{%wasm-url%}";

function log_bool(value) {
  console.log(Boolean(value));
  // Expected output: true
}

await WebAssembly.instantiateStreaming(fetch(url), {
  env: { log_bool },
});
```

## Syntax

```wat
;; load 2 numbers on to the stack
local.get $num
i32.const 2

;; check if $num is greater than '2'
i32.gt_u

;; if $num is greater than the `2`, `1` will be pushed on to the stack,
;; otherwise `0` will be pushed on to the stack.
```

| Anweisung  | Binärer Opcode |
| ---------- | -------------- |
| `i32.gt_s` | `0x4a`         |
| `i32.gt_u` | `0x4b`         |
| `i64.gt_s` | `0x55`         |
| `i64.gt_u` | `0x56`         |
| `f32.gt`   | `0x5e`         |
| `f64.gt`   | `0x64`         |
