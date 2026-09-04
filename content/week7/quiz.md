---
week: 7
title: Quiz Week 7 — API + EF Core & validatie
passScore: 70
questions:
  - id: w7q1
    question: Hoe geeft je API in week 7 de voertuigenlijst terug?
    options:
      - Uit de database via de DbContext (bijv. db.Voertuigen.ToList())
      - Vanuit een hardcoded List in je code
      - Uit een tekstbestand
      - Rechtstreeks vanuit de browser
    correct: 0
    explanation: "De API is de brug: hij haalt de data met EF Core uit de database en serveert die als JSON."
  - id: w7q2
    question: Waar lees je de inhoud (body) van een POST-verzoek uit?
    options:
      - "context.Response.OutputStream"
      - "context.Request.Url"
      - "context.Response.ContentLength64"
      - "context.Request.InputStream"
    correct: 3
    explanation: De verzonden gegevens komen binnen via de InputStream van de Request.
  - id: w7q3
    question: Wat is validatie?
    options:
      - Het controleren of invoer aan de voorwaarden voldoet
      - Het versleutelen van gegevens
      - Het opslaan van gegevens
      - Het omzetten van JSON naar objecten
    correct: 0
    explanation: Validatie controleert of de door de gebruiker aangeleverde gegevens bruikbaar en correct zijn.
  - id: w7q4
    question: Welke package bevat de attributen [Required], [MaxLength] en [Range]?
    options:
      - "System.Text.Json"
      - "Microsoft.EntityFrameworkCore"
      - "System.ComponentModel.DataAnnotations"
      - "System.Net"
    correct: 2
    explanation: Data Annotations zitten in System.ComponentModel.DataAnnotations.
  - id: w7q5
    question: Welke methode voert de validatie op basis van Data Annotations uit?
    options:
      - "Validator.TryValidateObject"
      - "JsonSerializer.Deserialize"
      - "context.SaveChanges"
      - "Regex.IsMatch"
    correct: 0
    explanation: TryValidateObject vult een lijst met ValidationResults en geeft true/false terug.
  - id: w7q6
    question: "Je schrijft `[Required]` in plaats van `[RequiredAttribute]`. Klopt dat?"
    options:
      - Nee, de volledige naam is verplicht
      - Alleen bij [Range]
      - Alleen in een console-app
      - Ja, bij attribute-classes mag je de 'Attribute'-suffix weglaten
    correct: 3
    explanation: Beide schrijfwijzen zijn geldig voor C#-attributes.
  - id: w7q7
    question: "Wat matcht de regex `^[0-9]{4}[A-Z]{2}$`?"
    options:
      - "1234ab"
      - "1234AB"
      - "12 34AB"
      - "AB1234"
    correct: 1
    explanation: 4 cijfers, dan 2 hoofdletters, niets ervoor of erna — precies het postcodeformaat 1234AB.
  - id: w7q8
    question: "Wat betekent `\\s?` in de regex `^[0-9]{4}\\s?[A-Z]{2}$`?"
    options:
      - Precies één spatie is verplicht
      - Een witruimte-teken is op die plek optioneel
      - Er mogen alleen letters staan
      - Het is het einde van de string
    correct: 1
    explanation: "`\\s` is witruimte, `?` maakt het optioneel — zo mag de postcode mét of zónder spatie."
---
