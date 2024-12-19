---
title: EXT_texture_compression_bptc Erweiterung
short-title: EXT_texture_compression_bptc
slug: Web/API/EXT_texture_compression_bptc
l10n:
  sourceCommit: 0c3f18aca2c8a93d3982183f64bf7762c2c310b0
---

{{APIRef("WebGL")}}

Die `EXT_texture_compression_bptc`-Erweiterung ist Teil der [WebGL API](/de/docs/Web/API/WebGL_API) und stellt 4 BPTC-komprimierte Texturformate bereit. Diese Kompressionsformate werden in [Microsofts DirectX API](https://learn.microsoft.com/en-us/windows/win32/direct3d11/texture-block-compression-in-direct3d-11) als [BC7](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc7-format) und [BC6H](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc6h-format) bezeichnet.

WebGL-Erweiterungen sind mittels der Methode [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension) verfügbar. Weitere Informationen finden Sie unter [Erweiterungen verwenden](/de/docs/Web/API/WebGL_API/Using_Extensions) im [WebGL-Leitfaden](/de/docs/Web/API/WebGL_API/Tutorial).

> [!NOTE]
> Die Unterstützung hängt vom Grafiktreiber des Systems ab. Es gibt keine Unterstützung unter Windows.
>
> Diese Erweiterung ist sowohl für [WebGL1](/de/docs/Web/API/WebGLRenderingContext)- als auch [WebGL2](/de/docs/Web/API/WebGL2RenderingContext)-Kontexte verfügbar.

## Konstanten

Die komprimierten Texturformate werden durch 4 Konstanten bereitgestellt und können in zwei Funktionen verwendet werden: [`compressedTexImage2D()`](/de/docs/Web/API/WebGLRenderingContext/compressedTexImage2D) und [`compressedTexSubImage2D()`](/de/docs/Web/API/WebGLRenderingContext/compressedTexSubImage2D).

- `ext.COMPRESSED_RGBA_BPTC_UNORM_EXT`
  - : Komprimiert 8-Bit-Festwertdaten. Jeder 4x4-Block von Texeln besteht aus 128 Bits von RGBA- oder Bilddaten. Siehe auch [BC7-Format](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc7-format).
- `ext.COMPRESSED_SRGB_ALPHA_BPTC_UNORM_EXT`
  - : Komprimiert 8-Bit-Festwertdaten. Jeder 4x4-Block von Texeln besteht aus 128 Bits von SRGB_ALPHA- oder Bilddaten. Siehe auch [BC7-Format](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc7-format).
- `ext.COMPRESSED_RGB_BPTC_SIGNED_FLOAT_EXT`
  - : Komprimiert hochdynamische Bereichswerte mit Vorzeichen und Gleitkommazahlen. Jeder 4x4-Block von Texeln besteht aus 128 Bits von RGB-Daten. Es enthält nur RGB-Daten, sodass der zurückgegebene Alphawert 1.0 ist. Siehe auch [BC6H-Format](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc6h-format).
- `ext.COMPRESSED_RGB_BPTC_UNSIGNED_FLOAT_EXT`
  - : Komprimiert hochdynamische Bereichswerte ohne Vorzeichen und Gleitkommazahlen. Jeder 4x4-Block von Texeln besteht aus 128 Bits von RGB-Daten. Es enthält nur RGB-Daten, sodass der zurückgegebene Alphawert 1.0 ist. Siehe auch [BC6H-Format](https://learn.microsoft.com/en-us/windows/win32/direct3d11/bc6h-format).

## Beispiele

```js
const ext = gl.getExtension("EXT_texture_compression_bptc");

const texture = gl.createTexture();
gl.bindTexture(gl.TEXTURE_2D, texture);

gl.compressedTexImage2D(
  gl.TEXTURE_2D,
  0,
  ext.COMPRESSED_RGBA_BPTC_UNORM_EXT,
  128,
  128,
  0,
  textureData,
);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension)
- [`WebGLRenderingContext.compressedTexImage2D()`](/de/docs/Web/API/WebGLRenderingContext/compressedTexImage2D)
- [`WebGLRenderingContext.compressedTexSubImage2D()`](/de/docs/Web/API/WebGLRenderingContext/compressedTexSubImage2D)
- [`WebGLRenderingContext.getParameter()`](/de/docs/Web/API/WebGLRenderingContext/getParameter)
