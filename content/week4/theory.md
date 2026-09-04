---
week: 4
title: EF Core — CRUD in een console-app
goal: je kunt in een console-app met EF Core gegevens toevoegen, ophalen, wijzigen en verwijderen en je begrijpt de rol van SaveChanges en Change Tracking
accent: amber
summary: Met de DbContext van week 3 ga je nu echt data bewerken. Je leert de vier CRUD-bewerkingen, waarom je SaveChanges nodig hebt, hoe Change Tracking werkt en wat batching en cascade delete zijn.
leeruitkomsten:
  - Ik kan een nieuw object toevoegen aan een DbSet en opslaan met SaveChanges
  - Ik kan gegevens ophalen met Single, First en FirstOrDefault
  - Ik kan een opgehaald object wijzigen en de wijziging opslaan
  - Ik kan een object verwijderen en weet wat cascade delete doet
  - Ik kan uitleggen wat Change Tracking en batching (roundtrips) zijn
---

## CRUD met Entity Framework

Met de 'Read' in 'CRUD' zijn we inmiddels goed bekend: we weten dat we in Entity Framework gegevens kunnen ophalen via een `DbSet` in een Database Context.

Het lijkt dat we nog veel moeten leren als we nog maar 1 van de 4 letters in de afkorting CRUD hebben behandeld, maar er is hoop: het invoeren (Create), aanpassen (Update) en verwijderen (Delete) van gegevens is in Entity Framework enorm makkelijk gemaakt! We zijn al ver over de helft van de lesstof van Entity Framework.

## 4.1 Gegevens invoeren

Entity Framework maakt het invoeren van gegevens makkelijk voor ons. Om bijvoorbeeld gegevens van een 'bedrijf' in te voeren doen we grofweg het volgende:

1. Open een verbinding met de database zoals je gewend bent:

   ```csharp
   using (var dbContext = new AppDbContext())
   {
       // ...
   }
   ```

2. Maak een instantie van een model dat je in de database wilt invoeren, bijvoorbeeld voor een model `Company`:

   ```csharp
   var myCompany = new Company { Name = "Curio" };
   ```

3. Voeg die instantie toe aan de relevante `DbSet` van de Database Context, bijvoorbeeld:

   ```csharp
   dbContext.Companies.Add(myCompany);
   ```

4. Sla de Database Context op met de `SaveChanges`-methode:

   ```csharp
   dbContext.SaveChanges();
   ```

Dat kan er bijvoorbeeld zo uitzien:

```csharp
Console.WriteLine("Wat is de naam van het bedrijf?");
string companyNameInput = Console.ReadLine();

dbContext.Companies.Add(new Company
{
    Name = companyNameInput
});
dbContext.SaveChanges();

Console.WriteLine();
Console.WriteLine($"Het bedrijf {companyNameInput} is toegevoegd!");
```

`dbContext` is zoals gewoonlijk beschikbaar dankzij `using (var dbContext = new AppDbContext())`.

<x-callout type="warning">

We zien dat de Database Context niet automatisch opslaat wanneer je een object aan de `DbSet` toevoegt. **Je moet met de `SaveChanges`-methode expliciet aangeven wijzigingen aan de `DbSet` op te slaan.**

</x-callout>

Hier kun je meer lezen over het invoeren van data: <https://learn.microsoft.com/en-us/ef/core/saving/basic>

## 4.2 Gegevens ophalen (Read)

Ophalen doe je via de `DbSet`. Een paar veelgebruikte manieren om precies één rij op te halen:

```csharp
var blog1 = context.Blogs.Single(b => b.Url == "http://someblog.microsoft.com");
var blog2 = context.Blogs.First(b => b.Url == "http://someblog.microsoft.com");
var blog3 = context.Blogs.FirstOrDefault(b => b.Url == "http://bestaatniet.com"); // null als niets gevonden
```

`Single` verwacht precies één resultaat (en geeft anders een fout), `First` pakt de eerste, en `FirstOrDefault` geeft `null` terug als er niets gevonden wordt. Wil je alle rijen? Dan loop je gewoon door de `DbSet`:

```csharp
foreach (var blog in context.Blogs)
{
    Console.WriteLine(blog.Url);
}
```

## 4.3 Gegevens updaten

Het bewerken van gegevens gaat volgens de volgende stappen:

1. Haal gegevens op uit een Database Context — je krijgt instanties van modellen.
2. Wijzig de gegevens door de instanties aan te passen.
3. Roep `SaveChanges` aan op **dezelfde** Database Context als waar de gegevens zijn uitgehaald. Dankzij Change Tracking weet Entity Framework hoe de `UPDATE`-query opgebouwd moet worden.

Je kunt voorbeeldcode vinden in de documentatie van Microsoft: <https://learn.microsoft.com/en-us/ef/core/performance/efficient-updating?tabs=ef7>. Daar kun je ook vinden hoe je efficiëntere updates kunt uitvoeren, bijvoorbeeld door **Batching**. Met Batching minimaliseert EF het aantal 'roundtrips' door automatisch alle updates samen te voegen in één roundtrip.

<x-callout type="info">

**Roundtrip.** Verwijst naar het proces waarbij gegevens van een client naar een server worden verzonden en vervolgens het antwoord van de server terug naar de client wordt ontvangen. Het omvat het heen en weer gaan van gegevens tussen de client en de server.

</x-callout>

Neem het volgende in overweging:

```csharp
var blog = context.Blogs.Single(b => b.Url == "http://someblog.microsoft.com");
blog.Url = "http://someotherblog.microsoft.com";
context.Add(new Blog { Url = "http://newblog1.microsoft.com" });
context.Add(new Blog { Url = "http://newblog2.microsoft.com" });
context.SaveChanges();
```

Bovenstaande code laadt een blog uit de database (je kunt in plaats van de `Single`-methode ook `First` of `FirstOrDefault` gebruiken), wijzigt de URL en voegt vervolgens twee nieuwe blogs toe. Om dit toe te passen, worden er twee SQL `INSERT`-opdrachten en één `UPDATE`-opdracht naar de database gestuurd. In plaats van ze één voor één te verzenden wanneer de `Blog`-instanties worden toegevoegd, houdt EF deze wijzigingen intern bij en voert ze uit in één roundtrip wanneer `SaveChanges` wordt aangeroepen.

Het aantal opdrachten dat EF bundelt in één roundtrip hangt af van de gebruikte databaseprovider. Bijvoorbeeld, uit prestatieanalyse is gebleken dat batching over het algemeen minder efficiënt is voor (Microsoft) SQL Server wanneer er minder dan 4 opdrachten zijn. Op vergelijkbare wijze verminderen de voordelen van batching na ongeveer 40 opdrachten voor SQL Server. Daarom zal EF standaard slechts maximaal 42 opdrachten in één batch uitvoeren en aanvullende opdrachten in afzonderlijke roundtrips uitvoeren.

Bron: <https://learn.microsoft.com/en-us/ef/core/performance/efficient-updating?tabs=ef7>

<x-keuzevraag>
question: Je haalt een klant op met context A, past de naam aan, en roept SaveChanges aan op context B. Wat gebeurt er?
options:
  - De wijziging wordt opgeslagen
  - De wijziging wordt niet opgeslagen; Change Tracking van context B kent dit object niet
  - Er ontstaat altijd een crash
  - Beide contexts slaan de wijziging op
correct: 1
explanation: SaveChanges werkt alleen voor wijzigingen die dezelfde context bijhoudt via Change Tracking.
</x-keuzevraag>

## 4.4 Gegevens verwijderen

Het verwijderen van gegevens ziet er bijvoorbeeld zo uit:

```csharp
using (var db = new AppDbContext())
{
    var chat = db.Chats.Single(b => b.Name == "Chatroom 1");
    db.Chats.Remove(chat);
    db.SaveChanges();
}
```

Zorg (net als bij Update) dat je `SaveChanges` aanroept op dezelfde database context als waar de verwijderde gegevens worden opgehaald. Alleen dan kan de Change Tracker van Entity Framework bijhouden welke gegevens zijn verwijderd.

Wanneer je gegevens verwijdert die een relatie hebben met een andere entiteit, moet je ook die gegevens verwijderen, of de relatie verbreken. Anders krijg je (op andere plekken) foutmeldingen, omdat er nog afhankelijke gegevens bestaan, maar die dan niet meer bij de verwijderde data kunnen.

Om op een snelle manier bijbehorende gegevens te verwijderen of ontkoppelen maak je gebruik van 'Cascade Delete': <https://learn.microsoft.com/en-us/ef/core/saving/cascade-delete>

<x-invul>
prompt: Vul de code aan die klant "Jansen" uit de database verwijdert.
code: |-
  var klant = db.Klanten.Single(k => k.Naam == "Jansen");
  db.Klanten.___(klant);
  db.___();
blanks:
  - answer: Remove
  - answer: SaveChanges
explanation: "Remove markeert het object als verwijderd; SaveChanges voert de DELETE echt uit."
</x-invul>

<x-callout type="tip">

**Onthoud de CRUD-methoden:** `Add` (Create), door de `DbSet` loopen of `Single`/`First` (Read), een property aanpassen (Update), `Remove` (Delete) — en telkens sluit je af met `SaveChanges()` op dezelfde context.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week4-oefeningen.html)
[Quiz](/pages/week4-meetmoment.html)
[Inleveropdracht](/pages/week4-inleveropdracht.html)
[Week 5](/pages/week5-theorie.html)
</x-nav>
