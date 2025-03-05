---
title: Linksschiebung
slug: WebAssembly/Reference/Numeric/Left_shift
l10n:
  sourceCommit: 5af6da1da593fae9b3208eb9fd308213d5c3359c
---

Die **`shl`**-Instruktionen, abgekürzt für _shift-left_, werden verwendet, um eine bitweise Linksschiebung durchzuführen, ähnlich dem **`<<`**-Operator in anderen Sprachen.

{{InteractiveExample("Wat Demo: shl", "tabbed-taller")}}

```wat interactive-example
(module

  (func (export "shift_left") (param $num i32) (param $by i32) (result i32)
    ;; load the number to shift and the by how many spots
    local.get $num
    local.get $by

    ;; shift and return the result
    i32.shl
  )

)
```

```js interactive-example
const url = "{%wasm-url%}";
await WebAssembly.instantiateStreaming(fetch(url), { console }).then(
  (result) => {
    const shift_left = result.instance.exports.shift_left;

    const res = shift_left(0b11100000_00000000_00000000_00000000, 1);
    console.log(numToBin(res));
    // Expected output: "11000000_00000000_00000000_00000000"
  },
);

function numToBin(num) {
  return (num >>> 0)
    .toString(2)
    .padStart(32, "0")
    .match(/.{1,8}/g)
    .join("_");
}
```

## Syntax

```wasm
;; load two numbers onto the stack
i32.const 7   ;; 00000111
i32.const 1   ;; left shift one spot

;; perform a bitwise left-shift
i32.shl

;; the top item on the stack will now be 14 (00001110)
```

| Instruktion | Binäroperand |
| ----------- | ------------ |
| `i32.shl`   | `0x74`       |
| `i64.shl`   | `0x86`       |
