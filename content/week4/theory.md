---
week: 4
title: Eindproject
goal: je bouwt zelfstandig een complete, responsive layout met Grid en Flexbox
accent: amber
leeruitkomsten:
  - Ik kan zelfstandig een realistische layout bouwen
  - Ik combineer Grid en Flexbox waar nodig
  - Ik heb hover-effecten toegepast (optioneel)
  - Mijn eindproject werkt op meerdere schermgroottes
---

## Alles samenbrengen

In week 4 pas je alles toe: een **realistische pagina-layout** met header, navigatie, content, sidebar en footer. Grid voor de grote structuur, Flexbox voor componenten.

<x-callout>
Werk alsof je een echte klantpagina bouwt: semantische HTML, leesbare CSS, responsive gedrag.
</x-callout>

## Checklist voor je eindproject

- Grid container met duidelijke areas of kolommen
- Minstens één responsive breakpoint
- Flexbox voor navigatie of knoppenrij
- Consistente gap en spacing
- Werkt op mobiel én desktop

## Grid + Flexbox samen

Gebruik elk systeem waar het het beste past:

<x-compare>
<x-compare-item title="Grid — pagina-skelet">

Header over volle breedte, sidebar naast main, footer onderaan.

```css
.site {
  display: grid;
  grid-template-areas:
    "header"
    "main"
    "footer";
}
```

</x-compare-item>
<x-compare-item title="Flexbox — componenten">

Menu-items horizontaal, kaart met icoon + tekst, gecentreerde knoppen.

```css
.nav {
  display: flex;
  gap: 1rem;
  align-items: center;
}
```

</x-compare-item>
</x-compare>

## Optioneel: hover en polish

Hover-effecten op kaarten of knoppen maken je project professioneler. Houd het subtiel: `transition` + lichte schaduw of achtergrondkleur.

<x-nav label="Klaar met de module?">
[Oefeningen](/pages/week4-oefeningen.html)
[Inleveropdracht](/pages/week4-inleveropdracht.html)
[Checklist](/pages/checklist.html)
</x-nav>
