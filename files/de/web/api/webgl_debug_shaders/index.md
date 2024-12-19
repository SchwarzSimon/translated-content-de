---
title: WEBGL_debug_shaders-Erweiterung
short-title: WEBGL_debug_shaders
slug: Web/API/WEBGL_debug_shaders
l10n:
  sourceCommit: 44c4ec928281dc2d7c5ea42b7d2c74a2013f16ac
---

{{APIRef("WebGL")}}

Die **`WEBGL_debug_shaders`**-Erweiterung ist Teil der [WebGL API](/de/docs/Web/API/WebGL_API) und stellt eine Methode zur Verfügung, um Shader aus privilegierten Kontexten zu debuggen.

Diese Erweiterung ist nicht direkt für Webseiten verfügbar, da die Art und Weise, wie der Shader übersetzt wird, persönlich identifizierbare Informationen über die Art der Grafikkarte im Computer des Benutzers an die Webseite preisgeben könnte.

WebGL-Erweiterungen sind über die Methode [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension) verfügbar. Weitere Informationen finden Sie auch unter [Verwendung von Erweiterungen](/de/docs/Web/API/WebGL_API/Using_Extensions) im [WebGL-Tutorial](/de/docs/Web/API/WebGL_API/Tutorial).

> [!NOTE]
> Abhängig von den Datenschutzeinstellungen des Browsers könnte diese Erweiterung nur in privilegierten Kontexten verfügbar sein.
>
> Diese Erweiterung ist sowohl für [WebGL1](/de/docs/Web/API/WebGLRenderingContext) als auch [WebGL2](/de/docs/Web/API/WebGL2RenderingContext) Kontexte verfügbar.

## Instanzmethoden

- [`WEBGL_debug_shaders.getTranslatedShaderSource()`](/de/docs/Web/API/WEBGL_debug_shaders/getTranslatedShaderSource)
  - : Gibt den übersetzten Shader-Quelltext zurück.

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.getExtension()`](/de/docs/Web/API/WebGLRenderingContext/getExtension)
