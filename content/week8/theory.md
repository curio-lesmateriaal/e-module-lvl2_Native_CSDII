---
week: 8
title: API — uitlezen (consumeren)
goal: je kunt in C# een API aanroepen met HttpClient en het JSON-antwoord deserialiseren naar objecten, ook met lijsten en geneste objecten
accent: blue
summary: "Je weet nu wat een API is. Deze week ga je er één consumeren: met HttpClient haal je JSON op, en met JsonSerializer zet je die om naar C#-objecten. Je leert hoe JSON is opgebouwd (arrays, geneste objecten) en hoe je een tijdelijke nep-API opzet om je client te testen."
leeruitkomsten:
  - Ik kan met HttpClient een API aanroepen in een async methode
  - Ik kan de opbouw van een JSON-object lezen (eigenschappen, waarden, arrays, geneste objecten)
  - Ik kan JSON deserialiseren naar een C#-class, ook met lijsten en geneste objecten
  - Ik kan een tijdelijke nep-API (mock) opzetten om mijn client te testen
---

## 8.1 Een API aanroepen

Wanneer een client-applicatie een API gebruikt noemen we dat 'consumeren' (Engels: *to consume*). Het aanroepen van een API is simpelweg het laden van een bijzondere webpagina. Laten we eens kijken naar een voorbeeld: **PokéAPI** (<https://pokeapi.co/>).

![Het logo van PokéAPI](./assets/pokeapi-logo.png)

In onze lessen gebruiken we graag PokéAPI omdat het een gratis toegankelijke API is, waar geen bijzonderheden zijn qua authenticatie. Waar je bij de meeste API's moet registreren, kunnen we hier direct bij allerlei gegevens uit de Pokémon-games.

Neem bijvoorbeeld deze API-route: <https://pokeapi.co/api/v2/pokemon/ditto>

Wanneer je deze in de browser bezoekt, zie je de volgende JSON:

![Een browservenster op pokeapi.co/api/v2/pokemon/ditto met een grote hoeveelheid platte JSON-tekst](./assets/browser-json-ditto.png)

<x-callout type="tip">

Sommige browsers stijlen JSON met extra opmaak en functies. Open de broncode van de pagina om te zien wat de API daadwerkelijk teruggeeft (alleen tekst).

</x-callout>

Om een API te consumeren in C# gebruiken we de `HttpClient`-klasse. Dat geeft ons een soort onzichtbare browser waarmee we webverzoeken kunnen doen:

```csharp
var client = new HttpClient();
var response = await client.GetAsync("https://pokeapi.co/api/v2/pokemon/ditto");
var content = await response.Content.ReadAsStringAsync();
```

Omdat het doen van een webverzoek lang kan duren zijn enkele methodes hier **asynchroon (Async)**. Om die reden moet de methode waarin dit gebruikt wordt ook asynchroon zijn. Bij een Console App ziet een asynchrone `Main`-signature er zo uit:

```csharp
static async Task Main(string[] args)
```

Na de bovenstaande code staat in de `content`-variabele de JSON van de Pokémon genaamd "ditto". Dat JSON-object bevat allerlei informatie die we mogelijk willen ophalen, zoals bijvoorbeeld de id, naam en het gewicht van de Pokémon. Om die gegevens op te halen moeten we in C# een klasse maken die overeenkomt met de JSON:

<x-compare>
<x-compare-item title="JSON">

```json
{
  "id": 132,
  "name": "ditto",
  "weight": 40
}
```

</x-compare-item>
<x-compare-item title="Klasse die overeenkomt met JSON">

```csharp
internal class Pokemon
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Weight { get; set; }
}
```

</x-compare-item>
</x-compare>

Vervolgens kunnen we de JSON 'deserialiseren' naar een C#-object. Met deserialiseren bedoelen we: van tekst naar een object. Serialiseren is het tegenovergestelde: van een object naar tekst. Deserialiseren gaat als volgt:

```csharp
var options = new JsonSerializerOptions
{
    PropertyNameCaseInsensitive = true
};

var pokemon = JsonSerializer.Deserialize<Pokemon>(content, options);

Console.WriteLine("Gedeserialiseerde gegevens:");
Console.WriteLine(pokemon.Id);
Console.WriteLine(pokemon.Name);
```

<x-callout type="note">

De functie om te (de)serialiseren werkt dankzij `using System.Text.Json;`

</x-callout>

We geven aan de generieke methode `JsonSerializer.Deserialize<T>` het type van de klasse op de plek `T`. Zo weet de serializer welke eigenschappen er in de JSON verwacht kunnen worden. Omdat we de C#-conventies voor eigenschappen willen aanhouden (PascalCase), maar in de JSON "id", "name" en "weight" zonder hoofdletters zijn geschreven, zetten we met een optie hoofdletterongevoeligheid aan:

```csharp
var options = new JsonSerializerOptions
{
    PropertyNameCaseInsensitive = true
};
```

<x-invul>
prompt: Vul de regel aan die de JSON in `content` omzet naar een Pokemon-object (met de options voor hoofdletterongevoeligheid).
code: |-
  var pokemon = JsonSerializer.___<___>(content, options);
blanks:
  - answer: Deserialize
  - answer: Pokemon
explanation: "Deserialize<T> zet tekst om naar een object van type T."
</x-invul>

## 8.2 JSON en deserialiseren

JSON staat voor **JavaScript Object Notation** en het is een gestructureerd datatransmissieformaat dat veel wordt gebruikt voor het uitwisselen van gegevens tussen een server en een client. Het is leesbaar voor zowel mensen als computers.

JSON is opgebouwd uit eigenschappen en waarden en gebruikt een structuur die lijkt op een dictionary. Een JSON-object begint met een openingsaccolade `{` en eindigt met een sluitende accolade `}`. Tussen de accolades bevinden zich eigenschap-waarde-paren, gescheiden door een dubbele punt `:`.

Een eigenschap heeft een string-naam en kan een waarde van verschillende typen bevatten, zoals een tekenreeks, een getal, een boolean, een array of zelfs een ander JSON-object.

Hier is een voorbeeld van een JSON-object:

```json
{
  "name": "John Doe",
  "age": 25,
  "married": false,
  "hobbies": ["football", "reading", "traveling"],
  "address": {
    "street": "Main St",
    "city": "New York",
    "state": "NY"
  }
}
```

In dit voorbeeld zijn er 5 eigenschappen:

- "name" heeft een string als waarde
- "age" heeft een getal als waarde
- De waarde van "married" is van het type boolean
- "hobbies" heeft een array als waarde. Ieder item in deze array is van het type "string"
- "address" heeft een JSON-object als waarde, met 3 eigenschappen: "street", "city", "state"

Arrays herken je in JSON aan blokhaken. Daarnaast kun je door 'nesting' JSON-objecten in JSON-objecten hebben, en arrays in arrays of arrays in JSON-objecten.

Wanneer je een JSON-array als "hobbies" wilt deserialiseren geef je de eigenschap het type `List<T>`. Voor "hobbies" is `T` logischerwijs `string`.

Wanneer een eigenschap weer een object is, moet daar een andere klasse voor gemaakt worden. Om de bovenstaande JSON te deserialiseren zijn de volgende klassen nodig:

```csharp
internal class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public bool Married { get; set; }
    public List<string> Hobbies { get; set; }
    public Address Address { get; set; }
}

internal class Address
{
    public string Street { get; set; }
    public string City { get; set; }
    public string State { get; set; }
}
```

Deserialiseren (weer met hoofdletterongevoeligheid):

```csharp
var options = new JsonSerializerOptions { PropertyNameCaseInsensitive = true };
var person = JsonSerializer.Deserialize<Person>(personJson, options);

Console.WriteLine($"{person.Name} woont in {person.Address.City}");
```

Soms is de JSON zelf een array. Dan geef je `Deserialize<T>` direct een `List` met passend type:

```csharp
var arrayJson = "[3, 4, 5]";
var numbers = JsonSerializer.Deserialize<List<int>>(arrayJson);

Console.WriteLine(numbers[1]); // 4
```

Als je geen van de `List`-methodes nodig hebt, werkt een array ook als type: `JsonSerializer.Deserialize<int[]>(arrayJson)`.

## 8.3 Een test-API

Wanneer je een client wilt bouwen, maar nog geen API hebt, zet je een tijdelijke **nep-API** op. Zo'n nep-API geeft simpelweg JSON als antwoord, zonder database erachter. We noemen dat 'mocking'. Twee manieren:

1. Een simpel PHP-script dat JSON teruggeeft:

   ```php
   <?php
   echo '['
       . '{"id":1,"name":"Curio","postalCode":"1234AB"},'
       . '{"id":2,"name":"Hizmet","postalCode":"4814AA"}'
       . ']';
   ```

2. Een online tool voor mock-data:
   1. <https://mocki.io/fake-json-api>
   2. <https://jsonplaceholder.typicode.com/>
   3. <https://mockend.com/>
   4. <https://mockapi.io/>

Zet je optie 1 via Laragon als `test.php` beschikbaar, dan krijg je een nep-API-route `http://localhost/test.php`:

![Een browser op localhost/test.php met de JSON-uitvoer van het PHP-script](./assets/localhost-test-php.png)

Die route kun je in C# gebruiken om je client te testen.

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week8-oefeningen.html)
[Quiz](/pages/week8-meetmoment.html)
[Week 9](/pages/week9-theorie.html)
</x-nav>
