---
title: "ARIA: landmark-Rolle"
slug: Web/Accessibility/ARIA/Reference/Roles/landmark_role
l10n:
  sourceCommit: ec98716dfe71c78db3f82ee3b1b9e7f68997fa19
---

Ein Landmark ist ein wichtiger Unterabschnitt einer Seite. Die `landmark`-Rolle ist eine abstrakte Superklasse für die ARIA-Rollenwerte für Inhaltsabschnitte, die so wichtig sind, dass Benutzer wahrscheinlich direkt zu ihnen navigieren möchten.

> [!NOTE]
> Die `landmark`-Rolle ist eine [abstrakte Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles#6._abstract_roles). Sie wird hier der Vollständigkeit halber dokumentiert. Sie sollte nicht von Web-Autoren verwendet werden.

## Beschreibung

Ein `landmark` ist eine abstrakte Rolle für einen Inhaltsabschnitt, der so wichtig ist, dass Benutzer wahrscheinlich leicht zu dem Abschnitt navigieren möchten und dieser in eine dynamisch generierte Zusammenfassung der Seite aufgenommen wird. Landmarks ermöglichen es unterstützenden Technologien, Inhalte schnell zu navigieren und zu finden.

Um eine Landmark-Rolle zu erstellen, definieren Sie den Zweck des Inhalts, indem Sie ein semantisches Element wie `<section>`, `<nav>` oder `<main>` verwenden oder eine ARIA-Rolle hinzufügen, die eine Unterklasse der `landmark`-Rolle ist, wie zum Beispiel [`role="banner"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/banner_role), [`role="complementary"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/complementary_role) oder [`role="region"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/region_role). Verwenden Sie nicht `role="landmark"`.

Ein sichtbares Label sollte bereitgestellt und mit [`aria-labelledby`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-labelledby) referenziert werden. Falls erforderlich, kann ein kurzes, beschreibendes Label mit [`aria-label`](/de/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-label) bereitgestellt werden.

Für Benutzer von Bildschirmlesern schaffen Landmark-Rollen effektiv 'Skip-Links' für diese Benutzer, ersetzen jedoch nicht die Seitennavigation, da die Landmark-Rollen sonst nicht sichtbar sind.

## Best Practices

Verwenden Sie nicht `role="landmark"`. Verwenden Sie HTML und Unterklassen-Landmark-Rollen.

Landmarks stellen sicher, dass Inhalte in navigierbaren Regionen sind. Verwenden Sie {{HTMLElement('main')}} für [`role="main"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/main_role), {{HTMLElement('header')}} für [`role="banner"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/banner_role), {{HTMLElement('nav')}} für [`role="navigation"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/navigation_role) und {{HTMLElement('footer')}} für [`role="contentinfo"`](/de/docs/Web/Accessibility/ARIA/Reference/Roles/contentinfo_role). Es ist auch eine gute Praxis, die Rolle redundant mit dem zugehörigen semantischen Element einzuschließen. Es ist weniger gute Praxis, nicht-semantische Elemente wie {{HTMLElement('div')}} zu verwenden und Semantik mit Landmark-Rollen hinzuzufügen. Aber verwenden Sie entweder das eine, das andere oder beides. Andernfalls ist Ihr Inhalt für Benutzer von Bildschirmlesern nicht mehr so navigierbar.

## Spezifikationen

{{Specifications}}

## Siehe auch

- [ARIA: `section`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/section_role)
- [ARIA: `banner`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/banner_role)
- [ARIA: `complementary`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/complementary_role)
- [ARIA: `contentinfo`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/contentinfo_role)
- [ARIA: `form`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/form_role)
- [ARIA: `main`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/main_role)
- [ARIA: `navigation`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/navigation_role)
- [ARIA: `region`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/region_role)
- [ARIA: `search`-Rolle](/de/docs/Web/Accessibility/ARIA/Reference/Roles/search_role)
- [Verwendung von HTML-Landmark-Rollen zur Verbesserung der Zugänglichkeit](/en-US/blog/aria-accessibility-html-landmark-roles/) im MDN-Blog (2023)
