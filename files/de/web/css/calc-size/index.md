---
title: calc-size()
slug: Web/CSS/calc-size
l10n:
  sourceCommit: e13b6ffe7c9cb05c6a89fcb3c8fcbc987eb05211
---

{{CSSRef}}{{seecompattable}}

Die **`calc-size()`** [CSS](/de/docs/Web/CSS) [Funktion](/de/docs/Web/CSS/CSS_Values_and_Units/CSS_Value_Functions) erlaubt es Ihnen, Berechnungen an {{Glossary("Intrinsic_Size", "intrinsische Größen")}} wie `auto`, [`fit-content`](/de/docs/Web/CSS/fit-content) und [`max-content`](/de/docs/Web/CSS/max-content) durchzuführen. Dies wird von der regulären {{cssxref("calc()")}} Funktion nicht unterstützt.

`calc-size()` Rückgabewerte können auch {{Glossary("Interpolation", "interpoliert")}} werden, was ermöglicht, dass Größen-Schlüsselwortwerte in [Animationen](/de/docs/Web/CSS/CSS_animations) und [Übergängen](/de/docs/Web/CSS/CSS_transitions) verwendet werden. Durch die Einbindung von `calc-size()` in einen Eigenschaftswert wird automatisch [`interpolate-size: allow-keywords`](/de/docs/Web/CSS/interpolate-size) auf die Auswahl angewendet.

Beachten Sie jedoch, dass `interpolate-size` vererbt wird. Das Anwenden auf ein Element ermöglicht die Interpolation von intrinsischen Größen-Schlüsselwörtern für jede auf dieses Element und seine Kinder angewendete Eigenschaft. Daher ist `interpolate-size` die bevorzugte Lösung zur Aktivierung von intrinsischen Größenanimationen. Sie sollten `calc-size()` nur verwenden, um intrinsische Größenanimationen zu aktivieren, wenn sie auch Berechnungen erfordern.

## Syntax

```css
/* Pass a value through calc-size() */
calc-size(auto, size)
calc-size(fit-content, size)

/* Perform a calculation */
calc-size(min-content, size + 100px)
calc-size(fit-content, size / 2)

/* Calculation including a function */
calc-size(auto, round(up, size, 50px))
```

### Parameter

Die Syntax der `calc-size()` Funktion ist wie folgt:

```plain
calc-size(<calc-size-basis>, <calc-sum>)
```

Die Parameter sind:

- `<calc-size-basis>`

  - : Der Wert (meistens eine intrinsische Größe), auf dem eine Berechnung durchgeführt werden soll.

- [`<calc-sum>`](/de/docs/Web/CSS/calc-sum)

  - : Ein Ausdruck, der die durchzuführende Berechnung auf dem `<calc-size-basis>` definiert.

### Rückgabewert

Gibt einen Wert zurück, der gleich dem `<calc-size-basis>` ist, modifiziert durch den `<calc-sum>` Ausdruck. Da der `<calc-size-basis>` Wert eine intrinsische Größenwert ist, ist der Rückgabewert ein modifizierter intrinsischer Größenwert, der sich wie der intrinsische Größenwert verhält, der in die Funktion eingegeben wurde.

## Beschreibung

Bestimmte Browser-Layout-Algorithmen haben besondere Verhaltensweisen für intrinsische Größen-Schlüsselwörter. Die `calc-size()` Funktion ist explizit definiert, um eine intrinsische Größe darzustellen und nicht ein [`<length-percentage>`](/de/docs/Web/CSS/length-percentage), um Korrektheit zu erzwingen. `calc-size()` ermöglicht es, Berechnungen an intrinsischen Größenwerten auf eine sichere, gut definierte Weise durchzuführen.

### Gültige Werte für das erste Argument (`<calc-size-basis>`)

Das erste `calc-size()` Argument kann einer der folgenden intrinsischen Werte sein:

- `auto`
- {{cssxref("min-content")}}
- {{cssxref("max-content")}}
- {{cssxref("fit-content")}}
- `content` (für Container, die mit {{cssxref("flex-basis")}} dimensioniert werden).

Es gibt auch einige spezielle Werte, die dieses Argument annehmen kann:

- Ein verschachtelter `calc-size()` Wert. Dies wird man nicht häufig tun, aber es ist verfügbar, sodass die Verwendung einer [CSS-Variable](/de/docs/Web/CSS/CSS_cascading_variables/Using_CSS_custom_properties) als `<calc-size-basis>` immer funktioniert, vorausgesetzt die Variable ist ein gültiger Wert für die Eigenschaft, auf der `calc-size()` gesetzt wird. Zum Beispiel wird dies funktionieren:

  ```css
  section {
    height: calc-size(calc-size(max-content, size), size + 2rem);
  }
  ```

  Ebenso dies:

  ```css
  :root {
    --intrinsic-size: calc-size(max-content, size);
  }

  section {
    height: calc-size(var(--intrinsic-size), size + 2rem);
  }
  ```

- Ein weiteres `<calc-sum>`, mit den gleichen Einschränkungen wie beim `<calc-sum>` des zweiten Arguments, außer dass das `size` Schlüsselwort nicht eingeschlossen werden kann. Dies werden Sie wahrscheinlich nicht tun, da Sie keine Berechnung an einem intrinsischen Größenwert mehr durchführen, aber falls ein benutzerdefinierter Eigenschaftswert ein `<calc-sum>` ist, wird die Funktion weiterhin funktionieren. Zum Beispiel wird dies direkt funktionieren oder wenn Sie eine benutzerdefinierte Eigenschaft mit einem Wert von `300px + 2rem` verwenden:

  ```css
  section {
    height: calc-size(300px + 2rem, size / 2);
  }
  ```

- Das Schlüsselwort `any`, das eine nicht spezifizierte definierte Größe darstellt. In diesem Fall kann das `size` Schlüsselwort nicht im zweiten Argument eingeschlossen werden, und `calc-size()` gibt das Ergebnis der Berechnung des zweiten Arguments zurück. Zum Beispiel:

  ```css
  section {
    height: calc-size(any, 300px * 1.5); /* Returns 450px */
  }
  ```

Das Mischen verschiedener intrinsischer Größen in derselben Berechnung funktioniert nicht. Zum Beispiel macht `max-content - min-content` keinen Sinn. `calc-size()` erlaubt nur einen einzigen intrinsischen Größenwert in jeder Berechnung, um dieses Problem zu vermeiden.

### Gültige Werte für das zweite Argument (`<calc-sum>`)

Das zweite `calc-size()` Argument ist ein [`<calc-sum>`](/de/docs/Web/CSS/calc-sum) Ausdruck.

In diesem Ausdruck:

- Das Schlüsselwort `size` repräsentiert das als erstes Argument spezifizierte `<calc-size-basis>`.
- Operanden können `size` und alle Werttypen einschließen, die im Kontext Sinn machen.
- Die Operatoren `+`, `-`, `*` und `/` können eingeschlossen werden.
- Andere mathematische Funktionen wie {{cssxref("round()")}}, {{cssxref("max()")}} oder sogar ein verschachteltes `calc-size()` können eingeschlossen werden.
- Der Gesamtausdruck muss [`<length-percentage>`](/de/docs/Web/CSS/length-percentage) entsprechen und zu einem [`<length>`](/de/docs/Web/CSS/length) aufgelöst werden.

### Aktivieren der Animation von intrinsischen Größenwerten

`calc-size()` Rückgabewerte können interpoliert werden, was Animationen zwischen einem [`<length-percentage>`](/de/docs/Web/CSS/length-percentage) Wert und einem `calc-size()` intrinsischen Größenrückgabewert ermöglicht.

> [!NOTE]
> Sie sollten vermeiden, Eigenschaften des Box-Modells zu animieren, wenn möglich, um Ereignisse des Layouts zu reduzieren und die resultierenden Auswirkungen auf die Leistung zu mindern (siehe [Kritischer Renderingpfad > Layout](/de/docs/Web/Performance/Guides/Critical_rendering_path#layout)).

Zum Beispiel könnten Sie einen [Übergang](/de/docs/Web/CSS/CSS_transitions) verwenden, um die `width` eines Containers zwischen `0` und `auto` wie folgt zu animieren:

```css
section {
  width: 0;
  transition: width ease 1s;
}

section:hover,
section:focus {
  width: calc-size(auto, size);
}
```

In dem oben genannten Fall berechnen wir nichts — wir setzen `auto` in `calc-size()` und geben es unverändert zurück. Die {{cssxref("interpolate-size")}} Eigenschaft macht Animationen wie die oben genannte einfacher umzusetzen, vor allem wenn es mehrere Animationen zu berücksichtigen gibt. Sie wird vererbt und muss daher nur einmal auf einer Vorfahren-Eigenschaft deklariert werden, was bedeutet, dass wir zwischen `0` und `auto` hätten wechseln können, ohne `calc-size()` zu verwenden.

Die `calc-size()` Funktion sollte nur verwendet werden, um intrinsische Größenanimationen zu aktivieren, wenn sie auch Berechnungen erfordern. Zum Beispiel passen wir im folgenden Fall die `width` an _und_ wenden eine Berechnung auf den Endzustand der intrinsischen Größe an:

```css
section {
  width: 0;
  transition: width ease 1s;
}

section:hover,
section:focus {
  width: calc-size(auto, size + 2rem);
}
```

Ein Fall, in dem `calc-size()` nützlich ist, ist, wenn Sie zwischen einer intrinsischen Größe und einer modifizierten Version der gleichen intrinsischen Größe animieren möchten. Dies ist mit `interpolate-size` und `calc()` nicht möglich. Zum Beispiel definiert die folgende {{cssxref("@keyframes")}} Definition eine Animation der `width` eines Containers zwischen `fit-content` und 70% des `fit-content`.

```css
@keyframes narrower {
  from {
    width: fit-content;
  }

  to {
    width: calc-size(fit-content, size * 0.7);
  }
}
```

> [!NOTE]
> Beachten Sie, dass `calc-size()` nicht das Animieren zwischen zwei verschiedenen intrinsischen Größenwerten ermöglicht.

## Formale Syntax

{{csssyntax}}

## Beispiele

### Grundlegende `calc-size` Nutzung

Dieses Beispiel zeigt eine grundlegende Dimensionierung eines Containers mit `calc-size()`

#### HTML

Das HTML enthält ein einzelnes {{htmlelement("section")}} Element, das einige Kinderinhalte enthält.

```html
<section>
  <h2>Favorite quote</h2>

  <p>
    Fashion is something so ugly it has to be changed every fifteen minutes.
  </p>
</section>
```

#### CSS

```css hidden
* {
  box-sizing: border-box;
}

section {
  font-family: Arial, Helvetica, sans-serif;
  border: 1px solid black;
}

h2 {
  margin: 0;
  font-weight: 400;
  font-size: 1.1rem;
  text-align: center;
  letter-spacing: 1px;
}

p {
  font-size: 0.8rem;
}
```

Im CSS verwenden wir [flexbox](/de/docs/Web/CSS/CSS_flexible_box_layout), um die Kindelemente innerhalb des `<section>` zu zentrieren, und setzen die `width` und `height` des `<section>` auf `calc-size()` Funktionen. Die `width` ist auf `fit-content` plus `6rem` gesetzt. Die `height` ist auf `auto` multipliziert mit zwei gesetzt.

```css
section {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  width: calc-size(fit-content, size + 6rem);
  height: calc-size(auto, size * 2);
}
```

Der Rest des CSS wurde der Kürze halber ausgeblendet.

#### Ergebnis

Wir haben einigen horizontalen und vertikalen Platz geschaffen, damit der Text ohne die Verwendung von Padding zentriert werden kann.

{{ EmbedLiveSample('Basic `calc-size` usage', '100%', '150') }}

### Grundlegende `calc-size` Animationen

Dieses Beispiel demonstriert, wie man `calc-size()` verwenden kann, um zwischen einer spezifischen Größe und einer intrinsischen Größe zu animieren. Die Demo zeigt ein Charakterabzeichen/"Namensschild", das beim Schweben oder Fokussieren Informationen über den Charakter zeigt. Die Offenlegung wird durch einen {{cssxref("height")}} Übergang zwischen einer festgelegten Länge und `max-content` gehandhabt.

#### HTML

Das HTML enthält ein einzelnes {{htmlelement("section")}} Element mit [`tabindex="0"`](/de/docs/Web/HTML/Global_attributes/tabindex), um Tastaturfokus zu erhalten. Das `<section>` enthält {{htmlelement("header")}} und {{htmlelement("main")}} Elemente, jedes mit eigenen Kinderinhalten.

```html
<section tabindex="0">
  <header>
    <h2>Chris Mills</h2>
  </header>
  <main>
    <p>Chris is the silent phantom of MDN.</p>
    <ul>
      <li><strong>Height</strong>: 3.03m</li>
      <li><strong>Weight</strong>: 160kg</li>
      <li><strong>Tech Fu</strong>: 7</li>
      <li><strong>Bad Jokes</strong>: 9</li>
    </ul>
  </main>
</section>
```

#### CSS

```css hidden
* {
  box-sizing: border-box;
}

section {
  font-family: Arial, Helvetica, sans-serif;
  width: 175px;
  border-radius: 5px;
  background: #eee;
  box-shadow:
    inset 1px 1px 4px rgb(255 255 255 / 0.5),
    inset -1px -1px 4px rgb(0 0 0 / 0.5);
}

header {
  padding: 10px;
  border-bottom: 2px solid #ccc;
}

main {
  padding: 0.7rem;
}

h2 {
  margin: 0;
  font-weight: 400;
  font-size: 1.1rem;
  text-align: center;
  letter-spacing: 1px;
}

p,
li {
  font-size: 0.8rem;
  line-height: 1.5;
}

p {
  margin-top: 0;
}
```

Im CSS setzen wir die {{cssxref("height")}} des `<section>` auf `2.5rem` und {{cssxref("overflow")}} auf `hidden`, sodass standardmäßig nur das `<header>` angezeigt wird. Dann spezifizieren wir einen `transition`, der die `<section>` `height` über eine Sekunde während der Zustandsänderungen animiert. Schließlich setzen wir die `<section>` `height` auf einen `calc-size()` Funktionsaufruf bei {{cssxref(":hover")}} und {{cssxref(":focus")}}. Der Funktionsrückgabewert entspricht `max-content` + `2rem`.

```css
section {
  height: 2.5rem;
  overflow: hidden;
  transition: height ease 1s;
}

section:hover,
section:focus {
  height: calc-size(max-content, size + 2rem);
}
```

Der Rest des CSS wurde der Kürze halber ausgeblendet.

#### Ergebnis

Versuchen Sie, über die `<section>` zu schweben oder sie über die Tastatur zu fokussieren — sie wird auf ihre volle Höhe + 2rem animiert, wodurch alle Inhalte mit 2rem zusätzlichem Platz am unteren Rand sichtbar werden.

{{ EmbedLiveSample('Basic `calc-size` animations', '100%', '250') }}

### Anpassen der Lesebreite basierend auf `fit-content`

Dieses Beispiel zeigt einen Container mit darin befindlichem Text und einem Button, der geklickt werden kann, um die Containerbreite je nach Lesepräferenz schmaler oder breiter zu machen.

#### HTML

Das HTML enthält ein einzelnes {{htmlelement("section")}} Element, das Kindtextinhalte enthält, plus einen {{htmlelement("button")}}, um die `<section>` Breite zu ändern.

```html
<section class="easy-reader">
  <h2>Easy reader</h2>

  <p>
    Eius velit aperiam ipsa. Deleniti eum excepturi ut magni maxime maxime
    beatae. Dicta aperiam est laudantium ut illum facere qui officiis. Sunt
    deleniti quam id. Quis sunt voluptatem praesentium minima dolorum autem
    consequatur velit.
  </p>

  <p>
    Vitae ab incidunt velit aspernatur deleniti distinctio rerum. Et natus sed
    et quos mollitia quia quod. Quae officia ex ea. Ducimus ut voluptatem et et
    debitis. Quidem provident laboriosam exercitationem similique deleniti.
    Temporibus vel veniam mollitia magni unde a nostrum.
  </p>

  <button class="width-adjust">Narrower</button>
</section>
```

#### CSS

```css hidden
* {
  box-sizing: border-box;
}

body {
  width: 600px;
  margin: 0 auto;
}

section {
  margin-top: 20px;
  font-family: Arial, Helvetica, sans-serif;
  background: #eee;
  border: 2px solid #ccc;
  padding: 0 20px;
  position: relative;
}

p,
li {
  font-size: 0.8rem;
  line-height: 1.5;
}

button {
  position: absolute;
  top: 2px;
  right: 2px;
}
```

Im CSS setzen wir die {{cssxref("width")}} der `<section>` standardmäßig auf {{cssxref("fit-content")}}. Wir definieren dann zwei Sätze von {{cssxref("@keyframes")}}, `narrower`, die von `fit-content` zu 70% von `fit-content` animiert werden (mit `calc-size()` berechnet), und `wider`, die die gleichen Werte, aber in entgegengesetzter Richtung animiert. Schließlich fügen wir diese Animationen zwei Klassen zu — `.narrower` und `.wider`. Jede Animation ist so definiert, dass sie eine Sekunde dauert und der Endzustand nach Abschluss angewendet bleibt.

```css
section {
  width: fit-content;
}

@keyframes narrower {
  from {
    width: fit-content;
  }

  to {
    width: calc-size(fit-content, size * 0.7);
  }
}

@keyframes wider {
  from {
    width: calc-size(fit-content, size * 0.7);
  }

  to {
    width: fit-content;
  }
}

.narrower {
  animation: narrower 1s ease forwards;
}

.wider {
  animation: wider 1s ease forwards;
}
```

Der Rest des CSS wurde der Kürze halber ausgeblendet.

#### JavaScript

Das JavaScript bietet einen Schalter für schmaler/breiter, der die entsprechende Klasse auf die `<section>` anwendet, wenn der Button geklickt wird:

```js
const widthAdjustBtn = document.querySelector(".width-adjust");
const easyReader = document.querySelector(".easy-reader");

widthAdjustBtn.addEventListener("click", () => {
  if (easyReader.classList.length === 1) {
    easyReader.classList.add("narrower");
    widthAdjustBtn.textContent = "Wider";
  } else if (easyReader.classList.contains("wider")) {
    easyReader.classList.replace("wider", "narrower");
    widthAdjustBtn.textContent = "Wider";
  } else if (easyReader.classList.contains("narrower")) {
    easyReader.classList.replace("narrower", "wider");
    widthAdjustBtn.textContent = "Narrower";
  }
});
```

#### Ergebnis

Versuchen Sie, den `<button>` einige Male zu klicken, um die `<section>` zwischen der breiten und schmalen Lesebreite zu wechseln, indem Sie die `width` basierend auf dem `fit-content` Wert anpassen.

{{ EmbedLiveSample('Adjusting reading width based on `fit-content`', '100%', '300') }}

### Verwendung einer Funktion innerhalb der `calc-size()` Funktion

Wie bereits erwähnt, ist es möglich, eine andere Funktion innerhalb von `calc-size()` zu verwenden. In diesem Beispiel wird [`field-sizing: content`](/de/docs/Web/CSS/field-sizing) auf {{htmlelement("input")}} Elemente gesetzt, um sie so breit wie den eingegebenen Inhalt zu machen. Dann wird eine [`max()`](/de/docs/Web/CSS/max) Funktion innerhalb von `calc-size()` verwendet, um sicherzustellen, dass die `<input>`s mindestens eine Mindestgröße haben und nur zu wachsen beginnen, wenn der eingegebene Text breiter als diese Größe wird — indem sie auf `fit-content` plus `20px` gesetzt werden.

#### HTML

Das HTML enthält ein {{htmlelement("form")}} Element mit drei textuellen `<input>` Typen. Jedes `<input>` hat ein {{htmlelement("label")}} zur Barrierefreiheit und ein [`maxlength`](/de/docs/Web/HTML/Attributes/maxlength), um zu verhindern, dass eingegebene Werte zu lang werden, um das Formularlayout zu unterbrechen.

```html
<form>
  <div>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" maxlength="48" />
  </div>
  <div>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" maxlength="48" />
  </div>
  <div>
    <label for="address">Address:</label>
    <input type="text" id="address" name="address" maxlength="60" />
  </div>
</form>
```

#### CSS

```css hidden
* {
  box-sizing: border-box;
}

body {
  width: 600px;
  margin: 0 auto;
}

form {
  margin-top: 20px;
  padding: 20px;
  font-family: Arial, Helvetica, sans-serif;
  background: #eee;
  border: 2px solid #ccc;
}

div {
  display: flex;
  align-items: center;
}

div:not(div:last-child) {
  margin-bottom: 20px;
}
```

Im CSS setzen wir die `width` der `<label>` Elemente auf `100px`. Wir setzen `field-sizing: content` auf die {{htmlelement("input")}} Elemente, um sie so breit wie den eingegebenen Inhalt zu machen — sie hätten standardmäßig keine Breite, weil nichts in sie eingetragen worden wäre. Um dies zu kompensieren, setzen wir ihre `width`-Werte auf `calc-size(fit-content, max(100px, size + 20px))`. Das bedeutet, dass sie mindestens `100px` breit sind, selbst wenn kein Wert eingegeben wurde. Wenn ein eingetragener Wert breiter als `100px` wird, ändert sich ihre `width` auf `fit-content` plus `20px`, was bedeutet, dass sie mit der Inhaltsgröße wachsen, aber einen `20px`-Abstand auf der rechten Seite behalten.

```css
label {
  width: 100px;
}

input {
  field-sizing: content;
  width: calc-size(fit-content, max(100px, size + 20px));
}
```

Der Rest des CSS wurde der Kürze halber ausgeblendet.

#### Ergebnis

Versuchen Sie, Text in das Formular einzugeben, und beobachten Sie, wie sie größer werden, wenn die Werte anfangen, so breit wie die Mindestbreite zu werden, die durch die `max()` Funktion erzwungen wird.

{{ EmbedLiveSample('Using a function inside the `calc-size()` function', '100%', '200') }}

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{cssxref("interpolate-size")}}
- {{cssxref("calc()")}}
- {{cssxref("round()")}}
- [Animate to height: auto; (and other intrinsic sizing keywords) in CSS](https://developer.chrome.com/docs/css-ui/animate-to-height-auto) auf developer.chrome.com (2024)
