---
week: 7
title: API — concept
goal: je begrijpt wat een API is, wat een client, server en endpoint zijn en welke HTTP-methoden er zijn
accent: sky
summary: Een API laat applicaties met elkaar communiceren via HTTP en JSON. Je leert wat een client, een server en een endpoint zijn, welke HTTP-methoden er zijn (GET, POST, PUT, DELETE) en waarom moderne systemen een API tussen de client en de database zetten.
leeruitkomsten:
  - Ik kan uitleggen wat een API, een client, een server en een endpoint zijn
  - Ik ken de HTTP-methoden GET, POST, PUT en DELETE en wat ze doen
  - Ik kan uitleggen waarom een API tussen de client en de database staat
---

## 7.1 Inleiding

In week 3 en 4 heb je geleerd hoe je gegevens in een C#-app op kunt slaan in een database, maar er zijn nog meer manieren om gegevens op te slaan en uit te wisselen met andere apps: API's.

## 7.2 Wat is een API?

Een API, of **Application Programming Interface**, is een set van protocollen, routines en tools die softwareapplicaties in staat stellen met elkaar te communiceren.

In eenvoudigere woorden dient een API als een tussenpersoon tussen verschillende softwaresystemen, waardoor ze gegevens en instructies kunnen uitwisselen. Het definieert de regels en standaarden voor hoe applicaties met elkaar kunnen communiceren en specificeert de soorten verzoeken en antwoorden die zijn toegestaan.

De API is vaak actief op de **server** en de applicatie die de API aanroept noemen we de **client**. Een client kan een webpagina zijn die *in JavaScript* via `fetch` de API aanroept. Het kan ook een C#-applicatie zijn die gebruik maakt van de `HttpClient`-klasse om de API aan te roepen.

Het "aanroepen van een API" is simpelweg het laden van een bijzondere webpagina. Wat de webpagina bijzonder maakt is dat deze geen HTML en CSS bevat, maar 'JSON' (of XML). Vrijwel alle programmeertalen en systemen kunnen JSON begrijpen en omzetten naar objecten in code. Daarmee kunnen we code laten reageren op gegevens die in JSON genoteerd zijn.

![Handgetekend diagram: een CLIENT stuurt via HTTP (GET, POST, DELETE, PUT) en een URL (/surveys, /surveys/123) een verzoek naar de SERVER, die met JSON terugantwoordt](./assets/rest-api-diagram.jpg)

<p style="text-align:center"><em>Bron: <a href="https://mannhowie.com/rest-api">https://mannhowie.com/rest-api</a></em></p>

In het bovenstaande plaatje zien we dat de **client** via de methodes GET, POST, DELETE of PUT een verzoek kan doen naar een bepaalde URL. Die URL is een weblocatie op een **server**. Er zijn verschillende URL's die verschillende acties uitvoeren; we noemen dat ook wel **API routes** of **endpoints**.

Bijvoorbeeld:

| Methode | Route / Endpoint | Beschrijving |
|---|---|---|
| GET | `/surveys` | Geeft alle enquêtes terug |
| GET | `/surveys/123` | Geeft de enquête terug met survey_id '123' |
| POST | `/surveys` | Voegt een enquête toe aan de server. De inhoud van het POST-verzoek moet een JSON-object zijn met daarin de gegevens van de enquête. |
| DELETE | `/surveys/123` | Verwijdert de enquête met survey_id '123' |

Een ander voorbeeld: stel dat je een weer-app ontwikkelt die informatie over de actuele weersomstandigheden nodig heeft. In plaats van je eigen meteorologische meetinstrumenten op verschillende locaties in Nederland te installeren, kun je de API van een weerprovider gebruiken om de benodigde gegevens in realtime op te halen.

Door een API te gebruiken, kun je tijd en middelen besparen door de functionaliteit van bestaande systemen te benutten, en het kan ook de algehele prestaties en schaalbaarheid van je applicatie verbeteren.

## 7.3 Moderne systemen

In de vorige module verbond je client-app rechtstreeks met de MySQL-database. Bij moderne systemen gebeurt dat meestal niet: de client stuurt een verzoek naar een **API**, en die API vormt de brug naar de database — ze ontvangt het verzoek, verwerkt het en praat namens de client met de database.

Dat heeft een paar voordelen:

- **Scheiding van verantwoordelijkheden** — de databaselogica zit achter de API, niet in de client. Onderdelen kun je zo makkelijker wijzigen of vervangen.
- **Gestandaardiseerde communicatie** — elke app kan met de API praten, ongeacht de gebruikte technologie.
- **Beveiliging** — de API kan per gebruiker of client bepalen wat wel en niet mag, zodat niet iedereen zomaar bij de database kan.

## 7.4 Voorbeelden

Netflix, Instagram en YouTube werken allemaal zo:

- **Netflix** — de website en app halen via API's gebruikersprofielen, aanbevelingen en film-/serie-informatie op bij de backend.
- **Instagram** — de app gebruikt API's om foto's te plaatsen en op te halen, gebruikers te volgen en de nieuwsfeed te tonen.
- **YouTube** — biedt API's waarmee ook externe ontwikkelaars video's kunnen zoeken, uploaden en afspeellijsten beheren.

Steeds is de API de tussenlaag tussen de client-app en de databases. In week 8 ga je zelf een API **consumeren** met `HttpClient`.

<x-koppelvraag>
prompt: Koppel elke HTTP-methode aan wat je ermee doet in een REST API.
pairs:
  - left: GET
    right: Gegevens ophalen
  - left: POST
    right: Nieuwe gegevens toevoegen
  - left: PUT
    right: Bestaande gegevens wijzigen
  - left: DELETE
    right: Gegevens verwijderen
</x-koppelvraag>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week7-oefeningen.html)
[Quiz](/pages/week7-meetmoment.html)
[Week 8](/pages/week8-theorie.html)
</x-nav>
