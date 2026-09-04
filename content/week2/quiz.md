---
week: 2
title: Quiz Week 2 — Accessibility & static
passScore: 70
questions:
  - id: w2q1
    question: Wat bepaalt een access modifier (public, private, ...)?
    options:
      - Hoe snel de code draait
      - Wie er aan een field, property of methode mag zitten
      - In welke map het bestand staat
      - Of een class een constructor heeft
    correct: 1
    explanation: De modifier bepaalt de toegankelijkheid — wie de member mag lezen, wijzigen of aanroepen.
  - id: w2q2
    question: Een public field is toegankelijk voor...
    options:
      - Alleen het eigen object
      - Alleen sub classes
      - Alles en iedereen
      - Alleen code in dezelfde map
    correct: 2
    explanation: Elk object kan een public field lezen of wijzigen en elke public methode aanroepen.
  - id: w2q3
    question: Waarom kan het onverstandig zijn om de snelheid van een auto public te maken?
    options:
      - Public fields kosten meer geheugen
      - Andere objecten kunnen de interne toestand dan ongecontroleerd veranderen
      - Public werkt niet met classes
      - De compiler geeft dan een fout
    correct: 1
    explanation: Zonder methode eromheen kan iedereen de snelheid op bijv. -50 of 100000 zetten.
  - id: w2q4
    question: Een private member van een base class is...
    options:
      - Niet toegankelijk voor sub classes
      - Wel toegankelijk voor sub classes
      - Alleen toegankelijk binnen dezelfde assembly
      - Altijd ook static
    correct: 0
    explanation: Private betekent echt alleen het eigen object. Wil je het wél doorgeven aan sub classes, gebruik dan protected.
  - id: w2q5
    question: Wat is het verschil tussen internal en public?
    options:
      - Internal is alleen toegankelijk binnen dezelfde assembly (app)
      - Internal is sneller
      - Internal kan niet op methoden
      - Er is geen verschil
    correct: 0
    explanation: Internal lijkt op public, maar stopt bij de grens van je eigen assembly.
  - id: w2q6
    question: Welke modifier is als private, maar dan óók toegankelijk voor sub classes?
    options:
      - internal
      - static
      - protected
      - public
    correct: 2
    explanation: Protected = private + toegankelijk voor objecten van een sub class.
  - id: w2q7
    question: Wat betekent het als een field static is?
    options:
      - Het field kan niet meer veranderen
      - Het field is automatisch private
      - Het field wordt niet opgeslagen
      - Het field hoort bij de class, niet bij een los object
    correct: 3
    explanation: Een static field of methode is een eigenschap of mogelijkheid van de class zelf.
  - id: w2q8
    question: "Hoe roep je een static field `StandaardAantalWielen` van class `Auto` aan?"
    options:
      - "mijnAuto.StandaardAantalWielen"
      - "new Auto().StandaardAantalWielen"
      - "Auto.StandaardAantalWielen"
      - "static Auto.StandaardAantalWielen"
    correct: 2
    explanation: Static members spreek je aan via de class-naam, niet via een object.
---
