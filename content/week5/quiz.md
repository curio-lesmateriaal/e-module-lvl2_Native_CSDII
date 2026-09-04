---
week: 5
title: Quiz Week 5 — API concept & consumeren
passScore: 70
questions:
  - id: w5q1
    question: Waar staat API voor?
    options:
      - Advanced Programming Instruction
      - Application Programming Interface
      - Automatic Page Indexer
      - Application Process Integration
    correct: 1
    explanation: Een API is een set afspraken waarmee softwaresystemen met elkaar communiceren.
  - id: w5q2
    question: Wie is in een API-gesprek meestal de client?
    options:
      - De database
      - De applicatie die de API aanroept
      - De server waarop de API draait
      - De programmeur
    correct: 1
    explanation: De client roept aan; de server draait de API.
  - id: w5q3
    question: Wat krijg je meestal terug van een REST API in plaats van HTML/CSS?
    options:
      - JSON (of XML)
      - Een afbeelding
      - Een SQL-bestand
      - Een zip
    correct: 0
    explanation: Vrijwel elke taal kan JSON omzetten naar objecten in code.
  - id: w5q4
    question: "Wat doet het endpoint `GET /surveys/123`?"
    options:
      - Voegt enquête 123 toe
      - Verwijdert enquête 123
      - Geeft de enquête met id 123 terug
      - Geeft alle enquêtes terug
    correct: 2
    explanation: GET met een id in de route haalt dat ene item op.
  - id: w5q5
    question: Waarom moet je Main asynchroon maken (`async Task Main`) als je HttpClient gebruikt?
    options:
      - Omdat HttpClient alleen in Main werkt
      - Omdat GetAsync en ReadAsStringAsync asynchroon zijn en je op hun resultaat wacht met await
      - Omdat een console-app anders niet start
      - Dat hoeft niet
    correct: 1
    explanation: Een webverzoek kan lang duren; daarom zijn die methoden async en moet de omliggende methode dat ook zijn.
  - id: w5q6
    question: Wat is deserialiseren?
    options:
      - Van een object naar tekst
      - Van tekst naar een object
      - Een object verwijderen
      - Een object kopiëren
    correct: 1
    explanation: Deserialiseren = tekst (JSON) omzetten naar een C#-object. Serialiseren is andersom.
  - id: w5q7
    question: "In de JSON staat `\"name\"` (kleine letter), in C# heet je property `Name`. Wat heb je nodig?"
    options:
      - "JsonSerializerOptions met PropertyNameCaseInsensitive = true"
      - Je property hernoemen naar name
      - Niets, het werkt vanzelf
      - Een tweede class
    correct: 0
    explanation: Met die optie matcht de serializer hoofdletterongevoelig.
  - id: w5q8
    question: "Welk C#-type gebruik je voor een JSON-array `\"hobbies\": [\"a\", \"b\"]`?"
    options:
      - "string"
      - "List<string> (of string[])"
      - "int"
      - Een aparte class Hobbies
    correct: 1
    explanation: Een JSON-array van strings deserialiseer je naar een lijst of array van string.
---
