---
title: OES_texture_half_float_linear Erweiterung
short-title: OES_texture_half_float_linear
slug: Web/API/OES_texture_half_float_linear
l10n:
  sourceCommit: aa8fa82a902746b0bd97839180fc2b5397088140
---

{{APIRef("WebGL")}}

Die **`OES_texture_half_float_linear`** Erweiterung ist Teil der [WebGL API](/de/docs/Web/API/WebGL_API) und ermöglicht lineares Filtern mit halb gleitenden Pixeltypen für Texturen.

WebGL-Erweiterungen sind über die Methode [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension) verfügbar. Für weitere Informationen siehe [Verwendung von Erweiterungen](/de/docs/Web/API/WebGL_API/Using_Extensions) im [WebGL Leitfaden](/de/docs/Web/API/WebGL_API/Tutorial).

> [!NOTE]
> Diese Erweiterung ist nur für [WebGL1](/de/docs/Web/API/WebGLRenderingContext) Kontexte verfügbar. In [WebGL2](/de/docs/Web/API/WebGL2RenderingContext) ist die Funktionalität dieser Erweiterung standardmäßig im WebGL2-Kontext verfügbar und die Erweiterung wird nicht benötigt.

## Lineares Filtern

Die [`OES_texture_half_float`](/de/docs/Web/API/OES_texture_half_float) Erweiterung allein erlaubt kein lineares Filtern mit halb gleitenden Texturen. Diese Erweiterung aktiviert diese Fähigkeit.

Mit Hilfe dieser Erweiterung können Sie nun den Vergrößerungs- oder Verkleinerungsfilter in der Methode [`WebGLRenderingContext.texParameter()`](/de/docs/Web/API/WebGLRenderingContext/texParameter) auf einen der Werte `gl.LINEAR`, `gl.LINEAR_MIPMAP_NEAREST`, `gl.NEAREST_MIPMAP_LINEAR` oder `gl.LINEAR_MIPMAP_LINEAR` setzen und halb gleitende Texturen verwenden.

## Beispiele

```js
const halfFloat = gl.getExtension("OES_texture_half_float");
gl.getExtension("OES_texture_half_float_linear");

const texture = gl.createTexture();
gl.bindTexture(gl.TEXTURE_2D, texture);

gl.texParameterf(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
gl.texImage2D(
  gl.TEXTURE_2D,
  0,
  gl.RGBA,
  gl.RGBA,
  halfFloat.HALF_FLOAT_OES,
  image,
);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension)
- [`WebGLRenderingContext.texImage2D()`](/de/docs/Web/API/WebGLRenderingContext/texImage2D)
- [`WebGLRenderingContext.texSubImage2D()`](/de/docs/Web/API/WebGLRenderingContext/texSubImage2D)
- [`OES_texture_float`](/de/docs/Web/API/OES_texture_float)
- [`OES_texture_float_linear`](/de/docs/Web/API/OES_texture_float_linear)
- [`OES_texture_half_float`](/de/docs/Web/API/OES_texture_half_float)
