---
week: 10
title: API — van elkaar uitlezen
goal: je kunt met HttpClient je eigen API consumeren — een GET-verzoek doen en de lijst tonen, en met een POST-verzoek nieuwe gegevens versturen
accent: fuchsia
summary: "In week 9 bouwde je een server, in week 8 leerde je een API consumeren. Deze week zet je beide samen: je schrijft een client die je eigen API uitleest met GET en er data naartoe stuurt met POST. Server en client draaien samen als één systeem."
leeruitkomsten:
  - Ik begrijp het verschil tussen een API die data serveert (server) en een app die data gebruikt (client)
  - Ik kan met HttpClient een GET-verzoek doen naar mijn eigen API en het antwoord deserialiseren naar een List
  - Ik kan met HttpClient een POST-verzoek doen met een JSON-body
  - Ik kan de statuscode en het antwoord van een POST-verzoek uitlezen
---

## 10.1 Inleiding

In week 9 heb je een **server** gebouwd met `HttpListener` die routes afhandelt. In week 8 leerde je een API **consumeren** met `HttpClient`. Deze week zet je die twee samen: je schrijft een **client** die je *eigen* API uitleest.

De server serveert data, de client gebruikt die. Samen vormen ze één systeem: je start de server (een console-app), en daarnaast draait de client (een tweede console-app, en later een WinUI-app).

## 10.2 Je eigen API consumeren met GET

Een GET-verzoek naar je eigen server werkt precies zoals naar PokéAPI in week 8 — alleen is de URL nu `http://localhost:8080/...`:

```csharp
var client = new HttpClient();
var response = await client.GetAsync("http://localhost:8080/all");
string json = await response.Content.ReadAsStringAsync();

var options = new JsonSerializerOptions { PropertyNameCaseInsensitive = true };
List<Car> cars = JsonSerializer.Deserialize<List<Car>>(json, options);

foreach (var car in cars)
{
    Console.WriteLine($"{car.Brand} {car.Model}");
}
```

De klasse `Car` in je client is (bijna) dezelfde als in je server-project — de JSON die de server verstuurt moet immers in de client weer een object worden.

## 10.3 Data versturen met POST

Bij een GET vraag je alleen om data. Bij een **POST** stuur je zelf inhoud mee: de JSON van het object dat toegevoegd moet worden. Die JSON maak je met `JsonSerializer.Serialize` en verpak je in een `StringContent`:

```csharp
var nieuweCar = new Car { Brand = "Mazda", Model = "CX-5" };

string body = JsonSerializer.Serialize(nieuweCar);
var content = new StringContent(body, Encoding.UTF8, "application/json");

var response = await client.PostAsync("http://localhost:8080/add", content);
```

<x-callout type="note">

`Encoding.UTF8` en `"application/json"` vertellen de server: dit is JSON-tekst. Zonder dat weet de server niet hoe hij de body moet lezen.

</x-callout>

<x-keuzevraag>
question: Waarom heeft een POST-verzoek een body en een GET niet?
options:
  - Dat is toeval, het mag allebei
  - Bij GET vraag je alleen om data; bij POST stuur je zelf gegevens mee die opgeslagen moeten worden
  - Een GET-body wordt door de browser geblokkeerd
  - POST is sneller
correct: 1
explanation: GET = ophalen (geen inhoud nodig). POST = toevoegen, dus je stuurt de nieuwe gegevens als request body mee.
</x-keuzevraag>

## 10.4 De response lezen

Na een POST wil je weten of het gelukt is. Dat lees je af aan de **statuscode**:

```csharp
if (response.IsSuccessStatusCode)
{
    string antwoord = await response.Content.ReadAsStringAsync();
    Car aangemaakt = JsonSerializer.Deserialize<Car>(antwoord, options);
    Console.WriteLine($"Toegevoegd met Id {aangemaakt.Id}");
}
else
{
    Console.WriteLine($"Mislukt: {response.StatusCode}");
}
```

`IsSuccessStatusCode` is `true` bij een code in de 200-reeks (bijv. `200 OK` of `201 Created`). Bij `400`, `404` of `500` is het `false`.

<x-invul>
prompt: Vul de regels aan die het nieuwe object als JSON-body naar de API sturen.
code: |-
  string body = JsonSerializer.Serialize(nieuweCar);
  var content = new ___(body, Encoding.UTF8, "application/json");
  var response = await client.___("http://localhost:8080/add", content);
blanks:
  - answer: StringContent
  - answer: PostAsync
explanation: "StringContent verpakt je JSON-tekst; PostAsync verstuurt het verzoek met die inhoud."
</x-invul>

## 10.5 Client én server samen draaien

Om te testen heb je **twee** apps tegelijk nodig:

1. Start eerst je **server** uit week 9 (die blijft draaien en wacht op verzoeken).
2. Start daarnaast je **client**. Die doet een GET of POST naar `http://localhost:8080/...`.

<x-callout type="tip">

Handig tijdens het bouwen: test je server-routes eerst los in de **browser** (voor GET) of met een API-testtool zoals **Postman of Insomnia**. Werkt de route daar? Dan weet je dat een fout in je client zit, niet in je server.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week10-oefeningen.html)
[Quiz](/pages/week10-meetmoment.html)
[Week 11](/pages/week11-theorie.html)
</x-nav>
