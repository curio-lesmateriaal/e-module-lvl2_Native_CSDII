---
week: 5
title: Quiz Week 5 — CRUD in een WinUI-app
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
    explanation: EnsureDeleted gooit elke keer de database weg. Prima met alleen seed-data, maar zodra je CRUD-wijzigingen wilt bewaren haal je die regel weg.
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
    question: "Je vult je ListView zo: <code>citizenListView.ItemsSource = db.Citizens;</code> binnen een using-blok. Wat gaat er mis?"
    options:
      - Niets, dit is correct
      - De lijst leest later data uit een DbContext die dan al is afgesloten — gebruik .ToList()
      - Je moet ItemSource schrijven, niet ItemsSource
      - Een DbSet kan nooit in een ListView
    correct: 1
    explanation: Zonder .ToList() haalt de ListView de gegevens pas op als hij ze nodig heeft; de context uit het using-blok is dan al gesloten. Met db.Citizens.ToList() haal je alles meteen op.
  - id: w5q6
    question: "In de ItemClick-handler doe je <code>Citizen c = (Citizen)e.ClickedItem;</code>. Waarom mag dat?"
    options:
      - Omdat e.ClickedItem altijd een Citizen is
      - Omdat wij de ListView met Citizen-objecten hebben gevuld, dus het geklikte item is er één
      - Omdat casten nooit fout gaat
      - Omdat ClickedItem al van het type Citizen is
    correct: 1
    explanation: "e.ClickedItem is van het type object. Omdat jouw ItemsSource een lijst Citizen was, is het geklikte item met zekerheid een Citizen."
  - id: w5q7
    question: Welke twee regels voegen een nieuwe bewoner echt toe aan de database?
    options:
      - "db.Citizens.Add(nieuw); db.SaveChanges();"
      - "db.Citizens.Add(nieuw);"
      - "db.Citizens.Find(nieuw); db.SaveChanges();"
      - "citizenListView.Items.Add(nieuw);"
    correct: 0
    explanation: Add zet het object klaar in de context; pas SaveChanges schrijft het echt naar de database. Items aan de ListView toevoegen verandert de database niet.
  - id: w5q8
    question: Je klikt op een bewoner en wilt zijn beroep wijzigen. Wat is de juiste volgorde?
    options:
      - Nieuwe Citizen maken met hetzelfde Id en SaveChanges
      - Bewoner ophalen met Find, de property aanpassen, SaveChanges
      - De property aanpassen in de ListView en SaveChanges
      - Remove en daarna Add
    correct: 1
    explanation: Haal het bestaande object op met db.Citizens.Find(id), wijzig de property en roep SaveChanges aan — Change Tracking (week 4) herkent de wijziging en maakt de UPDATE.
---
