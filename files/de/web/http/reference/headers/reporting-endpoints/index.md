---
title: Reporting-Endpoints
slug: Web/HTTP/Reference/Headers/Reporting-Endpoints
l10n:
  sourceCommit: 57b01b603385ca121240d52d542adfa60da0f92e
---

{{HTTPSidebar}}

Der HTTP **`Reporting-Endpoints`** {{Glossary("response_header", "Antwort-Header")}} erlaubt Website-Administratoren, ein oder mehrere Endpunkte anzugeben, an die Berichte gesendet werden können, die von der [Reporting-API](/de/docs/Web/API/Reporting_API) erzeugt werden.

Die Endpunkte können beispielsweise als Ziel zum Senden von CSP-Verstoßberichten, {{HTTPHeader("Cross-Origin-Opener-Policy")}} Berichten oder anderen allgemeinen Verstößen verwendet werden.

Wenn er zur Meldung von [Content Security Policy (CSP)](/de/docs/Web/HTTP/Guides/CSP#violation_reporting) Fehlern verwendet wird, wird der Header in Kombination mit dem {{HTTPHeader("Content-Security-Policy")}} Header {{CSP("report-to")}} Directive genutzt.
Für weitere Details zum Einrichten der CSP-Berichterstattung lesen Sie die [Content Security Policy (CSP)](/de/docs/Web/HTTP/Guides/CSP#violation_reporting) Dokumentation.

> [!NOTE]
> Dieser Header ersetzt {{HTTPHeader("Report-To")}} {{deprecated_inline}} zur Deklaration von Endpunkten und sollte bevorzugt verwendet werden.

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">Header-Typ</th>
      <td>{{Glossary("Response_header", "Antwort-Header")}}</td>
    </tr>
    <tr>
      <th scope="row">{{Glossary("Forbidden_request_header", "Verbotener Anfrage-Header")}}</th>
      <td>Nein</td>
    </tr>
    <tr>
      <th scope="row">
        {{Glossary("CORS-safelisted_response_header", "CORS-safelisted Antwort-Header")}}
      </th>
      <td>Nein</td>
    </tr>
  </tbody>
</table>

## Syntax

```http
Reporting-Endpoints: <endpoint>
Reporting-Endpoints: <endpoint>, …, <endpointN>
```

- `<endpoint>`
  - : Ein Reporting-Endpunkt im Format `<endpoint-name>="<URL>"`.
    Die Endpunkte müssen gültige URIs in Anführungszeichen sein (z. B. `my-endpoint="https://example.com/reports"`) und nicht-sichere Endpunkte werden ignoriert.
    Es kann eine durch Kommas getrennte Liste von Endpunkten angegeben werden.

## Beispiele

### Einrichten eines CSP-Verstoßbericht-Endpunkts

Das folgende Beispiel zeigt, wie der `Reporting-Endpoints` Antwort-Header in Verbindung mit dem {{HTTPHeader("Content-Security-Policy")}} Header verwendet wird, um anzugeben, wohin CSP-Verstoßberichte gesendet werden:

```http
Reporting-Endpoints: csp-endpoint="https://example.com/csp-reports"
Content-Security-Policy: default-src 'self'; report-to csp-endpoint
```

### Angabe mehrerer Reporting-Endpunkte

Es ist möglich, mehrere Endpunkte anzugeben, die für verschiedene Arten von Verstoßberichten verwendet werden können.

```http
Reporting-Endpoints: csp-endpoint="https://example.com/csp-reports",
                     permissions-endpoint="https://example.com/permissions-policy-reports"
```

## Spezifikationen

{{Specifications}}

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- [Reporting API](/de/docs/Web/API/Reporting_API)
- [Content Security Policy (CSP)](/de/docs/Web/HTTP/Guides/CSP#violation_reporting) Leitfaden
- {{HTTPHeader("Content-Security-Policy")}} Header
- {{CSP("report-to")}} Directive
