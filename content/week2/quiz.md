---
week: 2
title: Quiz Week 2 — Rijen, kolommen en gebieden
passScore: 70
questions:
  - id: w2q1
    question: Wat doet grid-template-rows?
    options:
      - Bepaalt de hoogte van rijen
      - Bepaalt kolombreedtes
      - Voegt rijen toe aan HTML
      - Verbergt rijen
    correct: 0
    explanation: grid-template-rows definieert rijhoogtes, net als columns voor breedtes.
  - id: w2q2
    question: Wat is grid-template-areas?
    options:
      - Een JavaScript functie
      - Een visuele manier om gebieden namen te geven
      - Een lijst van HTML-klassen
      - Een media query
    correct: 1
    explanation: Je tekent je layout met benoemde strings per rij.
  - id: w2q3
    question: Hoe laat je een item over 2 kolommen spannen?
    options:
      - "width: 200%"
      - "float: left"
      - "span: 2"
      - "grid-column: 1 / 3 of via grid-template-areas"
    correct: 3
    explanation: grid-column of een area die twee kolomnamen beslaat.
  - id: w2q4
    question: Welk item spant over 2 kolommen in dit grid?
    preview:
      css: '.demo { display: grid; grid-template-columns: 1fr 1fr 1fr;
        grid-template-areas: "wide wide side"; gap: 4px; } .wide { grid-area:
        wide; background: #52525b; padding: 14px; color: white; text-align:
        center; } .side { grid-area: side; background: #a1a1aa; padding: 14px;
        color: white; text-align: center; }'
      html: <div class="demo"><div class="wide">Breed</div><div
        class="side">Smal</div></div>
    options:
      - Het smalle item
      - Het brede item (wide)
      - Beide
      - Geen
    correct: 1
    explanation: '"wide wide side" laat wide twee kolommen beslaan.'
  - id: w2q5
    question: "Wat doet grid-area: header op een element?"
    options:
      - Maakt een header-tag aan
      - Stelt hoogte in
      - Verbergt het item
      - Plaatst het item in het gebied 'header'
    correct: 3
    explanation: grid-area koppelt het item aan een naam uit grid-template-areas.
  - id: w2q6
    question: Welke grid-template-areas hoort bij een header over de volle breedte
      (2 kolommen)?
    preview:
      css: '.demo { display: grid; grid-template-columns: 1fr 1fr;
        grid-template-areas: "head head" "a b"; gap: 4px; } .head { grid-area:
        head; background: #3f3f46; color: white; padding: 10px; text-align:
        center; } .a { grid-area: a; background: #71717a; color: white; padding:
        10px; text-align: center; } .b { grid-area: b; background: #a1a1aa;
        color: white; padding: 10px; text-align: center; }'
      html: <div class="demo"><div class="head">H</div><div class="a">A</div><div
        class="b">B</div></div>
    options:
      - '"head head" "a b"'
      - '"head a" "head b"'
      - '"a head" "b head"'
      - '"head" "a" "b"'
    correct: 0
    explanation: 'De header moet beide kolommen beslaan: "head head".'
  - id: w2q7
    question: "Wat betekent grid-column: 1 / -1?"
    options:
      - Alleen de eerste kolom
      - Verberg het element
      - Van de eerste tot de laatste kolomlijn
      - Eén pixel breed
    correct: 2
    explanation: -1 is altijd de laatste gridlijn — ideaal voor full-width headers.
  - id: w2q8
    question: "In een nieuws-layout: hoe geef je aan dat artikel D twee kolommen
      breed is?"
    options:
      - '"d e e" op de laatste rij'
      - '"d d e" op de laatste rij in grid-template-areas'
      - "width: 200% op D"
      - "grid-row: 2"
    correct: 1
    explanation: 'Herhaal de area-naam d op twee kolommen: "d d e".'
---
