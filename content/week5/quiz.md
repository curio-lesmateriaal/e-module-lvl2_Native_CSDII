---
week: 5
title: Quiz Week 5 — EF Core in een WinUI-app
passScore: 70
questions:
  - id: w5q1
    question: Wat doet <code>db.Database.EnsureCreated()</code>?
    options:
      - Het maakt een migratiebestand aan
      - Het bouwt de database op volgens je model als die nog niet bestaat, en roept daarna de seeding aan
      - Het verwijdert alle rijen uit je tabellen
      - Het opent een verbinding zonder iets aan te maken
    correct: 1
    explanation: EnsureCreated maakt de database + tabellen aan volgens je model (als die er nog niet zijn) en roept OnModelCreating aan voor de seed-data.
  - id: w5q2
    question: Wat is het risico van <code>db.Database.EnsureDeleted()</code> in je MainWindow-constructor?
    options:
      - De app start langzamer op
      - Bij elke start wordt de hele database gewist, dus toegevoegde of gewijzigde data verdwijnt
      - De verbinding wordt nooit gesloten
      - Migrations werken daarna niet meer
    correct: 1
    explanation: EnsureDeleted gooit elke keer de database weg. Prima met alleen seed-data, maar zodra je wijzigingen wilt bewaren haal je die regel weg.
  - id: w5q3
    question: Wat gebeurt er nadat <code>EnsureCreated()</code> de database heeft opgebouwd?
    options:
      - Er gebeurt niets meer; de database is klaar
      - OnModelCreating wordt aangeroepen, dus je seed-data (HasData) wordt toegevoegd
      - Er wordt automatisch een migratie gemaakt
      - De ListView wordt gevuld
    correct: 1
    explanation: EnsureCreated bouwt de database volgens je model en roept daarna OnModelCreating aan; daar staat je HasData-seeding, dus die testdata komt meteen in de database.
  - id: w5q4
    question: Waarvoor gebruik je <code>HasData</code> in <code>OnModelCreating</code>?
    options:
      - Om de databaseverbinding op te zetten
      - Om testgegevens (seed-data) aan de database mee te geven
      - Om een ListView te vullen
      - Om een migratie uit te voeren
    correct: 1
    explanation: Met modelBuilder.Entity<T>().HasData(...) geef je vaste beginrijen op; die worden bij EnsureCreated in de database gezet.
  - id: w5q5
    question: Waarom moet je bij <code>HasData</code> zelf de <code>Id</code>-waarden opgeven (1, 2, 3, …)?
    options:
      - Dat hoeft niet, EF Core vult ze zelf in
      - EF Core heeft die nodig om de seed-rijen te kunnen herkennen
      - Anders wordt de database niet aangemaakt
      - Omdat Id anders null wordt
    correct: 1
    explanation: Seed-data met HasData vereist expliciete sleutelwaarden; daarmee weet EF Core welke rijen het bij een volgende run al kent.
  - id: w5q6
    question: "In welk bestand/onderdeel beschrijf je hoe één item in de ListView eruitziet?"
    options:
      - In de AppDbContext
      - In een DataTemplate binnen de ListView.ItemTemplate in de XAML
      - In OnModelCreating
      - In Program.cs
    correct: 1
    explanation: Een DataTemplate met x:DataType beschrijft de opmaak van één item; daarin bind je met x:Bind aan properties van je model.
  - id: w5q7
    question: "Je vult je ListView met <code>citizenListView.ItemsSource = db.Citizens;</code> binnen een using-blok. Wat gaat er mis?"
    options:
      - Niets, dit is correct
      - De lijst leest later data uit een DbContext die dan al is afgesloten — gebruik .ToList()
      - Je moet ItemSource schrijven, niet ItemsSource
      - Een DbSet kan nooit in een ListView
    correct: 1
    explanation: Zonder .ToList() haalt de ListView de gegevens pas op als hij ze nodig heeft; de context uit het using-blok is dan al gesloten. Met db.Citizens.ToList() haal je alles meteen op.
  - id: w5q8
    question: Waar zet je je seed-data in de <code>AppDbContext</code>?
    options:
      - In OnConfiguring
      - In OnModelCreating, met modelBuilder.Entity<T>().HasData(...)
      - In de constructor
      - In een DbSet
    correct: 1
    explanation: OnConfiguring legt de verbinding; de seeding overschrijf je in OnModelCreating.
---
