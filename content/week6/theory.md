---
week: 6
title: WinUI-app 2 — selecteren & CRUD
goal: je kunt in een WinUI 3-app een item in een ListView selecteren en vanuit de UI objecten toevoegen, wijzigen en verwijderen, en de lijst daarna verversen
accent: cyan
summary: "Vorige week toonde je gegevens in een ListView. Deze week maak je de app interactief: je klikt op een item om het te selecteren, en je voegt met knoppen en invoervelden de vier CRUD-bewerkingen toe. Steeds ververs je de lijst zodat de gebruiker het resultaat ziet."
leeruitkomsten:
  - Ik kan op een ListView-item klikken en het aangeklikte object gebruiken
  - Ik kan vanuit de UI een object toevoegen, wijzigen en verwijderen en opslaan met SaveChanges
  - Ik kan de ListView verversen na een wijziging
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

## 6.5 Data laten blijven bestaan

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
