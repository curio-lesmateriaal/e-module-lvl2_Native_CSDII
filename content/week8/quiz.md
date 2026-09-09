---
week: 8
title: Quiz Week 8 — API uitlezen
passScore: 70
questions:
  - id: w8q1
    question: Welke klasse gebruik je in C# om een API aan te roepen?
    options:
      - WebRequest
      - HttpClient
      - ApiReader
      - JsonSerializer
    correct: 1
    explanation: "`HttpClient` is je onzichtbare browser: `client.GetAsync(url)` doet het verzoek."
  - id: w8q2
    question: Waarom moet je Main asynchroon maken (`async Task Main`) als je HttpClient gebruikt?
    options:
      - Omdat HttpClient alleen in Main werkt
      - Omdat GetAsync en ReadAsStringAsync asynchroon zijn en je op hun resultaat wacht met await
      - Omdat een console-app anders niet start
      - Dat hoeft niet
    correct: 1
    explanation: Een webverzoek kan lang duren; daarom zijn die methoden async en moet de omliggende methode dat ook zijn.
  - id: w8q3
    question: "Wat haal je op met `await response.Content.ReadAsStringAsync()`?"
    options:
      - De statuscode
      - De ruwe tekst (JSON) van het antwoord
      - Een lijst objecten
      - De URL
    correct: 1
    explanation: Je krijgt de body als string; daarna deserialiseer je die.
  - id: w8q4
    question: Wat is deserialiseren?
    options:
      - Van een object naar tekst
      - Van tekst naar een object
      - Een object verwijderen
      - Een object kopiëren
    correct: 1
    explanation: Deserialiseren = tekst (JSON) omzetten naar een C#-object. Serialiseren is andersom.
  - id: w8q5
    question: "In de JSON staat `\"name\"` (kleine letter), in C# heet je property `Name`. Wat heb je nodig?"
    options:
      - "JsonSerializerOptions met PropertyNameCaseInsensitive = true"
      - Je property hernoemen naar name
      - Niets, het werkt vanzelf
      - Een tweede class
    correct: 0
    explanation: Met die optie matcht de serializer hoofdletterongevoelig.
  - id: w8q6
    question: "Welk C#-type gebruik je voor een JSON-array `\"hobbies\": [\"a\", \"b\"]`?"
    options:
      - "string"
      - "List<string> (of string[])"
      - "int"
      - Een aparte class Hobbies
    correct: 1
    explanation: Een JSON-array van strings deserialiseer je naar een lijst of array van string.
  - id: w8q7
    question: "In de JSON zit `\"address\"` met daarin `street`, `city` en `state`. Hoe deserialiseer je dat?"
    options:
      - Als string
      - Met een aparte klasse Address die je als property-type gebruikt
      - Dat kan niet
      - Met een List<string>
    correct: 1
    explanation: Een genest JSON-object heeft een eigen klasse nodig; die zet je als het type van de property.
  - id: w8q8
    question: Waarvoor gebruik je een 'test-API' (mock)?
    options:
      - Om je client te testen terwijl de echte API nog niet bestaat
      - Om je database te vullen
      - Om sneller te compileren
      - Om JSON te vermijden
    correct: 0
    explanation: Een mock geeft vaste JSON terug zonder database; handig om je client alvast te bouwen en testen.
---
