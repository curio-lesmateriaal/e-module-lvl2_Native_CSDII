---
week: 1
title: De grote bouwstenen
goal: je begrijpt wat CSS Grid is, wanneer je het gebruikt, en kunt een eenvoudige pagina-indeling maken
accent: indigo
leeruitkomsten:
  - "Ik weet wat display: grid doet"
  - Ik kan kolommen definiëren met grid-template-columns
  - Ik gebruik gap voor ruimte tussen grid-items
  - Ik kan een complete pagina-layout bouwen (header, nav, main, sidebar, footer)
---

## Welk probleem lossen we op?

Vroeger bouwden developers pagina's met **tables**, **floats** of **absolute positionering**. Dat werkte, maar was fragiel: één element verschuiven en de hele layout brak.

Moderne websites hebben een **voorspelbare structuur**: header bovenaan, menu, hoofdinhoud naast een sidebar, footer onderaan. CSS Grid is gemaakt om precies dit soort **tweedimensionale layouts** (rijen én kolommen) eenvoudig en onderhoudbaar te maken.

<x-callout>

**Onthoud:** Grid is voor de *grote indeling* van je pagina. Niet voor elk klein detail — daarvoor heb je Flexbox (zie hieronder).

</x-callout>

## Wat is CSS Grid?

CSS Grid is een layout-systeem waarmee je een **raster** definieert op een container. Je tekent onzichtbare lijnen (kolommen en rijen) en plaatst elementen in de cellen — of laat ze over meerdere cellen spannen.

```css
.pagina {
  display: grid;
  grid-template-columns: 1fr 200px;
  gap: 16px;
}
```

Met drie regels CSS heb je al twee kolommen en ruimte ertussen.

## Flexbox vs Grid — wanneer wat?

Beide zijn modern en worden vaak **gecombineerd**. Het verschil zit in de dimensie:

<x-compare>
<x-compare-item title="Flexbox — één richting">

Items staan in een **rij** of **kolom**. Ideaal voor componenten: een navigatiebalk, knoppen naast elkaar, een kaart met icoon + tekst.

```css
.nav {
  display: flex;
  gap: 1rem;
}
```

**Voorbeeld:** menu-items horizontaal naast elkaar.

</x-compare-item>
<x-compare-item title="Grid — twee richtingen">

Items staan in **rijen én kolommen** tegelijk. Ideaal voor pagina-layouts: header over de volle breedte, sidebar links, content rechts.

```css
.pagina {
  display: grid;
  grid-template-columns: 1fr 250px;
}
```

**Voorbeeld:** hele website-indeling in één grid.

</x-compare-item>
</x-compare>

| Situatie | Gebruik |
|---------|---------|
| Navigatie met 5 links | Flexbox |
| Hele pagina met header/footer | Grid |
| Knoppen centreren in een kaart | Flexbox |
| Fotomatrix / productoverzicht | Grid |

## Container en items

Het element met `display: grid` heet de **grid container**. Alleen de **directe kinderen** worden automatisch grid items.

```html
<div class="pagina">        <!-- GRID CONTAINER -->
  <header>Logo</header>       <!-- grid item -->
  <nav>Menu</nav>             <!-- grid item -->
  <main>Inhoud</main>         <!-- grid item -->
  <aside>Sidebar</aside>      <!-- grid item -->
  <footer>Contact</footer>    <!-- grid item -->
</div>
```

<x-callout type="warning">
Let op: een `div` *binnen* main is géén grid item — alleen directe kinderen van de container.
</x-callout>

## Belangrijke properties

**`display: grid`** — Zet het element aan als grid container. Zonder deze regel doen de andere grid-properties niets.

**`grid-template-columns`** — Bepaalt hoeveel kolommen en hoe breed. `1fr 200px` = één flexibele kolom + één vaste kolom van 200px. `fr` = fraction, een deel van de vrije ruimte.

**`grid-template-rows`** — Zelfde als kolommen, maar voor rijhoogtes. Vaak hoef je dit niet — rijen passen zich aan de inhoud aan.

**`gap`** — Ruimte tussen rijen en kolommen. Vervangt oude hacks met margins. `gap: 16px` of `row-gap` / `column-gap` apart.

## Voorbeeld: simpele pagina-layout

```
+----------------+
| Header         |
+----------------+
| Nav            |
+------+---------+
| Main | Sidebar |
+------+---------+
| Footer         |
+----------------+
```

```css
.pagina {
  display: grid;
  grid-template-columns: 1fr 200px;
  gap: 8px;
  min-height: 100vh;
}
```

In week 2 leer je met `grid-template-areas` elk onderdeel exact op de juiste plek zetten.

<x-card title="Wat je níet moet doen">

- Geen `float: left` voor pagina-layout
- Geen `position: absolute` om blokken naast elkaar te zetten
- Geen tables voor layout (alleen voor echte tabellen met data)

</x-card>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week1-oefeningen.html)
[Quiz](/pages/week1-meetmoment.html)
[Inleveropdracht](/pages/week1-inleveropdracht.html)
[Week 2](/pages/week2-theorie.html)
</x-nav>
