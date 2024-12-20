---
title: "Testen Sie Ihre Fähigkeiten: Mathematik"
slug: Learn_web_development/Core/Scripting/Test_your_skills:_Math
l10n:
  sourceCommit: 5b20f5f4265f988f80f513db0e4b35c7e0cd70dc
---

{{learnsidebar}}

Ziel der Tests auf dieser Seite ist es, zu beurteilen, ob Sie den Artikel [Grundlagen der Mathematik in JavaScript — Zahlen und Operatoren](/de/docs/Learn_web_development/Core/Scripting/Math) verstanden haben.

> [!NOTE]
> Sie können die Lösungen in den interaktiven Editoren auf dieser Seite oder in einem Online-Editor wie [CodePen](https://codepen.io/), [JSFiddle](https://jsfiddle.net/) oder [Glitch](https://glitch.com/) ausprobieren.
> Wenn ein Fehler in Ihrem Code auftritt, wird dieser entweder im Ergebnisbereich dieser Seite oder in der JavaScript-Konsole protokolliert.
>
> Wenn Sie nicht weiterkommen, können Sie uns in einem unserer [Kommunikationskanäle](/de/docs/MDN/Community/Communication_channels) erreichen.

## Mathematik 1

Beginnen wir damit, Ihr Wissen über grundlegende mathematische Operatoren zu testen.
Sie werden vier numerische Werte erstellen, zwei davon addieren, einen von einem anderen subtrahieren und dann die Ergebnisse multiplizieren.
Abschließend müssen wir eine Überprüfung schreiben, die beweist, dass dieser Wert eine gerade Zahl ist.

Versuchen Sie, den Live-Code unten zu aktualisieren, um das fertige Beispiel nach diesen Schritten nachzubilden:

1. Erstellen Sie vier Variablen, die Zahlen enthalten. Geben Sie den Variablen sinnvolle Namen.
2. Addieren Sie die ersten beiden Variablen und speichern Sie das Ergebnis in einer anderen Variablen.
3. Subtrahieren Sie die vierte Variable von der dritten und speichern Sie das Ergebnis in einer anderen Variablen.
4. Multiplizieren Sie die Ergebnisse der Schritte **2** und **3** und speichern Sie das Ergebnis in einer Variablen namens `finalResult`.
5. Überprüfen Sie, ob `finalResult` eine gerade Zahl ist, indem Sie einen der [arithmetischen Operatoren](/de/docs/Learn_web_development/Core/Scripting/Math#arithmetic_operators) verwenden. Speichern Sie das Ergebnis (`0` für gerade, `1` für ungerade) in einer Variablen namens `evenOddResult`.

Um diesen Test zu bestehen, sollte `finalResult` einen Wert von `48` und `evenOddResult` einen Wert von `0` haben.

{{EmbedGHLiveSample("learning-area/javascript/introduction-to-js-1/tasks/math/math1.html", '100%', 400)}}

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/tasks/math/math1-download.html), um in Ihrem eigenen Editor oder in einem Online-Editor zu arbeiten.

## Mathematik 2

In der zweiten Aufgabe erhalten Sie zwei Berechnungen, deren Ergebnisse in den Variablen `result` und `result2` gespeichert werden.
Sie müssen die Berechnungen multiplizieren und das Ergebnis auf zwei Dezimalstellen formatieren.

Versuchen Sie, den Live-Code unten zu aktualisieren, um das fertige Beispiel nach diesen Schritten nachzubilden:

1. Multiplizieren Sie `result` und `result2` und weisen Sie das Ergebnis `result` erneut zu (verwenden Sie die Kurzschreibweise für die Zuweisung).
2. Formatieren Sie `result` so, dass es zwei Dezimalstellen hat, und speichern Sie es in einer Variablen namens `finalResult`.
3. Überprüfen Sie den Datentyp von `finalResult` mit `typeof`. Wenn es sich um einen `string` handelt, konvertieren Sie es in einen `number`-Typ und speichern Sie das Ergebnis in einer Variablen namens `finalNumber`.

Um diesen Test zu bestehen, sollte `finalNumber` einen Wert von `4633.33` ergeben.

{{EmbedGHLiveSample("learning-area/javascript/introduction-to-js-1/tasks/math/math2.html", '100%', 400)}}

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/tasks/math/math2-download.html), um in Ihrem eigenen Editor oder in einem Online-Editor zu arbeiten.

## Mathematik 3

In der letzten Aufgabe für diesen Artikel möchten wir, dass Sie einige Tests schreiben.
Es gibt drei Gruppen, die jeweils aus einer Aussage und zwei Variablen bestehen.
Für jede Gruppe schreiben Sie einen Test, der die gemachte Aussage beweist oder widerlegt.
Speichern Sie die Ergebnisse dieser Tests in Variablen namens `weightComparison`, `heightComparison` und `pwdMatch`.

{{EmbedGHLiveSample("learning-area/javascript/introduction-to-js-1/tasks/math/math3.html", '100%', 550)}}

> [!CALLOUT]
>
> [Laden Sie den Ausgangspunkt für diese Aufgabe herunter](https://github.com/mdn/learning-area/blob/main/javascript/introduction-to-js-1/tasks/math/math3-download.html), um in Ihrem eigenen Editor oder in einem Online-Editor zu arbeiten.
