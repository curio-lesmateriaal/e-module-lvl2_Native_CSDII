---
week: 5
title: EF Core in een WinUI-app — seeden & tonen
goal: je kunt in een WinUI 3-app de database bouwen en seeden met EnsureCreated en HasData, de inhoud tonen in een ListView, met een Frame en Navigate tussen Pages wisselen en met een knop iets aan de database toevoegen
accent: teal
summary: "Je kent EF Core al uit week 3 en 4. Deze week gebruik je dezelfde DbContext in een WinUI 3-desktop-app: je bouwt en seedt de database met EnsureCreated en HasData en toont de gegevens in een ListView. Daarna leer je met een Frame en Navigate tussen Pages wisselen, en koppel je een knop die met Add en SaveChanges iets nieuws aan de database toevoegt. Volgende week maak je de app nóg interactiever (selecteren, wijzigen en verwijderen)."
leeruitkomsten:
  - Ik ken het verschil tussen EnsureCreated/EnsureDeleted en migrations en weet wanneer ik wat gebruik
  - Ik kan de database seeden met HasData in OnModelCreating
  - Ik kan een lijst objecten uit de database tonen in een ListView
  - Ik kan met een Frame en Navigate tussen Pages wisselen
  - Ik kan een knop koppelen die met Add en SaveChanges een nieuw object opslaat
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

## 5.5 Werken met meerdere Pages: Frame en Navigate

Tot nu toe staat alles in één `MainWindow`: de `ListView`, de knoppen, alles. Een WinUI 3-app kan ook uit meerdere **Pages** bestaan die je binnen hetzelfde venster in- en uitwisselt — bijvoorbeeld een overzichtspagina met de lijst, en een aparte pagina om een nieuwe bewoner toe te voegen.

Een `Page` voeg je toe via *rechtsklik op je project → Add → New Item → Blank Page*. Noem 'm bijvoorbeeld `AddCitizenPage`.

Om Pages te kunnen tonen, zet je in `MainWindow.xaml` een `Frame`: een soort "venster binnen het venster" waarin steeds één Page zichtbaar is.

```xml
<Frame x:Name="contentFrame" />
```

Vanuit `MainWindow.xaml.cs` navigeer je naar een Page met `Navigate` en het `typeof(...)` van die Page:

```csharp
contentFrame.Navigate(typeof(AddCitizenPage));
```

Sta je al **in** een Page en wil je naar een andere Page navigeren? Dan hoef je niet naar `contentFrame` te zoeken: elke Page kent via `this.Frame` de Frame waarin hij zelf getoond wordt.

```csharp
this.Frame.Navigate(typeof(OverviewPage));
```

<x-callout type="note">

Je kunt `Navigate(...)` ook een tweede argument meegeven om gegevens naar de volgende Page te sturen, en die daar weer uitlezen door `OnNavigatedTo` te overschrijven. Dat is verdiepende stof — voor nu is het genoeg om te weten dat het kan.

</x-callout>

<x-keuzevraag>
question: Je staat in `AddCitizenPage` en wilt terug naar `OverviewPage`. Waarom gebruik je daarvoor `this.Frame.Navigate(...)` in plaats van `contentFrame.Navigate(...)`?
options:
  - "`contentFrame` bestaat niet meer zodra je in een Page zit"
  - "`this.Frame` verwijst vanzelf naar de Frame waarin deze Page getoond wordt; `contentFrame` is een veld van MainWindow, niet van de Page"
  - Het maakt niets uit, beide werken altijd
  - "`Navigate` bestaat alleen op `this.Frame`"
correct: 1
explanation: "`contentFrame` is een x:Name in MainWindow.xaml — een Page kent dat veld niet. Elke Page heeft via `this.Frame` automatisch toegang tot de Frame waarin hij draait."
</x-keuzevraag>

## 5.6 Een knop die iets toevoegt aan de database

Op `AddCitizenPage` zet je invoervelden (bijvoorbeeld `nameTextBox` en `jobTextBox`) en een knop "Opslaan". In de `Click`-handler van die knop maak je een nieuw object van de invoer, sla je het op met EF Core, en navigeer je terug naar het overzicht:

```csharp
private void saveButton_Click(object sender, RoutedEventArgs e)
{
    using (var db = new AppDbContext())
    {
        db.Citizens.Add(new Citizen
        {
            Name = nameTextBox.Text,
            Job = jobTextBox.Text
        });
        db.SaveChanges();
    }

    this.Frame.Navigate(typeof(OverviewPage));
}
```

<x-callout type="tip">

Dit is dezelfde `Add` + `SaveChanges` die je al kent uit week 4. Het enige nieuwe is dát de waarden nu uit invoervelden op een eigen Page komen, in plaats van uit `Console.ReadLine`.

</x-callout>

<x-invul>
prompt: Vul de twee regels aan die de nieuwe bewoner opslaan in de database.
code: |-
  db.Citizens.___(new Citizen { Name = nameTextBox.Text, Job = jobTextBox.Text });
  db.___();
blanks:
  - answer: Add
  - answer: SaveChanges
explanation: "Add zet het object klaar in de context; SaveChanges schrijft het echt naar de database."
</x-invul>

<x-callout type="note">

Volgende week (6) ga je hierop verder: een bewoner **selecteren** in de `ListView` en daarna **wijzigen** of **verwijderen** — nog zonder aparte Page.

</x-callout>

<x-nav label="Klaar met de theorie?">
[Oefeningen](/pages/week5-oefeningen.html)
[Quiz](/pages/week5-meetmoment.html)
[Week 6](/pages/week6-theorie.html)
</x-nav>
