---
title: EXT_texture_filter_anisotropic-Erweiterung
short-title: EXT_texture_filter_anisotropic
slug: Web/API/EXT_texture_filter_anisotropic
l10n:
  sourceCommit: d8f04d843dd81ab8cea1cfc0577ae3c5c9b77d5c
---

{{APIRef("WebGL")}}

Die **`EXT_texture_filter_anisotropic`**-Erweiterung ist Teil der [WebGL API](/de/docs/Web/API/WebGL_API) und stellt zwei Konstanten für das [anisotrope Filter (AF)](https://en.wikipedia.org/wiki/Anisotropic_filtering) bereit.

AF verbessert die Qualität des Zugriffs auf mipmap-texturierte Elemente, wenn ein Texturprimitiv aus einem schrägen Winkel betrachtet wird. Bei Verwendung von nur Mipmapping neigen diese Abfragen dazu, zu einem grauen Durchschnitt zu werden.

WebGL-Erweiterungen sind über die Methode [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension) verfügbar. Weitere Informationen finden Sie auch unter [Verwendung von Erweiterungen](/de/docs/Web/API/WebGL_API/Using_Extensions) im [WebGL-Leitfaden](/de/docs/Web/API/WebGL_API/Tutorial).

> [!NOTE]
> Diese Erweiterung ist sowohl für [WebGL1](/de/docs/Web/API/WebGLRenderingContext)- als auch [WebGL2](/de/docs/Web/API/WebGL2RenderingContext)-Kontexte verfügbar.

## Konstanten

- `ext.MAX_TEXTURE_MAX_ANISOTROPY_EXT`
  - : Dies ist das `pname`-Argument für den Aufruf von [`gl.getParameter()`](/de/docs/Web/API/WebGLRenderingContext/getParameter) und gibt die maximale verfügbare Anisotropie zurück.
- `ext.TEXTURE_MAX_ANISOTROPY_EXT`
  - : Dies ist das `pname`-Argument für die Aufrufe von [`gl.getTexParameter()`](/de/docs/Web/API/WebGLRenderingContext/getTexParameter) und [`gl.texParameterf()`](/de/docs/Web/API/WebGLRenderingContext/texParameter) / [`gl.texParameteri()`](/de/docs/Web/API/WebGLRenderingContext/texParameter) und setzt die gewünschte maximale Anisotropie für eine Textur fest.

## Beispiele

```js
const texture = gl.createTexture();
gl.bindTexture(gl.TEXTURE_2D, texture);
const ext =
  gl.getExtension("EXT_texture_filter_anisotropic") ||
  gl.getExtension("MOZ_EXT_texture_filter_anisotropic") ||
  gl.getExtension("WEBKIT_EXT_texture_filter_anisotropic");
if (ext) {
  const max = gl.getParameter(ext.MAX_TEXTURE_MAX_ANISOTROPY_EXT);
  gl.texParameterf(gl.TEXTURE_2D, ext.TEXTURE_MAX_ANISOTROPY_EXT, max);
}
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension)
