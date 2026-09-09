---
week: 11
title: Quiz Week 11 — API + EF Core (data aanleveren)
passScore: 70
questions:
  - id: w11q1
    question: Hoe geeft je API nu de voertuigenlijst terug?
    options:
      - Uit de database via de DbContext (bijv. db.Voertuigen.ToList())
      - Vanuit een hardcoded List in je code
      - Uit een tekstbestand
      - Rechtstreeks vanuit de browser
    correct: 0
    explanation: "De API is de brug: hij haalt de data met EF Core uit de database en serveert die als JSON."
  - id: w11q2
    question: Waar lees je de inhoud (body) van een POST-verzoek uit?
    options:
      - "context.Response.OutputStream"
      - "context.Request.Url"
      - "context.Response.ContentLength64"
      - "context.Request.InputStream"
    correct: 3
    explanation: De verzonden gegevens komen binnen via de InputStream van de Request.
  - id: w11q3
    question: Welke methode zet een C#-object (of lijst) om naar JSON-tekst voor je antwoord?
    options:
      - "JsonSerializer.Deserialize"
      - "JsonSerializer.Serialize"
      - "response.Write"
      - "ToString"
    correct: 1
    explanation: Serialize = object → tekst (voor je response). Deserialize = tekst → object (voor een binnenkomende body).
  - id: w11q4
    question: "Je wilt `/voertuigen/7` teruggeven of 404 als 7 niet bestaat. Wat gebruik je?"
    options:
      - "db.Voertuigen.ToList()"
      - "db.Voertuigen.FirstOrDefault(v => v.Id == id) en check op null"
      - "db.Voertuigen.Add(id)"
      - "db.Voertuigen.Remove(id)"
    correct: 1
    explanation: FirstOrDefault geeft het voertuig of null; is het null, dan zet je StatusCode 404.
  - id: w11q5
    question: Met welke twee regels sla je het gedeserialiseerde voertuig op?
    options:
      - "db.Voertuigen.Add(nieuw); db.SaveChanges();"
      - "db.Voertuigen.Add(nieuw);"
      - "db.SaveChanges();"
      - "db.Voertuigen.ToList();"
    correct: 0
    explanation: Add zet het klaar in de context; SaveChanges schrijft het echt naar de database.
  - id: w11q6
    question: Waarom stuur je bij een POST geen <code>Id</code> mee in de JSON?
    options:
      - Dat mag wel, het maakt niet uit
      - De database vult het Id zelf in via AUTO_INCREMENT
      - Id is verboden in JSON
      - Anders werkt Deserialize niet
    correct: 1
    explanation: De client kent het nieuwe Id nog niet; de database bepaalt dat bij het invoegen.
  - id: w11q7
    question: Welke HTTP-statuscode hoort bij een geslaagde POST die iets heeft aangemaakt?
    options:
      - "200 OK"
      - "201 Created"
      - "404 Not Found"
      - "500 Internal Server Error"
    correct: 1
    explanation: "201 Created betekent dat je verzoek is verwerkt en er een nieuwe resource is aangemaakt."
  - id: w11q8
    question: Wat is het risico als je de POST-body klakkeloos opslaat?
    options:
      - Er is geen risico
      - Je slaat mogelijk ongeldige of onzinnige gegevens op (leeg kenteken, negatieve prijs)
      - De database wordt trager
      - Je API stopt met werken
    correct: 1
    explanation: Daarom valideer je de invoer eerst — dat leer je in week 12.
---
