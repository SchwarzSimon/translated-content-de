---
title: EXT_color_buffer_half_float Erweiterung
short-title: EXT_color_buffer_half_float
slug: Web/API/EXT_color_buffer_half_float
l10n:
  sourceCommit: d8f04d843dd81ab8cea1cfc0577ae3c5c9b77d5c
---

{{APIRef("WebGL")}}

Die **`EXT_color_buffer_half_float`** Erweiterung ist Teil der [WebGL API](/de/docs/Web/API/WebGL_API) und fügt die Fähigkeit hinzu, in 16-Bit-Floating-Point-Farbpuffern zu rendern.

WebGL-Erweiterungen sind über die Methode [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension) verfügbar. Für weitere Informationen siehe auch [Erweiterungen nutzen](/de/docs/Web/API/WebGL_API/Using_Extensions) im [WebGL-Tutorial](/de/docs/Web/API/WebGL_API/Tutorial).

> [!NOTE]
> Diese Erweiterung ist sowohl für [WebGL1](/de/docs/Web/API/WebGLRenderingContext) als auch für [WebGL2](/de/docs/Web/API/WebGL2RenderingContext) Kontexte verfügbar. In WebGL 2 ist sie eine Alternative zur Verwendung der [`EXT_color_buffer_float`](/de/docs/Web/API/EXT_color_buffer_float) Erweiterung auf Plattformen, die 16-Bit-Floating-Point-Render-Ziele unterstützen, aber nicht 32-Bit-Floating-Point-Render-Ziele.
>
> Die [`OES_texture_half_float`](/de/docs/Web/API/OES_texture_half_float) Erweiterung aktiviert diese Erweiterung implizit.

## Konstanten

- `ext.RGBA16F_EXT`
  - : RGBA 16-Bit-Floating-Point-Farb-Renderformat.
- `ext.RGB16F_EXT`
  - : RGB 16-Bit-Floating-Point-Farb-Renderformat.
- `ext.FRAMEBUFFER_ATTACHMENT_COMPONENT_TYPE_EXT`
  - : ?
- `ext.UNSIGNED_NORMALIZED_EXT`
  - : ?

## Erweiterte Methoden

Diese Erweiterung erweitert [`WebGLRenderingContext.renderbufferStorage()`](/de/docs/Web/API/WebGLRenderingContext/renderbufferStorage):

- Der `internalformat` Parameter akzeptiert nun `ext.RGBA16F_EXT` und `ext.RGBA16F_EXT`.

## Beispiele

```js
const ext = gl.getExtension("EXT_color_buffer_half_float");

gl.renderbufferStorage(gl.RENDERBUFFER, ext.RGBA16F_EXT, 256, 256);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension)
- [`WebGLRenderingContext.renderbufferStorage()`](/de/docs/Web/API/WebGLRenderingContext/renderbufferStorage)
- [`OES_texture_half_float`](/de/docs/Web/API/OES_texture_half_float)
