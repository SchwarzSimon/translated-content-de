---
title: "Testen Sie Ihre Fähigkeiten: WAI-ARIA"
slug: Learn_web_development/Core/Accessibility/WAI-ARIA_basics/Test_your_skills:_WAI-ARIA
l10n:
  sourceCommit: 5b20f5f4265f988f80f513db0e4b35c7e0cd70dc
---

{{learnsidebar}}

Ziel dieses Fähigkeitstests ist es, zu überprüfen, ob Sie unseren [WAI-ARIA Grundlagen](/de/docs/Learn_web_development/Core/Accessibility/WAI-ARIA_basics) Artikel verstanden haben.

> [!NOTE]
> Sie können Lösungen in den interaktiven Editoren auf dieser Seite oder in einem Online-Editor wie [CodePen](https://codepen.io/), [JSFiddle](https://jsfiddle.net/) oder [Glitch](https://glitch.com/) ausprobieren.
>
> Wenn Sie nicht weiterkommen, können Sie sich über einen unserer [Kommunikationskanäle](/de/docs/MDN/Community/Communication_channels) an uns wenden.

## WAI-ARIA 1

In unserer ersten ARIA-Aufgabe präsentieren wir Ihnen einen Abschnitt mit nicht-semantischem Markup, das offensichtlich als Liste gemeint ist. Angenommen, Sie können die verwendeten Elemente nicht ändern: Wie können Sie es Nutzern von Screenreadern ermöglichen, dies als Liste zu erkennen?

Versuchen Sie, den Live-Code unten zu aktualisieren, um das fertige Beispiel nachzubilden:

{{EmbedGHLiveSample("learning-area/accessibility/tasks/html-css/aria/aria1.html", '100%', 700)}}

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/accessibility/tasks/html-css/aria/aria1-download.html), um in Ihrem eigenen Editor oder einem Online-Editor zu arbeiten.

## WAI-ARIA 2

In unserer zweiten WAI-ARIA-Aufgabe präsentieren wir ein einfaches Suchformular und möchten, dass Sie einige WAI-ARIA-Funktionen hinzufügen, um dessen Zugänglichkeit zu verbessern:

1. Wie können Sie es ermöglichen, dass das Suchformular von Screenreadern als separates Landmark auf der Seite aufgerufen wird, um es leicht auffindbar zu machen?
2. Wie können Sie dem Sucheingabefeld ein geeignetes Label geben, ohne explizit ein sichtbares Textlabel in das DOM einzufügen?

Versuchen Sie, den Live-Code unten zu aktualisieren, um das fertige Beispiel nachzubilden:

{{EmbedGHLiveSample("learning-area/accessibility/tasks/html-css/aria/aria2.html", '100%', 700)}}

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/accessibility/tasks/html-css/aria/aria2-download.html), um in Ihrem eigenen Editor oder einem Online-Editor zu arbeiten.

## WAI-ARIA 3

Für diese letzte WAI-ARIA-Aufgabe kehren wir zu einem Beispiel zurück, das wir bereits im [CSS und JavaScript Fähigkeitstest](/de/docs/Learn_web_development/Core/Accessibility/CSS_and_JavaScript/Test_your_skills:_CSS_and_JavaScript_accessibility) gesehen haben.
Wie zuvor haben wir eine App, die eine Liste von Tiernamen präsentiert. Wenn Sie auf einen der Tiernamen klicken, erscheint eine weitere Beschreibung dieses Tieres in einem Feld unterhalb der Liste. Hier beginnen wir mit einer Maus- und Tastaturzugänglichen Version.

Das Problem, das wir jetzt haben, ist, dass Screenreader nicht erkennen können, was sich geändert hat, wenn das DOM geändert wird, um eine neue Beschreibung anzuzeigen. Können Sie es so aktualisieren, dass Änderungen der Beschreibung vom Screenreader angekündigt werden?

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/accessibility/tasks/js/aria/aria-js1-download.html), um in Ihrem eigenen Editor oder einem Online-Editor zu arbeiten.
