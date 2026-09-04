---
week: 3
title: De Sleutel gaat de database in
subtitle: Inleveropdracht Week 3
client: Autoverhuur De Sleutel
maxPoints: 12
deliverables:
  - Een C#-project met EF Core-packages, een Model-map en een DbContext in de Data-map
  - Een uitgevoerde migratie (de Migrations-map zit in het project)
  - Screenshot van de aangemaakte tabellen in je database (phpMyAdmin / MySQL Workbench)
criteria:
  - id: w3h1
    text: De juiste NuGet-packages zijn geïnstalleerd met een versie die bij de .NET-versie past
    points: 2
  - id: w3h2
    text: Er is een DbContext met een correcte OnConfiguring (connection string)
    points: 3
  - id: w3h3
    text: Het model bestaat uit classes met properties (Voertuig, Klant, Verhuur)
    points: 2
  - id: w3h4
    text: Voor elke op te slaan class staat er een DbSet in de context
    points: 2
  - id: w3h5
    text: Add-Migration en Update-Database zijn uitgevoerd; de tabellen bestaan
    points: 2
  - id: w3h6
    text: Elke tabel heeft een kolom per property en een Id-kolom
    points: 1
tips:
  - Volg het stappenplan uit de theorie punt voor punt.
  - Geef elke model-class een `public int Id { get; set; }` — dat wordt automatisch de primaire sleutel.
  - Krijg je een fout bij Add-Migration? Controleer of Microsoft.EntityFrameworkCore.Tools en .Design geïnstalleerd zijn.
---

De eigenschappen van De Sleutel staan nu alleen in het geheugen: zodra de app sluit, is alles weg. Tijd om de gegevens echt op te slaan. In deze opdracht koppel je het objectmodel van De Sleutel aan een MySQL-database met Entity Framework Core.

Zet een nieuw C#-project op volgens het stappenplan uit de theorie. Installeer de EF Core-packages in de juiste versie, maak een `Data`-map met een `DeSleutelContext`, en vul de `OnConfiguring` met de gegevens van jouw lokale database. Zet je model-classes (`Voertuig`, `Klant`, `Verhuur`) in de `Model`-map als classes met properties, elk met een `Id`. Voeg voor elke class een `DbSet` toe aan de context. Maak daarna een migratie aan met `Add-Migration InitieleDatabase` en voer die uit met `Update-Database`. Controleer in je database-tool dat de tabellen zijn aangemaakt met een kolom per property.

## Inleveren

Lever je project (als `.zip`, zonder de `bin/` en `obj/` mappen) met de screenshot in via **Itslearning**, onder de map "Module: Native (C#)".
