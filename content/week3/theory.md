---
week: 3
title: Responsieve grids
goal: je bouwt responsive grids met repeat, minmax en media queries
accent: emerald
leeruitkomsten:
  - Ik gebruik repeat() in grid-definities
  - Ik begrijp minmax() en wanneer ik het gebruik
  - Ik ken het verschil tussen auto-fit en auto-fill
  - Ik combineer media queries met CSS Grid
---

## Layouts die meebewegen

Vaste kolommen breken op kleine schermen. Met **repeat()**, **minmax()** en **media queries** maak je grids die zich aanpassen aan elke viewport.

<x-callout>
Doel: op desktop meerdere kolommen, op mobiel één kolom — zonder HTML te wijzigen.
</x-callout>

## Responsive tools

**`repeat(n, 1fr)`** — Herhaalt een kolom- of rij-definitie. `repeat(3, 1fr)` = drie gelijke kolommen.

**`minmax(min, max)`** — Kolommen minimaal X breed, maximaal Y. Bijv. `minmax(200px, 1fr)` — nooit smaller dan 200px.

**`auto-fit` vs `auto-fill`** — `auto-fit` vouwt lege tracks in; `auto-fill` behoudt ze. Meestal kies je `auto-fit` voor kaartenrasters.

## Het klassieke kaartenraster

```css
.cards {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
}
```

Kolommen breken automatisch af wanneer er niet genoeg ruimte is — geen media query nodig voor het basisraster.

## Media queries combineren

Voor complexere layouts (sidebar verbergen, areas herschikken) combineer je Grid met `@media`.

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
}

@media (max-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
  }
}
```

<x-callout>
Wijzig alleen de grid-definitie in de media query — de HTML blijft hetzelfde.
</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week3-oefeningen.html)
[Quiz](/pages/week3-meetmoment.html)
[Inleveropdracht](/pages/week3-inleveropdracht.html)
[Week 4](/pages/week4-theorie.html)
</x-nav>
