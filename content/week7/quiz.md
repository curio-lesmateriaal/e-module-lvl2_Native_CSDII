---
week: 7
title: Quiz Week 7 — API zelf bouwen
passScore: 70
questions:
  - id: w7q1
    question: Uit welke drie lagen bestaat een webapp meestal?
    options:
      - Database, backend, front-end
      - HTML, CSS, JavaScript
      - Client, router, switch
      - Model, view, controller
    correct: 0
    explanation: Database (gegevens), backend (het brein), front-end (wat de gebruiker ziet).
  - id: w7q2
    question: Waar draait de backend-code van een webapp?
    options:
      - In de browser
      - In de database
      - Op de server
      - Op de computer van de gebruiker
    correct: 2
    explanation: Alleen de front-end (HTML/CSS of JSON) komt bij de gebruiker terecht.
  - id: w7q3
    question: Wat betekent het dat HTTP 'stateless' is?
    options:
      - Er is geen internetverbinding nodig
      - Er kan maar één gebruiker tegelijk zijn
      - De server slaat niets op in de database
      - De server onthoudt tussen twee requests niet dat jij dezelfde persoon bent
    correct: 3
    explanation: Elke request staat op zichzelf; technieken die wél onthouden wie je bent heten stateful.
  - id: w7q4
    question: Welke class gebruik je in C# om een eenvoudige webserver te bouwen?
    options:
      - HttpListener
      - HttpClient
      - WebBrowser
      - TcpClient
    correct: 0
    explanation: HttpClient consumeert API's; HttpListener luistert naar binnenkomende verzoeken.
  - id: w7q5
    question: Wat doet listener.GetContext()?
    options:
      - Start de server
      - Stuurt het antwoord
      - Wacht tot er een verzoek binnenkomt
      - Sluit de verbinding
    correct: 2
    explanation: De methode blokkeert tot er een HTTP-verzoek binnenkomt, net als Console.ReadLine().
  - id: w7q6
    question: Waarom zet je je antwoordtekst om naar bytes voordat je het verstuurt?
    options:
      - Bytes zijn kleiner
      - Anders wordt het versleuteld
      - Dat hoeft niet
      - Een Stream verstuurt byte-voor-byte; tekst kun je niet zomaar sturen
    correct: 3
    explanation: "`Encoding.UTF8.GetBytes(...)` zet de string om; de ontvanger bouwt hem weer op met GetString."
  - id: w7q7
    question: "Wat is `request.Url.AbsolutePath` bij een bezoek aan `http://localhost:8080/test`?"
    options:
      - "http://localhost:8080/test"
      - "/test"
      - "test"
      - "localhost:8080"
    correct: 1
    explanation: AbsolutePath is alleen het pad-gedeelte van de URL.
  - id: w7q8
    question: "Wat zit er in `request.Url.Segments` bij `http://localhost:8080/user/1`?"
    options:
      - "Alleen ['user', '1']"
      - "['localhost', 'user', '1']"
      - "['/', '/user/', '1']"
      - "['user/1']"
    correct: 2
    explanation: Segments splitst het pad inclusief de slashes; het laatste segment ('1') gebruik je vaak als id.
---
