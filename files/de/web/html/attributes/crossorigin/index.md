---
title: "HTML-Attribut: crossorigin"
short-title: crossorigin
slug: Web/HTML/Attributes/crossorigin
l10n:
  sourceCommit: 05187b0fecf39b9176d4a101623589309cf44dd0
---

{{HTMLSidebar}}

Das **`crossorigin`** Attribut, gültig für die {{HTMLElement("audio")}}, {{HTMLElement("img")}}, {{HTMLElement("link")}}, {{HTMLElement("script")}}, und {{HTMLElement("video")}} Elemente, bietet Unterstützung für [CORS](/de/docs/Web/HTTP/CORS) und definiert, wie das Element mit Cross-Origin-Anfragen umgeht. Dadurch kann die Konfiguration der CORS-Anfragen für die vom Element abgerufenen Daten ermöglicht werden. Je nach Element kann das Attribut ein CORS-Einstellungsattribut sein.

Das `crossorigin` Inhaltsattribut bei Medienelementen ist ein CORS-Einstellungsattribut.

Diese Attribute sind {{Glossary("Enumerated", "aufgezählt")}} und haben folgende mögliche Werte:

- `anonymous`
  - : Die Anfrage verwendet CORS-Header und das Credentials-Flag ist auf `'same-origin'` gesetzt. Es gibt keinen Austausch von **Benutzeranmeldeinformationen** über Cookies, Client-seitige TLS-Zertifikate oder HTTP-Authentifizierung, es sei denn, das Ziel ist derselbe Ursprung.
- `use-credentials`
  - : Die Anfrage verwendet CORS-Header, das Credentials-Flag ist auf `'include'` gesetzt, und **Benutzeranmeldeinformationen** werden immer einbezogen.
- `""`
  - : Das Setzen des Attributnamens auf einen leeren Wert, wie `crossorigin` oder `crossorigin=""`, ist dasselbe wie `anonymous`.

Ein ungültiges Schlüsselwort und ein leerer String werden als das Schlüsselwort `anonymous` behandelt.

Standardmäßig (d. h. wenn das Attribut nicht angegeben ist) wird CORS überhaupt nicht verwendet. Der Benutzeragent fragt nicht um Erlaubnis für den vollständigen Zugriff auf die Ressource, und im Falle einer Cross-Origin-Anfrage werden bestimmte Einschränkungen angewendet, abhängig vom betreffenden Elementtyp:

<table class="no-markdown">
  <tbody>
    <tr>
      <td class="header">Element</td>
      <td class="header">Einschränkungen</td>
    </tr>
    <tr>
      <td><code>img</code>, <code>audio</code>, <code>video</code></td>
      <td>
        Wenn die Ressource in {{HTMLElement("canvas")}} platziert wird, wird das Element als <a href="/de/docs/Web/HTML/CORS_enabled_image#security_and_tainted_canvases"><em>verfälscht</em></a> markiert.
      </td>
    </tr>
    <tr>
      <td><code>script</code></td>
      <td>
        Der Zugriff auf Fehlerprotokollierung über [`window.onerror`](/de/docs/Web/API/Window/error_event) wird eingeschränkt.
      </td>
    </tr>
    <tr>
      <td><code>link</code></td>
      <td>
        Anfragen ohne passenden <code>crossorigin</code> Header können verworfen werden.
      </td>
    </tr>
  </tbody>
</table>

> [!NOTE]
> Das `crossorigin` Attribut wird bei [`rel="icon"`](/de/docs/Web/HTML/Attributes/rel#icon) in auf Chromium basierten Browsern nicht unterstützt. Siehe das [offene Chromium-Problem](https://crbug.com/1121645).

### Beispiel: `crossorigin` mit dem `<script>` Element

Sie können das folgende {{HTMLElement("script")}} Element verwenden, um einem Browser mitzuteilen, das Skript `https://example.com/example-framework.js` auszuführen, ohne Benutzeranmeldeinformationen zu senden.

```html
<script
  src="https://example.com/example-framework.js"
  crossorigin="anonymous"></script>
```

### Beispiel: Web-Manifest mit Anmeldedaten

Der Wert `use-credentials` muss verwendet werden, wenn ein [Manifest](/de/docs/Web/Progressive_web_apps/Manifest) abgerufen wird, das Anmeldeinformationen erfordert, selbst wenn die Datei aus demselben Ursprung stammt.

```html
<link rel="manifest" href="/app.webmanifest" crossorigin="use-credentials" />
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Cross-Origin Resource Sharing (CORS)](/de/docs/Web/HTTP/CORS)
- [HTML-Attribut: `rel`](/de/docs/Web/HTML/Attributes/rel)

{{QuickLinksWithSubpages("/de/docs/Web/HTML/")}}
