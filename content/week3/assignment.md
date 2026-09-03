---
week: 3
title: StyleGrid — de webshop gaat live
subtitle: Inleveropdracht Week 3
client: StyleGrid Vintage
maxPoints: 11
deliverables:
  - index.html met productkaarten (minimaal 6)
  - styles.css met responsive grid
  - "Drie screenshots: desktop, tablet en mobiel (browser devtools mag)"
criteria:
  - id: w3h1
    text: "Desktop: 4 producten naast elkaar"
    points: 2
  - id: w3h2
    text: "Tablet: 2 kolommen via media query"
    points: 2
  - id: w3h3
    text: "Mobiel: 1 kolom via media query"
    points: 2
  - id: w3h4
    text: repeat() is gebruikt in grid-template-columns
    points: 2
  - id: w3h5
    text: gap zorgt voor consistente ruimte tussen kaarten
    points: 1
  - id: w3h6
    text: Kaarten zien er uit als echte producttegels (border, padding of schaduw)
    points: 2
tips:
  - Test met de viewport-knoppen in de browser (F12 → responsive mode).
  - Breakpoints hoeven niet exact 900 en 500 te zijn, maar moeten logisch zijn.
  - "Optioneel: probeer auto-fit met minmax() als extra uitdaging."
---

StyleGrid verkoopt vintage kleding online. De eigenaar merkt dat 70% van de bezoekers via hun telefoon komt, maar de productpagina toont nog steeds vier kolommen op elk scherm — op mobiel zijn de kaarten veel te klein. Jij maakt de productpagina responsive met CSS Grid.

Bouw een productoverzicht met minstens 6 productkaarten. Op desktop: 4 kolommen. Op tablet (max 900px): 2 kolommen. Op mobiel (max 500px): 1 kolom. Gebruik media queries en repeat().
