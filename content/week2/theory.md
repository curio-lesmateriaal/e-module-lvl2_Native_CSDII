---
week: 2
title: Rijen, kolommen en gebieden
goal: je kunt onderdelen bewust plaatsen binnen een grid met areas en spanning
accent: violet
leeruitkomsten:
  - Ik kan rijen instellen met grid-template-rows
  - Ik kan grid-template-areas gebruiken met namen
  - Ik laat items spannen over meerdere kolommen/rijen
  - Ik plaats items met grid-column en grid-row
---

## Van automatisch naar bewust plaatsen

In week 1 liet je Grid items automatisch in volgorde vallen. Nu **bepaal jij** waar elk onderdeel staat — met rijen, named areas en spanning over meerdere cellen.

<x-callout>
Denk aan Grid als een plattegrond: je tekent kamers (areas) en wijst elk element een kamer toe.
</x-callout>

## Nieuwe properties

**`grid-template-rows`** — Definieert rijhoogtes, bijvoorbeeld `auto 1fr auto` voor header, flexibele content en footer.

**`grid-template-areas`** — Geeft elke cel een naam. Je tekent een ASCII-plattegrond met strings als `"header header"`.

**`grid-column` / `grid-row`** — Plaats een item op specifieke lijnen, bijv. `grid-column: 1 / 3` (span 2 kolommen).

## grid-template-areas in actie

```
"header header"
"nav    main"
"footer footer"
```

```css
.pagina {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-areas:
    "header header"
    "nav    main"
    "footer footer";
  gap: 12px;
}

header { grid-area: header; }
nav    { grid-area: nav; }
main   { grid-area: main; }
footer { grid-area: footer; }
```

Elke rij heeft evenveel namen als er kolommen zijn. Herhaal een naam om te spannen.

## Spanning zonder areas

Soms wil je één item over meerdere kolommen zonder areas. Gebruik dan `grid-column: span 2` of lijnnummers.

```css
.hero {
  grid-column: 1 / -1; /* volle breedte */
}

.feature {
  grid-column: span 2;
}
```

<x-callout>
`-1` is de laatste gridlijn — handig voor full-width secties.
</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week2-oefeningen.html)
[Quiz](/pages/week2-meetmoment.html)
[Inleveropdracht](/pages/week2-inleveropdracht.html)
[Week 3](/pages/week3-theorie.html)
</x-nav>
