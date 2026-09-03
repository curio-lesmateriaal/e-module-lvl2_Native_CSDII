---
week: 3
title: Quiz Week 3 — Responsieve grids
passScore: 70
questions:
  - id: w3q1
    question: Wat doet repeat(4, 1fr)?
    options:
      - 4 kolommen die de ruimte gelijk verdelen
      - 4 rijen
      - Herhaal de animatie 4 keer
      - 4px gap
    correct: 0
    explanation: repeat(4, 1fr) maakt vier gelijke kolommen.
  - id: w3q2
    question: Wat doet minmax(200px, 1fr)?
    options:
      - Exact 200px breed
      - Alleen op desktop
      - Minimaal 200px, maximaal een deel van de vrije ruimte
      - Verbergt kleine schermen
    correct: 2
    explanation: minmax stelt een minimum en maximum in voor een track.
  - id: w3q3
    question: Hoeveel kolommen heeft dit grid?
    preview:
      css: ".demo { display: grid; grid-template-columns: repeat(3, 1fr); gap: 4px; }
        .demo > div { padding: 10px; background: #52525b; color: white;
        text-align: center; font-size: 12px; }"
      html: <div class="demo"><div>1</div><div>2</div><div>3</div></div>
    options:
      - "2"
      - "3"
      - "4"
      - "6"
    correct: 1
    explanation: repeat(3, 1fr) definieert 3 kolommen.
  - id: w3q4
    question: Wat is het verschil tussen auto-fit en auto-fill?
    options:
      - Geen verschil
      - auto-fit klapt lege tracks in, auto-fill behoudt ze
      - auto-fill is alleen voor mobiel
      - auto-fit is voor rijen
    correct: 1
    explanation: auto-fit laat items de beschikbare ruimte vullen.
  - id: w3q5
    question: Welke code maakt 2 kolommen op tablet?
    options:
      - "@media (max-width: 900px) { .grid { grid-template-columns: repeat(2,
        1fr); } }"
      - ".grid { columns: 2; }"
      - "@media (max-width: 900px) { .grid { display: block; } }"
      - "grid-template-columns: tablet;"
    correct: 0
    explanation: Media queries met aangepaste grid-template-columns is de standaard aanpak.
  - id: w3q6
    question: Welk patroon hoort bij een webshop op mobiel?
    options:
      - 4 kolommen op alle schermen
      - Alleen Flexbox op mobiel
      - 4 kolommen desktop → 2 tablet → 1 mobiel
      - Grid uitzetten op mobiel
    correct: 2
    explanation: Breakpoints met steeds minder kolommen is het klassieke responsive
      grid-patroon.
  - id: w3q7
    question: Welk CSS-snippet past het beste bij automatisch wrappende productkaarten?
    options:
      - "grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));"
      - "grid-template-columns: 250px;"
      - "float: left; width: 25%;"
      - "display: flex; flex-wrap: nowrap;"
    correct: 0
    explanation: auto-fit + minmax is populair voor flexibele kaartgrids.
  - id: w3q8
    question: Waarom combineer je media queries met Grid?
    options:
      - Dat kan niet
      - Om het aantal kolommen aan te passen per schermbreedte
      - Alleen voor kleuren
      - Om Grid te vervangen door tables
    correct: 1
    explanation: Responsive layout = andere grid-definitie per breakpoint.
---
