---
title: "WebGLRenderingContext: getTexParameter()-Methode"
short-title: getTexParameter()
slug: Web/API/WebGLRenderingContext/getTexParameter
l10n:
  sourceCommit: 2b942f0d8f84641c233d701cb5d1f4e6c23120ff
---

{{APIRef("WebGL")}}{{AvailableInWorkers}}

Die **`WebGLRenderingContext.getTexParameter()`**-Methode der [WebGL-API](/de/docs/Web/API/WebGL_API) gibt Informationen über die angegebene Textur zurück.

## Syntax

```js-nolint
getTexParameter(target, pname)
```

### Parameter

- `target`

  - : Ein [`GLenum`](/de/docs/Web/API/WebGL_API/Types), das den Bindungspunkt (target) angibt. Mögliche Werte:

    - `gl.TEXTURE_2D`: Eine zweidimensionale Textur.
    - `gl.TEXTURE_CUBE_MAP`: Eine Würfelmappen-Textur.

    Bei Verwendung eines [WebGL 2-Kontexts](/de/docs/Web/API/WebGL2RenderingContext), sind zusätzlich die folgenden Werte verfügbar:

    - `gl.TEXTURE_3D`: Eine dreidimensionale Textur.
    - `gl.TEXTURE_2D_ARRAY`: Eine zweidimensionale Array-Textur.

- `pname`

  - : Ein [`GLenum`](/de/docs/Web/API/WebGL_API/Types), das die abzufragenden Informationen angibt. Mögliche Werte:

    <table class="standard-table">
      <thead>
        <tr>
          <th scope="col">pname</th>
          <th scope="col">Rückgabewerttyp</th>
          <th scope="col">Beschreibung</th>
          <th scope="col">Mögliche Rückgabewerte</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th colspan="4">Verfügbar in einem WebGL 1-Kontext</th>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_MAG_FILTER</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Texturvergrößerungsfilter</td>
          <td><code>gl.LINEAR</code> (Standardwert), <code>gl.NEAREST</code>.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_MIN_FILTER</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Texturverkleinerungsfilter</td>
          <td>
            <code>gl.LINEAR</code>, <code>gl.NEAREST</code>,
            <code>gl.NEAREST_MIPMAP_NEAREST</code>,
            <code>gl.LINEAR_MIPMAP_NEAREST</code>,
            <code>gl.NEAREST_MIPMAP_LINEAR</code> (Standardwert),
            <code>gl.LINEAR_MIPMAP_LINEAR</code>.
          </td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_WRAP_S</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Wickelfunktion für Texturkoordinate <code>s</code></td>
          <td>
            <code>gl.REPEAT</code> (Standardwert), <code>gl.CLAMP_TO_EDGE</code>,
            <code>gl.MIRRORED_REPEAT</code>.
          </td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_WRAP_T</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Wickelfunktion für Texturkoordinate <code>t</code></td>
          <td>
            <code>gl.REPEAT</code> (Standardwert), <code>gl.CLAMP_TO_EDGE</code>,
            <code>gl.MIRRORED_REPEAT</code>.
          </td>
        </tr>
        <tr>
          <th colspan="4">
            Zusätzlich verfügbar bei Verwendung der
            [`EXT_texture_filter_anisotropic`](/de/docs/Web/API/EXT_texture_filter_anisotropic)-Erweiterung
          </th>
        </tr>
        <tr>
          <td><code>ext.TEXTURE_MAX_ANISOTROPY_EXT</code></td>
          <td>[`GLfloat`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Maximale Anisotropie für eine Textur</td>
          <td>Beliebige Float-Werte.</td>
        </tr>
        <tr>
          <th colspan="4">Zusätzlich verfügbar bei Nutzung eines WebGL 2-Kontexts</th>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_BASE_LEVEL</code></td>
          <td>[`GLint`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Textur-Mipmap-Level</td>
          <td>Beliebige int-Werte.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_COMPARE_FUNC</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Vergleichsfunktion</td>
          <td>
            <code>gl.LEQUAL</code> (Standardwert), <code>gl.GEQUAL</code>,
            <code>gl.LESS</code>, <code>gl.GREATER</code>, <code>gl.EQUAL</code>,
            <code>gl.NOTEQUAL</code>, <code>gl.ALWAYS</code>, <code>gl.NEVER</code>.
          </td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_COMPARE_MODE</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Textur-Vergleichsmodus</td>
          <td>
            <code>gl.NONE</code> (Standardwert),
            <code>gl.COMPARE_REF_TO_TEXTURE</code>.
          </td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_IMMUTABLE_FORMAT</code></td>
          <td>[`GLboolean`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Unveränderlichkeit des Texturformats und der Größe</td>
          <td>true oder false.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_IMMUTABLE_LEVELS</code></td>
          <td>[`GLuint`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>?</td>
          <td>Beliebige uint-Werte.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_MAX_LEVEL</code></td>
          <td>[`GLint`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Maximales Textur-Mipmap-Array-Level</td>
          <td>Beliebige int-Werte.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_MAX_LOD</code></td>
          <td>[`GLfloat`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Maximaler Wert für die Textur-Detailstufe (Level-of-Detail)</td>
          <td>Beliebige Float-Werte.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_MIN_LOD</code></td>
          <td>[`GLfloat`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Minimaler Wert für die Textur-Detailstufe (Level-of-Detail)</td>
          <td>Beliebige Float-Werte.</td>
        </tr>
        <tr>
          <td><code>gl.TEXTURE_WRAP_R</code></td>
          <td>[`GLenum`](/de/docs/Web/API/WebGL_API/Types)</td>
          <td>Wickelfunktion für Texturkoordinate <code>r</code></td>
          <td>
            <code>gl.REPEAT</code> (Standardwert), <code>gl.CLAMP_TO_EDGE</code>,
            <code>gl.MIRRORED_REPEAT</code>.
          </td>
        </tr>
      </tbody>
    </table>

### Rückgabewert

Gibt die angeforderten Texturinformationen zurück (wie durch `pname` angegeben). Tritt ein Fehler auf, wird [`null`](/de/docs/Web/JavaScript/Reference/Operators/null) zurückgegeben.

## Beispiele

```js
gl.getTexParameter(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER);
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [`WebGLRenderingContext.texParameterf()`](/de/docs/Web/API/WebGLRenderingContext/texParameter)
- [`WebGLRenderingContext.texParameteri()`](/de/docs/Web/API/WebGLRenderingContext/texParameter)
- [`EXT_texture_filter_anisotropic`](/de/docs/Web/API/EXT_texture_filter_anisotropic)
