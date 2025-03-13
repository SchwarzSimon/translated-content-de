---
title: "Permissions-Policy: browsing-topics"
slug: Web/HTTP/Reference/Headers/Permissions-Policy/browsing-topics
l10n:
  sourceCommit: 4d929bb0a021c7130d5a71a4bf505bcb8070378d
---

{{HTTPSidebar}}{{SeeCompatTable}}{{non-standard_header}}

Die HTTP {{HTTPHeader("Permissions-Policy")}}-Header-Direktive `browsing-topics` steuert den Zugriff auf die [Topics API](/de/docs/Web/API/Topics_API).

Falls eine Richtlinie die Nutzung der Topics API ausdrücklich verbietet, werden alle Versuche, die Methode [`Document.browsingTopics()`](/de/docs/Web/API/Document/browsingTopics) aufzurufen oder eine Anfrage mit einem {{httpheader("Sec-Browsing-Topics")}}-Header zu senden, mit einem `NotAllowedError`-[`DOMException`](/de/docs/Web/API/DOMException) fehlschlagen.

## Syntax

```http
Permissions-Policy: browsing-topics=<allowlist>;
```

- `<allowlist>`
  - : Eine Liste von Ursprüngen, für die die Berechtigung zur Nutzung des Features erteilt wird. Siehe [`Permissions-Policy` > Syntax](/de/docs/Web/HTTP/Reference/Headers/Permissions-Policy#syntax) für weitere Details.

## Standardrichtlinie

Die Standard-Allowlist für `browsing-topics` ist `*`.

## Spezifikationen

Dieses Feature ist kein Teil eines offiziellen Standards, wird jedoch im [Topics API Unofficial Proposal Draft](https://patcg-individual-drafts.github.io/topics/) spezifiziert.

## Browser-Kompatibilität

{{Compat}}

## Siehe auch

- {{HTTPHeader("Permissions-Policy")}}-Header
- [Permissions Policy](/de/docs/Web/HTTP/Guides/Permissions_Policy)
- [Topics API](/de/docs/Web/API/Topics_API)
- [`Document.browsingTopics()`](/de/docs/Web/API/Document/browsingTopics)
