---
week: 6
title: Quiz Week 6 — WinUI-app 2 (selecteren & CRUD)
passScore: 70
questions:
  - id: w6q1
    question: "In de ItemClick-handler doe je <code>Citizen c = (Citizen)e.ClickedItem;</code>. Waarom mag dat?"
    options:
      - Omdat e.ClickedItem altijd een Citizen is
      - Omdat wij de ListView met Citizen-objecten hebben gevuld, dus het geklikte item is er één
      - Omdat casten nooit fout gaat
      - Omdat ClickedItem al van het type Citizen is
    correct: 1
    explanation: "e.ClickedItem is van het type object. Omdat jouw ItemsSource een lijst Citizen was, is het geklikte item met zekerheid een Citizen."
  - id: w6q2
    question: Welke twee regels voegen een nieuwe bewoner echt toe aan de database?
    options:
      - "db.Citizens.Add(nieuw); db.SaveChanges();"
      - "db.Citizens.Add(nieuw);"
      - "db.Citizens.Find(nieuw); db.SaveChanges();"
      - "citizenListView.Items.Add(nieuw);"
    correct: 0
    explanation: Add zet het object klaar in de context; pas SaveChanges schrijft het echt naar de database. Iets aan de ListView toevoegen verandert de database niet.
  - id: w6q3
    question: Je klikt op een bewoner en wilt zijn beroep wijzigen. Wat is de juiste volgorde?
    options:
      - Nieuwe Citizen maken met hetzelfde Id en SaveChanges
      - Bewoner ophalen met Find, de property aanpassen, SaveChanges
      - De property aanpassen in de ListView en SaveChanges
      - Remove en daarna Add
    correct: 1
    explanation: Haal het bestaande object op met db.Citizens.Find(id), wijzig de property en roep SaveChanges aan — Change Tracking (week 4) herkent de wijziging en maakt de UPDATE.
  - id: w6q4
    question: Welke methode markeert een object voor verwijdering?
    options:
      - Delete()
      - Remove()
      - Clear()
      - Drop()
    correct: 1
    explanation: "db.Citizens.Remove(c); gevolgd door db.SaveChanges(); verwijdert de rij."
  - id: w6q5
    question: Waarom roep je na elke wijziging <code>RefreshList()</code> aan?
    options:
      - Anders wordt de database niet opgeslagen
      - Anders ziet de gebruiker het resultaat niet; de ListView toont nog de oude lijst
      - Anders crasht de app
      - Dat hoeft niet
    correct: 1
    explanation: SaveChanges verandert de database, maar de ListView blijft de oude ItemsSource tonen tot je hem opnieuw vult.
  - id: w6q6
    question: Je hebt CRUD werkend, maar na een herstart zijn je toegevoegde bewoners weg. Wat is de oorzaak?
    options:
      - SaveChanges werkt niet
      - EnsureDeleted() staat nog in je constructor en wist elke start de database
      - De ListView cachet oude data
      - Find() verwijdert het object
    correct: 1
    explanation: Haal db.Database.EnsureDeleted(); weg en laat alleen EnsureCreated() staan, zodat bestaande data blijft.
  - id: w6q7
    question: Wat doet <code>db.Citizens.Find(selectedCitizen.Id)</code>?
    options:
      - Het maakt een nieuw Citizen-object aan
      - Het haalt de bewoner met dat Id op uit de database (of null)
      - Het verwijdert de bewoner
      - Het geeft alle bewoners terug
    correct: 1
    explanation: Find zoekt op de primaire sleutel en geeft dat ene object terug, of null als het niet bestaat.
  - id: w6q8
    question: Waarom werkt de CRUD-code voor <code>Building</code> bijna hetzelfde als die voor <code>Citizen</code>?
    options:
      - Toeval
      - Het is één patroon: ophalen → wijzigen → SaveChanges → lijst verversen, ongeacht de klasse
      - Omdat Building van Citizen erft
      - Omdat ze in dezelfde ListView staan
    correct: 1
    explanation: EF Core werkt via de DbSet<T>; het patroon is voor elk model identiek.
---
