---
title: "NavigatorUAData: getHighEntropyValues() Methode"
short-title: getHighEntropyValues()
slug: Web/API/NavigatorUAData/getHighEntropyValues
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{APIRef("User-Agent Client Hints API")}}{{SeeCompatTable}}{{AvailableInWorkers}}

Die **`getHighEntropyValues()`**-Methode des [`NavigatorUAData`](/de/docs/Web/API/NavigatorUAData)-Interfaces ist ein {{jsxref("Promise")}}, das mit einem Wörterbuch-Objekt aufgelöst wird, welches die _High Entropy_-Werte enthält, die der User-Agent zurückgibt.

> [!NOTE]
> Die Begriffe _High Entropy_ und _Low Entropy_ beziehen sich auf die Menge an Informationen, die diese Werte über den Browser preisgeben.
> Die als Eigenschaften zurückgegebenen Werte gelten als Low Entropy und sind wahrscheinlich nicht geeignet, einen Benutzer zu identifizieren.
> Die von `getHighEntropyValues()` zurückgegebenen Werte könnten potenziell mehr Informationen preisgeben.
> Diese Werte werden daher über ein {{jsxref("Promise")}} abgerufen, welches dem Browser Zeit gibt, die Erlaubnis des Benutzers anzufordern oder andere Prüfungen durchzuführen.

## Syntax

```js-nolint
getHighEntropyValues(hints)
```

### Parameter

- `hints`

  - : Ein Array, das die zurückzugebenden Hinweise enthält, einer oder mehrere von:

    - `"architecture"`
    - `"bitness"`
    - `"formFactor"`
    - `"fullVersionList"`
    - `"model"`
    - `"platformVersion"`
    - `"uaFullVersion"` {{Deprecated_Inline}}
    - `"wow64"`

### Rückgabewert

Ein {{jsxref("Promise")}}, das auf ein Objekt aufgelöst wird, das einige oder alle der folgenden Werte enthält (basierend auf den angeforderten Hinweisen):

- `brands`
  - : Gibt ein Array von Objekten zurück, das `brand` und `version` enthält, welche die Browsermarke und ihre Version angeben (die gleichen Informationen wie von [`NavigatorUAData.brands`](/de/docs/Web/API/NavigatorUAData/brands) bereitgestellt).
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA")}}-Header (ein [low-entropy client hint](/de/docs/Web/HTTP/Guides/Client_hints#low_entropy_hints)) an einen Server gesendet werden können.
- `mobile`
  - : Gibt `true` zurück, wenn der User-Agent auf einem mobilen Gerät läuft (die gleichen Informationen wie von [`NavigatorUAData.mobile`](/de/docs/Web/API/NavigatorUAData/mobile) bereitgestellt).
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Mobile")}}-Header (ein [low-entropy client hint](/de/docs/Web/HTTP/Guides/Client_hints#low_entropy_hints)) an einen Server gesendet werden können.
- `platform`
  - : Gibt einen String zurück, der die Plattform beschreibt, auf der der User-Agent läuft, wie `"Windows"` (die gleichen Informationen wie von [`NavigatorUAData.platform`](/de/docs/Web/API/NavigatorUAData/platform) bereitgestellt).
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Platform")}}-Header (ein [low-entropy client hint](/de/docs/Web/HTTP/Guides/Client_hints#low_entropy_hints)) an einen Server gesendet werden können.
- `architecture`
  - : Ein String, der die Plattform-Architektur enthält. Zum Beispiel `"x86"`.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Arch")}}-Header gesendet werden können, nachdem der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `bitness`
  - : Ein String, der die Architektur-Bitness enthält. Zum Beispiel `"32"` oder `"64"`.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Bitness")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `formFactor`
  - : Ein String, der den Formfaktor eines Geräts enthält. Zum Beispiel `"Tablet"` oder `"VR"`.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Form-Factors")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `fullVersionList`
  - : Ein Array von Objekten mit den Eigenschaften `"brand"` und `"version"`, die den Browsernamen und die vollständige Version darstellen.
    Zum Beispiel, `{"brand": "Google Chrome", "version": "103.0.5060.134"}, {"brand": "Chromium", "version": "103.0.5060.134"}`.
    Bitte beachten Sie, dass ein Objekt absichtlich ungültige Informationen enthalten kann, um zu verhindern, dass Websites sich auf eine feste Liste von Browsern verlassen.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Full-Version-List")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `model`
  - : Ein String, der das Modell des mobilen Geräts enthält. Zum Beispiel `"Pixel 2XL"`. Wenn das Gerät kein mobiles Gerät ist oder das Gerätemodell nicht bekannt ist, wird `model` `""` sein.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Model")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `platformVersion`
  - : Ein String, der die Plattformversion enthält. Der Plattformname selbst ist immer als Low-Entropy-Hinweis `platform` verfügbar. Zum Beispiel `"10.0"`.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Platform-Version")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `uaFullVersion` {{Deprecated_Inline}}
  - : Ein String, der die vollständige Browserversion enthält. Zum Beispiel `"103.0.5060.134"`. Veraltet zugunsten von `fullVersionList`.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-Full-Version")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.
- `wow64`
  - : Ein Boolean, der anzeigt, ob das Binary des User-Agents im 32-Bit-Modus auf einem 64-Bit-Windows läuft.
    Beachten Sie, dass diese Informationen in der {{HTTPHeader("Sec-CH-UA-WoW64")}}-Header gesendet werden können, wenn der Server sie explizit in der {{HTTPHeader("Accept-CH")}}-Header angefordert hat.

### Ausnahmen

- `NotAllowedError` [`DOMException`](/de/docs/Web/API/DOMException)
  - : Wird ausgelöst, wenn der User-Agent entscheidet, dass einer oder mehrere der angeforderten `hints` nicht zurückgegeben werden sollen.

## Beispiele

Im folgenden Beispiel werden mehrere Hinweise mit der `getHighEntropyValues()`-Methode angefordert.
Wenn das Versprechen aufgelöst wird, werden diese Informationen in der Konsole angezeigt.

```js
navigator.userAgentData
  .getHighEntropyValues([
    "architecture",
    "model",
    "platformVersion",
    "fullVersionList",
  ])
  .then((values) => console.log(values));
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- Diese Werte sind auch über HTTP-Request-Header verfügbar:
  - [Low-entropy client hints](/de/docs/Web/HTTP/Guides/Client_hints#low_entropy_hints) werden automatisch gesendet:
    - {{HTTPHeader("Sec-CH-UA")}}
    - {{HTTPHeader("Sec-CH-UA-Mobile")}}
    - {{HTTPHeader("Sec-CH-UA-Platform")}}
  - Server können anfordern, dass High-Entropy-Client-Hinweise in nachfolgenden Anfragen gesendet werden, indem sie die {{HTTPHeader("Accept-CH")}}-Header verwenden:
    - {{HTTPHeader("Sec-CH-UA-Arch")}}
    - {{HTTPHeader("Sec-CH-UA-Bitness")}}
    - {{HTTPHeader("Sec-CH-UA-Full-Version")}}
    - {{HTTPHeader("Sec-CH-UA-Model")}}
    - {{HTTPHeader("Sec-CH-UA-Platform-Version")}}
