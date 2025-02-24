---
title: Expires
slug: Web/HTTP/Headers/Expires
l10n:
  sourceCommit: 442db82028668b17b888ee439468ae2ac9d589a5
---

{{HTTPSidebar}}

Der HTTP **`Expires`** {{Glossary("response_header", "Antwortheader")}} enthält das Datum/Uhrzeit, nach dem die Antwort im Kontext von [HTTP-Caching](/de/docs/Web/HTTP/Caching) als abgelaufen gilt.

Der Wert `0` wird verwendet, um ein Datum in der Vergangenheit darzustellen, was darauf hinweist, dass die Ressource bereits abgelaufen ist.

> [!NOTE]
> Wenn ein {{HTTPHeader("Cache-Control")}}-Header mit der Anweisung `max-age` oder `s-maxage` in der Antwort vorhanden ist, wird der `Expires`-Header ignoriert.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Header-Typ</th>
      <td>{{Glossary("Response_header", "Antwortheader")}}</td>
    </tr>
    <tr>
      <th scope="row">{{Glossary("Forbidden_request_header", "Verbotener Anforderungsheader")}}</th>
      <td>Nein</td>
    </tr>
    <tr>
      <th scope="row">
        {{Glossary("CORS-safelisted_response_header", "CORS-safelisted Antwortheader")}}
      </th>
      <td>Ja</td>
    </tr>
  </tbody>
</table>

## Syntax

```http
Expires: <day-name>, <day> <month> <year> <hour>:<minute>:<second> GMT
```

## Direktiven

- `<day-name>`
  - : Einer von `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat` oder `Sun` (Groß-/Kleinschreibung beachten).
- `<day>`
  - : 2-stellige Tagesnummer, z.B. "04" oder "23".
- `<month>`
  - : Einer von `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov`, `Dec` (Groß-/Kleinschreibung beachten).
- `<year>`
  - : 4-stellige Jahreszahl, z.B. "1990" oder "2016".
- `<hour>`
  - : 2-stellige Stundenzahl, z.B. "09" oder "23".
- `<minute>`
  - : 2-stellige Minutenzahl, z.B. "04" oder "59".
- `<second>`
  - : 2-stellige Sekundenzahl, z.B. "04" oder "59".
- GMT
  - : Greenwich Mean Time. HTTP-Daten werden immer in GMT ausgedrückt, nie in Ortszeit.

## Beispiele

```http
Expires: Wed, 21 Oct 2015 07:28:00 GMT
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [HTTP-Caching](/de/docs/Web/HTTP/Caching) Leitfaden
- {{HTTPHeader("Cache-Control")}}
- {{HTTPHeader("Age")}}
