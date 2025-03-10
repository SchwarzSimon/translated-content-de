---
title: "<dfn>: Das Definitionselement"
slug: Web/HTML/Element/dfn
l10n:
  sourceCommit: f65f7f6e4fda2cb1bd0e7db17777e2cb20be7d27
---

{{HTMLSidebar}}

Das **`<dfn>`** [HTML](/de/docs/Web/HTML)-Element zeigt an, dass ein Begriff definiert werden soll. Das `<dfn>`-Element sollte in einem vollständigen Definitionssatz verwendet werden, bei dem die vollständige Definition des Begriffs eine der folgenden sein kann:

- Der übergeordnete Absatz (ein Textblock, manchmal durch ein {{HTMLElement("p")}}-Element gekennzeichnet)
- Das {{HTMLElement("dt")}}/{{HTMLElement("dd")}}-Paar
- Der nächstgelegene [Abschnitt](/de/docs/Web/HTML/Content_categories#sectioning_content), der Vorfahre des `<dfn>`-Elements ist,

{{InteractiveExample("HTML Demo: &lt;dfn&gt;", "tabbed-shorter")}}

```html interactive-example
<p>
  A <dfn id="def-validator">validator</dfn> is a program that checks for syntax
  errors in code or documents.
</p>
```

```css interactive-example
/* stylelint-disable-next-line block-no-empty */
dfn {
}
```

## Attribute

Zu den Attributen dieses Elements gehören die [globalen Attribute](/de/docs/Web/HTML/Global_attributes).

Das [`title`](/de/docs/Web/HTML/Global_attributes/title)-Attribut hat eine besondere Bedeutung, wie unten angemerkt.

## Nutzungshinweise

Es gibt einige nicht ganz offensichtliche Aspekte bei der Verwendung des `<dfn>`-Elements. Diese betrachten wir hier.

### Definition des zu definierenden Begriffs

Der zu definierende Begriff wird anhand dieser Regeln identifiziert:

1. Wenn das `<dfn>`-Element ein [`title`](/de/docs/Web/HTML/Global_attributes/title)-Attribut hat, wird der Wert des `title`-Attributs als der zu definierende Begriff angesehen. Das Element muss dennoch Text enthalten, dieser Text kann jedoch eine Abkürzung (vielleicht unter Verwendung von {{HTMLElement("abbr")}}) oder eine andere Form des Begriffs sein.
2. Wenn das `<dfn>`-Element ein einzelnes Kindelement enthält und keinen eigenen Textinhalt hat, und das Kindelement ein {{HTMLElement("abbr")}}-Element mit einem eigenen `title`-Attribut ist, dann ist der exakte Wert des `title`-Attributs des `<abbr>`-Elements der zu definierende Begriff.
3. Andernfalls ist der Textinhalt des `<dfn>`-Elements der zu definierende Begriff. Dies wird [im ersten Beispiel unten](#grundlegende_identifizierung_eines_begriffs) gezeigt.

> [!NOTE]
> Wenn das `<dfn>`-Element ein `title`-Attribut hat, _muss_ es den zu definierenden Begriff und keinen anderen Text enthalten.

### Links zu `<dfn>`-Elementen

Wenn Sie auf dem `<dfn>`-Element ein [`id`](/de/docs/Web/HTML/Global_attributes/id)-Attribut hinzufügen, können Sie dann mit {{HTMLElement("a")}}-Elementen darauf verlinken. Solche Links sollten Verwendungen des Begriffs darstellen, mit der Absicht, dass der Leser schnell zur Definition des Begriffs navigieren kann, wenn er nicht bereits bekannt ist, indem er auf den Link des Begriffs klickt.

Dies wird im Beispiel unter [Links zu Definitionen](#links_zu_definitionen) unten gezeigt.

## Beispiele

Schauen wir uns einige Beispiele für verschiedene Nutzungsszenarien an.

### Grundlegende Identifizierung eines Begriffs

Dieses Beispiel verwendet ein einfaches `<dfn>`-Element, um die Position eines Begriffs innerhalb der Definition zu identifizieren.

#### HTML

```html
<p>
  The <strong>HTML Definition element (<dfn>&lt;dfn&gt;</dfn>)</strong> is used
  to indicate the term being defined within the context of a definition phrase
  or sentence.
</p>
```

Da das `<dfn>`-Element kein `title` hat, werden die Textinhalte des `<dfn>`-Elements selbst als der zu definierende Begriff verwendet.

#### Ergebnis

{{EmbedLiveSample("Basic_identification_of_a_term", 650, 120)}}

### Links zu Definitionen

Um Links zu den Definitionen hinzuzufügen, erstellen Sie den Link auf die gleiche Weise wie immer, mit dem {{HTMLElement("a")}}-Element.

#### HTML

```html-nolint
<p>
  The
  <strong>HTML Definition element (<dfn id="definition-dfn">&lt;dfn&gt;</dfn>)</strong>
  is used to indicate the term being defined within the context of a definition
  phrase or sentence.
</p>

<p>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Graece donan, Latine
  voluptatem vocant. Confecta res esset. Duo Reges: constructio interrete.
  Scrupulum, inquam, abeunti;
</p>

<p>
  Because of all of that, we decided to use the
  <code><a href="#definition-dfn">&lt;dfn&gt;</a></code> element for this
  project.
</p>
```

Hier sehen wir die Definition — jetzt mit einem [`id`](/de/docs/Web/HTML/Global_attributes/id)-Attribut, `"definition-dfn"`, das als Ziel eines Links verwendet werden kann. Später wird ein Link mit `<a>` erstellt, wobei das [`href`](/de/docs/Web/HTML/Element/a#href)-Attribut auf `"#definition-dfn"` gesetzt wird, um den Link zurück zur Definition einzurichten.

#### Ergebnis

{{EmbedLiveSample("Links_to_definitions", 650, 300)}}

### Verwendung von Abkürzungen und Definitionen zusammen

In einigen Fällen möchten Sie möglicherweise eine Abkürzung für einen Begriff verwenden, wenn Sie ihn definieren. Dies kann durch die Verwendung der `<dfn>`- und {{HTMLElement("abbr")}}-Elemente zusammen erfolgen, wie folgt:

#### HTML

```html
<p>
  The <dfn><abbr title="Hubble Space Telescope">HST</abbr></dfn> is among the
  most productive scientific instruments ever constructed. It has been in orbit
  for over 20 years, scanning the sky and returning data and photographs of
  unprecedented quality and detail.
</p>

<p>
  Indeed, the <abbr title="Hubble Space Telescope">HST</abbr> has arguably done
  more to advance science than any device ever built.
</p>
```

Beachten Sie das `<abbr>`-Element innerhalb des `<dfn>`. Das erstere stellt fest, dass der Begriff eine Abkürzung ("HST") ist und gibt den vollständigen Begriff ("Hubble Space Telescope") in seinem `title`-Attribut an. Das letztere zeigt an, dass der abgekürzte Begriff einen zu definierenden Begriff darstellt.

#### Ergebnis

{{EmbedLiveSample("Using_abbreviations_and_definitions_together", 650, 200)}}

## Technische Zusammenfassung

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/de/docs/Web/HTML/Content_categories">Inhaltskategorien</a>
      </th>
      <td>
        <a href="/de/docs/Web/HTML/Content_categories#flow_content">Fließender Inhalt</a>,
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phraseninhalt</a>,
        <a href="/de/docs/Web/HTML/Content_categories#palpable_content">spürbarer Inhalt</a>.
      </td>
    </tr>
    <tr>
      <th scope="row">Erlaubter Inhalt</th>
      <td>
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phraseninhalt</a>,
        aber kein <code>&lt;dfn&gt;</code>-Element darf ein Nachfahre sein.
      </td>
    </tr>
    <tr>
      <th scope="row">Tag-Ausslassung</th>
      <td>Keine, sowohl das Start- als auch das End-Tag sind obligatorisch.</td>
    </tr>
    <tr>
      <th scope="row">Erlaubte Eltern</th>
      <td>
        Jedes Element, das
        <a href="/de/docs/Web/HTML/Content_categories#phrasing_content">Phraseninhalt</a> akzeptiert.
      </td>
    </tr>
    <tr>
      <th scope="row">Implizierte ARIA-Rolle</th>
      <td><a href="/de/docs/Web/Accessibility/ARIA/Reference/Roles/term_role"><code>term</code></a></td>
    </tr>
    <tr>
      <th scope="row">Erlaubte ARIA-Rollen</th>
      <td>Beliebig</td>
    </tr>
    <tr>
      <th scope="row">DOM-Schnittstelle</th>
      <td>[`HTMLElement`](/de/docs/Web/API/HTMLElement)</td>
    </tr>
  </tbody>
</table>

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- Elemente im Zusammenhang mit Definitionslisten: {{HTMLElement("dl")}}, {{HTMLElement("dt")}}, {{HTMLElement("dd")}}
- {{HTMLElement("abbr")}}
