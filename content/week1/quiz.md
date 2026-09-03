---
week: 1
title: Quiz Week 1 — Pagina indelen
passScore: 70
questions:
  - id: w1q1
    question: Waarvoor gebruik je CSS Grid vooral?
    options:
      - Tekst kleuren instellen
      - Animaties maken
      - Tweedimensionale pagina-layouts (rijen én kolommen)
      - Alleen navigatiebalken
    correct: 2
    explanation: Grid is bedoeld voor layouts in twee richtingen tegelijk.
  - id: w1q2
    question: Wanneer kies je Flexbox in plaats van Grid?
    options:
      - Voor een complete pagina-indeling
      - Voor componenten in één richting (bijv. menu-items in een rij)
      - Nooit, Grid is altijd beter
      - Alleen op mobiel
    correct: 1
    explanation: Flexbox = één dimensie. Grid = pagina-layout.
  - id: w1q3
    question: Welke property activeert CSS Grid op een element?
    options:
      - "grid: on"
      - "layout: grid"
      - "position: grid"
      - "display: grid"
    correct: 3
    explanation: "display: grid maakt het element een grid container."
  - id: w1q4
    question: "Wat doet grid-template-columns: 1fr 200px?"
    options:
      - Een flexibele kolom en een vaste kolom van 200px
      - Twee rijen
      - 200 kolommen
      - Alleen gap instellen
    correct: 0
    explanation: 1fr deelt vrije ruimte, 200px is een vaste breedte.
  - id: w1q5
    question: Wat is een grid item?
    options:
      - "Het element met display: grid"
      - Elk element op de pagina
      - Een direct kind van de grid container
      - Alleen een div
    correct: 2
    explanation: Alleen directe kinderen van de container worden grid items.
  - id: w1q6
    question: Welk CSS-snippet maakt twee gelijke kolommen?
    preview:
      css: ".demo { display: grid; grid-template-columns: 1fr 1fr; gap: 4px; } .demo >
        div { padding: 12px; background: #71717a; color: white; text-align:
        center; }"
      html: <div class="demo"><div>1</div><div>2</div></div>
    options:
      - "display: flex;"
      - "float: left;"
      - "display: grid; grid-template-columns: 1fr 1fr;"
      - "grid-template-rows: 2;"
    correct: 2
    explanation: grid-template-columns met twee 1fr-kolommen deelt de ruimte gelijk.
  - id: w1q7
    question: Waarom gebruik je geen floats voor pagina-layout?
    options:
      - Floats zijn deprecated
      - Floats zijn voor tekstomloop, niet voor structurele layouts
      - Floats werken niet in Chrome
      - Floats zijn trager
    correct: 1
    explanation: Grid is gemaakt voor betrouwbare pagina-indelingen.
  - id: w1q8
    question: Wat doet de gap property?
    options:
      - Padding binnen items
      - Buitenmarge van de body
      - Ruimte tussen grid-items
      - Border-radius
    correct: 2
    explanation: gap bepaalt de ruimte tussen rijen en kolommen.
---
