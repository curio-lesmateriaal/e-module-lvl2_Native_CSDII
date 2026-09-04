---
week: 4
title: Quiz Week 4 — CRUD met EF Core
passScore: 70
questions:
  - id: w4q1
    question: Welke methode voegt een nieuw object toe aan een DbSet?
    options:
      - Insert()
      - Add()
      - New()
      - Create()
    correct: 1
    explanation: "`dbContext.Companies.Add(myCompany);` voegt het object toe aan de tracking; SaveChanges slaat het op."
  - id: w4q2
    question: Wat gebeurt er als je Add() aanroept maar SaveChanges() vergeet?
    options:
      - Het object wordt toch opgeslagen
      - Het object wordt niet in de database opgeslagen
      - Je krijgt een compilerfout
      - De hele database wordt gewist
    correct: 1
    explanation: EF slaat pas op bij een expliciete SaveChanges-aanroep.
  - id: w4q3
    question: Welke methode geeft null terug als er niets gevonden wordt?
    options:
      - Single()
      - First()
      - FirstOrDefault()
      - Add()
    correct: 2
    explanation: FirstOrDefault geeft de default-waarde (null voor objecten) als de query niets oplevert.
  - id: w4q4
    question: Hoe wijzig je de naam van een bestaande klant in de database?
    options:
      - Klant ophalen, property aanpassen, SaveChanges op dezelfde context
      - Een nieuwe Klant maken met dezelfde Id
      - Klanten.Update(naam) aanroepen
      - Dat kan niet met EF Core
    correct: 0
    explanation: Dankzij Change Tracking herkent EF de wijziging en bouwt het de UPDATE-query.
  - id: w4q5
    question: Waarom moet je SaveChanges aanroepen op dezelfde context als waar je de data hebt opgehaald?
    options:
      - Anders is de verbinding verbroken
      - Alleen die context houdt via Change Tracking bij wat er is gewijzigd of verwijderd
      - Het is sneller
      - Dat hoeft niet
    correct: 1
    explanation: Change Tracking hoort bij één context-instantie.
  - id: w4q6
    question: Wat is een 'roundtrip' in de context van batching?
    options:
      - Een backup-cyclus
      - Het heen en weer sturen van gegevens tussen client en server
      - Een lus in je code
      - Een migratie terugdraaien
    correct: 1
    explanation: EF bundelt meerdere opdrachten in één roundtrip om het verkeer met de database te beperken.
  - id: w4q7
    question: Welke methode markeert een object voor verwijdering?
    options:
      - Delete()
      - Drop()
      - Remove()
      - Clear()
    correct: 2
    explanation: "`db.Chats.Remove(chat);` gevolgd door `db.SaveChanges();` verwijdert de rij."
  - id: w4q8
    question: Je verwijdert een Voertuig waar nog Verhuren naar verwijzen. Wat is waar?
    options:
      - EF verwijdert automatisch alles, altijd, zonder configuratie
      - Je krijgt foutmeldingen tenzij je de afhankelijke data verwijdert of de relatie verbreekt (bijv. via Cascade Delete)
      - Het voertuig wordt stilletjes overgeslagen
      - De hele tabel wordt geleegd
    correct: 1
    explanation: Afhankelijke gegevens moeten mee verwijderd of ontkoppeld worden; daarvoor bestaat Cascade Delete.
---
