---
week: 5
title: EF Core in een WinUI-app — seeden & tonen
goal: je kunt in een WinUI 3-app de database bouwen en seeden met EnsureCreated en HasData, en de inhoud tonen in een ListView
accent: teal
summary: "Je kent EF Core al uit week 3 en 4. Deze week gebruik je dezelfde DbContext in een WinUI 3-desktop-app: je bouwt en seedt de database met EnsureCreated en HasData en toont de gegevens in een ListView. Volgende week maak je de app interactief (selecteren en CRUD)."
leeruitkomsten:
  - Ik ken het verschil tussen EnsureCreated/EnsureDeleted en migrations en weet wanneer ik wat gebruik
  - Ik kan de database seeden met HasData in OnModelCreating
  - Ik kan een lijst objecten uit de database tonen in een ListView
---

## 5.1 Inleiding

In week 3 en 4 heb je met Entity Framework Core gewerkt in een **console-app**: een model, een `AppDbContext` met een `DbSet` per klasse, en gegevens ophalen en opslaan. In deze week gebruik je precies diezelfde onderdelen, maar dan in een **WinUI 3-desktop-app** met een echte gebruikersinterface.

Het project, het model en de `AppDbContext` maak je zoals je gewend bent. De nieuwe stof zit deze week in twee dingen: de database **seeden** met testdata en de inhoud tonen in een **ListView**. Volgende week maak je die lijst interactief — selecteren, toevoegen, wijzigen en verwijderen. We bouwen mee aan **DevCitySim**, een stadsimulator, met de klasse `Citizen` (een bewoner) als voorbeeld.

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

`EnsureDeleted()` wist **elke keer dat je de app start** al je gegevens. Handig zolang je alleen met seed-data werkt, maar zodra je (volgende week) objecten gaat toevoegen of verwijderen die moeten blijven bestaan, haal je die regel weg en laat je alleen `EnsureCreated()` staan.

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

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week5-oefeningen.html)
[Quiz](/pages/week5-meetmoment.html)
[Week 6](/pages/week6-theorie.html)
</x-nav>
