---
week: 10
title: Quiz Week 10 — API van elkaar uitlezen
passScore: 70
questions:
  - id: w10q1
    question: Wat is in dit systeem de server en wat de client?
    options:
      - De HttpListener-app serveert (server), de HttpClient-app gebruikt (client)
      - Andersom
      - Beide zijn server
      - Beide zijn client
    correct: 0
    explanation: De server luistert en antwoordt; de client doet verzoeken en verwerkt de antwoorden.
  - id: w10q2
    question: Welke URL gebruik je om je eigen, lokaal draaiende API aan te roepen?
    options:
      - "https://pokeapi.co/..."
      - "http://localhost:8080/..."
      - "file:///all"
      - "www.mijnapi.nl"
    correct: 1
    explanation: Je server draait op je eigen machine op de poort die je bij Prefixes.Add hebt ingesteld (8080).
  - id: w10q3
    question: Naar welk C#-type deserialiseer je het antwoord van <code>GET /all</code>?
    options:
      - "string"
      - "Car"
      - "List<Car>"
      - "int"
    correct: 2
    explanation: "/all geeft een JSON-array terug; die deserialiseer je naar een List<Car> (of Car[])."
  - id: w10q4
    question: Waarom heeft een POST-verzoek een body en een GET niet?
    options:
      - Toeval
      - Bij GET vraag je alleen om data; bij POST stuur je zelf gegevens mee die opgeslagen moeten worden
      - Een GET-body wordt geblokkeerd
      - POST is sneller
    correct: 1
    explanation: GET = ophalen (geen inhoud). POST = toevoegen, dus de nieuwe gegevens gaan als request body mee.
  - id: w10q5
    question: Hoe verpak je je JSON-tekst voor een POST-verzoek?
    options:
      - "new StringContent(body, Encoding.UTF8, \"application/json\")"
      - "new FileStream(body)"
      - "body.ToArray()"
      - "JsonSerializer.Deserialize(body)"
    correct: 0
    explanation: StringContent met UTF8 en het content-type "application/json" vertelt de server dat het JSON is.
  - id: w10q6
    question: Wat betekent <code>response.IsSuccessStatusCode == true</code>?
    options:
      - De statuscode zit in de 200-reeks (bijv. 200 of 201)
      - Het antwoord is leeg
      - De server is offline
      - De JSON is geldig
    correct: 0
    explanation: Bij 400/404/500 is het false; bij 200/201 true.
  - id: w10q7
    question: Je client geeft een foutmelding bij het verbinden. Wat check je eerst?
    options:
      - Of je database draait
      - Of je server (week 9) draait en op poort 8080 luistert
      - Of je internet hebt
      - Of Visual Studio geüpdatet is
    correct: 1
    explanation: Zonder draaiende server is er niets om verbinding mee te maken; test de route ook los in de browser of Postman.
  - id: w10q8
    question: Heeft de WinUI-client een database of EF Core nodig?
    options:
      - Ja, dezelfde als de server
      - Nee, de database zit aan de API-kant; de client praat alleen via HttpClient
      - Alleen Pomelo
      - Alleen voor GET
    correct: 1
    explanation: De client kent alleen de API; die praat op zijn beurt (vanaf week 11) met de database.
---
