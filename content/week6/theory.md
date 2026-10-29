---
week: 6
title: WinUI-app 2 — selecteren & CRUD
goal: je kunt in een WinUI 3-app een item in een ListView selecteren en vanuit de UI objecten toevoegen, wijzigen en verwijderen, en de lijst daarna verversen
accent: cyan
summary: "Vorige week toonde je gegevens in een ListView. Deze week maak je de app interactief: je klikt op een item om het te selecteren, en je voegt met knoppen en invoervelden de vier CRUD-bewerkingen toe. Je leert ook met LINQ (Where, Contains, OrderBy) de database filteren en sorteren, bijvoorbeeld voor een zoekveld. Steeds ververs je de lijst zodat de gebruiker het resultaat ziet."
leeruitkomsten:
  - Ik kan op een ListView-item klikken en het aangeklikte object gebruiken
  - Ik kan vanuit de UI een object toevoegen, wijzigen en verwijderen en opslaan met SaveChanges
  - Ik kan de ListView verversen na een wijziging
  - Ik kan met Where, FirstOrDefault, Contains en OrderBy de database filteren en sorteren
  - Ik weet hoe ik mijn wijzigingen laat blijven bestaan na een herstart
---

## 6.1 Inleiding

In week 5 heb je je `DevCitySim`-app de bewoners uit de database laten tonen in een `ListView`. Nu maak je die lijst **interactief**: je klikt op een bewoner om hem te selecteren, en je voegt knoppen en invoervelden toe waarmee de gebruiker bewoners kan toevoegen, wijzigen en verwijderen.

De databasekant verandert niet — het is dezelfde `AppDbContext`, dezelfde `SaveChanges` als in week 4. Alleen komen de gegevens nu uit de UI in plaats van uit `Console.ReadLine`.

## 6.2 Op een ListView-item klikken

Maak de items klikbaar met `IsItemClickEnabled` en een `ItemClick`-event:

```xml
<ListView x:Name="citizenListView"
          IsItemClickEnabled="True"
          ItemClick="citizenListView_ItemClick">
```

Tijdens het typen van `ItemClick="..."` biedt Visual Studio aan de event handler voor je aan te maken. In die handler weet je zeker dat het aangeklikte item een `Citizen` is (want dat zit in de lijst), dus je kunt `e.ClickedItem` **casten**:

```csharp
private Citizen selectedCitizen;

private void citizenListView_ItemClick(object sender, ItemClickEventArgs e)
{
    selectedCitizen = (Citizen)e.ClickedItem;
    // nu kun je bij selectedCitizen.Name, .Job, .Id ...
    nameTextBox.Text = selectedCitizen.Name;
    jobTextBox.Text = selectedCitizen.Job;
}
```

Sla het geselecteerde object (of minstens zijn `Id`) op in een veld — dat heb je nodig bij Update en Delete.

<x-keuzevraag>
question: Waarom mag je `e.ClickedItem` casten naar `Citizen`?
options:
  - Omdat ClickedItem altijd een Citizen is, ongeacht de lijst
  - Omdat wij de ListView met een lijst Citizen-objecten hebben gevuld, dus het aangeklikte item is er één
  - Omdat een cast nooit fout kan gaan
  - Omdat Citizen van object erft
correct: 1
explanation: "`ClickedItem` is van het type `object`. Omdat jouw `ItemsSource` een lijst `Citizen` was, weet je zeker dat het geklikte item een `Citizen` is en kun je veilig casten."
</x-keuzevraag>

## 6.3 CRUD vanuit de UI

De vier bewerkingen werken exact zoals in week 4 — dezelfde `DbContext`, dezelfde `SaveChanges`.

**Create** — een nieuwe bewoner toevoegen op basis van invoervelden:

```csharp
using (var db = new AppDbContext())
{
    db.Citizens.Add(new Citizen
    {
        Name = nameTextBox.Text,
        Job = jobTextBox.Text,
        DateOfBirth = birthDatePicker.Date.DateTime
    });
    db.SaveChanges();
}
RefreshList();   // zie 6.4
```

**Update** — de geselecteerde bewoner ophalen met `Find`, een property wijzigen, opslaan:

```csharp
using (var db = new AppDbContext())
{
    Citizen c = db.Citizens.Find(selectedCitizen.Id);
    c.Job = jobTextBox.Text;
    db.SaveChanges();
}
RefreshList();
```

**Delete** — de geselecteerde bewoner ophalen en verwijderen:

```csharp
using (var db = new AppDbContext())
{
    Citizen c = db.Citizens.Find(selectedCitizen.Id);
    db.Citizens.Remove(c);
    db.SaveChanges();
}
RefreshList();
```

<x-invul>
prompt: Vul de twee regels aan die de geselecteerde bewoner uit de database verwijderen.
code: |-
  Citizen c = db.Citizens.Find(selectedCitizen.Id);
  db.Citizens.___(c);
  db.___();
blanks:
  - answer: Remove
  - answer: SaveChanges
explanation: "Remove markeert het object als verwijderd; SaveChanges voert de DELETE echt uit op de database."
</x-invul>

## 6.4 De ListView verversen na een wijziging

Na elke wijziging moet de `ListView` opnieuw gevuld worden, anders ziet de gebruiker het resultaat niet. Zet dat in één methode die je overal kunt aanroepen:

```csharp
private void RefreshList()
{
    using (var db = new AppDbContext())
    {
        citizenListView.ItemsSource = db.Citizens.ToList();
    }
}
```

Roep `RefreshList()` aan bij het opstarten (in plaats van de vul-code die je in week 5 in de constructor zette) én na elke `SaveChanges`.

## 6.5 Filteren met LINQ: Where en meer

Tot nu toe haal je altijd **alles** op (`db.Citizens.ToList()`) of precies **één** item (`Find`). Vaak wil je maar een deel: bijvoorbeeld alleen bewoners met een bepaald beroep, of alleen bewoners van wie de naam met iets begint. Daarvoor gebruik je **LINQ** (Language Integrated Query). `Single`, `First` en `FirstOrDefault` uit week 4 zijn trouwens zelf ook al LINQ-methoden — die geven alleen één object terug in plaats van een lijst.

`Where(...)` filtert op een voorwaarde (een lambda, net als bij `Single`/`First`) en levert een **collectie** op — geen enkel object, dus:

```csharp
using (var db = new AppDbContext())
{
    List<Citizen> developers = db.Citizens
        .Where(c => c.Job == "Software Developer")
        .ToList();
}
```

Wil je niet een hele lijst, maar maar **één** bewoner die aan een voorwaarde voldoet? Dan gebruik je, net als in week 4, `FirstOrDefault` — alleen nu met een eigen voorwaarde in plaats van een vaste:

```csharp
using (var db = new AppDbContext())
{
    Citizen? developer = db.Citizens
        .FirstOrDefault(c => c.Job == "Software Developer");

    if (developer == null)
    {
        // geen enkele bewoner heeft dit beroep
    }
    else
    {
        nameTextBox.Text = developer.Name;
    }
}
```

<x-callout type="note">

Het verschil met `Find` (zie 6.3): `Find` zoekt altijd op de primaire sleutel (`Id`). `FirstOrDefault` (en `Where`) zoeken op **elke** voorwaarde die je zelf opgeeft — hier bijvoorbeeld op `Job` in plaats van `Id`.

</x-callout>

<x-keuzevraag>
question: "Je doet `db.Citizens.FirstOrDefault(c => c.Job == \"Astronaut\")` en er is geen enkele bewoner met dat beroep. Wat gebeurt er?"
options:
  - Je krijgt een foutmelding (exception)
  - Je krijgt null terug
  - Je krijgt een lege Citizen terug met alle properties op hun standaardwaarde
  - De app blijft hangen
correct: 1
explanation: "FirstOrDefault geeft de 'default'-waarde terug als niets voldoet — voor een class is dat null. Controleer dus altijd op null voordat je verder werkt met het resultaat."
</x-keuzevraag>

Je kunt `Where` combineren met andere LINQ-methoden, bijvoorbeeld `Contains` om op tekst te zoeken en `OrderBy` om te sorteren:

```csharp
using (var db = new AppDbContext())
{
    List<Citizen> resultaten = db.Citizens
        .Where(c => c.Name.Contains(zoekterm))
        .OrderBy(c => c.Name)
        .ToList();
}
```

Dat is meteen bruikbaar in je eigen app: breid `RefreshList()` (zie 6.4) uit met een zoekterm, bijvoorbeeld uit een `searchTextBox`:

```csharp
private void RefreshList(string zoekterm = "")
{
    using (var db = new AppDbContext())
    {
        citizenListView.ItemsSource = db.Citizens
            .Where(c => c.Name.Contains(zoekterm))
            .OrderBy(c => c.Name)
            .ToList();
    }
}
```

Roep je `RefreshList()` aan zonder argument, dan is `zoekterm` leeg en is `c.Name.Contains("")` altijd waar — je ziet dus gewoon iedereen. Vul je iets in `searchTextBox` in en roep je `RefreshList(searchTextBox.Text)` aan, dan filtert de lijst live.

Een paar andere veelgebruikte LINQ-methoden:

- `Count()` — hoeveel items voldoen (een getal, geen lijst);
- `Any(...)` — bestaat er minstens één item dat voldoet (`true`/`false`);
- `OrderByDescending(...)` — sorteert aflopend in plaats van oplopend.

<x-callout type="tip">

`Where` en `OrderBy` stellen alleen de query samen. Pas bij `.ToList()` (of een `foreach`) wordt die echt tegen de database uitgevoerd.

</x-callout>

<x-invul>
prompt: Vul de regel aan die alle bewoners met beroep "Software Developer" ophaalt.
code: |-
  List<Citizen> developers = db.Citizens.___(c => c.Job == "Software Developer").ToList();
blanks:
  - answer: Where
explanation: "Where filtert de DbSet op een voorwaarde en levert een collectie op; ToList() voert de query uit."
</x-invul>

## 6.6 Data laten blijven bestaan

In week 5 zette je `EnsureDeleted()` én `EnsureCreated()` in je `MainWindow`-constructor. `EnsureDeleted()` gooit bij **elke** start de hele database weg — dan zijn je toegevoegde en gewijzigde bewoners na een herstart weer verdwenen.

Zodra je CRUD gaat testen, haal je `db.Database.EnsureDeleted();` weg en laat je alleen `EnsureCreated()` staan. Die maakt de database (met de seed-data) alleen aan als hij nog niet bestaat, en laat bestaande data met rust.

<x-callout type="warning">

Verander je later je model (een property erbij)? Dan moet je de database één keer handmatig verwijderen (of `EnsureDeleted()` tijdelijk terugzetten), want `EnsureCreated()` past een bestaande database niet aan. Voor echte projecten gebruik je daarvoor migrations (week 3).

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week6-oefeningen.html)
[Quiz](/pages/week6-meetmoment.html)
[Week 7](/pages/week7-theorie.html)
</x-nav>
