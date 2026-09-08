---
week: 7
title: Quiz Week 7 — API concept
passScore: 70
questions:
  - id: w7q1
    question: Waar staat API voor?
    options:
      - Advanced Programming Instruction
      - Application Programming Interface
      - Automatic Page Indexer
      - Application Process Integration
    correct: 1
    explanation: Een API is een set afspraken waarmee softwaresystemen met elkaar communiceren.
  - id: w7q2
    question: Wie is in een API-gesprek meestal de client?
    options:
      - De database
      - De applicatie die de API aanroept
      - De server waarop de API draait
      - De programmeur
    correct: 1
    explanation: De client roept aan; de server draait de API.
  - id: w7q3
    question: Wat krijg je meestal terug van een REST API in plaats van HTML/CSS?
    options:
      - JSON (of XML)
      - Een afbeelding
      - Een SQL-bestand
      - Een zip
    correct: 0
    explanation: Vrijwel elke taal kan JSON omzetten naar objecten in code.
  - id: w7q4
    question: "Wat doet het endpoint `GET /surveys/123`?"
    options:
      - Voegt enquête 123 toe
      - Verwijdert enquête 123
      - Geeft de enquête met id 123 terug
      - Geeft alle enquêtes terug
    correct: 2
    explanation: GET met een id in de route haalt dat ene item op.
  - id: w7q5
    question: Welke HTTP-methode gebruik je om nieuwe gegevens toe te voegen?
    options:
      - GET
      - POST
      - DELETE
      - HEAD
    correct: 1
    explanation: "GET = ophalen, POST = toevoegen, PUT = wijzigen, DELETE = verwijderen."
  - id: w7q6
    question: Wat is een 'endpoint'?
    options:
      - Het einde van je programma
      - Een specifieke URL op de server die een bepaalde actie uitvoert
      - De laatste regel JSON
      - De databaseverbinding
    correct: 1
    explanation: Elke route/endpoint (bijv. /surveys of /surveys/123) koppelt een URL + methode aan een actie.
  - id: w7q7
    question: Waarom zetten moderne systemen een API tussen de client en de database?
    options:
      - Het is verplicht van Microsoft
      - Scheiding van verantwoordelijkheden, gestandaardiseerde communicatie en toegangscontrole
      - Het maakt de database sneller
      - Zodat je geen JSON hoeft te gebruiken
    correct: 1
    explanation: De client praat met de API, de API met de database; de databaselogica en toegangscontrole zitten op één plek.
  - id: w7q8
    question: "Twee endpoints hebben dezelfde URL `/books` maar `GET` respectievelijk `POST`. Hoe weet de server wat te doen?"
    options:
      - Dat kan niet, URLs moeten uniek zijn
      - De server kijkt naar de HTTP-methode van het verzoek
      - Hij kiest willekeurig
      - De client stuurt een extra parameter mee
    correct: 1
    explanation: Route-afhandeling kijkt naar het pad én de methode (GET/POST/…).
---
