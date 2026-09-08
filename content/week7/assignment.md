---
week: 7
title: De Sleutel — de eerste eigen API
subtitle: Inleveropdracht Week 7
client: Autoverhuur De Sleutel
maxPoints: 13
deliverables:
  - Een console-app die met HttpListener op een poort luistert
  - Minstens drie routes die JSON teruggeven
  - Screenshot van de routes in de browser (of in een tool zoals Postman / Thunder Client)
criteria:
  - id: w7h1
    text: De server start met HttpListener op een ingestelde poort en blijft draaien (lus rond GetContext)
    points: 3
  - id: w7h2
    text: Er is een route GET /voertuigen die een JSON-lijst teruggeeft
    points: 3
  - id: w7h3
    text: Er is een route GET /voertuigen/{id} die één voertuig teruggeeft (id uit de URL gehaald)
    points: 3
  - id: w7h4
    text: Onbekende routes geven een net antwoord (bijv. status 404 of een JSON-foutmelding)
    points: 2
  - id: w7h5
    text: Het antwoord wordt correct omgezet naar bytes, ContentLength64 gezet en de OutputStream gesloten
    points: 1
  - id: w7h6
    text: De Content-Type van het antwoord staat op application/json
    points: 1
tips:
  - Voor nu mag je de voertuigenlijst nog hardcoderen (bijv. een `List<Voertuig>` in het geheugen). In week 8 koppel je EF Core.
  - Gebruik `JsonSerializer.Serialize(lijst)` om je objecten naar JSON-tekst om te zetten.
  - Zet een `while (true)`-lus om `listener.GetContext()` zodat de server meerdere verzoeken kan afhandelen.
---

De Sleutel wil dat straks meerdere apps (de balie, een klantwebsite, misschien een mobiele app) dezelfde gegevens kunnen gebruiken. Daarvoor bouw je nu zelf een kleine API-server: een console-app die op een poort luistert en op verzoeken antwoordt met JSON.

Bouw met `HttpListener` een webserver die luistert op bijvoorbeeld `http://localhost:8080/`. Handel minstens drie routes af: `GET /voertuigen` (alle voertuigen als JSON-lijst), `GET /voertuigen/{id}` (één voertuig, waarbij je het id uit `request.Url.Segments` of `AbsolutePath` haalt), en een nette afhandeling voor onbekende routes. De voertuigenlijst mag je voor nu nog hardcoderen. Zet je antwoord om naar bytes, stel `ContentLength64` en de `Content-Type` (`application/json`) in en sluit de `OutputStream`.

## Inleveren

Lever je project (als `.zip`, zonder `bin/` en `obj/`) met de screenshots in via **Itslearning**, onder de map "Module: Native (C#)".
