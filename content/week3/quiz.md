---
week: 3
title: Quiz Week 3 — EF Core opzet & model
passScore: 70
questions:
  - id: w3q1
    question: Waar staat ORM voor?
    options:
      - Object Relational Mapper
      - Online Resource Manager
      - Ordered Record Model
      - Object Reference Machine
    correct: 0
    explanation: EF Core is een Object-Relational Mapper — de brug tussen C#-objecten en database-tabellen.
  - id: w3q2
    question: Wat is het belangrijkste voordeel van werken met EF Core?
    options:
      - Je database wordt automatisch geback-upt
      - Je hoeft vrijwel geen handmatig SQL te schrijven
      - Je hebt geen database meer nodig
      - Je code draait altijd sneller
    correct: 1
    explanation: Je blijft in C# programmeren; EF Core vertaalt naar SQL.
  - id: w3q3
    question: Wat is een migration?
    options:
      - Het verhuizen van je project naar een andere computer
      - Een back-up van je database
      - Een 'patch' die je database in de juiste vorm brengt voor die versie van je app
      - Een lijst met gebruikers
    correct: 2
    explanation: Migrations houden je databasestructuur in de pas met je C#-classes.
  - id: w3q4
    question: Je gebruikt .NET 8.0. Welke package-versie kies je?
    options:
      - De allernieuwste, bijv. 9.0.0
      - Altijd 1.0.0
      - De hoogste versie die begint met 8.
      - Maakt niet uit
    correct: 2
    explanation: Kies de laatste minor versie die bij je .NET-versie past (bij .NET 8 dus 8.*).
  - id: w3q5
    question: Waarom maak je in je model properties en geen fields?
    options:
      - EF Core werkt met properties (get/set)
      - Fields bestaan niet in C#
      - Properties zijn korter
      - Fields kunnen niet public zijn
    correct: 0
    explanation: EF Core leest je model via properties; met kale fields werkt het niet.
  - id: w3q6
    question: Wat doet de OnConfiguring-methode?
    options:
      - Ze maakt de migratie aan
      - Ze vult de database met testdata
      - Ze genereert de C#-classes
      - Ze maakt verbinding met de database via de connection string
    correct: 3
    explanation: OnConfiguring wordt door EF Core aangeroepen om de verbinding op te zetten.
  - id: w3q7
    question: "Je wilt de class Klant opslaan. Welke regel hoort in je DbContext?"
    options:
      - "public Klant Klanten { get; set; }"
      - "public List<Klant> Klanten;"
      - "public DbSet<Klant> Klanten { get; set; }"
      - "public DbSet Klanten = new Klant();"
    correct: 2
    explanation: Voor elke op te slaan class maak je een DbSet-property met de class tussen < >.
  - id: w3q8
    question: In welke volgorde voer je deze commando's uit?
    options:
      - Eerst Add-Migration, daarna Update-Database
      - Update-Database, daarna Add-Migration
      - Alleen Update-Database is genoeg
      - De volgorde maakt niet uit
    correct: 0
    explanation: Add-Migration maakt het migratiebestand; Update-Database voert het uit op de database.
---
