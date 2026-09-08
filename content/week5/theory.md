---
week: 5
title: CRUD in een WinUI-applicatie
goal: je kunt in een WinUI 3-app de database seeden met testdata, de inhoud tonen in een ListView, op een item klikken en de CRUD-bewerkingen uitvoeren vanuit de UI
accent: teal
summary: "Je kent EF Core al uit week 3 en 4. Deze week gebruik je dezelfde DbContext in een WinUI 3-desktop-app: je bouwt en seedt de database met EnsureCreated en HasData, toont bewoners in een ListView, maakt items klikbaar en voegt Create, Update en Delete toe vanuit de UI."
leeruitkomsten:
  - Ik kan de database seeden met HasData in OnModelCreating
  - Ik ken het verschil tussen EnsureCreated/EnsureDeleted en migrations en weet wanneer ik wat gebruik
  - Ik kan een lijst objecten tonen in een ListView en op een item klikken
  - Ik kan vanuit de UI een object toevoegen, wijzigen en verwijderen en opslaan met SaveChanges
---

## 5.1 Inleiding

In week 3 en 4 heb je met Entity Framework Core gewerkt in een **console-app**: een model, een `AppDbContext` met een `DbSet` per klasse, en gegevens ophalen en opslaan. In deze week gebruik je precies diezelfde onderdelen, maar dan in een **WinUI 3-desktop-app** met een echte gebruikersinterface.

Het project, het model en de `AppDbContext` maak je zoals je gewend bent. De nieuwe stof zit in drie dingen: de database **seeden** met testdata, de inhoud tonen in een **ListView**, en die lijst gebruiken om objecten te selecteren, toe te voegen en te verwijderen. We bouwen mee aan **DevCitySim**, een stadsimulator, met de klasse `Citizen` (een bewoner) als voorbeeld.

## 5.2 De database opbouwen: EnsureCreated / EnsureDeleted

In week 3 maakte je je database aan met **migrations** (`Add-Migration` + `Update-Database`). Dat is de manier voor productie: je bouwt de database stap voor stap op en houdt bestaande data.

Tijdens het ontwikkelen van een oefenproject is dat vaak omslachtig. Daarom gebruiken we hier twee methoden op `db.Database`:

- `EnsureDeleted()` — gooit de hele database weg;
- `EnsureCreated()` — bouwt de database opnieuw op volgens je model en roept daarna `OnModelCreating` aan (de seeding, zie 5.3).

Je roept ze aan bij het opstarten van de app, in de constructor van je `MainWindow`:

```csharp
public MainWindow()
{
    this.InitializeComponent();

    using (var db = new AppDbContext())
    {
        db.Database.EnsureDeleted();
        db.Database.EnsureCreated();
    }
}
```

<x-callout type="tip">

Het `using`-blok zorgt dat de databaseverbinding binnen de accolades beschikbaar is en daarna netjes wordt afgesloten.

</x-callout>

<x-callout type="warning">

`EnsureDeleted()` wist **elke keer dat je de app start** al je gegevens. Handig zolang je alleen met seed-data werkt, maar zodra je in 5.6 objecten gaat toevoegen of verwijderen die moeten blijven bestaan, haal je die regel weg en laat je alleen `EnsureCreated()` staan.

</x-callout>

## 5.3 Seeden met testdata

"Seeden" is je database vast vullen met testgegevens, zodat je app niet met een lege lijst begint. Je doet dit door `OnModelCreating` in je `AppDbContext` te overschrijven en `HasData` te gebruiken:

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    base.OnModelCreating(modelBuilder);

    modelBuilder.Entity<Citizen>().HasData(
        new Citizen { Id = 1, Name = "Jane Doe", DateOfBirth = new DateTime(2001, 10, 24), Job = "Software Developer" },
        new Citizen { Id = 2, Name = "John Doe", DateOfBirth = new DateTime(2004, 2, 1), Job = "Data Analist" }
    );
}
```

`EnsureCreated()` (zie 5.2) roept `OnModelCreating` aan, dus bij het opstarten van de app staat deze data meteen in de database.

<x-callout type="tip">

Bij `HasData` geef je zelf de `Id`-waarden op (1, 2, 3, …). EF Core heeft die nodig om de seed-rijen te kunnen herkennen.

</x-callout>

## 5.4 Data tonen in een ListView

Een `ListView` toont een lijst objecten. In de XAML beschrijf je met een `DataTemplate` hoe één item eruitziet. Om je eigen klasse als type te gebruiken, voeg je bovenin `MainWindow.xaml` de namespace van je model toe:

```xml
<Window
    xmlns:local="using:DevCitySim.Data"
    ... >

    <StackPanel Padding="15">
        <ListView x:Name="citizenListView">
            <ListView.ItemTemplate>
                <DataTemplate x:DataType="local:Citizen">
                    <StackPanel>
                        <TextBlock Text="{x:Bind Name}" />
                        <TextBlock Text="{x:Bind Job}" Opacity="0.6" />
                    </StackPanel>
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackPanel>
</Window>
```

In de code-behind vul je de lijst. Haal de gegevens op met `ToList()` en zet die op `ItemsSource`:

```csharp
using (var db = new AppDbContext())
{
    citizenListView.ItemsSource = db.Citizens.ToList();
}
```

<x-callout type="tip">

Gebruik `.ToList()` om de gegevens **nu** op te halen. Zonder `ToList()` probeert de ListView later data uit een `DbContext` te lezen die dan al is afgesloten — dat geeft een foutmelding.

</x-callout>

<x-invul>
prompt: Vul de regel aan die de ListView vult met alle bewoners uit de database.
code: |-
  citizenListView.ItemsSource = db.Citizens.___();
blanks:
  - answer: ToList
explanation: "Met `ToList()` haal je de rijen meteen op als een echte lijst; die kan de ListView tonen, ook nadat de DbContext is gesloten."
</x-invul>

## 5.5 Op een ListView-item klikken

Maak de items klikbaar met `IsItemClickEnabled` en een `ItemClick`-event:

```xml
<ListView x:Name="citizenListView"
          IsItemClickEnabled="True"
          ItemClick="citizenListView_ItemClick">
```

Tijdens het typen van `ItemClick="..."` biedt Visual Studio aan de event handler voor je aan te maken. In die handler weet je zeker dat het aangeklikte item een `Citizen` is (want dat zit in de lijst), dus je kunt `e.ClickedItem` **casten**:

```csharp
private void citizenListView_ItemClick(object sender, ItemClickEventArgs e)
{
    Citizen selected = (Citizen)e.ClickedItem;
    // nu kun je bij selected.Name, selected.Job, selected.Id ...
}
```

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

## 5.6 CRUD vanuit de UI

De vier bewerkingen werken exact zoals in week 4 — dezelfde `DbContext`, dezelfde `SaveChanges`. Alleen komen de gegevens nu uit invoervelden en knoppen in plaats van uit `Console.ReadLine`.

**Create** — een nieuwe bewoner toevoegen:

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
RefreshList();   // ListView opnieuw vullen, zie 5.4
```

**Read** — de hele lijst (`db.Citizens.ToList()`) of één object op sleutel (`db.Citizens.Find(id)`).

**Update** — object ophalen, property wijzigen, opslaan:

```csharp
using (var db = new AppDbContext())
{
    Citizen c = db.Citizens.Find(selectedId);
    c.Job = jobTextBox.Text;
    db.SaveChanges();
}
```

**Delete** — object ophalen en verwijderen:

```csharp
using (var db = new AppDbContext())
{
    Citizen c = db.Citizens.Find(selectedId);
    db.Citizens.Remove(c);
    db.SaveChanges();
}
```

Na elke wijziging vul je de `ListView` opnieuw zodat de gebruiker het resultaat ziet.

<x-callout type="warning">

Wil je dat je toegevoegde en gewijzigde bewoners na het herstarten van de app blijven bestaan? Haal dan de regel `db.Database.EnsureDeleted();` uit je `MainWindow`-constructor (zie 5.2). Anders begint de app elke keer weer met alleen de seed-data.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week5-oefeningen.html)
[Quiz](/pages/week5-meetmoment.html)
[Week 6](/pages/week6-theorie.html)
</x-nav>
