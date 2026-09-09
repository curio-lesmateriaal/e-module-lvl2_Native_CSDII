---
week: 11
title: API + EF Core — data aanleveren
goal: je kunt je zelfgebouwde API de echte databasegegevens laten teruggeven via EF Core en een POST-verzoek uitlezen, deserialiseren en opslaan
accent: slate
summary: "Je API geeft geen hardcoded lijst meer terug, maar echte data uit de database via de DbContext. Je haalt de hele lijst en één item op id op, en je verwerkt een POST-verzoek: de JSON-body uitlezen, deserialiseren en opslaan met SaveChanges."
leeruitkomsten:
  - Ik kan in een API-endpoint een lijst en één item ophalen uit de database met EF Core
  - Ik kan de body van een POST-verzoek uitlezen via de InputStream
  - Ik kan die JSON deserialiseren naar een model en opslaan met SaveChanges
---

## 11.1 Data ophalen uit de database

Met de 'Read' in 'CRUD' zijn we inmiddels goed bekend: we weten dat we in Entity Framework gegevens kunnen ophalen via een `DbSet` in een Database Context. In week 9 gaf je API nog een hardcoded lijst terug. Nu vervangen we die door echte databasegegevens.

In je route-afhandeling open je gewoon een context, net als in de console-app van week 4:

```csharp
if (pad == "/voertuigen")
{
    using var db = new DeSleutelContext();
    List<Voertuig> voertuigen = db.Voertuigen.ToList();

    string json = JsonSerializer.Serialize(voertuigen);
    // ... omzetten naar bytes en versturen (zie week 9)
}
```

<x-callout type="tip">

Je API is nu de brug tussen de client en de database, precies zoals bij "moderne systemen" in week 7: de client praat met de API, de API praat met de database.

</x-callout>

## 11.2 Eén item op id

Voor één voertuig combineer je het uitlezen van het id uit de URL (week 9) met een query op de database:

```csharp
using var db = new DeSleutelContext();
Voertuig? voertuig = db.Voertuigen.FirstOrDefault(v => v.Id == id);

if (voertuig == null)
{
    context.Response.StatusCode = 404;
    // stuur een JSON-foutmelding
}
else
{
    string json = JsonSerializer.Serialize(voertuig);
    // stuur het voertuig
}
```

## 11.3 Een POST-verzoek verwerken

Een POST-verzoek (nieuw voertuig toevoegen) lees je uit via de `InputStream` van de request:

```csharp
if (context.Request.HttpMethod == "POST" && pad == "/voertuigen")
{
    using var reader = new StreamReader(context.Request.InputStream);
    string body = reader.ReadToEnd();

    var options = new JsonSerializerOptions { PropertyNameCaseInsensitive = true };
    Voertuig? nieuw = JsonSerializer.Deserialize<Voertuig>(body, options);

    using var db = new DeSleutelContext();
    db.Voertuigen.Add(nieuw);
    db.SaveChanges();

    context.Response.StatusCode = 201; // Created
    // stuur het aangemaakte voertuig als JSON terug
}
```

<x-invul>
prompt: Vul de twee regels aan die het gedeserialiseerde voertuig opslaan in de database.
code: |-
  using var db = new DeSleutelContext();
  db.Voertuigen.___(nieuw);
  db.___();
blanks:
  - answer: Add
  - answer: SaveChanges
explanation: "Add zet het object klaar in de context; SaveChanges schrijft het echt weg. De database vult zelf het Id in via AUTO_INCREMENT."
</x-invul>

<x-callout type="warning">

Wat als de client onzin meestuurt (leeg kenteken, negatieve prijs)? Dan sla je nu klakkeloos rommel op. Volgende week leer je die invoer **valideren** voordat je opslaat.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week11-oefeningen.html)
[Quiz](/pages/week11-meetmoment.html)
[Week 12](/pages/week12-theorie.html)
</x-nav>
