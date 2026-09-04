---
week: 5
title: De Sleutel — koppeling met de RDW-API
subtitle: Inleveropdracht Week 5
client: Autoverhuur De Sleutel
maxPoints: 12
deliverables:
  - Een console-app die een externe API aanroept met HttpClient
  - Minstens één C#-class die overeenkomt met de JSON van die API
  - Screenshot van de console met de opgehaalde en gedeserialiseerde gegevens
criteria:
  - id: w5h1
    text: Main is async (async Task Main) en HttpClient wordt correct gebruikt
    points: 2
  - id: w5h2
    text: Het JSON-antwoord wordt als string opgehaald met ReadAsStringAsync
    points: 2
  - id: w5h3
    text: Er is een class die de structuur van de JSON weerspiegelt (juiste types)
    points: 3
  - id: w5h4
    text: De JSON wordt gedeserialiseerd met JsonSerializer.Deserialize en PropertyNameCaseInsensitive
    points: 3
  - id: w5h5
    text: Minstens één genest object of lijst uit de JSON wordt correct uitgelezen
    points: 1
  - id: w5h6
    text: Ongeldige of lege antwoorden geven een nette melding
    points: 1
tips:
  - Kun je niet bij een RDW-API? Gebruik PokéAPI of jsonplaceholder.typicode.com — het gaat om de techniek.
  - Bekijk eerst de JSON in je browser (broncode) en teken de class-structuur op papier.
  - Test met één vast kenteken/id voordat je gebruikersinvoer toevoegt.
---

De Sleutel wil bij het invoeren van een nieuw voertuig niet meer alles met de hand typen. Als de baliemedewerker een kenteken invoert, moeten merk en type automatisch worden opgehaald uit een externe bron. Zo'n bron is een API.

Bouw een console-app die met `HttpClient` een externe API aanroept (bijvoorbeeld de open voertuig-API van de RDW, PokéAPI, of `jsonplaceholder.typicode.com`). Haal het JSON-antwoord op als string, maak een C#-class (of meerdere) die overeenkomt met de structuur van die JSON, en deserialiseer het antwoord naar een object met `PropertyNameCaseInsensitive = true`. Lees minstens één genest veld of lijst uit en print een paar velden netjes in de console. Zorg dat de app niet crasht als de API niets of iets onverwachts teruggeeft.

## Inleveren

Lever je project (als `.zip`, zonder `bin/` en `obj/`) met de screenshot in via **Itslearning**, onder de map "Module: Native (C#)".
