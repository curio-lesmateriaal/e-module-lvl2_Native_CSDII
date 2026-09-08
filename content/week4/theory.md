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

Bijwerken gaat in drie stappen:

1. Haal het object op uit de Database Context (`Single`, `First` of `FirstOrDefault`).
2. Pas de property('s) aan.
3. Roep `SaveChanges` aan op **dezelfde** context als waar je het object hebt opgehaald.

```csharp
using (var db = new AppDbContext())
{
    var blog = db.Blogs.Single(b => b.Url == "http://someblog.microsoft.com");
    blog.Url = "http://someotherblog.microsoft.com";
    db.SaveChanges();
}
```

Je roept dus géén `Update`-methode aan. Dankzij **Change Tracking** onthoudt EF Core welke opgehaalde objecten je hebt gewijzigd en bouwt het bij `SaveChanges` automatisch de juiste `UPDATE`-query. Dat werkt alleen als je opvraagt én opslaat op dezelfde context-instantie.

Heb je in één keer meerdere wijzigingen (bijvoorbeeld één `UPDATE` en twee `INSERT`s)? Dan stuurt EF Core die bij `SaveChanges` gebundeld naar de database in zo min mogelijk **roundtrips**, in plaats van één voor één. Dit heet *batching*.

<x-callout type="info">

**Roundtrip.** Het heen en weer sturen van gegevens tussen client en server: een verzoek naar de database en het antwoord terug.

</x-callout>

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

Verwijderen ziet er zo uit:

```csharp
using (var db = new AppDbContext())
{
    var chat = db.Chats.Single(c => c.Name == "Chatroom 1");
    db.Chats.Remove(chat);
    db.SaveChanges();
}
```

Ook hier: roep `SaveChanges` aan op dezelfde context als waar je het object ophaalde, zodat de Change Tracker weet wat er verwijderd moet worden.

Verwijder je een object waar nog andere gegevens naar verwijzen? Dan moet je die afhankelijke gegevens mee verwijderen of de relatie verbreken, anders krijg je foutmeldingen. **Cascade Delete** doet dat automatisch: <https://learn.microsoft.com/en-us/ef/core/saving/cascade-delete>

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
[Week 5](/pages/week5-theorie.html)
</x-nav>
