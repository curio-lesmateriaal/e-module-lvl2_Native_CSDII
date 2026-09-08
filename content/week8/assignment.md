---
week: 8
title: De Sleutel — API op de database met validatie
subtitle: Inleveropdracht Week 8 (eindopdracht-basis)
client: Autoverhuur De Sleutel
maxPoints: 16
deliverables:
  - Een API (HttpListener-console-app) die zijn data uit de database haalt via EF Core
  - GET-routes voor de lijst en voor één item, en een POST-route om toe te voegen
  - Validatie op de POST-invoer (if-statements of Data Annotations) met een [RegularExpression] op minstens één veld
  - Screenshots van de routes (browser of Thunder Client / Postman), inclusief een geweigerde invoer
criteria:
  - id: w8h1
    text: "GET /voertuigen haalt de lijst op via de DbContext (db.Voertuigen.ToList())"
    points: 3
  - id: w8h2
    text: "GET /voertuigen/{id} haalt één voertuig uit de database; onbekend id geeft 404"
    points: 3
  - id: w8h3
    text: "POST /voertuigen leest de body via InputStream, deserialiseert de JSON en slaat op met SaveChanges"
    points: 3
  - id: w8h4
    text: De POST-invoer wordt gevalideerd; ongeldige invoer wordt geweigerd met een duidelijke JSON-foutmelding en status 400
    points: 3
  - id: w8h5
    text: Minstens één veld heeft een [RegularExpression] (bijv. kenteken of postcode) met een eigen ErrorMessage
    points: 2
  - id: w8h6
    text: Alle antwoorden zijn geldige JSON met Content-Type application/json
    points: 1
  - id: w8h7
    text: De code is opgedeeld in methoden/routes; geen copy-paste van de verzendlogica
    points: 1
tips:
  - Hergebruik je StuurJson-helper uit week 7 voor alle antwoorden, ook de foutmeldingen.
  - Test de POST met Thunder Client (VS Code) of Postman — een browser kan alleen GET.
  - Begin met de GET-routes werkend op de database, voeg daarna pas POST + validatie toe.
  - Dit project is de basis voor je eindopdracht in de bufferweken — bouw het netjes op.
---

Alle losse onderdelen komen nu samen. De Sleutel wil één API die door alle toekomstige apps gebruikt kan worden: de balie-app, een klantwebsite en later misschien een mobiele app. Die API praat met de database en bewaakt dat er geen onzin in komt.

Bouw voort op je API van week 7. Vervang de hardcoded lijst door echte databasegegevens: `GET /voertuigen` en `GET /voertuigen/{id}` halen hun data op via de `DeSleutelContext`. Voeg een `POST /voertuigen` toe die de request-body uitleest via de `InputStream`, de JSON deserialiseert naar een `Voertuig`, de gegevens **valideert** (kies if-statements óf Data Annotations) en bij goedkeuring opslaat met `SaveChanges`. Zet op minstens één veld een `[RegularExpression]` — bijvoorbeeld een kenteken-formaat of een postcode. Weiger ongeldige invoer met status 400 en een JSON-foutmelding die vertelt wat er mis is.

## Inleveren

Lever je project (als `.zip`, zonder `bin/` en `obj/`) met de screenshots in via **Itslearning**, onder de map "Module: Native (C#)". Dit project vormt de basis voor je eindopdracht in de buffer- en toetsweken.
