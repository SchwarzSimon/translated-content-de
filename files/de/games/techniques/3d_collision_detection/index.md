---
title: 3D-Kollisionsdetektion
slug: Games/Techniques/3D_collision_detection
l10n:
  sourceCommit: 702cd9e4d2834e13aea345943efc8d0c03d92ec9
---

{{GamesSidebar}}

Dieser Artikel bietet eine Einführung in die verschiedenen Volumentechniken, die zur Implementierung der Kollisionsdetektion in 3D-Umgebungen verwendet werden. Folgeartikel werden Implementierungen in spezifischen 3D-Bibliotheken behandeln.

## Achsen-ausgerichtete Begrenzungsrahmen

Wie bei der Kollisionsdetektion in 2D sind **achsen-ausgerichtete Begrenzungsrahmen** (AABB) der schnellste Algorithmus, um festzustellen, ob zwei Spielelemente überlappen oder nicht. Dies besteht darin, Spielelemente in einem nicht-rotierenden (also achsen-ausgerichteten) Rahmen zu umhüllen und die Position dieser Rahmen im 3D-Koordinatenraum zu überprüfen, um zu sehen, ob sie sich überschneiden.

![Zwei dreidimensionale, nicht quadratische Objekte, die im Raum schweben und von virtuellen rechteckigen Boxen umhüllt sind.](screen_shot_2015-10-16_at_15.11.21.png)

Die **achsen-ausgerichtete Einschränkung** besteht aus Leistungsgründen. Der Überlappungsbereich zwischen zwei nicht-rotierenden Boxen kann nur mit logischen Vergleichen überprüft werden, während rotierende Boxen zusätzliche trigonometrische Operationen erfordern, die langsamer zu berechnen sind. Wenn Sie Elemente haben, die sich drehen werden, können Sie entweder die Dimensionen des Begrenzungsrahmens anpassen, sodass er das Objekt immer noch umhüllt, oder Sie entscheiden sich für einen anderen Begrenzungstyp wie Kugeln (die rotationsinvariant sind). Das unten gezeigte animierte GIF zeigt ein grafisches Beispiel eines AABB, der seine Größe anpasst, um das rotierende Element zu umschließen. Der Rahmen ändert ständig seine Dimensionen, um das innenliegende Element eng zu umschließen.

![Animierter rotierender Knoten zeigt, wie die virtuelle rechteckige Box schrumpft und wächst, während der Knoten in ihr rotiert. Die Box dreht sich nicht.](rotating_knot.gif)

> [!NOTE]
> Lesen Sie den Artikel [Begrenzungsvolumen mit Three.js](/de/docs/Games/Techniques/3D_collision_detection/Bounding_volume_collision_detection_with_THREE.js), um eine praktische Implementierung dieser Technik zu sehen.

### Punkt vs. AABB

Zu überprüfen, ob ein Punkt innerhalb eines AABB liegt, ist ziemlich einfach — wir müssen nur prüfen, ob die Koordinaten des Punktes innerhalb des AABB liegen, indem wir jede Achse separat betrachten. Wenn wir annehmen, dass _P<sub>x</sub>_, _P<sub>y</sub>_ und _P<sub>z</sub>_ die Koordinaten des Punktes sind und _B<sub>minX</sub>_–_B<sub>maxX</sub>_, _B<sub>minY</sub>_–_B<sub>maxY</sub>_ und _B<sub>minZ</sub>_–_B<sub>maxZ</sub>_ die Bereiche jeder Achse des AABB sind, können wir mit der folgenden Formel berechnen, ob eine Kollision zwischen den beiden stattgefunden hat:

<!-- prettier-ignore-start -->
<math display="block">
  <semantics><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>P</mi><mo>,</mo><mi>B</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><msub><mi>P</mi><mi>x</mi></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>X</mi></mrow></msub><mo>∧</mo><msub><mi>P</mi><mi>x</mi></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>X</mi></mrow></msub><mo stretchy="false">)</mo><mo>∧</mo><mo stretchy="false">(</mo><msub><mi>P</mi><mi>y</mi></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Y</mi></mrow></msub><mo>∧</mo><msub><mi>P</mi><mi>y</mi></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Y</mi></mrow></msub><mo stretchy="false">)</mo><mo>∧</mo><mo stretchy="false">(</mo><msub><mi>P</mi><mi>z</mi></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Z</mi></mrow></msub><mo>∧</mo><msub><mi>P</mi><mi>z</mi></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Z</mi></mrow></msub><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">f(P, B)= (P_x \ge B_{minX} \wedge P_x \le B_{maxX}) \wedge (P_y \ge B_{minY} \wedge P_y \le B_{maxY}) \wedge (P_z \ge B_{minZ} \wedge P_z \le B_{maxZ})</annotation></semantics>
</math>
<!-- prettier-ignore-end -->

Oder in JavaScript:

```js
function isPointInsideAABB(point, box) {
  return (
    point.x >= box.minX &&
    point.x <= box.maxX &&
    point.y >= box.minY &&
    point.y <= box.maxY &&
    point.z >= box.minZ &&
    point.z <= box.maxZ
  );
}
```

### AABB vs. AABB

Zu überprüfen, ob ein AABB mit einem anderen AABB überschneidet, ist dem Punkt-Test ähnlich. Wir müssen nur einen Test pro Achse durchführen, indem wir die Grenzen der Boxen verwenden. Das unten stehende Diagramm zeigt den Test, den wir über die X-Achse durchführen würden — im Wesentlichen, überschneiden sich die Bereiche _A<sub>minX</sub>_–_A<sub>maxX</sub>_ und _B<sub>minX</sub>_–_B<sub>maxX</sub>_?

![Handzeichnung von zwei Rechtecken, die zeigen, dass die obere rechte Ecke von A die untere linke Ecke von B überlappt, da A's größter x-Wert größer als B's kleinster x-Wert ist.](aabb_test.png)

Mathematisch würde dies so aussehen:

<!-- prettier-ignore-start -->
<math display="block">
  <semantics><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>A</mi><mo>,</mo><mi>B</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>X</mi></mrow></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>X</mi></mrow></msub><mo>∧</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>X</mi></mrow></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>X</mi></mrow></msub><mo stretchy="false">)</mo><mo>∧</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Y</mi></mrow></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Y</mi></mrow></msub><mo>∧</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Y</mi></mrow></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Y</mi></mrow></msub><mo stretchy="false">)</mo><mo>∧</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Z</mi></mrow></msub><mo>≤</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Z</mi></mrow></msub><mo>∧</mo><msub><mi>A</mi><mrow><mi>m</mi><mi>a</mi><mi>x</mi><mi>Z</mi></mrow></msub><mo>≥</mo><msub><mi>B</mi><mrow><mi>m</mi><mi>i</mi><mi>n</mi><mi>Z</mi></mrow></msub><mo stretchy="false">)</mo></mrow><annotation encoding="TeX">f(A, B) = (A_{minX} \le B_{maxX} \wedge A_{maxX} \ge B_{minX}) \wedge ( A_{minY} \le B_{maxY} \wedge A_{maxY} \ge B_{minY}) \wedge (A_{minZ} \le B_{maxZ} \wedge A_{maxZ} \ge B_{minZ})</annotation></semantics>
</math>
<!-- prettier-ignore-end -->

Und in JavaScript würden wir das so schreiben:

```js
function intersect(a, b) {
  return (
    a.minX <= b.maxX &&
    a.maxX >= b.minX &&
    a.minY <= b.maxY &&
    a.maxY >= b.minY &&
    a.minZ <= b.maxZ &&
    a.maxZ >= b.minZ
  );
}
```

## Begrenzungskugeln

Die Verwendung von Begrenzungskugeln zur Kollisionsdetektion ist etwas komplexer als AABB, aber immer noch relativ schnell zu testen. Der Hauptvorteil von Kugeln ist, dass sie rotationsinvariant sind, sodass die Begrenzungskugel gleich bleibt, wenn das umhüllte Objekt rotiert. Der Hauptnachteil ist, dass, es sei denn, das umhüllte Objekt ist tatsächlich kugelförmig, die Umhüllung normalerweise nicht gut passt (z.B. wird eine Person mit einer Begrenzungskugel abgewickelt viele falsche Positive hervorrufen, während AABB besser passen würde).

### Punkt vs. Kugel

Um zu prüfen, ob eine Kugel einen Punkt enthält, müssen wir den Abstand zwischen dem Punkt und dem Mittelpunkt der Kugel berechnen. Wenn dieser Abstand kleiner oder gleich dem Radius der Kugel ist, liegt der Punkt innerhalb der Kugel.

![Handzeichnung einer 2D-Projektion einer Kugel und eines Punktes in einem kartesischen Koordinatensystem. Der Punkt liegt rechts unten außerhalb des Kreises. Die Distanz ist durch eine gestrichelte Linie, die mit D gekennzeichnet ist, vom Mittelpunkt des Kreises zum Punkt markiert. Eine hellere Linie zeigt den Radius, labeled R, vom Mittelpunkt des Kreises bis zur Grenze des Kreises.](point_vs_sphere.png)

Unter Berücksichtigung, dass der euklidische Abstand zwischen zwei Punkten _A_ und _B_ <math><semantics><msqrt><mrow><mo stretchy="false">(</mo><msub><mi>A</mi><mi>x</mi></msub><mo>−</mo><msub><mi>B</mi><mi>x</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mi>y</mi></msub><mo>−</mo><msub><mi>B</mi><mi>y</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mi>z</mi></msub><mo>−</mo><msub><mi>B</mi><mi>z</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup></mrow></msqrt><annotation encoding="TeX">\sqrt{(A_x - B_x)^2 + (A_y - B_y)^2 + (A_z - B_z)^2}</annotation></semantics></math> ist, würde unsere Formel für die Kollisionsdetektion Punkt vs. Kugel so aussehen:

<!-- prettier-ignore-start -->
<math display="block">
  <semantics><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>P</mi><mo>,</mo><mi>S</mi><mo stretchy="false">)</mo><mo>=</mo><msub><mi>S</mi><mrow><mi>r</mi><mi>a</mi><mi>d</mi><mi>i</mi><mi>u</mi><mi>s</mi></mrow></msub><mo>≥</mo><msqrt><mo stretchy="false">(</mo><msub><mi>P</mi><mi>x</mi></msub><mo>−</mo><msub><mi>S</mi><mi>x</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>P</mi><mi>y</mi></msub><mo>−</mo><msub><mi>S</mi><mi>y</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>P</mi><mi>z</mi></msub><mo>−</mo><msub><mi>S</mi><mi>z</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup></msqrt></mrow><annotation encoding="TeX">f(P,S) = S_{radius} \ge \sqrt{(P_x - S_x)^2 + (P_y - S_y)^2 + (P_z - S_z)^2}</annotation></semantics>
</math>
<!-- prettier-ignore-end -->

Oder in JavaScript:

```js
function isPointInsideSphere(point, sphere) {
  // we are using multiplications because is faster than calling Math.pow
  const distance = Math.sqrt(
    (point.x - sphere.x) * (point.x - sphere.x) +
      (point.y - sphere.y) * (point.y - sphere.y) +
      (point.z - sphere.z) * (point.z - sphere.z),
  );
  return distance < sphere.radius;
}
```

> [!NOTE]
> Der obige Code enthält eine Quadratwurzel, die teuer in der Berechnung sein kann. Eine einfache Optimierung besteht darin, sie zu vermeiden, indem die quadratische Distanz mit dem quadratischen Radius verglichen wird, sodass die optimierte Gleichung stattdessen `distanceSqr < sphere.radius * sphere.radius` verwenden würde.

### Kugel vs. Kugel

Der Kugel-gegen-Kugel-Test ähnelt dem Punkt-gegen-Kugel-Test. Was wir hier testen müssen, ist, dass der Abstand zwischen den Mittelpunkten der Kugeln kleiner oder gleich der Summe ihrer Radien ist.

![Handzeichnung von zwei teilweise überlappenden Kreisen. Jeder Kreis (unterschiedlicher Größen) hat eine helle Linienradius, die von seinem Mittelpunkt bis zur Grenze verläuft, gekennzeichnet als R. Der Abstand ist durch eine gepunktete Linie markiert, die mit D gekennzeichnet ist, die die Mittelpunkte beider Kreise verbindet.](sphere_vs_sphere.png)

Mathematisch sieht das so aus:

<!-- prettier-ignore-start -->
<math display="block">
  <semantics><mrow><mi>f</mi><mo stretchy="false">(</mo><mi>A</mi><mo>,</mo><mi>B</mi><mo stretchy="false">)</mo><mo>=</mo><msqrt><mo stretchy="false">(</mo><msub><mi>A</mi><mi>x</mi></msub><mo>−</mo><msub><mi>B</mi><mi>x</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mi>y</mi></msub><mo>−</mo><msub><mi>B</mi><mi>y</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup><mo>+</mo><mo stretchy="false">(</mo><msub><mi>A</mi><mi>z</mi></msub><mo>−</mo><msub><mi>B</mi><mi>z</mi></msub><msup><mo stretchy="false">)</mo><mn>2</mn></msup></msqrt><mo>≤</mo><msub><mi>A</mi><mrow><mi>r</mi><mi>a</mi><mi>d</mi><mi>i</mi><mi>u</mi><mi>s</mi></mrow></msub><mo>+</mo><msub><mi>B</mi><mrow><mi>r</mi><mi>a</mi><mi>d</mi><mi>i</mi><mi>u</mi><mi>s</mi></mrow></msub></mrow><annotation encoding="TeX">f(A,B) = \sqrt{(A_x - B_x)^2 + (A_y - B_y)^2 + (A_z - B_z)^2} \le A_{radius} + B_{radius}</annotation></semantics>
</math>
<!-- prettier-ignore-end -->

Oder in JavaScript:

```js
function intersect(sphere, other) {
  // we are using multiplications because it's faster than calling Math.pow
  const distance = Math.sqrt(
    (sphere.x - other.x) * (sphere.x - other.x) +
      (sphere.y - other.y) * (sphere.y - other.y) +
      (sphere.z - other.z) * (sphere.z - other.z),
  );
  return distance < sphere.radius + other.radius;
}
```

### Kugel vs. AABB

Zu testen, ob eine Kugel und ein AABB kollidieren, ist etwas komplizierter, bleibt aber einfach und schnell. Ein logischer Ansatz wäre, jeden Scheitelpunkt des AABB zu prüfen und für jeden einen Punkt-gegen-Kugel-Test durchzuführen. Das ist jedoch übertrieben — alle Scheitelpunkte zu testen ist unnötig, da wir den Abstand vom nächsten Punkt des AABB (nicht unbedingt ein Scheitelpunkt) zum Mittelpunkt der Kugel berechnen können, um zu prüfen, ob er kleiner oder gleich dem Radius der Kugel ist. Dieser Wert kann durch Clamping des Mittelpunkts der Kugel an die Grenzen des AABB erhalten werden.

![Handzeichnung eines Quadrats, das teilweise den oberen Teil eines Kreises überlappt. Der Radius ist durch eine helle Linie markiert, gekennzeichnet als R. Die Distanzlinie geht vom Mittelpunkt des Kreises zum nächsten Punkt des Quadrats.](sphere_vs_aabb.png)

In JavaScript würden wir diesen Test so durchführen:

```js
function intersect(sphere, box) {
  // get box closest point to sphere center by clamping
  const x = Math.max(box.minX, Math.min(sphere.x, box.maxX));
  const y = Math.max(box.minY, Math.min(sphere.y, box.maxY));
  const z = Math.max(box.minZ, Math.min(sphere.z, box.maxZ));

  // this is the same as isPointInsideSphere
  const distance = Math.sqrt(
    (x - sphere.x) * (x - sphere.x) +
      (y - sphere.y) * (y - sphere.y) +
      (z - sphere.z) * (z - sphere.z),
  );

  return distance < sphere.radius;
}
```

## Die Verwendung einer Physik-Engine

**3D-Physik-Engines** bieten Kollisionsdetektionsalgorithmen, von denen die meisten ebenfalls auf Begrenzungsvolumen basieren. Eine Physik-Engine funktioniert, indem sie einen **physischen Körper** erstellt, der üblicherweise an eine visuelle Darstellung davon angehängt wird. Dieser Körper hat Eigenschaften wie Geschwindigkeit, Position, Drehung, Drehmoment, etc., und auch eine **physische Form**. Diese Form wird in den Kollisionsberechnungen berücksichtigt.

Wir haben eine [Live-Kollisionsdemonstration](https://mozdevs.github.io/gamedev-js-3d-aabb/physics.html) (mit [Quellcode](https://github.com/mozdevs/gamedev-js-3d-aabb)) vorbereitet, die Sie sich ansehen können, um solche Techniken in Aktion zu sehen — diese verwendet die Open-Source 3D-Physik-Engine [cannon.js](https://github.com/schteppe/cannon.js).

## Siehe auch

Verwandte Artikel auf MDN:

- [Kollisionsdetektion von Begrenzungsvolumina mit Three.js](/de/docs/Games/Techniques/3D_collision_detection/Bounding_volume_collision_detection_with_THREE.js)
- [2D-Kollisionsdetektion](/de/docs/Games/Techniques/2D_collision_detection)

Externe Ressourcen:

- [Einfache Schnitttests für Spiele](https://www.gamedeveloper.com/game-platforms/simple-intersection-tests-for-games) auf Game Developer
- [Begrenzungsvolumen](https://en.wikipedia.org/wiki/Bounding_volume) auf Wikipedia
